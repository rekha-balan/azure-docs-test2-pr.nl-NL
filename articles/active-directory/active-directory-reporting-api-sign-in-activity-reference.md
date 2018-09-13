---
title: Azure Active Directory sign-in activity report API reference | Microsoft Docs
description: Reference for the Azure Active Directory sign-in activity report API
services: active-directory
documentationcenter: ''
author: dhanyahk
manager: femila
editor: ''
ms.assetid: ddcd9ae0-f6b7-4f13-a5e1-6cbf51a25634
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 09/25/2016
ms.author: dhanyahk;markvi
ms.openlocfilehash: dce65678f9fc96d5802a7b705689cc63e6532c84
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551813"
---
# <a name="azure-active-directory-sign-in-activity-report-api-reference"></a><span data-ttu-id="b9ea3-103">Azure Active Directory sign-in activity report API reference</span><span class="sxs-lookup"><span data-stu-id="b9ea3-103">Azure Active Directory sign-in activity report API reference</span></span>
<span data-ttu-id="b9ea3-104">This topic is part of a collection of topics about the Azure Active Directory reporting API.</span><span class="sxs-lookup"><span data-stu-id="b9ea3-104">This topic is part of a collection of topics about the Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="b9ea3-105">Azure AD reporting provides you with an API that enables you to access sign-in activity report data using code or related tools.</span><span class="sxs-lookup"><span data-stu-id="b9ea3-105">Azure AD reporting provides you with an API that enables you to access sign-in activity report data using code or related tools.</span></span>
<span data-ttu-id="b9ea3-106">The scope of this topic is to provide you with reference information about the **sign-in activity report API**.</span><span class="sxs-lookup"><span data-stu-id="b9ea3-106">The scope of this topic is to provide you with reference information about the **sign-in activity report API**.</span></span>

<span data-ttu-id="b9ea3-107">See:</span><span class="sxs-lookup"><span data-stu-id="b9ea3-107">See:</span></span>

* <span data-ttu-id="b9ea3-108">[Sign-in activities](active-directory-reporting-azure-portal.md#sign-in-activities) for more conceptual information</span><span class="sxs-lookup"><span data-stu-id="b9ea3-108">[Sign-in activities](active-directory-reporting-azure-portal.md#sign-in-activities) for more conceptual information</span></span>
* <span data-ttu-id="b9ea3-109">[Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about the reporting API.</span><span class="sxs-lookup"><span data-stu-id="b9ea3-109">[Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about the reporting API.</span></span>

<span data-ttu-id="b9ea3-110">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="b9ea3-110">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="who-can-access-the-api-data"></a><span data-ttu-id="b9ea3-111">Who can access the API data?</span><span class="sxs-lookup"><span data-stu-id="b9ea3-111">Who can access the API data?</span></span>
* <span data-ttu-id="b9ea3-112">Users in the Security Admin or Security Reader role</span><span class="sxs-lookup"><span data-stu-id="b9ea3-112">Users in the Security Admin or Security Reader role</span></span>
* <span data-ttu-id="b9ea3-113">Global Admins</span><span class="sxs-lookup"><span data-stu-id="b9ea3-113">Global Admins</span></span>
* <span data-ttu-id="b9ea3-114">Any app that has authorization to access the API (app authorization can be setup only based on Global Admin’s permission)</span><span class="sxs-lookup"><span data-stu-id="b9ea3-114">Any app that has authorization to access the API (app authorization can be setup only based on Global Admin’s permission)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9ea3-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b9ea3-115">Prerequisites</span></span>
<span data-ttu-id="b9ea3-116">To access this report through the reporting API, you must have:</span><span class="sxs-lookup"><span data-stu-id="b9ea3-116">To access this report through the reporting API, you must have:</span></span>

* <span data-ttu-id="b9ea3-117">An [Azure Active Directory Premium P1 or P2 edition](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="b9ea3-117">An [Azure Active Directory Premium P1 or P2 edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="b9ea3-118">Completed the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="b9ea3-118">Completed the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-the-api"></a><span data-ttu-id="b9ea3-119">Accessing the API</span><span class="sxs-lookup"><span data-stu-id="b9ea3-119">Accessing the API</span></span>
<span data-ttu-id="b9ea3-120">You can either access this API through the [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b9ea3-120">You can either access this API through the [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="b9ea3-121">In order for PowerShell to correctly interpret the OData filter syntax used in AAD Graph REST calls, you must use the backtick (aka: grave accent) character to “escape” the $ character.</span><span class="sxs-lookup"><span data-stu-id="b9ea3-121">In order for PowerShell to correctly interpret the OData filter syntax used in AAD Graph REST calls, you must use the backtick (aka: grave accent) character to “escape” the $ character.</span></span> <span data-ttu-id="b9ea3-122">The backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell to do a literal interpretation of the $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span><span class="sxs-lookup"><span data-stu-id="b9ea3-122">The backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell to do a literal interpretation of the $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="b9ea3-123">The focus of this topic is on the Graph Explorer.</span><span class="sxs-lookup"><span data-stu-id="b9ea3-123">The focus of this topic is on the Graph Explorer.</span></span> <span data-ttu-id="b9ea3-124">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).</span><span class="sxs-lookup"><span data-stu-id="b9ea3-124">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="b9ea3-125">API Endpoint</span><span class="sxs-lookup"><span data-stu-id="b9ea3-125">API Endpoint</span></span>
<span data-ttu-id="b9ea3-126">You can access this API using the following base URI:</span><span class="sxs-lookup"><span data-stu-id="b9ea3-126">You can access this API using the following base URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta  



<span data-ttu-id="b9ea3-127">Due to the volume of data, this API has a limit of one million returned records.</span><span class="sxs-lookup"><span data-stu-id="b9ea3-127">Due to the volume of data, this API has a limit of one million returned records.</span></span> 

<span data-ttu-id="b9ea3-128">This call returns the data in batches.</span><span class="sxs-lookup"><span data-stu-id="b9ea3-128">This call returns the data in batches.</span></span> <span data-ttu-id="b9ea3-129">Each batch has a maximum of 1000 records.</span><span class="sxs-lookup"><span data-stu-id="b9ea3-129">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="b9ea3-130">To get the next batch of records, use the Next link.</span><span class="sxs-lookup"><span data-stu-id="b9ea3-130">To get the next batch of records, use the Next link.</span></span> <span data-ttu-id="b9ea3-131">Get the [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) information from the first set of returned records.</span><span class="sxs-lookup"><span data-stu-id="b9ea3-131">Get the [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) information from the first set of returned records.</span></span> <span data-ttu-id="b9ea3-132">The skip token will be at the end of the result set.</span><span class="sxs-lookup"><span data-stu-id="b9ea3-132">The skip token will be at the end of the result set.</span></span>  

    https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&%24skiptoken=-1339686058


## <a name="supported-filters"></a><span data-ttu-id="b9ea3-133">Supported filters</span><span class="sxs-lookup"><span data-stu-id="b9ea3-133">Supported filters</span></span>
<span data-ttu-id="b9ea3-134">You can narrow down the number of records that are returned by an API call in form of a filter.</span><span class="sxs-lookup"><span data-stu-id="b9ea3-134">You can narrow down the number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="b9ea3-135">For sign-in API related data, the following filters are supported:</span><span class="sxs-lookup"><span data-stu-id="b9ea3-135">For sign-in API related data, the following filters are supported:</span></span>

* <span data-ttu-id="b9ea3-136">**$top=\<number of records to be returned\>** - to limit the number of returned records.</span><span class="sxs-lookup"><span data-stu-id="b9ea3-136">**$top=\<number of records to be returned\>** - to limit the number of returned records.</span></span> <span data-ttu-id="b9ea3-137">This is an expensive operation.</span><span class="sxs-lookup"><span data-stu-id="b9ea3-137">This is an expensive operation.</span></span> <span data-ttu-id="b9ea3-138">You should not use this filter if you want to return thousands of objects.</span><span class="sxs-lookup"><span data-stu-id="b9ea3-138">You should not use this filter if you want to return thousands of objects.</span></span>  
* <span data-ttu-id="b9ea3-139">**$filter=\<your filter statement\>** - to specify, on the basis of supported filter fields, the type of records you care about</span><span class="sxs-lookup"><span data-stu-id="b9ea3-139">**$filter=\<your filter statement\>** - to specify, on the basis of supported filter fields, the type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="b9ea3-140">Supported filter fields and operators</span><span class="sxs-lookup"><span data-stu-id="b9ea3-140">Supported filter fields and operators</span></span>
<span data-ttu-id="b9ea3-141">To specify the type of records you care about, you can build a filter statement that can contain either one or a combination of the following filter fields:</span><span class="sxs-lookup"><span data-stu-id="b9ea3-141">To specify the type of records you care about, you can build a filter statement that can contain either one or a combination of the following filter fields:</span></span>

* <span data-ttu-id="b9ea3-142">[signinDateTime](#signindatetime) - defines a date or date range</span><span class="sxs-lookup"><span data-stu-id="b9ea3-142">[signinDateTime](#signindatetime) - defines a date or date range</span></span>
* <span data-ttu-id="b9ea3-143">[userId](#userid) - defines a specific user based the user's ID.</span><span class="sxs-lookup"><span data-stu-id="b9ea3-143">[userId](#userid) - defines a specific user based the user's ID.</span></span>
* <span data-ttu-id="b9ea3-144">[userPrincipalName](#userprincipalname) - defines a specific user based the user's user principal name (UPN)</span><span class="sxs-lookup"><span data-stu-id="b9ea3-144">[userPrincipalName](#userprincipalname) - defines a specific user based the user's user principal name (UPN)</span></span>
* <span data-ttu-id="b9ea3-145">[appId](#appid) - defines a specific app based the app's ID</span><span class="sxs-lookup"><span data-stu-id="b9ea3-145">[appId](#appid) - defines a specific app based the app's ID</span></span>
* <span data-ttu-id="b9ea3-146">[appDisplayName](#appdisplayname) - defines a specific app based the app's display name</span><span class="sxs-lookup"><span data-stu-id="b9ea3-146">[appDisplayName](#appdisplayname) - defines a specific app based the app's display name</span></span>
* <span data-ttu-id="b9ea3-147">[loginStatus](#loginStatus) - defines the status of the logins (success / failure)</span><span class="sxs-lookup"><span data-stu-id="b9ea3-147">[loginStatus](#loginStatus) - defines the status of the logins (success / failure)</span></span>

> [!NOTE]
> <span data-ttu-id="b9ea3-148">When using Graph Explorer, you the need to use the correct case for each letter is your filter fields.</span><span class="sxs-lookup"><span data-stu-id="b9ea3-148">When using Graph Explorer, you the need to use the correct case for each letter is your filter fields.</span></span>
> 
> 

<span data-ttu-id="b9ea3-149">To narrow down the scope of the returned data, you can build combinations of the supported filters and filter fields.</span><span class="sxs-lookup"><span data-stu-id="b9ea3-149">To narrow down the scope of the returned data, you can build combinations of the supported filters and filter fields.</span></span> <span data-ttu-id="b9ea3-150">For example, the following statement returns the top 10 records between July 1st 2016 and July 6th 2016:</span><span class="sxs-lookup"><span data-stu-id="b9ea3-150">For example, the following statement returns the top 10 records between July 1st 2016 and July 6th 2016:</span></span>

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta&$top=10&$filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T00:00:00Z


- - -
### <a name="signindatetime"></a><span data-ttu-id="b9ea3-151">signinDateTime</span><span class="sxs-lookup"><span data-stu-id="b9ea3-151">signinDateTime</span></span>
<span data-ttu-id="b9ea3-152">**Supported operators**: eq, ge, le, gt, lt</span><span class="sxs-lookup"><span data-stu-id="b9ea3-152">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="b9ea3-153">**Example**:</span><span class="sxs-lookup"><span data-stu-id="b9ea3-153">**Example**:</span></span>

<span data-ttu-id="b9ea3-154">Using a specific date</span><span class="sxs-lookup"><span data-stu-id="b9ea3-154">Using a specific date</span></span>

    $filter=signinDateTime+eq+2016-04-25T23:59:00Z    



<span data-ttu-id="b9ea3-155">Using a date range</span><span class="sxs-lookup"><span data-stu-id="b9ea3-155">Using a date range</span></span>    

    $filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T17:05:21Z


<span data-ttu-id="b9ea3-156">**Notes**:</span><span class="sxs-lookup"><span data-stu-id="b9ea3-156">**Notes**:</span></span>

<span data-ttu-id="b9ea3-157">The datetime parameter should be in the UTC format</span><span class="sxs-lookup"><span data-stu-id="b9ea3-157">The datetime parameter should be in the UTC format</span></span> 

- - -
### <a name="userid"></a><span data-ttu-id="b9ea3-158">userId</span><span class="sxs-lookup"><span data-stu-id="b9ea3-158">userId</span></span>
<span data-ttu-id="b9ea3-159">**Supported operators**: eq</span><span class="sxs-lookup"><span data-stu-id="b9ea3-159">**Supported operators**: eq</span></span>

<span data-ttu-id="b9ea3-160">**Example**:</span><span class="sxs-lookup"><span data-stu-id="b9ea3-160">**Example**:</span></span>

    $filter=userId+eq+’00000000-0000-0000-0000-000000000000’

<span data-ttu-id="b9ea3-161">**Notes**:</span><span class="sxs-lookup"><span data-stu-id="b9ea3-161">**Notes**:</span></span>

<span data-ttu-id="b9ea3-162">The value of userId is a string value</span><span class="sxs-lookup"><span data-stu-id="b9ea3-162">The value of userId is a string value</span></span>

- - -
### <a name="userprincipalname"></a><span data-ttu-id="b9ea3-163">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="b9ea3-163">userPrincipalName</span></span>
<span data-ttu-id="b9ea3-164">**Supported operators**: eq</span><span class="sxs-lookup"><span data-stu-id="b9ea3-164">**Supported operators**: eq</span></span>

<span data-ttu-id="b9ea3-165">**Example**:</span><span class="sxs-lookup"><span data-stu-id="b9ea3-165">**Example**:</span></span>

    $filter=userPrincipalName+eq+'audrey.oliver@wingtiptoysonline.com' 


<span data-ttu-id="b9ea3-166">**Notes**:</span><span class="sxs-lookup"><span data-stu-id="b9ea3-166">**Notes**:</span></span>

<span data-ttu-id="b9ea3-167">The value of userPrincipalName is a string value</span><span class="sxs-lookup"><span data-stu-id="b9ea3-167">The value of userPrincipalName is a string value</span></span>

- - -
### <a name="appid"></a><span data-ttu-id="b9ea3-168">appId</span><span class="sxs-lookup"><span data-stu-id="b9ea3-168">appId</span></span>
<span data-ttu-id="b9ea3-169">**Supported operators**: eq</span><span class="sxs-lookup"><span data-stu-id="b9ea3-169">**Supported operators**: eq</span></span>

<span data-ttu-id="b9ea3-170">**Example**:</span><span class="sxs-lookup"><span data-stu-id="b9ea3-170">**Example**:</span></span>

    $filter=appId+eq+’00000000-0000-0000-0000-000000000000’



<span data-ttu-id="b9ea3-171">**Notes**:</span><span class="sxs-lookup"><span data-stu-id="b9ea3-171">**Notes**:</span></span>

<span data-ttu-id="b9ea3-172">The value of appId is a string value</span><span class="sxs-lookup"><span data-stu-id="b9ea3-172">The value of appId is a string value</span></span>

- - -
### <a name="appdisplayname"></a><span data-ttu-id="b9ea3-173">appDisplayName</span><span class="sxs-lookup"><span data-stu-id="b9ea3-173">appDisplayName</span></span>
<span data-ttu-id="b9ea3-174">**Supported operators**: eq</span><span class="sxs-lookup"><span data-stu-id="b9ea3-174">**Supported operators**: eq</span></span>

<span data-ttu-id="b9ea3-175">**Example**:</span><span class="sxs-lookup"><span data-stu-id="b9ea3-175">**Example**:</span></span>

    $filter=appDisplayName+eq+'Azure+Portal' 


<span data-ttu-id="b9ea3-176">**Notes**:</span><span class="sxs-lookup"><span data-stu-id="b9ea3-176">**Notes**:</span></span>

<span data-ttu-id="b9ea3-177">The value of appDisplayName is a string value</span><span class="sxs-lookup"><span data-stu-id="b9ea3-177">The value of appDisplayName is a string value</span></span>

- - -
### <a name="loginstatus"></a><span data-ttu-id="b9ea3-178">loginStatus</span><span class="sxs-lookup"><span data-stu-id="b9ea3-178">loginStatus</span></span>
<span data-ttu-id="b9ea3-179">**Supported operators**: eq</span><span class="sxs-lookup"><span data-stu-id="b9ea3-179">**Supported operators**: eq</span></span>

<span data-ttu-id="b9ea3-180">**Example**:</span><span class="sxs-lookup"><span data-stu-id="b9ea3-180">**Example**:</span></span>

    $filter=loginStatus+eq+'1'  


<span data-ttu-id="b9ea3-181">**Notes**:</span><span class="sxs-lookup"><span data-stu-id="b9ea3-181">**Notes**:</span></span>

<span data-ttu-id="b9ea3-182">There are two options for the loginStatus: 0 - success, 1 - failure</span><span class="sxs-lookup"><span data-stu-id="b9ea3-182">There are two options for the loginStatus: 0 - success, 1 - failure</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="b9ea3-183">Next steps</span><span class="sxs-lookup"><span data-stu-id="b9ea3-183">Next steps</span></span>
* <span data-ttu-id="b9ea3-184">Do you want to see examples for filtered sign-in activities?</span><span class="sxs-lookup"><span data-stu-id="b9ea3-184">Do you want to see examples for filtered sign-in activities?</span></span> <span data-ttu-id="b9ea3-185">Check out the [Azure Active Directory sign-in activity report API samples](active-directory-reporting-api-sign-in-activity-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b9ea3-185">Check out the [Azure Active Directory sign-in activity report API samples](active-directory-reporting-api-sign-in-activity-samples.md).</span></span>
* <span data-ttu-id="b9ea3-186">Do you want to know more about the Azure AD reporting API?</span><span class="sxs-lookup"><span data-stu-id="b9ea3-186">Do you want to know more about the Azure AD reporting API?</span></span> <span data-ttu-id="b9ea3-187">See [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="b9ea3-187">See [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

