---
title: Azure Active Directory reporting - preview | Microsoft Docs
description: Lists the various available reports for Azure Active Directory preview
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: femila
editor: ''
ms.assetid: 6141a333-38db-478a-927e-526f1e7614f4
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/06/2017
ms.author: markvi
ms.openlocfilehash: 09784cf891b460fc6561f313caa3657d8ffcaccc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554966"
---
# <a name="azure-active-directory-reporting---preview"></a><span data-ttu-id="70a81-103">Azure Active Directory reporting - preview</span><span class="sxs-lookup"><span data-stu-id="70a81-103">Azure Active Directory reporting - preview</span></span>


<span data-ttu-id="70a81-104">*This documentation is part of the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).*</span><span class="sxs-lookup"><span data-stu-id="70a81-104">*This documentation is part of the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).*</span></span>

<span data-ttu-id="70a81-105">With reporting in the Azure Active Directory preview, you get all the information you need to determine how your environment is doing.</span><span class="sxs-lookup"><span data-stu-id="70a81-105">With reporting in the Azure Active Directory preview, you get all the information you need to determine how your environment is doing.</span></span> [<span data-ttu-id="70a81-106">What's in the preview?</span><span class="sxs-lookup"><span data-stu-id="70a81-106">What's in the preview?</span></span>](active-directory-preview-explainer.md)

<span data-ttu-id="70a81-107">There are two main areas of reporting:</span><span class="sxs-lookup"><span data-stu-id="70a81-107">There are two main areas of reporting:</span></span>

* <span data-ttu-id="70a81-108">**Sign-in activities** – Information about the usage of managed applications and user sign-in activities</span><span class="sxs-lookup"><span data-stu-id="70a81-108">**Sign-in activities** – Information about the usage of managed applications and user sign-in activities</span></span>
* <span data-ttu-id="70a81-109">**Audit logs** - System activity information about users and group management, your managed applications and directory activities</span><span class="sxs-lookup"><span data-stu-id="70a81-109">**Audit logs** - System activity information about users and group management, your managed applications and directory activities</span></span>

<span data-ttu-id="70a81-110">Depending on the scope of the data you are looking for, you can access these reports either by clicking **Users and groups** or **Enterprise applications** in the services list in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="70a81-110">Depending on the scope of the data you are looking for, you can access these reports either by clicking **Users and groups** or **Enterprise applications** in the services list in the [Azure portal](https://portal.azure.com).</span></span>

## <a name="sign-in-activities"></a><span data-ttu-id="70a81-111">Sign-in activities</span><span class="sxs-lookup"><span data-stu-id="70a81-111">Sign-in activities</span></span>
### <a name="user-sign-in-activities"></a><span data-ttu-id="70a81-112">User sign-in activities</span><span class="sxs-lookup"><span data-stu-id="70a81-112">User sign-in activities</span></span>
<span data-ttu-id="70a81-113">With the information provided by the user sign-in report, you find answers to questions such as:</span><span class="sxs-lookup"><span data-stu-id="70a81-113">With the information provided by the user sign-in report, you find answers to questions such as:</span></span>

* <span data-ttu-id="70a81-114">What is the sign-in pattern of a user?</span><span class="sxs-lookup"><span data-stu-id="70a81-114">What is the sign-in pattern of a user?</span></span>
* <span data-ttu-id="70a81-115">How many users have users signed in over a week?</span><span class="sxs-lookup"><span data-stu-id="70a81-115">How many users have users signed in over a week?</span></span>
* <span data-ttu-id="70a81-116">What’s the status of these sign-ins?</span><span class="sxs-lookup"><span data-stu-id="70a81-116">What’s the status of these sign-ins?</span></span>

<span data-ttu-id="70a81-117">Your entry point to this data is the user sign-in graph in the **Overview** section under **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="70a81-117">Your entry point to this data is the user sign-in graph in the **Overview** section under **Users and groups**.</span></span>

 <span data-ttu-id="70a81-118">![Reporting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/05.png "Reporting")</span><span class="sxs-lookup"><span data-stu-id="70a81-118">![Reporting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/05.png "Reporting")</span></span>

<span data-ttu-id="70a81-119">The user sign-in graph shows weekly aggregations of sign ins for all users in a given time period.</span><span class="sxs-lookup"><span data-stu-id="70a81-119">The user sign-in graph shows weekly aggregations of sign ins for all users in a given time period.</span></span> <span data-ttu-id="70a81-120">The default for the time period is 30 days.</span><span class="sxs-lookup"><span data-stu-id="70a81-120">The default for the time period is 30 days.</span></span>

<span data-ttu-id="70a81-121">![Reporting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/02.png "Reporting")</span><span class="sxs-lookup"><span data-stu-id="70a81-121">![Reporting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/02.png "Reporting")</span></span>

<span data-ttu-id="70a81-122">When you click on a day in the sign-in graph, you get a detailed list of the sign-in activities.</span><span class="sxs-lookup"><span data-stu-id="70a81-122">When you click on a day in the sign-in graph, you get a detailed list of the sign-in activities.</span></span>

<span data-ttu-id="70a81-123">![Reporting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/03.png "Reporting")</span><span class="sxs-lookup"><span data-stu-id="70a81-123">![Reporting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/03.png "Reporting")</span></span>

<span data-ttu-id="70a81-124">Each row in the sign-in activities list gives you the detailed information about the selected sign-in such as:</span><span class="sxs-lookup"><span data-stu-id="70a81-124">Each row in the sign-in activities list gives you the detailed information about the selected sign-in such as:</span></span>

* <span data-ttu-id="70a81-125">Who has signed in?</span><span class="sxs-lookup"><span data-stu-id="70a81-125">Who has signed in?</span></span>
* <span data-ttu-id="70a81-126">What was the related UPN?</span><span class="sxs-lookup"><span data-stu-id="70a81-126">What was the related UPN?</span></span>
* <span data-ttu-id="70a81-127">What application was the target of the sign-in?</span><span class="sxs-lookup"><span data-stu-id="70a81-127">What application was the target of the sign-in?</span></span>
* <span data-ttu-id="70a81-128">What is the IP address of the sign-in?</span><span class="sxs-lookup"><span data-stu-id="70a81-128">What is the IP address of the sign-in?</span></span>
* <span data-ttu-id="70a81-129">What was the status of the sign-in?</span><span class="sxs-lookup"><span data-stu-id="70a81-129">What was the status of the sign-in?</span></span>

### <a name="usage-of-managed-applications"></a><span data-ttu-id="70a81-130">Usage of managed applications</span><span class="sxs-lookup"><span data-stu-id="70a81-130">Usage of managed applications</span></span>
<span data-ttu-id="70a81-131">With an application-centric view of your sign-in data, you can answer questions such as:</span><span class="sxs-lookup"><span data-stu-id="70a81-131">With an application-centric view of your sign-in data, you can answer questions such as:</span></span>

* <span data-ttu-id="70a81-132">Who is using my applications?</span><span class="sxs-lookup"><span data-stu-id="70a81-132">Who is using my applications?</span></span>
* <span data-ttu-id="70a81-133">What are the top 3 applications in your organization?</span><span class="sxs-lookup"><span data-stu-id="70a81-133">What are the top 3 applications in your organization?</span></span>
* <span data-ttu-id="70a81-134">I have recently rolled out an application.</span><span class="sxs-lookup"><span data-stu-id="70a81-134">I have recently rolled out an application.</span></span> <span data-ttu-id="70a81-135">How is it doing?</span><span class="sxs-lookup"><span data-stu-id="70a81-135">How is it doing?</span></span>

<span data-ttu-id="70a81-136">Your entry point to this data is the top 3 applications in your organization within the last 30 days report in the **Overview** section under **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="70a81-136">Your entry point to this data is the top 3 applications in your organization within the last 30 days report in the **Overview** section under **Enterprise applications**.</span></span>

 <span data-ttu-id="70a81-137">![Reporting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/06.png "Reporting")</span><span class="sxs-lookup"><span data-stu-id="70a81-137">![Reporting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/06.png "Reporting")</span></span>

<span data-ttu-id="70a81-138">The app usage graph weekly aggregations of sign ins for your top 3 applications in a given time period.</span><span class="sxs-lookup"><span data-stu-id="70a81-138">The app usage graph weekly aggregations of sign ins for your top 3 applications in a given time period.</span></span> <span data-ttu-id="70a81-139">The default for the time period is 30 days.</span><span class="sxs-lookup"><span data-stu-id="70a81-139">The default for the time period is 30 days.</span></span>

<span data-ttu-id="70a81-140">![Reporting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/78.png "Reporting")</span><span class="sxs-lookup"><span data-stu-id="70a81-140">![Reporting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/78.png "Reporting")</span></span>

<span data-ttu-id="70a81-141">If you want to, you can set the focus on a specific application.</span><span class="sxs-lookup"><span data-stu-id="70a81-141">If you want to, you can set the focus on a specific application.</span></span>

<span data-ttu-id="70a81-142">![Reporting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/single_spp_usage_graph.png "Reporting")</span><span class="sxs-lookup"><span data-stu-id="70a81-142">![Reporting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/single_spp_usage_graph.png "Reporting")</span></span>

<span data-ttu-id="70a81-143">When you click on a day in the app usage graph, you get a detailed list of the sign-in activities.</span><span class="sxs-lookup"><span data-stu-id="70a81-143">When you click on a day in the app usage graph, you get a detailed list of the sign-in activities.</span></span>

<span data-ttu-id="70a81-144">![Reporting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/top_app_sign_ins.png "Reporting")</span><span class="sxs-lookup"><span data-stu-id="70a81-144">![Reporting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/top_app_sign_ins.png "Reporting")</span></span>

<span data-ttu-id="70a81-145">The **Sign-ins** option gives you a complete overview of all sign-in events to your applications.</span><span class="sxs-lookup"><span data-stu-id="70a81-145">The **Sign-ins** option gives you a complete overview of all sign-in events to your applications.</span></span>

<span data-ttu-id="70a81-146">![Reporting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/85.png "Reporting")</span><span class="sxs-lookup"><span data-stu-id="70a81-146">![Reporting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/85.png "Reporting")</span></span>

<span data-ttu-id="70a81-147">By using the column chooser, you can select the data fields you want to display.</span><span class="sxs-lookup"><span data-stu-id="70a81-147">By using the column chooser, you can select the data fields you want to display.</span></span>

<span data-ttu-id="70a81-148">![Reporting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/column_chooser.png "Reporting")</span><span class="sxs-lookup"><span data-stu-id="70a81-148">![Reporting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/column_chooser.png "Reporting")</span></span>

### <a name="filtering-sign-ins"></a><span data-ttu-id="70a81-149">Filtering sign-ins</span><span class="sxs-lookup"><span data-stu-id="70a81-149">Filtering sign-ins</span></span>
<span data-ttu-id="70a81-150">You can filter sign-ins to limit the amount of displayed data using the following fields:</span><span class="sxs-lookup"><span data-stu-id="70a81-150">You can filter sign-ins to limit the amount of displayed data using the following fields:</span></span>

* <span data-ttu-id="70a81-151">Date and time</span><span class="sxs-lookup"><span data-stu-id="70a81-151">Date and time</span></span> 
* <span data-ttu-id="70a81-152">User's user principal name</span><span class="sxs-lookup"><span data-stu-id="70a81-152">User's user principal name</span></span>
* <span data-ttu-id="70a81-153">Application name</span><span class="sxs-lookup"><span data-stu-id="70a81-153">Application name</span></span>
* <span data-ttu-id="70a81-154">Client name</span><span class="sxs-lookup"><span data-stu-id="70a81-154">Client name</span></span>
* <span data-ttu-id="70a81-155">Sign-in status</span><span class="sxs-lookup"><span data-stu-id="70a81-155">Sign-in status</span></span>

<span data-ttu-id="70a81-156">![Reporting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/293.png "Reporting")</span><span class="sxs-lookup"><span data-stu-id="70a81-156">![Reporting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/293.png "Reporting")</span></span>

<span data-ttu-id="70a81-157">Another method to filter the entries of the sign-in activities is to search for specific entries.</span><span class="sxs-lookup"><span data-stu-id="70a81-157">Another method to filter the entries of the sign-in activities is to search for specific entries.</span></span>
<span data-ttu-id="70a81-158">The search method enables you to scope your sign-ins around specific **users**, **groups** or **applications**.</span><span class="sxs-lookup"><span data-stu-id="70a81-158">The search method enables you to scope your sign-ins around specific **users**, **groups** or **applications**.</span></span>

<span data-ttu-id="70a81-159">![Reporting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/84.png "Reporting")</span><span class="sxs-lookup"><span data-stu-id="70a81-159">![Reporting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/84.png "Reporting")</span></span>

## <a name="audit-logs"></a><span data-ttu-id="70a81-160">Audit logs</span><span class="sxs-lookup"><span data-stu-id="70a81-160">Audit logs</span></span>
<span data-ttu-id="70a81-161">The auditing logs in Azure Active Directory provide records of system activities for compliance.</span><span class="sxs-lookup"><span data-stu-id="70a81-161">The auditing logs in Azure Active Directory provide records of system activities for compliance.</span></span>

<span data-ttu-id="70a81-162">There are three main categories for auditing related activities in the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="70a81-162">There are three main categories for auditing related activities in the Azure portal:</span></span>

* <span data-ttu-id="70a81-163">Users and groups</span><span class="sxs-lookup"><span data-stu-id="70a81-163">Users and groups</span></span>   
* <span data-ttu-id="70a81-164">Applications</span><span class="sxs-lookup"><span data-stu-id="70a81-164">Applications</span></span>
* <span data-ttu-id="70a81-165">Directory</span><span class="sxs-lookup"><span data-stu-id="70a81-165">Directory</span></span>   

<span data-ttu-id="70a81-166">For a complete list of audit report activities, see the [list of audit report events](active-directory-reporting-audit-events.md#list-of-audit-report-events).</span><span class="sxs-lookup"><span data-stu-id="70a81-166">For a complete list of audit report activities, see the [list of audit report events](active-directory-reporting-audit-events.md#list-of-audit-report-events).</span></span>

<span data-ttu-id="70a81-167">Your entry point to all auditing data is **Audit logs** in the **Activity** section of **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="70a81-167">Your entry point to all auditing data is **Audit logs** in the **Activity** section of **Azure Active Directory**.</span></span>

<span data-ttu-id="70a81-168">![Auditing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/61.png "Auditing")</span><span class="sxs-lookup"><span data-stu-id="70a81-168">![Auditing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/61.png "Auditing")</span></span>

<span data-ttu-id="70a81-169">An audit log has a list view that shows the actors (who), the activities (what) and the targets.</span><span class="sxs-lookup"><span data-stu-id="70a81-169">An audit log has a list view that shows the actors (who), the activities (what) and the targets.</span></span>

<span data-ttu-id="70a81-170">![Auditing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/345.png "Auditing")</span><span class="sxs-lookup"><span data-stu-id="70a81-170">![Auditing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/345.png "Auditing")</span></span>

<span data-ttu-id="70a81-171">By clicking an item in the list view, you can get more details about it.</span><span class="sxs-lookup"><span data-stu-id="70a81-171">By clicking an item in the list view, you can get more details about it.</span></span>

<span data-ttu-id="70a81-172">![Auditing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/873.png "Auditing")</span><span class="sxs-lookup"><span data-stu-id="70a81-172">![Auditing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/873.png "Auditing")</span></span>

### <a name="users-and-groups-audit-logs"></a><span data-ttu-id="70a81-173">Users and groups audit logs</span><span class="sxs-lookup"><span data-stu-id="70a81-173">Users and groups audit logs</span></span>
<span data-ttu-id="70a81-174">With user and group-based audit reports, you can get answers to questions such as:</span><span class="sxs-lookup"><span data-stu-id="70a81-174">With user and group-based audit reports, you can get answers to questions such as:</span></span>

* <span data-ttu-id="70a81-175">What types of updates have been applied the users?</span><span class="sxs-lookup"><span data-stu-id="70a81-175">What types of updates have been applied the users?</span></span>
* <span data-ttu-id="70a81-176">How many users were changed?</span><span class="sxs-lookup"><span data-stu-id="70a81-176">How many users were changed?</span></span>
* <span data-ttu-id="70a81-177">How many passwords were changed?</span><span class="sxs-lookup"><span data-stu-id="70a81-177">How many passwords were changed?</span></span>
* <span data-ttu-id="70a81-178">What has an administrator done in a directory?</span><span class="sxs-lookup"><span data-stu-id="70a81-178">What has an administrator done in a directory?</span></span>
* <span data-ttu-id="70a81-179">What are the groups that have been added?</span><span class="sxs-lookup"><span data-stu-id="70a81-179">What are the groups that have been added?</span></span>
* <span data-ttu-id="70a81-180">Are there groups with membership changes?</span><span class="sxs-lookup"><span data-stu-id="70a81-180">Are there groups with membership changes?</span></span>
* <span data-ttu-id="70a81-181">Have the owners of group been changed?</span><span class="sxs-lookup"><span data-stu-id="70a81-181">Have the owners of group been changed?</span></span>
* <span data-ttu-id="70a81-182">What licenses have been assigned to a group or a user?</span><span class="sxs-lookup"><span data-stu-id="70a81-182">What licenses have been assigned to a group or a user?</span></span>

<span data-ttu-id="70a81-183">If you just want to review auditing data that is related to users and groups, you can find a filtered view under **Audit logs** in the **Activity** section of **Users and Groups**.</span><span class="sxs-lookup"><span data-stu-id="70a81-183">If you just want to review auditing data that is related to users and groups, you can find a filtered view under **Audit logs** in the **Activity** section of **Users and Groups**.</span></span>

<span data-ttu-id="70a81-184">![Auditing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/93.png "Auditing")</span><span class="sxs-lookup"><span data-stu-id="70a81-184">![Auditing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/93.png "Auditing")</span></span>

### <a name="application-audit-logs"></a><span data-ttu-id="70a81-185">Application audit logs</span><span class="sxs-lookup"><span data-stu-id="70a81-185">Application audit logs</span></span>
<span data-ttu-id="70a81-186">With application-based audit reports, you can get answers to questions such as:</span><span class="sxs-lookup"><span data-stu-id="70a81-186">With application-based audit reports, you can get answers to questions such as:</span></span>

* <span data-ttu-id="70a81-187">What are the applications that have been added or updated?</span><span class="sxs-lookup"><span data-stu-id="70a81-187">What are the applications that have been added or updated?</span></span>
* <span data-ttu-id="70a81-188">What are the applications that have been removed?</span><span class="sxs-lookup"><span data-stu-id="70a81-188">What are the applications that have been removed?</span></span>
* <span data-ttu-id="70a81-189">Has a service principle for an application changed?</span><span class="sxs-lookup"><span data-stu-id="70a81-189">Has a service principle for an application changed?</span></span>
* <span data-ttu-id="70a81-190">Have the names of applications been changed?</span><span class="sxs-lookup"><span data-stu-id="70a81-190">Have the names of applications been changed?</span></span>
* <span data-ttu-id="70a81-191">Who gave consent to an application?</span><span class="sxs-lookup"><span data-stu-id="70a81-191">Who gave consent to an application?</span></span>

<span data-ttu-id="70a81-192">If you just want to review auditing data that is related to applications, you can find a filtered view under **Audit logs** in the **Activity** section of **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="70a81-192">If you just want to review auditing data that is related to applications, you can find a filtered view under **Audit logs** in the **Activity** section of **Enterprise applications**.</span></span>

<span data-ttu-id="70a81-193">![Auditing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/134.png "Auditing")</span><span class="sxs-lookup"><span data-stu-id="70a81-193">![Auditing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/134.png "Auditing")</span></span>

### <a name="filtering-audit-logs"></a><span data-ttu-id="70a81-194">Filtering audit logs</span><span class="sxs-lookup"><span data-stu-id="70a81-194">Filtering audit logs</span></span>
<span data-ttu-id="70a81-195">You can filter sign-ins to limit the amount of displayed data using the following fields:</span><span class="sxs-lookup"><span data-stu-id="70a81-195">You can filter sign-ins to limit the amount of displayed data using the following fields:</span></span>

* <span data-ttu-id="70a81-196">Date and time</span><span class="sxs-lookup"><span data-stu-id="70a81-196">Date and time</span></span>
* <span data-ttu-id="70a81-197">Actor's user principal name</span><span class="sxs-lookup"><span data-stu-id="70a81-197">Actor's user principal name</span></span>
* <span data-ttu-id="70a81-198">Activity type</span><span class="sxs-lookup"><span data-stu-id="70a81-198">Activity type</span></span>
* <span data-ttu-id="70a81-199">Activity</span><span class="sxs-lookup"><span data-stu-id="70a81-199">Activity</span></span>

<span data-ttu-id="70a81-200">![Auditing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/356.png "Auditing")</span><span class="sxs-lookup"><span data-stu-id="70a81-200">![Auditing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/356.png "Auditing")</span></span>

<span data-ttu-id="70a81-201">The content of the **Activity Type** list, is tied to your entry point to this blade.</span><span class="sxs-lookup"><span data-stu-id="70a81-201">The content of the **Activity Type** list, is tied to your entry point to this blade.</span></span>  
<span data-ttu-id="70a81-202">If your entry point is Azure Active Directory, this list contains all possible activity types:</span><span class="sxs-lookup"><span data-stu-id="70a81-202">If your entry point is Azure Active Directory, this list contains all possible activity types:</span></span>

* <span data-ttu-id="70a81-203">Application</span><span class="sxs-lookup"><span data-stu-id="70a81-203">Application</span></span> 
* <span data-ttu-id="70a81-204">Group</span><span class="sxs-lookup"><span data-stu-id="70a81-204">Group</span></span> 
* <span data-ttu-id="70a81-205">User</span><span class="sxs-lookup"><span data-stu-id="70a81-205">User</span></span>
* <span data-ttu-id="70a81-206">Device</span><span class="sxs-lookup"><span data-stu-id="70a81-206">Device</span></span>
* <span data-ttu-id="70a81-207">Directory</span><span class="sxs-lookup"><span data-stu-id="70a81-207">Directory</span></span>
* <span data-ttu-id="70a81-208">Policy</span><span class="sxs-lookup"><span data-stu-id="70a81-208">Policy</span></span>
* <span data-ttu-id="70a81-209">Other</span><span class="sxs-lookup"><span data-stu-id="70a81-209">Other</span></span>

<span data-ttu-id="70a81-210">![Auditing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/825.png "Auditing")</span><span class="sxs-lookup"><span data-stu-id="70a81-210">![Auditing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/825.png "Auditing")</span></span>

<span data-ttu-id="70a81-211">The listed activities are scoped by activity type.</span><span class="sxs-lookup"><span data-stu-id="70a81-211">The listed activities are scoped by activity type.</span></span>
<span data-ttu-id="70a81-212">For example, if you have **Group** selected as **Activity Type**, the **Activity** list only contains group related activities.</span><span class="sxs-lookup"><span data-stu-id="70a81-212">For example, if you have **Group** selected as **Activity Type**, the **Activity** list only contains group related activities.</span></span>   

<span data-ttu-id="70a81-213">![Auditing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/654.png "Auditing")</span><span class="sxs-lookup"><span data-stu-id="70a81-213">![Auditing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/654.png "Auditing")</span></span>

<span data-ttu-id="70a81-214">Another method to filter the entries of a audit log is to search for specific entries.</span><span class="sxs-lookup"><span data-stu-id="70a81-214">Another method to filter the entries of a audit log is to search for specific entries.</span></span>

<span data-ttu-id="70a81-215">![Auditing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/237.png "Auditing")</span><span class="sxs-lookup"><span data-stu-id="70a81-215">![Auditing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-azure-portal/237.png "Auditing")</span></span>

## <a name="next-steps"></a><span data-ttu-id="70a81-216">Next steps</span><span class="sxs-lookup"><span data-stu-id="70a81-216">Next steps</span></span>
<span data-ttu-id="70a81-217">See the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="70a81-217">See the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>





















