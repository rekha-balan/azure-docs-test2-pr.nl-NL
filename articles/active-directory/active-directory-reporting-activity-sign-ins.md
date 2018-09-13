---
title: Sign-in activity reports in the Azure Active Directory portal - preview | Microsoft Docs
description: Introduction to sign-in activity reports in the Azure Active Directory portal - preview
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: femila
editor: ''
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/06/2017
ms.author: markvi
ms.openlocfilehash: 3fc69bd579a9c31cf45aebf640e500c01dde43b0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553876"
---
# <a name="sign-in-activity-reports-in-the-azure-active-directory-portal---preview"></a><span data-ttu-id="d99d4-103">Sign-in activity reports in the Azure Active Directory portal - preview</span><span class="sxs-lookup"><span data-stu-id="d99d4-103">Sign-in activity reports in the Azure Active Directory portal - preview</span></span>

<span data-ttu-id="d99d4-104">With reporting in the Azure Active Directory [preview](active-directory-preview-explainer.md), you get all the information you need to determine how your environment is doing.</span><span class="sxs-lookup"><span data-stu-id="d99d4-104">With reporting in the Azure Active Directory [preview](active-directory-preview-explainer.md), you get all the information you need to determine how your environment is doing.</span></span>

<span data-ttu-id="d99d4-105">The reporting architecture in Azure Active Directory consists of the following components:</span><span class="sxs-lookup"><span data-stu-id="d99d4-105">The reporting architecture in Azure Active Directory consists of the following components:</span></span>

- <span data-ttu-id="d99d4-106">**Activity**</span><span class="sxs-lookup"><span data-stu-id="d99d4-106">**Activity**</span></span> 
    - <span data-ttu-id="d99d4-107">**Sign-in activities** – Information about the usage of managed applications and user sign-in activities</span><span class="sxs-lookup"><span data-stu-id="d99d4-107">**Sign-in activities** – Information about the usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="d99d4-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span><span class="sxs-lookup"><span data-stu-id="d99d4-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span></span>
- <span data-ttu-id="d99d4-109">**Security**</span><span class="sxs-lookup"><span data-stu-id="d99d4-109">**Security**</span></span> 
    - <span data-ttu-id="d99d4-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span><span class="sxs-lookup"><span data-stu-id="d99d4-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> <span data-ttu-id="d99d4-111">For more details, see Risky sign-ins.</span><span class="sxs-lookup"><span data-stu-id="d99d4-111">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="d99d4-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span><span class="sxs-lookup"><span data-stu-id="d99d4-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="d99d4-113">For more details, see Users flagged for risk.</span><span class="sxs-lookup"><span data-stu-id="d99d4-113">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="d99d4-114">This topic gives you an overview of the sign-in activities.</span><span class="sxs-lookup"><span data-stu-id="d99d4-114">This topic gives you an overview of the sign-in activities.</span></span>

## <a name="signs-in-activities"></a><span data-ttu-id="d99d4-115">Signs-in activities</span><span class="sxs-lookup"><span data-stu-id="d99d4-115">Signs-in activities</span></span>

<span data-ttu-id="d99d4-116">With the information provided by the user sign-in report, you find answers to questions such as:</span><span class="sxs-lookup"><span data-stu-id="d99d4-116">With the information provided by the user sign-in report, you find answers to questions such as:</span></span>

* <span data-ttu-id="d99d4-117">What is the sign-in pattern of a user?</span><span class="sxs-lookup"><span data-stu-id="d99d4-117">What is the sign-in pattern of a user?</span></span>
* <span data-ttu-id="d99d4-118">How many users have users signed in over a week?</span><span class="sxs-lookup"><span data-stu-id="d99d4-118">How many users have users signed in over a week?</span></span>
* <span data-ttu-id="d99d4-119">What’s the status of these sign-ins?</span><span class="sxs-lookup"><span data-stu-id="d99d4-119">What’s the status of these sign-ins?</span></span>

<span data-ttu-id="d99d4-120">Your first entry point to all sign-in activities data is **Sign-ins** in the Activity section of **Azure Active**.</span><span class="sxs-lookup"><span data-stu-id="d99d4-120">Your first entry point to all sign-in activities data is **Sign-ins** in the Activity section of **Azure Active**.</span></span> <span data-ttu-id="d99d4-121">Directory.</span><span class="sxs-lookup"><span data-stu-id="d99d4-121">Directory.</span></span>


<span data-ttu-id="d99d4-122">![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/61.png "Sign-in activity")</span><span class="sxs-lookup"><span data-stu-id="d99d4-122">![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/61.png "Sign-in activity")</span></span>


<span data-ttu-id="d99d4-123">An audit log has a default list view that shows:</span><span class="sxs-lookup"><span data-stu-id="d99d4-123">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="d99d4-124">the related user</span><span class="sxs-lookup"><span data-stu-id="d99d4-124">the related user</span></span>
- <span data-ttu-id="d99d4-125">the application the user has signed-in to</span><span class="sxs-lookup"><span data-stu-id="d99d4-125">the application the user has signed-in to</span></span>
- <span data-ttu-id="d99d4-126">the sign-in status</span><span class="sxs-lookup"><span data-stu-id="d99d4-126">the sign-in status</span></span>
- <span data-ttu-id="d99d4-127">the sign-in time</span><span class="sxs-lookup"><span data-stu-id="d99d4-127">the sign-in time</span></span>

<span data-ttu-id="d99d4-128">![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span><span class="sxs-lookup"><span data-stu-id="d99d4-128">![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="d99d4-129">You can customize the list view by clicking **Columns** in the toolbar.</span><span class="sxs-lookup"><span data-stu-id="d99d4-129">You can customize the list view by clicking **Columns** in the toolbar.</span></span>

<span data-ttu-id="d99d4-130">![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/19.png "Sign-in activity")</span><span class="sxs-lookup"><span data-stu-id="d99d4-130">![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/19.png "Sign-in activity")</span></span>

<span data-ttu-id="d99d4-131">This enables you to display additional fields or remove fields that are already displayed.</span><span class="sxs-lookup"><span data-stu-id="d99d4-131">This enables you to display additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="d99d4-132">![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/42.png "Sign-in activity")</span><span class="sxs-lookup"><span data-stu-id="d99d4-132">![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/42.png "Sign-in activity")</span></span>

<span data-ttu-id="d99d4-133">By clicking an item in the list view, you get all available details about it.</span><span class="sxs-lookup"><span data-stu-id="d99d4-133">By clicking an item in the list view, you get all available details about it.</span></span>

<span data-ttu-id="d99d4-134">![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/43.png "Sign-in activity")</span><span class="sxs-lookup"><span data-stu-id="d99d4-134">![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/43.png "Sign-in activity")</span></span>


## <a name="filtering-sign-in-activities"></a><span data-ttu-id="d99d4-135">Filtering sign-in activities</span><span class="sxs-lookup"><span data-stu-id="d99d4-135">Filtering sign-in activities</span></span>

<span data-ttu-id="d99d4-136">To narrow down the reported data to a level that works for you, you can filter the sign-ins data using the following fields:</span><span class="sxs-lookup"><span data-stu-id="d99d4-136">To narrow down the reported data to a level that works for you, you can filter the sign-ins data using the following fields:</span></span>

- <span data-ttu-id="d99d4-137">Time interval</span><span class="sxs-lookup"><span data-stu-id="d99d4-137">Time interval</span></span>
- <span data-ttu-id="d99d4-138">User</span><span class="sxs-lookup"><span data-stu-id="d99d4-138">User</span></span>
- <span data-ttu-id="d99d4-139">Application</span><span class="sxs-lookup"><span data-stu-id="d99d4-139">Application</span></span>
- <span data-ttu-id="d99d4-140">Client</span><span class="sxs-lookup"><span data-stu-id="d99d4-140">Client</span></span>
- <span data-ttu-id="d99d4-141">Sign-in status</span><span class="sxs-lookup"><span data-stu-id="d99d4-141">Sign-in status</span></span>

<span data-ttu-id="d99d4-142">![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/44.png "Sign-in activity")</span><span class="sxs-lookup"><span data-stu-id="d99d4-142">![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/44.png "Sign-in activity")</span></span>


<span data-ttu-id="d99d4-143">The **time interval** filter enables to you to define a timeframe for the returned data.</span><span class="sxs-lookup"><span data-stu-id="d99d4-143">The **time interval** filter enables to you to define a timeframe for the returned data.</span></span>  
<span data-ttu-id="d99d4-144">Possible values are:</span><span class="sxs-lookup"><span data-stu-id="d99d4-144">Possible values are:</span></span>

- <span data-ttu-id="d99d4-145">1 month</span><span class="sxs-lookup"><span data-stu-id="d99d4-145">1 month</span></span>
- <span data-ttu-id="d99d4-146">7 days</span><span class="sxs-lookup"><span data-stu-id="d99d4-146">7 days</span></span>
- <span data-ttu-id="d99d4-147">24 hours</span><span class="sxs-lookup"><span data-stu-id="d99d4-147">24 hours</span></span>
- <span data-ttu-id="d99d4-148">Custom</span><span class="sxs-lookup"><span data-stu-id="d99d4-148">Custom</span></span>

<span data-ttu-id="d99d4-149">When you select a custom timeframe, you can configure a start time and an end time.</span><span class="sxs-lookup"><span data-stu-id="d99d4-149">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="d99d4-150">The **user** filter enables you to specify the name or the user principal name (UPN) of the user you care about.</span><span class="sxs-lookup"><span data-stu-id="d99d4-150">The **user** filter enables you to specify the name or the user principal name (UPN) of the user you care about.</span></span>

<span data-ttu-id="d99d4-151">The **application** filter enables you to specify the name of the application you care about.</span><span class="sxs-lookup"><span data-stu-id="d99d4-151">The **application** filter enables you to specify the name of the application you care about.</span></span>

<span data-ttu-id="d99d4-152">The **client** filter enables you to specify information about the device you care about.</span><span class="sxs-lookup"><span data-stu-id="d99d4-152">The **client** filter enables you to specify information about the device you care about.</span></span>

<span data-ttu-id="d99d4-153">The **sign-in status** filter enables you to select one of the following filter:</span><span class="sxs-lookup"><span data-stu-id="d99d4-153">The **sign-in status** filter enables you to select one of the following filter:</span></span>

- <span data-ttu-id="d99d4-154">All</span><span class="sxs-lookup"><span data-stu-id="d99d4-154">All</span></span>
- <span data-ttu-id="d99d4-155">Success</span><span class="sxs-lookup"><span data-stu-id="d99d4-155">Success</span></span>
- <span data-ttu-id="d99d4-156">Failure</span><span class="sxs-lookup"><span data-stu-id="d99d4-156">Failure</span></span>


## <a name="sign-in-activities-shortcuts"></a><span data-ttu-id="d99d4-157">Sign-in activities shortcuts</span><span class="sxs-lookup"><span data-stu-id="d99d4-157">Sign-in activities shortcuts</span></span>

<span data-ttu-id="d99d4-158">In addition to Azure Active Directory, the Azure portal provides you with two additional entry points to sign-in activities data:</span><span class="sxs-lookup"><span data-stu-id="d99d4-158">In addition to Azure Active Directory, the Azure portal provides you with two additional entry points to sign-in activities data:</span></span>

- <span data-ttu-id="d99d4-159">Users and groups</span><span class="sxs-lookup"><span data-stu-id="d99d4-159">Users and groups</span></span>
- <span data-ttu-id="d99d4-160">Enterprise applications</span><span class="sxs-lookup"><span data-stu-id="d99d4-160">Enterprise applications</span></span>


### <a name="users-and-groups-sign-ins-activities"></a><span data-ttu-id="d99d4-161">Users and groups sign-ins activities</span><span class="sxs-lookup"><span data-stu-id="d99d4-161">Users and groups sign-ins activities</span></span>

<span data-ttu-id="d99d4-162">With the information provided by the user sign-in report, you find answers to questions such as:</span><span class="sxs-lookup"><span data-stu-id="d99d4-162">With the information provided by the user sign-in report, you find answers to questions such as:</span></span>

- <span data-ttu-id="d99d4-163">What is the sign-in pattern of a user?</span><span class="sxs-lookup"><span data-stu-id="d99d4-163">What is the sign-in pattern of a user?</span></span>
- <span data-ttu-id="d99d4-164">How many users have users signed in over a week?</span><span class="sxs-lookup"><span data-stu-id="d99d4-164">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="d99d4-165">What’s the status of these sign-ins?</span><span class="sxs-lookup"><span data-stu-id="d99d4-165">What’s the status of these sign-ins?</span></span>



<span data-ttu-id="d99d4-166">Your entry point to this data is the user sign-in graph in the **Overview** section under **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="d99d4-166">Your entry point to this data is the user sign-in graph in the **Overview** section under **Users and groups**.</span></span>

<span data-ttu-id="d99d4-167">![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/45.png "Sign-in activity")</span><span class="sxs-lookup"><span data-stu-id="d99d4-167">![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/45.png "Sign-in activity")</span></span>

<span data-ttu-id="d99d4-168">The user sign-in graph shows weekly aggregations of sign ins for all users in a given time period.</span><span class="sxs-lookup"><span data-stu-id="d99d4-168">The user sign-in graph shows weekly aggregations of sign ins for all users in a given time period.</span></span> <span data-ttu-id="d99d4-169">The default for the time period is 30 days.</span><span class="sxs-lookup"><span data-stu-id="d99d4-169">The default for the time period is 30 days.</span></span>

<span data-ttu-id="d99d4-170">![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/46.png "Sign-in activity")</span><span class="sxs-lookup"><span data-stu-id="d99d4-170">![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/46.png "Sign-in activity")</span></span>

<span data-ttu-id="d99d4-171">When you click on a day in the sign-in graph, you get a detailed list of the sign-in activities for this day.</span><span class="sxs-lookup"><span data-stu-id="d99d4-171">When you click on a day in the sign-in graph, you get a detailed list of the sign-in activities for this day.</span></span>

<span data-ttu-id="d99d4-172">![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span><span class="sxs-lookup"><span data-stu-id="d99d4-172">![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="d99d4-173">Each row in the sign-in activities list gives you the detailed information about the selected sign-in such as:</span><span class="sxs-lookup"><span data-stu-id="d99d4-173">Each row in the sign-in activities list gives you the detailed information about the selected sign-in such as:</span></span>

* <span data-ttu-id="d99d4-174">Who has signed in?</span><span class="sxs-lookup"><span data-stu-id="d99d4-174">Who has signed in?</span></span>
* <span data-ttu-id="d99d4-175">What was the related UPN?</span><span class="sxs-lookup"><span data-stu-id="d99d4-175">What was the related UPN?</span></span>
* <span data-ttu-id="d99d4-176">What application was the target of the sign-in?</span><span class="sxs-lookup"><span data-stu-id="d99d4-176">What application was the target of the sign-in?</span></span>
* <span data-ttu-id="d99d4-177">What is the IP address of the sign-in?</span><span class="sxs-lookup"><span data-stu-id="d99d4-177">What is the IP address of the sign-in?</span></span>
* <span data-ttu-id="d99d4-178">What was the status of the sign-in?</span><span class="sxs-lookup"><span data-stu-id="d99d4-178">What was the status of the sign-in?</span></span>

<span data-ttu-id="d99d4-179">The **Sign-ins** option gives you a complete overview of all user sign-ins.</span><span class="sxs-lookup"><span data-stu-id="d99d4-179">The **Sign-ins** option gives you a complete overview of all user sign-ins.</span></span>

<span data-ttu-id="d99d4-180">![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/51.png "Sign-in activity")</span><span class="sxs-lookup"><span data-stu-id="d99d4-180">![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/51.png "Sign-in activity")</span></span>



## <a name="usage-of-managed-applications"></a><span data-ttu-id="d99d4-181">Usage of managed applications</span><span class="sxs-lookup"><span data-stu-id="d99d4-181">Usage of managed applications</span></span>

<span data-ttu-id="d99d4-182">With an application-centric view of your sign-in data, you can answer questions such as:</span><span class="sxs-lookup"><span data-stu-id="d99d4-182">With an application-centric view of your sign-in data, you can answer questions such as:</span></span>

* <span data-ttu-id="d99d4-183">Who is using my applications?</span><span class="sxs-lookup"><span data-stu-id="d99d4-183">Who is using my applications?</span></span>
* <span data-ttu-id="d99d4-184">What are the top 3 applications in your organization?</span><span class="sxs-lookup"><span data-stu-id="d99d4-184">What are the top 3 applications in your organization?</span></span>
* <span data-ttu-id="d99d4-185">I have recently rolled out an application.</span><span class="sxs-lookup"><span data-stu-id="d99d4-185">I have recently rolled out an application.</span></span> <span data-ttu-id="d99d4-186">How is it doing?</span><span class="sxs-lookup"><span data-stu-id="d99d4-186">How is it doing?</span></span>

<span data-ttu-id="d99d4-187">Your entry point to this data is the top 3 applications in your organization within the last 30 days report in the **Overview** section under **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="d99d4-187">Your entry point to this data is the top 3 applications in your organization within the last 30 days report in the **Overview** section under **Enterprise applications**.</span></span>

<span data-ttu-id="d99d4-188">![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/64.png "Sign-in activity")</span><span class="sxs-lookup"><span data-stu-id="d99d4-188">![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/64.png "Sign-in activity")</span></span>

<span data-ttu-id="d99d4-189">The app usage graph weekly aggregations of sign ins for your top 3 applications in a given time period.</span><span class="sxs-lookup"><span data-stu-id="d99d4-189">The app usage graph weekly aggregations of sign ins for your top 3 applications in a given time period.</span></span> <span data-ttu-id="d99d4-190">The default for the time period is 30 days.</span><span class="sxs-lookup"><span data-stu-id="d99d4-190">The default for the time period is 30 days.</span></span>

<span data-ttu-id="d99d4-191">![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/47.png "Sign-in activity")</span><span class="sxs-lookup"><span data-stu-id="d99d4-191">![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/47.png "Sign-in activity")</span></span>

<span data-ttu-id="d99d4-192">If you want to, you can set the focus on a specific application.</span><span class="sxs-lookup"><span data-stu-id="d99d4-192">If you want to, you can set the focus on a specific application.</span></span>


<span data-ttu-id="d99d4-193">![Reporting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Reporting")</span><span class="sxs-lookup"><span data-stu-id="d99d4-193">![Reporting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Reporting")</span></span>

<span data-ttu-id="d99d4-194">When you click on a day in the app usage graph, you get a detailed list of the sign-in activities.</span><span class="sxs-lookup"><span data-stu-id="d99d4-194">When you click on a day in the app usage graph, you get a detailed list of the sign-in activities.</span></span>


<span data-ttu-id="d99d4-195">![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/48.png "Sign-in activity")</span><span class="sxs-lookup"><span data-stu-id="d99d4-195">![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/48.png "Sign-in activity")</span></span>


<span data-ttu-id="d99d4-196">The **Sign-ins** option gives you a complete overview of all sign-in events to your applications.</span><span class="sxs-lookup"><span data-stu-id="d99d4-196">The **Sign-ins** option gives you a complete overview of all sign-in events to your applications.</span></span>

<span data-ttu-id="d99d4-197">![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/49.png "Sign-in activity")</span><span class="sxs-lookup"><span data-stu-id="d99d4-197">![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/49.png "Sign-in activity")</span></span>



## <a name="next-steps"></a><span data-ttu-id="d99d4-198">Next steps</span><span class="sxs-lookup"><span data-stu-id="d99d4-198">Next steps</span></span>
<span data-ttu-id="d99d4-199">See the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="d99d4-199">See the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>
















