---
title: Find activity reports in the Azure portal | Microsoft Docs
description: Learn how to find Azure Active Directory activity reports in the Azure portal.
services: active-directory
documentationcenter: ''
author: dhanyahk
manager: femila
editor: ''
ms.assetid: d93521f8-dc21-4feb-aaff-4bb300f04812
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/01/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 1a4a376126a6bdb07206968b9052c335c9d069fc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550450"
---
# <a name="find-activity-reports-in-the-azure-portal"></a><span data-ttu-id="e424b-103">Find activity reports in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="e424b-103">Find activity reports in the Azure portal</span></span>

<span data-ttu-id="e424b-104">If you are moving from the Azure classic portal to the Azure portal, you get a new look at Azure Active Directory (Azure AD) activity logs.</span><span class="sxs-lookup"><span data-stu-id="e424b-104">If you are moving from the Azure classic portal to the Azure portal, you get a new look at Azure Active Directory (Azure AD) activity logs.</span></span> <span data-ttu-id="e424b-105">In a recent [blog post](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), we explain how you can see activity logs in the context of the resource you are working on in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e424b-105">In a recent [blog post](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), we explain how you can see activity logs in the context of the resource you are working on in the Azure portal.</span></span> <span data-ttu-id="e424b-106">In this article, we describe how to find reports that you used in the Azure classic portal in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e424b-106">In this article, we describe how to find reports that you used in the Azure classic portal in the Azure portal.</span></span>

## <a name="whats-new"></a><span data-ttu-id="e424b-107">What's new</span><span class="sxs-lookup"><span data-stu-id="e424b-107">What's new</span></span>

<span data-ttu-id="e424b-108">Reports in the Azure classic portal are separated into categories:</span><span class="sxs-lookup"><span data-stu-id="e424b-108">Reports in the Azure classic portal are separated into categories:</span></span>

1.  <span data-ttu-id="e424b-109">Security reports</span><span class="sxs-lookup"><span data-stu-id="e424b-109">Security reports</span></span>
2.  <span data-ttu-id="e424b-110">Activity reports</span><span class="sxs-lookup"><span data-stu-id="e424b-110">Activity reports</span></span>
3.  <span data-ttu-id="e424b-111">Integrated app reports</span><span class="sxs-lookup"><span data-stu-id="e424b-111">Integrated app reports</span></span>

### <a name="activity-and-integrated-app-reports"></a><span data-ttu-id="e424b-112">Activity and integrated app reports</span><span class="sxs-lookup"><span data-stu-id="e424b-112">Activity and integrated app reports</span></span>

<span data-ttu-id="e424b-113">For context-based reporting in the Azure portal, existing reports are merged into a single view.</span><span class="sxs-lookup"><span data-stu-id="e424b-113">For context-based reporting in the Azure portal, existing reports are merged into a single view.</span></span> <span data-ttu-id="e424b-114">A single, underlying API provides the data to the view.</span><span class="sxs-lookup"><span data-stu-id="e424b-114">A single, underlying API provides the data to the view.</span></span>

<span data-ttu-id="e424b-115">To see this view, on the **Azure Active Directory** blade, under **ACTIVITY**, select **Audit logs**.</span><span class="sxs-lookup"><span data-stu-id="e424b-115">To see this view, on the **Azure Active Directory** blade, under **ACTIVITY**, select **Audit logs**.</span></span>

<span data-ttu-id="e424b-116">![Audit logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-migration/482.png "Audit logs")</span><span class="sxs-lookup"><span data-stu-id="e424b-116">![Audit logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-migration/482.png "Audit logs")</span></span>

<span data-ttu-id="e424b-117">The following reports are consolidated in this view:</span><span class="sxs-lookup"><span data-stu-id="e424b-117">The following reports are consolidated in this view:</span></span>

-   <span data-ttu-id="e424b-118">Audit report</span><span class="sxs-lookup"><span data-stu-id="e424b-118">Audit report</span></span>
-   <span data-ttu-id="e424b-119">Password reset activity</span><span class="sxs-lookup"><span data-stu-id="e424b-119">Password reset activity</span></span>
-   <span data-ttu-id="e424b-120">Password reset registration activity</span><span class="sxs-lookup"><span data-stu-id="e424b-120">Password reset registration activity</span></span>
-   <span data-ttu-id="e424b-121">Self-service groups activity</span><span class="sxs-lookup"><span data-stu-id="e424b-121">Self-service groups activity</span></span>
-   <span data-ttu-id="e424b-122">Office365 Group Name Changes</span><span class="sxs-lookup"><span data-stu-id="e424b-122">Office365 Group Name Changes</span></span>
-   <span data-ttu-id="e424b-123">Account provisioning activity</span><span class="sxs-lookup"><span data-stu-id="e424b-123">Account provisioning activity</span></span>
-   <span data-ttu-id="e424b-124">Password rollover status</span><span class="sxs-lookup"><span data-stu-id="e424b-124">Password rollover status</span></span>
-   <span data-ttu-id="e424b-125">Account provisioning errors</span><span class="sxs-lookup"><span data-stu-id="e424b-125">Account provisioning errors</span></span>


<span data-ttu-id="e424b-126">The Application Usage report has been enhanced and is included in the **Sign-ins** view.</span><span class="sxs-lookup"><span data-stu-id="e424b-126">The Application Usage report has been enhanced and is included in the **Sign-ins** view.</span></span> <span data-ttu-id="e424b-127">To see this view, on the **Azure Active Directory** blade, under **ACTIVITY**, select **Sign-ins**.</span><span class="sxs-lookup"><span data-stu-id="e424b-127">To see this view, on the **Azure Active Directory** blade, under **ACTIVITY**, select **Sign-ins**.</span></span>

<span data-ttu-id="e424b-128">![Sign-ins view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-migration/483.png "Sign-ins view")</span><span class="sxs-lookup"><span data-stu-id="e424b-128">![Sign-ins view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-migration/483.png "Sign-ins view")</span></span>

<span data-ttu-id="e424b-129">The **Sign-ins** view includes all user sign-ins. You can use this information to get application usage information.</span><span class="sxs-lookup"><span data-stu-id="e424b-129">The **Sign-ins** view includes all user sign-ins. You can use this information to get application usage information.</span></span> <span data-ttu-id="e424b-130">You also can view application usage information in the **Enterprise applications** overview, in the **MANAGE** section.</span><span class="sxs-lookup"><span data-stu-id="e424b-130">You also can view application usage information in the **Enterprise applications** overview, in the **MANAGE** section.</span></span>

<span data-ttu-id="e424b-131">![Enterprise applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-migration/484.png "Enterprise applications")</span><span class="sxs-lookup"><span data-stu-id="e424b-131">![Enterprise applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-migration/484.png "Enterprise applications")</span></span>

## <a name="access-a-specific-report"></a><span data-ttu-id="e424b-132">Access a specific report</span><span class="sxs-lookup"><span data-stu-id="e424b-132">Access a specific report</span></span>

<span data-ttu-id="e424b-133">Although the Azure portal offers a single view, you also can look at specific reports.</span><span class="sxs-lookup"><span data-stu-id="e424b-133">Although the Azure portal offers a single view, you also can look at specific reports.</span></span>

### <a name="audit-logs"></a><span data-ttu-id="e424b-134">Audit logs</span><span class="sxs-lookup"><span data-stu-id="e424b-134">Audit logs</span></span>

<span data-ttu-id="e424b-135">In response to customer feedback, in the Azure portal, you can use advanced filtering to access the data you want.</span><span class="sxs-lookup"><span data-stu-id="e424b-135">In response to customer feedback, in the Azure portal, you can use advanced filtering to access the data you want.</span></span> <span data-ttu-id="e424b-136">One filter you can use is an *activity category*, which lists the different types of activity logs in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e424b-136">One filter you can use is an *activity category*, which lists the different types of activity logs in Azure AD.</span></span> <span data-ttu-id="e424b-137">To narrow results to what you are looking for, you can select a category.</span><span class="sxs-lookup"><span data-stu-id="e424b-137">To narrow results to what you are looking for, you can select a category.</span></span>

<span data-ttu-id="e424b-138">For example, if you are interested only in activities related to self-service password resets, you can choose the **Self-service Password Management** category.</span><span class="sxs-lookup"><span data-stu-id="e424b-138">For example, if you are interested only in activities related to self-service password resets, you can choose the **Self-service Password Management** category.</span></span> <span data-ttu-id="e424b-139">The categories you see are based on the resource you are working in.</span><span class="sxs-lookup"><span data-stu-id="e424b-139">The categories you see are based on the resource you are working in.</span></span>  

<span data-ttu-id="e424b-140">![Category options on the Filter Audit Logs page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-migration/06.png "Category options on the Filter Audit Logs page")</span><span class="sxs-lookup"><span data-stu-id="e424b-140">![Category options on the Filter Audit Logs page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-migration/06.png "Category options on the Filter Audit Logs page")</span></span>

<span data-ttu-id="e424b-141">Activity categories include:</span><span class="sxs-lookup"><span data-stu-id="e424b-141">Activity categories include:</span></span>

- <span data-ttu-id="e424b-142">Core Directory</span><span class="sxs-lookup"><span data-stu-id="e424b-142">Core Directory</span></span>
- <span data-ttu-id="e424b-143">Self-service Password Management</span><span class="sxs-lookup"><span data-stu-id="e424b-143">Self-service Password Management</span></span>
- <span data-ttu-id="e424b-144">Self-service Group Management</span><span class="sxs-lookup"><span data-stu-id="e424b-144">Self-service Group Management</span></span>
- <span data-ttu-id="e424b-145">Account Provisioning</span><span class="sxs-lookup"><span data-stu-id="e424b-145">Account Provisioning</span></span>

### <a name="application-usage"></a><span data-ttu-id="e424b-146">Application usage</span><span class="sxs-lookup"><span data-stu-id="e424b-146">Application usage</span></span>

<span data-ttu-id="e424b-147">To view details about application usage for all apps or for a single app, under **ACTIVITY**, select **Sign-ins**. To narrow the results, you can filter on user name or application name.</span><span class="sxs-lookup"><span data-stu-id="e424b-147">To view details about application usage for all apps or for a single app, under **ACTIVITY**, select **Sign-ins**. To narrow the results, you can filter on user name or application name.</span></span>

<span data-ttu-id="e424b-148">![Filter Sign-In Events page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-migration/07.png "Filter Sign-In Events page")</span><span class="sxs-lookup"><span data-stu-id="e424b-148">![Filter Sign-In Events page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-migration/07.png "Filter Sign-In Events page")</span></span>

### <a name="security-reports"></a><span data-ttu-id="e424b-149">Security reports</span><span class="sxs-lookup"><span data-stu-id="e424b-149">Security reports</span></span>

#### <a name="azure-ad-anomalous-activity-reports"></a><span data-ttu-id="e424b-150">Azure AD anomalous activity reports</span><span class="sxs-lookup"><span data-stu-id="e424b-150">Azure AD anomalous activity reports</span></span>

<span data-ttu-id="e424b-151">Azure AD anomalous activity security reports from the Azure classic portal have been consolidated to provide you with one, central view.</span><span class="sxs-lookup"><span data-stu-id="e424b-151">Azure AD anomalous activity security reports from the Azure classic portal have been consolidated to provide you with one, central view.</span></span> <span data-ttu-id="e424b-152">This view shows all security-related risk events that Azure AD can detect and report on.</span><span class="sxs-lookup"><span data-stu-id="e424b-152">This view shows all security-related risk events that Azure AD can detect and report on.</span></span>

<span data-ttu-id="e424b-153">The following table lists the Azure AD anomalous activity security reports, and corresponding risk event types in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e424b-153">The following table lists the Azure AD anomalous activity security reports, and corresponding risk event types in the Azure portal.</span></span>

| <span data-ttu-id="e424b-154">Azure AD anomalous activity report</span><span class="sxs-lookup"><span data-stu-id="e424b-154">Azure AD anomalous activity report</span></span> |  <span data-ttu-id="e424b-155">Identity protection risk event type</span><span class="sxs-lookup"><span data-stu-id="e424b-155">Identity protection risk event type</span></span>|
| :--- | :--- |
| <span data-ttu-id="e424b-156">Users with leaked credentials</span><span class="sxs-lookup"><span data-stu-id="e424b-156">Users with leaked credentials</span></span> | <span data-ttu-id="e424b-157">Leaked credentials</span><span class="sxs-lookup"><span data-stu-id="e424b-157">Leaked credentials</span></span> |
| <span data-ttu-id="e424b-158">Irregular sign-in activity</span><span class="sxs-lookup"><span data-stu-id="e424b-158">Irregular sign-in activity</span></span> | <span data-ttu-id="e424b-159">Impossible travel to atypical locations</span><span class="sxs-lookup"><span data-stu-id="e424b-159">Impossible travel to atypical locations</span></span> |
| <span data-ttu-id="e424b-160">Sign-ins from possibly infected devices</span><span class="sxs-lookup"><span data-stu-id="e424b-160">Sign-ins from possibly infected devices</span></span> | <span data-ttu-id="e424b-161">Sign-ins from infected devices</span><span class="sxs-lookup"><span data-stu-id="e424b-161">Sign-ins from infected devices</span></span>|
| <span data-ttu-id="e424b-162">Sign-ins from unknown sources</span><span class="sxs-lookup"><span data-stu-id="e424b-162">Sign-ins from unknown sources</span></span> | <span data-ttu-id="e424b-163">Sign-ins from anonymous IP addresses</span><span class="sxs-lookup"><span data-stu-id="e424b-163">Sign-ins from anonymous IP addresses</span></span> |
| <span data-ttu-id="e424b-164">Sign-ins from IP addresses with suspicious activity</span><span class="sxs-lookup"><span data-stu-id="e424b-164">Sign-ins from IP addresses with suspicious activity</span></span> | <span data-ttu-id="e424b-165">Sign-ins from IP addresses with suspicious activity</span><span class="sxs-lookup"><span data-stu-id="e424b-165">Sign-ins from IP addresses with suspicious activity</span></span> |
| - | <span data-ttu-id="e424b-166">Sign-ins from unfamiliar locations</span><span class="sxs-lookup"><span data-stu-id="e424b-166">Sign-ins from unfamiliar locations</span></span> |

<span data-ttu-id="e424b-167">The following Azure AD anomalous activity security reports are not included as risk events in the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="e424b-167">The following Azure AD anomalous activity security reports are not included as risk events in the Azure portal:</span></span>

* <span data-ttu-id="e424b-168">Sign-ins after multiple failures</span><span class="sxs-lookup"><span data-stu-id="e424b-168">Sign-ins after multiple failures</span></span>
* <span data-ttu-id="e424b-169">Sign-ins from multiple geographies</span><span class="sxs-lookup"><span data-stu-id="e424b-169">Sign-ins from multiple geographies</span></span>

<span data-ttu-id="e424b-170">These reports are still available in the Azure classic portal, but they will be deprecated at some time in the future.</span><span class="sxs-lookup"><span data-stu-id="e424b-170">These reports are still available in the Azure classic portal, but they will be deprecated at some time in the future.</span></span>

<span data-ttu-id="e424b-171">For more information, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="e424b-171">For more information, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>  


#### <a name="detected-risk-events"></a><span data-ttu-id="e424b-172">Detected risk events</span><span class="sxs-lookup"><span data-stu-id="e424b-172">Detected risk events</span></span>

<span data-ttu-id="e424b-173">In the Azure portal, you can access reports about detected risk events on the **Azure Active Directory** blade, under **SECURITY**.</span><span class="sxs-lookup"><span data-stu-id="e424b-173">In the Azure portal, you can access reports about detected risk events on the **Azure Active Directory** blade, under **SECURITY**.</span></span> <span data-ttu-id="e424b-174">Detected risk events are tracked in the following reports:</span><span class="sxs-lookup"><span data-stu-id="e424b-174">Detected risk events are tracked in the following reports:</span></span>   

- <span data-ttu-id="e424b-175">Users at Risk</span><span class="sxs-lookup"><span data-stu-id="e424b-175">Users at Risk</span></span>
- <span data-ttu-id="e424b-176">Risky Sign-ins</span><span class="sxs-lookup"><span data-stu-id="e424b-176">Risky Sign-ins</span></span>

<span data-ttu-id="e424b-177">![Security reports](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-migration/04.png "Security reports")</span><span class="sxs-lookup"><span data-stu-id="e424b-177">![Security reports](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-migration/04.png "Security reports")</span></span>

<span data-ttu-id="e424b-178">For more information about security reports, see:</span><span class="sxs-lookup"><span data-stu-id="e424b-178">For more information about security reports, see:</span></span>

- [<span data-ttu-id="e424b-179">Users at Risk security report in the Azure Active Directory portal - preview</span><span class="sxs-lookup"><span data-stu-id="e424b-179">Users at Risk security report in the Azure Active Directory portal - preview</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="e424b-180">Risky Sign-ins report in the Azure Active Directory portal - preview</span><span class="sxs-lookup"><span data-stu-id="e424b-180">Risky Sign-ins report in the Azure Active Directory portal - preview</span></span>](active-directory-reporting-security-risky-sign-ins.md)


## <a name="activity-reports-in-the-azure-classic-portal-vs-the-azure-portal"></a><span data-ttu-id="e424b-181">Activity reports in the Azure classic portal vs. the Azure portal</span><span class="sxs-lookup"><span data-stu-id="e424b-181">Activity reports in the Azure classic portal vs. the Azure portal</span></span>

<span data-ttu-id="e424b-182">The table in this section lists existing reports in the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="e424b-182">The table in this section lists existing reports in the Azure classic portal.</span></span> <span data-ttu-id="e424b-183">It also describes how you can get the same information in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e424b-183">It also describes how you can get the same information in the Azure portal.</span></span>

<span data-ttu-id="e424b-184">To view all auditing data, on the **Azure Active Directory** blade, under **ACTIVITY**, go to **Audit logs**.</span><span class="sxs-lookup"><span data-stu-id="e424b-184">To view all auditing data, on the **Azure Active Directory** blade, under **ACTIVITY**, go to **Audit logs**.</span></span>

<span data-ttu-id="e424b-185">![Audit logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-migration/61.png "Audit logs")</span><span class="sxs-lookup"><span data-stu-id="e424b-185">![Audit logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-migration/61.png "Audit logs")</span></span>

| <span data-ttu-id="e424b-186">Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="e424b-186">Azure classic portal</span></span>                 | <span data-ttu-id="e424b-187">To find in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="e424b-187">To find in the Azure portal</span></span>                                                         |
| ---                                  | ---                                                                        |
| <span data-ttu-id="e424b-188">Audit logs</span><span class="sxs-lookup"><span data-stu-id="e424b-188">Audit logs</span></span>                           | <span data-ttu-id="e424b-189">For **Activity Category**, select **Core Directory**.</span><span class="sxs-lookup"><span data-stu-id="e424b-189">For **Activity Category**, select **Core Directory**.</span></span>                       |
| <span data-ttu-id="e424b-190">Password reset activity</span><span class="sxs-lookup"><span data-stu-id="e424b-190">Password reset activity</span></span>              | <span data-ttu-id="e424b-191">For **Activity Category**, select **Self-service Password Management**.</span><span class="sxs-lookup"><span data-stu-id="e424b-191">For **Activity Category**, select **Self-service Password Management**.</span></span> |
| <span data-ttu-id="e424b-192">Password reset registration activity</span><span class="sxs-lookup"><span data-stu-id="e424b-192">Password reset registration activity</span></span> | <span data-ttu-id="e424b-193">For **Activity Category**, select **Self-service Password Management**.</span><span class="sxs-lookup"><span data-stu-id="e424b-193">For **Activity Category**, select **Self-service Password Management**.</span></span>     |
| <span data-ttu-id="e424b-194">Self-service groups activity</span><span class="sxs-lookup"><span data-stu-id="e424b-194">Self-service groups activity</span></span>         | <span data-ttu-id="e424b-195">For **Activity Category**, select **Self-service Group Management**.</span><span class="sxs-lookup"><span data-stu-id="e424b-195">For **Activity Category**, select **Self-service Group Management**.</span></span>        |
| <span data-ttu-id="e424b-196">Account provisioning activity</span><span class="sxs-lookup"><span data-stu-id="e424b-196">Account provisioning activity</span></span>        | <span data-ttu-id="e424b-197">For **Activity Category**, select **Account User Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="e424b-197">For **Activity Category**, select **Account User Provisioning**.</span></span>         |
| <span data-ttu-id="e424b-198">Password rollover status</span><span class="sxs-lookup"><span data-stu-id="e424b-198">Password rollover status</span></span>             | <span data-ttu-id="e424b-199">For **Activity Category**, select **Automatic App Password Rollover**.</span><span class="sxs-lookup"><span data-stu-id="e424b-199">For **Activity Category**, select **Automatic App Password Rollover**.</span></span>      |
| <span data-ttu-id="e424b-200">Account provisioning errors</span><span class="sxs-lookup"><span data-stu-id="e424b-200">Account provisioning errors</span></span>          | <span data-ttu-id="e424b-201">For **Activity Category**, select **Account User Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="e424b-201">For **Activity Category**, select **Account User Provisioning**.</span></span>        |
| <span data-ttu-id="e424b-202">Office365 Group Name Changes</span><span class="sxs-lookup"><span data-stu-id="e424b-202">Office365 Group Name Changes</span></span>         | <span data-ttu-id="e424b-203">For **Activity Category**, select **Self-service Password Management**.</span><span class="sxs-lookup"><span data-stu-id="e424b-203">For **Activity Category**, select **Self-service Password Management**.</span></span> <span data-ttu-id="e424b-204">For **Activity Resource Type**, select **Group**.</span><span class="sxs-lookup"><span data-stu-id="e424b-204">For **Activity Resource Type**, select **Group**.</span></span> <span data-ttu-id="e424b-205">For **Activity Source**, select **O365 groups**.</span><span class="sxs-lookup"><span data-stu-id="e424b-205">For **Activity Source**, select **O365 groups**.</span></span>|

<span data-ttu-id="e424b-206">To view the **Application Usage** report, on the **Azure Active Directory** blade, under **MANAGE**, select **Enterprise Applications**, and then select **Sign-ins**.</span><span class="sxs-lookup"><span data-stu-id="e424b-206">To view the **Application Usage** report, on the **Azure Active Directory** blade, under **MANAGE**, select **Enterprise Applications**, and then select **Sign-ins**.</span></span>


<span data-ttu-id="e424b-207">![Enterprise Applications Sign-Ins report](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-migration/199.png "Enterprise Applications Sign-Ins report")</span><span class="sxs-lookup"><span data-stu-id="e424b-207">![Enterprise Applications Sign-Ins report](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-migration/199.png "Enterprise Applications Sign-Ins report")</span></span>








