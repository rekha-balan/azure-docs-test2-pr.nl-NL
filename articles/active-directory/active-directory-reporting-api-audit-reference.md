---
title: Azure Active Directory audit API reference | Microsoft Docs
description: How to get started with the Azure Active Directory audit API
services: active-directory
documentationcenter: ''
author: markusvi
manager: femila
editor: ''
ms.assetid: 44e46be8-09e5-4981-be2b-d474aaa92792
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/05/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 87c7990834eaf2aa6c4aff0c341150ba9bd9eed4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661571"
---
# <a name="azure-active-directory-audit-api-reference"></a><span data-ttu-id="4cc18-103">Azure Active Directory audit API reference</span><span class="sxs-lookup"><span data-stu-id="4cc18-103">Azure Active Directory audit API reference</span></span>
<span data-ttu-id="4cc18-104">This topic is part of a collection of topics about the Azure Active Directory reporting API.</span><span class="sxs-lookup"><span data-stu-id="4cc18-104">This topic is part of a collection of topics about the Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="4cc18-105">Azure AD reporting provides you with an API that enables you to access audit data using code or related tools.</span><span class="sxs-lookup"><span data-stu-id="4cc18-105">Azure AD reporting provides you with an API that enables you to access audit data using code or related tools.</span></span>
<span data-ttu-id="4cc18-106">The scope of this topic is to provide you with reference information about the **audit API**.</span><span class="sxs-lookup"><span data-stu-id="4cc18-106">The scope of this topic is to provide you with reference information about the **audit API**.</span></span>

<span data-ttu-id="4cc18-107">See:</span><span class="sxs-lookup"><span data-stu-id="4cc18-107">See:</span></span>

* <span data-ttu-id="4cc18-108">[Audit logs](active-directory-reporting-azure-portal.md#audit-logs)  for more conceptual information</span><span class="sxs-lookup"><span data-stu-id="4cc18-108">[Audit logs](active-directory-reporting-azure-portal.md#audit-logs)  for more conceptual information</span></span>
* <span data-ttu-id="4cc18-109">[Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about the reporting API.</span><span class="sxs-lookup"><span data-stu-id="4cc18-109">[Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about the reporting API.</span></span>

<span data-ttu-id="4cc18-110">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="4cc18-110">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="who-can-access-the-data"></a><span data-ttu-id="4cc18-111">Who can access the data?</span><span class="sxs-lookup"><span data-stu-id="4cc18-111">Who can access the data?</span></span>
* <span data-ttu-id="4cc18-112">Users in the Security Admin or Security Reader role</span><span class="sxs-lookup"><span data-stu-id="4cc18-112">Users in the Security Admin or Security Reader role</span></span>
* <span data-ttu-id="4cc18-113">Global Admins</span><span class="sxs-lookup"><span data-stu-id="4cc18-113">Global Admins</span></span>
* <span data-ttu-id="4cc18-114">Any app that has authorization to access the API (app authorization can be setup only based on Global Admin’s permission)</span><span class="sxs-lookup"><span data-stu-id="4cc18-114">Any app that has authorization to access the API (app authorization can be setup only based on Global Admin’s permission)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4cc18-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4cc18-115">Prerequisites</span></span>
<span data-ttu-id="4cc18-116">In order to access this report through the Reporting API, you must have:</span><span class="sxs-lookup"><span data-stu-id="4cc18-116">In order to access this report through the Reporting API, you must have:</span></span>

* <span data-ttu-id="4cc18-117">An [Azure Active Directory Free or better edition](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="4cc18-117">An [Azure Active Directory Free or better edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="4cc18-118">Completed the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="4cc18-118">Completed the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-the-api"></a><span data-ttu-id="4cc18-119">Accessing the API</span><span class="sxs-lookup"><span data-stu-id="4cc18-119">Accessing the API</span></span>
<span data-ttu-id="4cc18-120">You can either access this API through the [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4cc18-120">You can either access this API through the [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="4cc18-121">In order for PowerShell to correctly interpret the OData filter syntax used in AAD Graph REST calls, you must use the backtick (aka: grave accent) character to “escape” the $ character.</span><span class="sxs-lookup"><span data-stu-id="4cc18-121">In order for PowerShell to correctly interpret the OData filter syntax used in AAD Graph REST calls, you must use the backtick (aka: grave accent) character to “escape” the $ character.</span></span> <span data-ttu-id="4cc18-122">The backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell to do a literal interpretation of the $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span><span class="sxs-lookup"><span data-stu-id="4cc18-122">The backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell to do a literal interpretation of the $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="4cc18-123">The focus of this topic is on the Graph Explorer.</span><span class="sxs-lookup"><span data-stu-id="4cc18-123">The focus of this topic is on the Graph Explorer.</span></span> <span data-ttu-id="4cc18-124">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-audit-samples.md#powershell-script).</span><span class="sxs-lookup"><span data-stu-id="4cc18-124">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-audit-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="4cc18-125">API Endpoint</span><span class="sxs-lookup"><span data-stu-id="4cc18-125">API Endpoint</span></span>
<span data-ttu-id="4cc18-126">You can access this API using the following URI:</span><span class="sxs-lookup"><span data-stu-id="4cc18-126">You can access this API using the following URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta

<span data-ttu-id="4cc18-127">There is no limit on the number of records returned by the Azure AD audit API (using OData pagination).</span><span class="sxs-lookup"><span data-stu-id="4cc18-127">There is no limit on the number of records returned by the Azure AD audit API (using OData pagination).</span></span>
<span data-ttu-id="4cc18-128">For retention limits on reporting data, check out [Reporting Retention Policies](active-directory-reporting-retention.md).</span><span class="sxs-lookup"><span data-stu-id="4cc18-128">For retention limits on reporting data, check out [Reporting Retention Policies](active-directory-reporting-retention.md).</span></span>

<span data-ttu-id="4cc18-129">This call returns the data in batches.</span><span class="sxs-lookup"><span data-stu-id="4cc18-129">This call returns the data in batches.</span></span> <span data-ttu-id="4cc18-130">Each batch has a maximum of 1000 records.</span><span class="sxs-lookup"><span data-stu-id="4cc18-130">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="4cc18-131">To get the next batch of records, use the Next link.</span><span class="sxs-lookup"><span data-stu-id="4cc18-131">To get the next batch of records, use the Next link.</span></span> <span data-ttu-id="4cc18-132">Get the skiptoken information from the first set of returned records.</span><span class="sxs-lookup"><span data-stu-id="4cc18-132">Get the skiptoken information from the first set of returned records.</span></span> <span data-ttu-id="4cc18-133">The skip token will be at the end of the result set.</span><span class="sxs-lookup"><span data-stu-id="4cc18-133">The skip token will be at the end of the result set.</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta&%24skiptoken=-1339686058




## <a name="supported-filters"></a><span data-ttu-id="4cc18-134">Supported filters</span><span class="sxs-lookup"><span data-stu-id="4cc18-134">Supported filters</span></span>
<span data-ttu-id="4cc18-135">You can narrow down the number of records that are returned by an API call in form of a filter.</span><span class="sxs-lookup"><span data-stu-id="4cc18-135">You can narrow down the number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="4cc18-136">For sign-in API related data, the following filters are supported:</span><span class="sxs-lookup"><span data-stu-id="4cc18-136">For sign-in API related data, the following filters are supported:</span></span>

* <span data-ttu-id="4cc18-137">**$top=\<number of records to be returned\>** - to limit the number of returned records.</span><span class="sxs-lookup"><span data-stu-id="4cc18-137">**$top=\<number of records to be returned\>** - to limit the number of returned records.</span></span> <span data-ttu-id="4cc18-138">This is an expensive operation.</span><span class="sxs-lookup"><span data-stu-id="4cc18-138">This is an expensive operation.</span></span> <span data-ttu-id="4cc18-139">You should not use this filter if you want to return thousands of objects.</span><span class="sxs-lookup"><span data-stu-id="4cc18-139">You should not use this filter if you want to return thousands of objects.</span></span>     
* <span data-ttu-id="4cc18-140">**$filter=\<your filter statement\>** - to specify, on the basis of supported filter fields, the type of records you care about</span><span class="sxs-lookup"><span data-stu-id="4cc18-140">**$filter=\<your filter statement\>** - to specify, on the basis of supported filter fields, the type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="4cc18-141">Supported filter fields and operators</span><span class="sxs-lookup"><span data-stu-id="4cc18-141">Supported filter fields and operators</span></span>
<span data-ttu-id="4cc18-142">To specify the type of records you care about, you can build a filter statement that can contain either one or a combination of the following filter fields:</span><span class="sxs-lookup"><span data-stu-id="4cc18-142">To specify the type of records you care about, you can build a filter statement that can contain either one or a combination of the following filter fields:</span></span>

* <span data-ttu-id="4cc18-143">[activityDate](#activitydate)  - defines a date or date range</span><span class="sxs-lookup"><span data-stu-id="4cc18-143">[activityDate](#activitydate)  - defines a date or date range</span></span>
* <span data-ttu-id="4cc18-144">[category](#category) - defines the category you want to filter on.</span><span class="sxs-lookup"><span data-stu-id="4cc18-144">[category](#category) - defines the category you want to filter on.</span></span>
* <span data-ttu-id="4cc18-145">[activityStatus](#activitystatus) - defines the status of an activity</span><span class="sxs-lookup"><span data-stu-id="4cc18-145">[activityStatus](#activitystatus) - defines the status of an activity</span></span>
* <span data-ttu-id="4cc18-146">[activityType](#activitytype)  - defines the type of an activity</span><span class="sxs-lookup"><span data-stu-id="4cc18-146">[activityType](#activitytype)  - defines the type of an activity</span></span>
* <span data-ttu-id="4cc18-147">[activity](#activity) - defines the activity as string</span><span class="sxs-lookup"><span data-stu-id="4cc18-147">[activity](#activity) - defines the activity as string</span></span>  
* <span data-ttu-id="4cc18-148">[actor/name](#actorname) -   defines the actor in form of the actor's name</span><span class="sxs-lookup"><span data-stu-id="4cc18-148">[actor/name](#actorname) -   defines the actor in form of the actor's name</span></span>
* <span data-ttu-id="4cc18-149">[actor/objectid](#actorobjectid) - defines the actor in form of the actor's ID</span><span class="sxs-lookup"><span data-stu-id="4cc18-149">[actor/objectid](#actorobjectid) - defines the actor in form of the actor's ID</span></span>   
* <span data-ttu-id="4cc18-150">[actor/upn](#actorupn)  - defines the actor in form of the actor's user principle name (UPN)</span><span class="sxs-lookup"><span data-stu-id="4cc18-150">[actor/upn](#actorupn)  - defines the actor in form of the actor's user principle name (UPN)</span></span> 
* <span data-ttu-id="4cc18-151">[target/name](#targetname)  - defines the target in form of the actor's name</span><span class="sxs-lookup"><span data-stu-id="4cc18-151">[target/name](#targetname)  - defines the target in form of the actor's name</span></span>
* <span data-ttu-id="4cc18-152">[target/objectid](#targetobjectid) - defines the target in form of the target's ID</span><span class="sxs-lookup"><span data-stu-id="4cc18-152">[target/objectid](#targetobjectid) - defines the target in form of the target's ID</span></span>  
* <span data-ttu-id="4cc18-153">[target/upn](#targetupn) - defines the actor in form of the actor's user principle name (UPN)</span><span class="sxs-lookup"><span data-stu-id="4cc18-153">[target/upn](#targetupn) - defines the actor in form of the actor's user principle name (UPN)</span></span>   

- - -
### <a name="activitydate"></a><span data-ttu-id="4cc18-154">activityDate</span><span class="sxs-lookup"><span data-stu-id="4cc18-154">activityDate</span></span>
<span data-ttu-id="4cc18-155">**Supported operators**: eq, ge, le, gt, lt</span><span class="sxs-lookup"><span data-stu-id="4cc18-155">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="4cc18-156">**Example**:</span><span class="sxs-lookup"><span data-stu-id="4cc18-156">**Example**:</span></span>

    $filter=tdomain + 'activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago    

<span data-ttu-id="4cc18-157">**Notes**:</span><span class="sxs-lookup"><span data-stu-id="4cc18-157">**Notes**:</span></span>

<span data-ttu-id="4cc18-158">datetime should be in UTC format</span><span class="sxs-lookup"><span data-stu-id="4cc18-158">datetime should be in UTC format</span></span>

- - -
### <a name="category"></a><span data-ttu-id="4cc18-159">category</span><span class="sxs-lookup"><span data-stu-id="4cc18-159">category</span></span>

<span data-ttu-id="4cc18-160">**Supported values**:</span><span class="sxs-lookup"><span data-stu-id="4cc18-160">**Supported values**:</span></span>

| <span data-ttu-id="4cc18-161">Category</span><span class="sxs-lookup"><span data-stu-id="4cc18-161">Category</span></span>                         | <span data-ttu-id="4cc18-162">Value</span><span class="sxs-lookup"><span data-stu-id="4cc18-162">Value</span></span>     |
| :--                              | ---       |
| <span data-ttu-id="4cc18-163">Core Directory</span><span class="sxs-lookup"><span data-stu-id="4cc18-163">Core Directory</span></span>                   | <span data-ttu-id="4cc18-164">Directory</span><span class="sxs-lookup"><span data-stu-id="4cc18-164">Directory</span></span> |
| <span data-ttu-id="4cc18-165">Self-service Password Management</span><span class="sxs-lookup"><span data-stu-id="4cc18-165">Self-service Password Management</span></span> | <span data-ttu-id="4cc18-166">SSPR</span><span class="sxs-lookup"><span data-stu-id="4cc18-166">SSPR</span></span>      |
| <span data-ttu-id="4cc18-167">Self-service Group Management</span><span class="sxs-lookup"><span data-stu-id="4cc18-167">Self-service Group Management</span></span>    | <span data-ttu-id="4cc18-168">SSGM</span><span class="sxs-lookup"><span data-stu-id="4cc18-168">SSGM</span></span>      |
| <span data-ttu-id="4cc18-169">Account Provisioning</span><span class="sxs-lookup"><span data-stu-id="4cc18-169">Account Provisioning</span></span>             | <span data-ttu-id="4cc18-170">Sync</span><span class="sxs-lookup"><span data-stu-id="4cc18-170">Sync</span></span>      |
| <span data-ttu-id="4cc18-171">Automated Password Rollover</span><span class="sxs-lookup"><span data-stu-id="4cc18-171">Automated Password Rollover</span></span>      | <span data-ttu-id="4cc18-172">Automated Password Rollover</span><span class="sxs-lookup"><span data-stu-id="4cc18-172">Automated Password Rollover</span></span> |
| <span data-ttu-id="4cc18-173">Identity Protection</span><span class="sxs-lookup"><span data-stu-id="4cc18-173">Identity Protection</span></span>              | <span data-ttu-id="4cc18-174">IdentityProtection</span><span class="sxs-lookup"><span data-stu-id="4cc18-174">IdentityProtection</span></span> |
| <span data-ttu-id="4cc18-175">Invited Users</span><span class="sxs-lookup"><span data-stu-id="4cc18-175">Invited Users</span></span>                    | <span data-ttu-id="4cc18-176">Invited Users</span><span class="sxs-lookup"><span data-stu-id="4cc18-176">Invited Users</span></span> |
| <span data-ttu-id="4cc18-177">MIM Service</span><span class="sxs-lookup"><span data-stu-id="4cc18-177">MIM Service</span></span>                      | <span data-ttu-id="4cc18-178">MIM Service</span><span class="sxs-lookup"><span data-stu-id="4cc18-178">MIM Service</span></span> |



<span data-ttu-id="4cc18-179">**Supported operators**: eq</span><span class="sxs-lookup"><span data-stu-id="4cc18-179">**Supported operators**: eq</span></span>

<span data-ttu-id="4cc18-180">**Example**:</span><span class="sxs-lookup"><span data-stu-id="4cc18-180">**Example**:</span></span>

    $filter=category eq 'SSPR'
- - -
### <a name="activitystatus"></a><span data-ttu-id="4cc18-181">activityStatus</span><span class="sxs-lookup"><span data-stu-id="4cc18-181">activityStatus</span></span>

<span data-ttu-id="4cc18-182">**Supported values**:</span><span class="sxs-lookup"><span data-stu-id="4cc18-182">**Supported values**:</span></span>

| <span data-ttu-id="4cc18-183">Activity Status</span><span class="sxs-lookup"><span data-stu-id="4cc18-183">Activity Status</span></span> | <span data-ttu-id="4cc18-184">Value</span><span class="sxs-lookup"><span data-stu-id="4cc18-184">Value</span></span> |
| :--             | ---   |
| <span data-ttu-id="4cc18-185">Success</span><span class="sxs-lookup"><span data-stu-id="4cc18-185">Success</span></span>         | <span data-ttu-id="4cc18-186">0</span><span class="sxs-lookup"><span data-stu-id="4cc18-186">0</span></span>     |
| <span data-ttu-id="4cc18-187">Failure</span><span class="sxs-lookup"><span data-stu-id="4cc18-187">Failure</span></span>         | <span data-ttu-id="4cc18-188">- 1</span><span class="sxs-lookup"><span data-stu-id="4cc18-188">- 1</span></span>   |

<span data-ttu-id="4cc18-189">**Supported operators**: eq</span><span class="sxs-lookup"><span data-stu-id="4cc18-189">**Supported operators**: eq</span></span>

<span data-ttu-id="4cc18-190">**Example**:</span><span class="sxs-lookup"><span data-stu-id="4cc18-190">**Example**:</span></span>

    $filter=activityStatus eq -1    

---
### <a name="activitytype"></a><span data-ttu-id="4cc18-191">activityType</span><span class="sxs-lookup"><span data-stu-id="4cc18-191">activityType</span></span>
<span data-ttu-id="4cc18-192">**Supported operators**: eq</span><span class="sxs-lookup"><span data-stu-id="4cc18-192">**Supported operators**: eq</span></span>

<span data-ttu-id="4cc18-193">**Example**:</span><span class="sxs-lookup"><span data-stu-id="4cc18-193">**Example**:</span></span>

    $filter=activityType eq 'User'    

<span data-ttu-id="4cc18-194">**Notes**:</span><span class="sxs-lookup"><span data-stu-id="4cc18-194">**Notes**:</span></span>

<span data-ttu-id="4cc18-195">case-sensitive</span><span class="sxs-lookup"><span data-stu-id="4cc18-195">case-sensitive</span></span>

- - -
### <a name="activity"></a><span data-ttu-id="4cc18-196">activity</span><span class="sxs-lookup"><span data-stu-id="4cc18-196">activity</span></span>
<span data-ttu-id="4cc18-197">**Supported operators**: eq, contains, startsWith</span><span class="sxs-lookup"><span data-stu-id="4cc18-197">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="4cc18-198">**Example**:</span><span class="sxs-lookup"><span data-stu-id="4cc18-198">**Example**:</span></span>

    $filter=activity eq 'Add application' or contains(activity, 'Application') or startsWith(activity, 'Add')    

<span data-ttu-id="4cc18-199">**Notes**:</span><span class="sxs-lookup"><span data-stu-id="4cc18-199">**Notes**:</span></span>

<span data-ttu-id="4cc18-200">case-sensitive</span><span class="sxs-lookup"><span data-stu-id="4cc18-200">case-sensitive</span></span>

- - -
### <a name="actorname"></a><span data-ttu-id="4cc18-201">actor/name</span><span class="sxs-lookup"><span data-stu-id="4cc18-201">actor/name</span></span>
<span data-ttu-id="4cc18-202">**Supported operators**: eq, contains, startsWith</span><span class="sxs-lookup"><span data-stu-id="4cc18-202">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="4cc18-203">**Example**:</span><span class="sxs-lookup"><span data-stu-id="4cc18-203">**Example**:</span></span>

    $filter=actor/name eq 'test' or contains(actor/name, 'test') or startswith(actor/name, 'test')    

<span data-ttu-id="4cc18-204">**Notes**:</span><span class="sxs-lookup"><span data-stu-id="4cc18-204">**Notes**:</span></span>

<span data-ttu-id="4cc18-205">case-insensitive</span><span class="sxs-lookup"><span data-stu-id="4cc18-205">case-insensitive</span></span>

- - -
### <a name="actorobjectid"></a><span data-ttu-id="4cc18-206">actor/objectId</span><span class="sxs-lookup"><span data-stu-id="4cc18-206">actor/objectId</span></span>
<span data-ttu-id="4cc18-207">**Supported operators**: eq</span><span class="sxs-lookup"><span data-stu-id="4cc18-207">**Supported operators**: eq</span></span>

<span data-ttu-id="4cc18-208">**Example**:</span><span class="sxs-lookup"><span data-stu-id="4cc18-208">**Example**:</span></span>

    $filter=actor/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba'    


- - -
### <a name="targetname"></a><span data-ttu-id="4cc18-209">target/name</span><span class="sxs-lookup"><span data-stu-id="4cc18-209">target/name</span></span>
<span data-ttu-id="4cc18-210">**Supported operators**: eq, contains, startsWith</span><span class="sxs-lookup"><span data-stu-id="4cc18-210">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="4cc18-211">**Example**:</span><span class="sxs-lookup"><span data-stu-id="4cc18-211">**Example**:</span></span>

    $filter=targets/any(t: t/name eq 'some name')    

<span data-ttu-id="4cc18-212">**Notes**:</span><span class="sxs-lookup"><span data-stu-id="4cc18-212">**Notes**:</span></span>

<span data-ttu-id="4cc18-213">Case-insensitive</span><span class="sxs-lookup"><span data-stu-id="4cc18-213">Case-insensitive</span></span>

- - -
### <a name="targetupn"></a><span data-ttu-id="4cc18-214">target/upn</span><span class="sxs-lookup"><span data-stu-id="4cc18-214">target/upn</span></span>
<span data-ttu-id="4cc18-215">**Supported operators**: eq, startsWith</span><span class="sxs-lookup"><span data-stu-id="4cc18-215">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="4cc18-216">**Example**:</span><span class="sxs-lookup"><span data-stu-id="4cc18-216">**Example**:</span></span>

    $filter=targets/any(t: startswith(t/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity/userPrincipalName,'abc'))    

<span data-ttu-id="4cc18-217">**Notes**:</span><span class="sxs-lookup"><span data-stu-id="4cc18-217">**Notes**:</span></span>

* <span data-ttu-id="4cc18-218">Case-insensitive</span><span class="sxs-lookup"><span data-stu-id="4cc18-218">Case-insensitive</span></span>
* <span data-ttu-id="4cc18-219">You need to add the full namespace when querying  Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity</span><span class="sxs-lookup"><span data-stu-id="4cc18-219">You need to add the full namespace when querying  Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity</span></span>

- - -
### <a name="targetobjectid"></a><span data-ttu-id="4cc18-220">target/objectId</span><span class="sxs-lookup"><span data-stu-id="4cc18-220">target/objectId</span></span>
<span data-ttu-id="4cc18-221">**Supported operators**: eq</span><span class="sxs-lookup"><span data-stu-id="4cc18-221">**Supported operators**: eq</span></span>

<span data-ttu-id="4cc18-222">**Example**:</span><span class="sxs-lookup"><span data-stu-id="4cc18-222">**Example**:</span></span>

    $filter=targets/any(t: t/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba')    

- - -
### <a name="actorupn"></a><span data-ttu-id="4cc18-223">actor/upn</span><span class="sxs-lookup"><span data-stu-id="4cc18-223">actor/upn</span></span>
<span data-ttu-id="4cc18-224">**Supported operators**: eq, startsWith</span><span class="sxs-lookup"><span data-stu-id="4cc18-224">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="4cc18-225">**Example**:</span><span class="sxs-lookup"><span data-stu-id="4cc18-225">**Example**:</span></span>

    $filter=startswith(actor/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity/userPrincipalName,'abc')    

<span data-ttu-id="4cc18-226">**Notes**:</span><span class="sxs-lookup"><span data-stu-id="4cc18-226">**Notes**:</span></span>

* <span data-ttu-id="4cc18-227">Case-insensitive</span><span class="sxs-lookup"><span data-stu-id="4cc18-227">Case-insensitive</span></span> 
* <span data-ttu-id="4cc18-228">You need to add the full namespace when querying Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity</span><span class="sxs-lookup"><span data-stu-id="4cc18-228">You need to add the full namespace when querying Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="4cc18-229">Next Steps</span><span class="sxs-lookup"><span data-stu-id="4cc18-229">Next Steps</span></span>
* <span data-ttu-id="4cc18-230">Do you want to see examples for filtered system activities?</span><span class="sxs-lookup"><span data-stu-id="4cc18-230">Do you want to see examples for filtered system activities?</span></span> <span data-ttu-id="4cc18-231">Check out the [Azure Active Directory audit API samples](active-directory-reporting-api-audit-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4cc18-231">Check out the [Azure Active Directory audit API samples](active-directory-reporting-api-audit-samples.md).</span></span>
* <span data-ttu-id="4cc18-232">Do you want to know more about the Azure AD reporting API?</span><span class="sxs-lookup"><span data-stu-id="4cc18-232">Do you want to know more about the Azure AD reporting API?</span></span> <span data-ttu-id="4cc18-233">See [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="4cc18-233">See [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

