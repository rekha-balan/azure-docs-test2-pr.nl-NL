---
title: Audit activity reports in the Azure Active Directory portal | Microsoft Docs
description: Introduction to the audit activity reports in the Azure Active Directory portal
services: active-directory
documentationcenter: ''
author: priyamohanram
manager: mtillman
editor: ''
ms.assetid: a1f93126-77d1-4345-ab7d-561066041161
ms.service: active-directory
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.component: report-monitor
ms.date: 04/19/2018
ms.author: priyamo
ms.reviewer: dhanyahk
ms.openlocfilehash: b6fa26cb7947658af77496831d7239b4331aa1f2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870503"
---
# <a name="audit-activity-reports-in-the-azure-active-directory-portal"></a><span data-ttu-id="75fa3-103">Audit activity reports in the Azure Active Directory portal</span><span class="sxs-lookup"><span data-stu-id="75fa3-103">Audit activity reports in the Azure Active Directory portal</span></span> 

<span data-ttu-id="75fa3-104">With reporting in Azure Active Directory (Azure AD), you can get the information you need to determine how your environment is doing.</span><span class="sxs-lookup"><span data-stu-id="75fa3-104">With reporting in Azure Active Directory (Azure AD), you can get the information you need to determine how your environment is doing.</span></span>

<span data-ttu-id="75fa3-105">The reporting architecture in Azure AD consists of the following components:</span><span class="sxs-lookup"><span data-stu-id="75fa3-105">The reporting architecture in Azure AD consists of the following components:</span></span>

- <span data-ttu-id="75fa3-106">**Activity**</span><span class="sxs-lookup"><span data-stu-id="75fa3-106">**Activity**</span></span> 
    - <span data-ttu-id="75fa3-107">**Sign-in activities** – Information about the usage of managed applications and user sign-in activities</span><span class="sxs-lookup"><span data-stu-id="75fa3-107">**Sign-in activities** – Information about the usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="75fa3-108">**Audit logs** - Provides traceability through logs for all changes done by various features within Azure AD.</span><span class="sxs-lookup"><span data-stu-id="75fa3-108">**Audit logs** - Provides traceability through logs for all changes done by various features within Azure AD.</span></span> <span data-ttu-id="75fa3-109">Examples of audit logs include changes made to any resources within Azure AD like users, apps, groups, roles, policies, authentications etc...</span><span class="sxs-lookup"><span data-stu-id="75fa3-109">Examples of audit logs include changes made to any resources within Azure AD like users, apps, groups, roles, policies, authentications etc...</span></span>
- <span data-ttu-id="75fa3-110">**Security**</span><span class="sxs-lookup"><span data-stu-id="75fa3-110">**Security**</span></span> 
    - <span data-ttu-id="75fa3-111">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span><span class="sxs-lookup"><span data-stu-id="75fa3-111">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> <span data-ttu-id="75fa3-112">For more details, see Risky sign-ins.</span><span class="sxs-lookup"><span data-stu-id="75fa3-112">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="75fa3-113">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span><span class="sxs-lookup"><span data-stu-id="75fa3-113">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="75fa3-114">For more details, see Users flagged for risk.</span><span class="sxs-lookup"><span data-stu-id="75fa3-114">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="75fa3-115">This topic gives you an overview of the audit activities.</span><span class="sxs-lookup"><span data-stu-id="75fa3-115">This topic gives you an overview of the audit activities.</span></span>
 
## <a name="who-can-access-the-data"></a><span data-ttu-id="75fa3-116">Who can access the data?</span><span class="sxs-lookup"><span data-stu-id="75fa3-116">Who can access the data?</span></span>
* <span data-ttu-id="75fa3-117">Users in the Security Admin or Security Reader role</span><span class="sxs-lookup"><span data-stu-id="75fa3-117">Users in the Security Admin or Security Reader role</span></span>
* <span data-ttu-id="75fa3-118">Global Admins</span><span class="sxs-lookup"><span data-stu-id="75fa3-118">Global Admins</span></span>
* <span data-ttu-id="75fa3-119">Individual users (non-admins) can see their own activities</span><span class="sxs-lookup"><span data-stu-id="75fa3-119">Individual users (non-admins) can see their own activities</span></span>


## <a name="audit-logs"></a><span data-ttu-id="75fa3-120">Audit logs</span><span class="sxs-lookup"><span data-stu-id="75fa3-120">Audit logs</span></span>

<span data-ttu-id="75fa3-121">The audit logs in Azure Active Directory provide records of system activities for compliance.</span><span class="sxs-lookup"><span data-stu-id="75fa3-121">The audit logs in Azure Active Directory provide records of system activities for compliance.</span></span>  
<span data-ttu-id="75fa3-122">Your first entry point to all auditing data is **Audit logs** in the **Activity** section of **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="75fa3-122">Your first entry point to all auditing data is **Audit logs** in the **Activity** section of **Azure Active Directory**.</span></span>

<span data-ttu-id="75fa3-123">![Audit logs](./media/concept-audit-logs/61.png "Audit logs")</span><span class="sxs-lookup"><span data-stu-id="75fa3-123">![Audit logs](./media/concept-audit-logs/61.png "Audit logs")</span></span>

<span data-ttu-id="75fa3-124">An audit log has a default list view that shows:</span><span class="sxs-lookup"><span data-stu-id="75fa3-124">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="75fa3-125">the date and time of the occurrence</span><span class="sxs-lookup"><span data-stu-id="75fa3-125">the date and time of the occurrence</span></span>
- <span data-ttu-id="75fa3-126">the initiator / actor (*who*) of an activity</span><span class="sxs-lookup"><span data-stu-id="75fa3-126">the initiator / actor (*who*) of an activity</span></span> 
- <span data-ttu-id="75fa3-127">the activity (*what*)</span><span class="sxs-lookup"><span data-stu-id="75fa3-127">the activity (*what*)</span></span> 
- <span data-ttu-id="75fa3-128">the target</span><span class="sxs-lookup"><span data-stu-id="75fa3-128">the target</span></span>

<span data-ttu-id="75fa3-129">![Audit logs](./media/concept-audit-logs/18.png "Audit logs")</span><span class="sxs-lookup"><span data-stu-id="75fa3-129">![Audit logs](./media/concept-audit-logs/18.png "Audit logs")</span></span>

<span data-ttu-id="75fa3-130">You can customize the list view by clicking **Columns** in the toolbar.</span><span class="sxs-lookup"><span data-stu-id="75fa3-130">You can customize the list view by clicking **Columns** in the toolbar.</span></span>

<span data-ttu-id="75fa3-131">![Audit logs](./media/concept-audit-logs/19.png "Audit logs")</span><span class="sxs-lookup"><span data-stu-id="75fa3-131">![Audit logs](./media/concept-audit-logs/19.png "Audit logs")</span></span>

<span data-ttu-id="75fa3-132">This enables you to display additional fields or remove fields that are already displayed.</span><span class="sxs-lookup"><span data-stu-id="75fa3-132">This enables you to display additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="75fa3-133">![Audit logs](./media/concept-audit-logs/21.png "Audit logs")</span><span class="sxs-lookup"><span data-stu-id="75fa3-133">![Audit logs](./media/concept-audit-logs/21.png "Audit logs")</span></span>


<span data-ttu-id="75fa3-134">By clicking an item in the list view, you get all available details about it.</span><span class="sxs-lookup"><span data-stu-id="75fa3-134">By clicking an item in the list view, you get all available details about it.</span></span>

<span data-ttu-id="75fa3-135">![Audit logs](./media/concept-audit-logs/22.png "Audit logs")</span><span class="sxs-lookup"><span data-stu-id="75fa3-135">![Audit logs](./media/concept-audit-logs/22.png "Audit logs")</span></span>


## <a name="filtering-audit-logs"></a><span data-ttu-id="75fa3-136">Filtering audit logs</span><span class="sxs-lookup"><span data-stu-id="75fa3-136">Filtering audit logs</span></span>

<span data-ttu-id="75fa3-137">To narrow down the reported data to a level that works for you, you can filter the audit data using the following fields:</span><span class="sxs-lookup"><span data-stu-id="75fa3-137">To narrow down the reported data to a level that works for you, you can filter the audit data using the following fields:</span></span>

- <span data-ttu-id="75fa3-138">Date range</span><span class="sxs-lookup"><span data-stu-id="75fa3-138">Date range</span></span>
- <span data-ttu-id="75fa3-139">Initiated by (Actor)</span><span class="sxs-lookup"><span data-stu-id="75fa3-139">Initiated by (Actor)</span></span>
- <span data-ttu-id="75fa3-140">Category</span><span class="sxs-lookup"><span data-stu-id="75fa3-140">Category</span></span>
- <span data-ttu-id="75fa3-141">Activity resource type</span><span class="sxs-lookup"><span data-stu-id="75fa3-141">Activity resource type</span></span>
- <span data-ttu-id="75fa3-142">Activity</span><span class="sxs-lookup"><span data-stu-id="75fa3-142">Activity</span></span>

<span data-ttu-id="75fa3-143">![Audit logs](./media/concept-audit-logs/23.png "Audit logs")</span><span class="sxs-lookup"><span data-stu-id="75fa3-143">![Audit logs](./media/concept-audit-logs/23.png "Audit logs")</span></span>


<span data-ttu-id="75fa3-144">The **date range** filter enables to you to define a timeframe for the returned data.</span><span class="sxs-lookup"><span data-stu-id="75fa3-144">The **date range** filter enables to you to define a timeframe for the returned data.</span></span>  
<span data-ttu-id="75fa3-145">Possible values are:</span><span class="sxs-lookup"><span data-stu-id="75fa3-145">Possible values are:</span></span>

- <span data-ttu-id="75fa3-146">1 month</span><span class="sxs-lookup"><span data-stu-id="75fa3-146">1 month</span></span>
- <span data-ttu-id="75fa3-147">7 days</span><span class="sxs-lookup"><span data-stu-id="75fa3-147">7 days</span></span>
- <span data-ttu-id="75fa3-148">24 hours</span><span class="sxs-lookup"><span data-stu-id="75fa3-148">24 hours</span></span>
- <span data-ttu-id="75fa3-149">Custom</span><span class="sxs-lookup"><span data-stu-id="75fa3-149">Custom</span></span>

<span data-ttu-id="75fa3-150">When you select a custom timeframe, you can configure a start time and an end time.</span><span class="sxs-lookup"><span data-stu-id="75fa3-150">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="75fa3-151">The **initiated by** filter enables you to define an actor's name or its universal principal name (UPN).</span><span class="sxs-lookup"><span data-stu-id="75fa3-151">The **initiated by** filter enables you to define an actor's name or its universal principal name (UPN).</span></span>

<span data-ttu-id="75fa3-152">The **category** filter enables you to select one of the following filter:</span><span class="sxs-lookup"><span data-stu-id="75fa3-152">The **category** filter enables you to select one of the following filter:</span></span>

- <span data-ttu-id="75fa3-153">All</span><span class="sxs-lookup"><span data-stu-id="75fa3-153">All</span></span>
- <span data-ttu-id="75fa3-154">Core category</span><span class="sxs-lookup"><span data-stu-id="75fa3-154">Core category</span></span>
- <span data-ttu-id="75fa3-155">Core directory</span><span class="sxs-lookup"><span data-stu-id="75fa3-155">Core directory</span></span>
- <span data-ttu-id="75fa3-156">Self-service password management</span><span class="sxs-lookup"><span data-stu-id="75fa3-156">Self-service password management</span></span>
- <span data-ttu-id="75fa3-157">Self-service group management</span><span class="sxs-lookup"><span data-stu-id="75fa3-157">Self-service group management</span></span>
- <span data-ttu-id="75fa3-158">Account provisioning- Automated password rollover</span><span class="sxs-lookup"><span data-stu-id="75fa3-158">Account provisioning- Automated password rollover</span></span>
- <span data-ttu-id="75fa3-159">Invited users</span><span class="sxs-lookup"><span data-stu-id="75fa3-159">Invited users</span></span>
- <span data-ttu-id="75fa3-160">MIM service</span><span class="sxs-lookup"><span data-stu-id="75fa3-160">MIM service</span></span>
- <span data-ttu-id="75fa3-161">Identity Protection</span><span class="sxs-lookup"><span data-stu-id="75fa3-161">Identity Protection</span></span>
- <span data-ttu-id="75fa3-162">B2C</span><span class="sxs-lookup"><span data-stu-id="75fa3-162">B2C</span></span>

<span data-ttu-id="75fa3-163">The **activity resource type** filter enables you to select one of the following filters:</span><span class="sxs-lookup"><span data-stu-id="75fa3-163">The **activity resource type** filter enables you to select one of the following filters:</span></span>

- <span data-ttu-id="75fa3-164">All</span><span class="sxs-lookup"><span data-stu-id="75fa3-164">All</span></span> 
- <span data-ttu-id="75fa3-165">Group</span><span class="sxs-lookup"><span data-stu-id="75fa3-165">Group</span></span>
- <span data-ttu-id="75fa3-166">Directory</span><span class="sxs-lookup"><span data-stu-id="75fa3-166">Directory</span></span>
- <span data-ttu-id="75fa3-167">User</span><span class="sxs-lookup"><span data-stu-id="75fa3-167">User</span></span>
- <span data-ttu-id="75fa3-168">Application</span><span class="sxs-lookup"><span data-stu-id="75fa3-168">Application</span></span>
- <span data-ttu-id="75fa3-169">Policy</span><span class="sxs-lookup"><span data-stu-id="75fa3-169">Policy</span></span>
- <span data-ttu-id="75fa3-170">Device</span><span class="sxs-lookup"><span data-stu-id="75fa3-170">Device</span></span>
- <span data-ttu-id="75fa3-171">Other</span><span class="sxs-lookup"><span data-stu-id="75fa3-171">Other</span></span>

<span data-ttu-id="75fa3-172">When you select **Group** as **activity resource type**, you get an additional filter category that enables you to also provide a **Source**:</span><span class="sxs-lookup"><span data-stu-id="75fa3-172">When you select **Group** as **activity resource type**, you get an additional filter category that enables you to also provide a **Source**:</span></span>

- <span data-ttu-id="75fa3-173">Azure AD</span><span class="sxs-lookup"><span data-stu-id="75fa3-173">Azure AD</span></span>
- <span data-ttu-id="75fa3-174">O365</span><span class="sxs-lookup"><span data-stu-id="75fa3-174">O365</span></span>


<span data-ttu-id="75fa3-175">The **activity** filter is based on the category and Activity resource type selection you make.</span><span class="sxs-lookup"><span data-stu-id="75fa3-175">The **activity** filter is based on the category and Activity resource type selection you make.</span></span> <span data-ttu-id="75fa3-176">You can select a specific activity you want to see or choose all.</span><span class="sxs-lookup"><span data-stu-id="75fa3-176">You can select a specific activity you want to see or choose all.</span></span> 

<span data-ttu-id="75fa3-177">You can get the list of all Audit Activities using the Graph API https://graph.windows.net/$tenantdomain/activities/auditActivityTypes?api-version=beta, where $tenantdomain = your domain name or refer to the article [audit report events](concept-audit-logs.md).</span><span class="sxs-lookup"><span data-stu-id="75fa3-177">You can get the list of all Audit Activities using the Graph API https://graph.windows.net/$tenantdomain/activities/auditActivityTypes?api-version=beta, where $tenantdomain = your domain name or refer to the article [audit report events](concept-audit-logs.md).</span></span>


## <a name="audit-logs-shortcuts"></a><span data-ttu-id="75fa3-178">Audit logs shortcuts</span><span class="sxs-lookup"><span data-stu-id="75fa3-178">Audit logs shortcuts</span></span>

<span data-ttu-id="75fa3-179">In addition to **Azure Active Directory**, the Azure portal provides you with two additional entry points to audit data:</span><span class="sxs-lookup"><span data-stu-id="75fa3-179">In addition to **Azure Active Directory**, the Azure portal provides you with two additional entry points to audit data:</span></span>

- <span data-ttu-id="75fa3-180">Users and groups</span><span class="sxs-lookup"><span data-stu-id="75fa3-180">Users and groups</span></span>
- <span data-ttu-id="75fa3-181">Enterprise applications</span><span class="sxs-lookup"><span data-stu-id="75fa3-181">Enterprise applications</span></span>

### <a name="users-and-groups-audit-logs"></a><span data-ttu-id="75fa3-182">Users and groups audit logs</span><span class="sxs-lookup"><span data-stu-id="75fa3-182">Users and groups audit logs</span></span>

<span data-ttu-id="75fa3-183">With user and group-based audit reports, you can get answers to questions such as:</span><span class="sxs-lookup"><span data-stu-id="75fa3-183">With user and group-based audit reports, you can get answers to questions such as:</span></span>

- <span data-ttu-id="75fa3-184">What types of updates have been applied the users?</span><span class="sxs-lookup"><span data-stu-id="75fa3-184">What types of updates have been applied the users?</span></span>

- <span data-ttu-id="75fa3-185">How many users were changed?</span><span class="sxs-lookup"><span data-stu-id="75fa3-185">How many users were changed?</span></span>

- <span data-ttu-id="75fa3-186">How many passwords were changed?</span><span class="sxs-lookup"><span data-stu-id="75fa3-186">How many passwords were changed?</span></span>

- <span data-ttu-id="75fa3-187">What has an administrator done in a directory?</span><span class="sxs-lookup"><span data-stu-id="75fa3-187">What has an administrator done in a directory?</span></span>

- <span data-ttu-id="75fa3-188">What are the groups that have been added?</span><span class="sxs-lookup"><span data-stu-id="75fa3-188">What are the groups that have been added?</span></span>

- <span data-ttu-id="75fa3-189">Are there groups with membership changes?</span><span class="sxs-lookup"><span data-stu-id="75fa3-189">Are there groups with membership changes?</span></span>

- <span data-ttu-id="75fa3-190">Have the owners of group been changed?</span><span class="sxs-lookup"><span data-stu-id="75fa3-190">Have the owners of group been changed?</span></span>

- <span data-ttu-id="75fa3-191">What licenses have been assigned to a group or a user?</span><span class="sxs-lookup"><span data-stu-id="75fa3-191">What licenses have been assigned to a group or a user?</span></span>

<span data-ttu-id="75fa3-192">If you just want to review auditing data that is related to users and groups, you can find a filtered view under **Audit logs** in the **Activity** section of the **Users and Groups**.</span><span class="sxs-lookup"><span data-stu-id="75fa3-192">If you just want to review auditing data that is related to users and groups, you can find a filtered view under **Audit logs** in the **Activity** section of the **Users and Groups**.</span></span> <span data-ttu-id="75fa3-193">This entry point has **Users and groups** as preselected **Activity Resource Type**.</span><span class="sxs-lookup"><span data-stu-id="75fa3-193">This entry point has **Users and groups** as preselected **Activity Resource Type**.</span></span>

<span data-ttu-id="75fa3-194">![Audit logs](./media/concept-audit-logs/93.png "Audit logs")</span><span class="sxs-lookup"><span data-stu-id="75fa3-194">![Audit logs](./media/concept-audit-logs/93.png "Audit logs")</span></span>

### <a name="enterprise-applications-audit-logs"></a><span data-ttu-id="75fa3-195">Enterprise applications audit logs</span><span class="sxs-lookup"><span data-stu-id="75fa3-195">Enterprise applications audit logs</span></span>

<span data-ttu-id="75fa3-196">With application-based audit reports, you can get answers to questions such as:</span><span class="sxs-lookup"><span data-stu-id="75fa3-196">With application-based audit reports, you can get answers to questions such as:</span></span>

* <span data-ttu-id="75fa3-197">What are the applications that have been added or updated?</span><span class="sxs-lookup"><span data-stu-id="75fa3-197">What are the applications that have been added or updated?</span></span>
* <span data-ttu-id="75fa3-198">What are the applications that have been removed?</span><span class="sxs-lookup"><span data-stu-id="75fa3-198">What are the applications that have been removed?</span></span>
* <span data-ttu-id="75fa3-199">Has a service principle for an application changed?</span><span class="sxs-lookup"><span data-stu-id="75fa3-199">Has a service principle for an application changed?</span></span>
* <span data-ttu-id="75fa3-200">Have the names of applications been changed?</span><span class="sxs-lookup"><span data-stu-id="75fa3-200">Have the names of applications been changed?</span></span>
* <span data-ttu-id="75fa3-201">Who gave consent to an application?</span><span class="sxs-lookup"><span data-stu-id="75fa3-201">Who gave consent to an application?</span></span>

<span data-ttu-id="75fa3-202">If you just want to review auditing data that is related to your applications, you can find a filtered view under **Audit logs** in the **Activity** section of the **Enterprise applications** blade.</span><span class="sxs-lookup"><span data-stu-id="75fa3-202">If you just want to review auditing data that is related to your applications, you can find a filtered view under **Audit logs** in the **Activity** section of the **Enterprise applications** blade.</span></span> <span data-ttu-id="75fa3-203">This entry point has **Enterprise applications** as preselected **Activity Resource Type**.</span><span class="sxs-lookup"><span data-stu-id="75fa3-203">This entry point has **Enterprise applications** as preselected **Activity Resource Type**.</span></span>

<span data-ttu-id="75fa3-204">![Audit logs](./media/concept-audit-logs/134.png "Audit logs")</span><span class="sxs-lookup"><span data-stu-id="75fa3-204">![Audit logs](./media/concept-audit-logs/134.png "Audit logs")</span></span>

<span data-ttu-id="75fa3-205">You can filter this view further down to just **groups** or just **users**.</span><span class="sxs-lookup"><span data-stu-id="75fa3-205">You can filter this view further down to just **groups** or just **users**.</span></span>

<span data-ttu-id="75fa3-206">![Audit logs](./media/concept-audit-logs/25.png "Audit logs")</span><span class="sxs-lookup"><span data-stu-id="75fa3-206">![Audit logs](./media/concept-audit-logs/25.png "Audit logs")</span></span>



## <a name="next-steps"></a><span data-ttu-id="75fa3-207">Next steps</span><span class="sxs-lookup"><span data-stu-id="75fa3-207">Next steps</span></span>

- <span data-ttu-id="75fa3-208">For an overview of reporting, see the [Azure Active Directory reporting](overview-reports.md).</span><span class="sxs-lookup"><span data-stu-id="75fa3-208">For an overview of reporting, see the [Azure Active Directory reporting](overview-reports.md).</span></span>

- <span data-ttu-id="75fa3-209">For a complete list of all audit activities, see [Azure AD audit activity reference](reference-audit-activities.md)</span><span class="sxs-lookup"><span data-stu-id="75fa3-209">For a complete list of all audit activities, see [Azure AD audit activity reference](reference-audit-activities.md)</span></span>

