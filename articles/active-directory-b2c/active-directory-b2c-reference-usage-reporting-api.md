---
title: Azure AD B2C Usage Reporting API Samples and Definitions| Microsoft Docs
description: Guide and sample on how to get reports on B2C Tenant users, authentications, and MFA.
services: active-directory-b2c
documentationcenter: dev-center-name
author: rojasja
manager: mbaldwin
ms.service: active-directory-b2c
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/08/2017
ms.author: joroja
ms.openlocfilehash: 9bb528aa0172fb7179b5498be89aee9a92b788f8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540795"
---
# <a name="accessing-usage-reports-in-azure-ad-b2c-via-the-reporting-api"></a><span data-ttu-id="d7478-103">Accessing usage reports in Azure AD B2C via the reporting API</span><span class="sxs-lookup"><span data-stu-id="d7478-103">Accessing usage reports in Azure AD B2C via the reporting API</span></span>

<span data-ttu-id="d7478-104">Azure Active Directory B2C, provides login and MFA-based authentication for all the end users of your family of applications across Identity Providers.</span><span class="sxs-lookup"><span data-stu-id="d7478-104">Azure Active Directory B2C, provides login and MFA-based authentication for all the end users of your family of applications across Identity Providers.</span></span>  <span data-ttu-id="d7478-105">Knowing the number of users registered in the tenant, the providers they used to register, and the number of authentications by type, answers questions like:</span><span class="sxs-lookup"><span data-stu-id="d7478-105">Knowing the number of users registered in the tenant, the providers they used to register, and the number of authentications by type, answers questions like:</span></span>
* <span data-ttu-id="d7478-106">How many users from each type of Identity Provider (for example, Microsoft Account, LinkedIn) have registered in the last 10 days?</span><span class="sxs-lookup"><span data-stu-id="d7478-106">How many users from each type of Identity Provider (for example, Microsoft Account, LinkedIn) have registered in the last 10 days?</span></span>
* <span data-ttu-id="d7478-107">How many Multi-Factor-Authentications have completed successfully in the last month?</span><span class="sxs-lookup"><span data-stu-id="d7478-107">How many Multi-Factor-Authentications have completed successfully in the last month?</span></span>
* <span data-ttu-id="d7478-108">How many login-based authentications were completed this month?</span><span class="sxs-lookup"><span data-stu-id="d7478-108">How many login-based authentications were completed this month?</span></span> <span data-ttu-id="d7478-109">Per day?</span><span class="sxs-lookup"><span data-stu-id="d7478-109">Per day?</span></span> <span data-ttu-id="d7478-110">Per application?</span><span class="sxs-lookup"><span data-stu-id="d7478-110">Per application?</span></span>
* <span data-ttu-id="d7478-111">How can I approximate the expected monthly cost of my B2C Tenant activity?</span><span class="sxs-lookup"><span data-stu-id="d7478-111">How can I approximate the expected monthly cost of my B2C Tenant activity?</span></span>

<span data-ttu-id="d7478-112">This article focuses on reports most closely tied to billing activity, which is based on number of users, number of billable login-based authentications and number of multi-factor authentications.</span><span class="sxs-lookup"><span data-stu-id="d7478-112">This article focuses on reports most closely tied to billing activity, which is based on number of users, number of billable login-based authentications and number of multi-factor authentications.</span></span>


## <a name="prerequisites-to-access-the-azure-ad-reporting-api"></a><span data-ttu-id="d7478-113">Prerequisites to access the Azure AD reporting API</span><span class="sxs-lookup"><span data-stu-id="d7478-113">Prerequisites to access the Azure AD reporting API</span></span>
<span data-ttu-id="d7478-114">Before you get started, you need to complete the [Prerequisites to access the Azure AD reporting APIs](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="d7478-114">Before you get started, you need to complete the [Prerequisites to access the Azure AD reporting APIs](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span></span>  <span data-ttu-id="d7478-115">Create an application, obtain a secret for it, and grant it access rights to your Azure AD B2C tenant’s reports.</span><span class="sxs-lookup"><span data-stu-id="d7478-115">Create an application, obtain a secret for it, and grant it access rights to your Azure AD B2C tenant’s reports.</span></span> <span data-ttu-id="d7478-116">*Bash script* and *Python script* examples are also provided here.</span><span class="sxs-lookup"><span data-stu-id="d7478-116">*Bash script* and *Python script* examples are also provided here.</span></span>

## <a name="powershell-script"></a><span data-ttu-id="d7478-117">PowerShell script</span><span class="sxs-lookup"><span data-stu-id="d7478-117">PowerShell script</span></span>
<span data-ttu-id="d7478-118">This script demonstrates the four usage reports using the **TimeStamp** parameter and the **-ApplicationId** filter.</span><span class="sxs-lookup"><span data-stu-id="d7478-118">This script demonstrates the four usage reports using the **TimeStamp** parameter and the **-ApplicationId** filter.</span></span>

```
# This script will require the Web Application and permissions setup in Azure Active Directory

# Constants
$ClientID      = "your-client-application-id-here"  
$ClientSecret  = "your-client-application-secret-here"
$loginURL      = "https://login.windows.net"
$tenantdomain  = "your-b2c-tenant-domain.onmicrosoft.com"  
# Get an Oauth 2 access token based on client id, secret and tenant domain
$body          = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
$oauth         = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body
if ($oauth.access_token -ne $null) {
    $headerParams  = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

    Write-host Data from the tenantUserCount report
    Write-host ====================================================
     # Returns a JSON document for the report
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the tenantUserCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?%24filter=TimeStamp+gt+2016-10-15&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cAuthenticationCountSummary report
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cAuthenticationCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=TimeStamp+gt+2016-09-20+and+TimeStamp+lt+2016-10-03&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cAuthenticationCount report with ApplicationId filter
    Write-host ====================================================
    # Returns a JSON document for the " " report
        $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cMfaRequestCountSummary
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cMfaRequestCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCount?%24filter=TimeStamp+gt+2016-09-10+and+TimeStamp+lt+2016-10-04&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cMfaRequestCount report with ApplicationId filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
     Write-host $myReport.Content

} else {
    Write-Host "ERROR: No Access Token"
    }
```


## <a name="usage-report-definitions"></a><span data-ttu-id="d7478-119">Usage report definitions</span><span class="sxs-lookup"><span data-stu-id="d7478-119">Usage report definitions</span></span>
<span data-ttu-id="d7478-120">**tenantUserCount** – Count of the number of users in the tenant by type of Identity Provider per day in the last 30 days.</span><span class="sxs-lookup"><span data-stu-id="d7478-120">**tenantUserCount** – Count of the number of users in the tenant by type of Identity Provider per day in the last 30 days.</span></span> <span data-ttu-id="d7478-121">(optionally, a TimeStamp filter provides User Counts from a specified date to the current date).</span><span class="sxs-lookup"><span data-stu-id="d7478-121">(optionally, a TimeStamp filter provides User Counts from a specified date to the current date).</span></span> <span data-ttu-id="d7478-122">Report provides:</span><span class="sxs-lookup"><span data-stu-id="d7478-122">Report provides:</span></span>
 * <span data-ttu-id="d7478-123">TotalUserCount = Count of all user objects</span><span class="sxs-lookup"><span data-stu-id="d7478-123">TotalUserCount = Count of all user objects</span></span>
 * <span data-ttu-id="d7478-124">OtherUserCount = # of AAD Directory users (non-B2C users)</span><span class="sxs-lookup"><span data-stu-id="d7478-124">OtherUserCount = # of AAD Directory users (non-B2C users)</span></span>
 * <span data-ttu-id="d7478-125">LocalUserCount = # of B2C user accounts created with credentials local to the B2C Tenant</span><span class="sxs-lookup"><span data-stu-id="d7478-125">LocalUserCount = # of B2C user accounts created with credentials local to the B2C Tenant</span></span>
 * <span data-ttu-id="d7478-126">AlternateIdUserCount\*\* = # of B2C users registered with external Identity providers (for example, facebook, Microsoft Account, other AAD tenants - aka OrgId)</span><span class="sxs-lookup"><span data-stu-id="d7478-126">AlternateIdUserCount\*\* = # of B2C users registered with external Identity providers (for example, facebook, Microsoft Account, other AAD tenants - aka OrgId)</span></span>

<span data-ttu-id="d7478-127">**b2cAuthenticationCountSummary** – Sum the daily count of billable authentications over the last 30 days by day and by type of authentication flow</span><span class="sxs-lookup"><span data-stu-id="d7478-127">**b2cAuthenticationCountSummary** – Sum the daily count of billable authentications over the last 30 days by day and by type of authentication flow</span></span>

<span data-ttu-id="d7478-128">**b2cAuthenticationCount** -Count the Number of authentications within a time period.</span><span class="sxs-lookup"><span data-stu-id="d7478-128">**b2cAuthenticationCount** -Count the Number of authentications within a time period.</span></span> <span data-ttu-id="d7478-129">Default is last 30 days.</span><span class="sxs-lookup"><span data-stu-id="d7478-129">Default is last 30 days.</span></span>  <span data-ttu-id="d7478-130">(optional: beginning and ending TimeStamp (s) define a specific period of counts desired) Output includes a StartTimeStamp (earliest date of activity for this tenant) and EndTimeStamp (latest update)</span><span class="sxs-lookup"><span data-stu-id="d7478-130">(optional: beginning and ending TimeStamp (s) define a specific period of counts desired) Output includes a StartTimeStamp (earliest date of activity for this tenant) and EndTimeStamp (latest update)</span></span>

<span data-ttu-id="d7478-131">**b2cMfaRequestCountSummary** - Sum the daily count of Multi-Factor Authentications by day and by type of MFA (SMS or Voice)</span><span class="sxs-lookup"><span data-stu-id="d7478-131">**b2cMfaRequestCountSummary** - Sum the daily count of Multi-Factor Authentications by day and by type of MFA (SMS or Voice)</span></span>


## <a name="limitations"></a><span data-ttu-id="d7478-132">Limitations</span><span class="sxs-lookup"><span data-stu-id="d7478-132">Limitations</span></span>
* <span data-ttu-id="d7478-133">User count data is refreshed every 24 to 48 hours.</span><span class="sxs-lookup"><span data-stu-id="d7478-133">User count data is refreshed every 24 to 48 hours.</span></span>  <span data-ttu-id="d7478-134">Authentications are updated several times a day.</span><span class="sxs-lookup"><span data-stu-id="d7478-134">Authentications are updated several times a day.</span></span>
* <span data-ttu-id="d7478-135">When using the ApplicationId filter, an empty report response may be due to one of following conditions:</span><span class="sxs-lookup"><span data-stu-id="d7478-135">When using the ApplicationId filter, an empty report response may be due to one of following conditions:</span></span>
 * <span data-ttu-id="d7478-136">The Application Id does not exist in the tenant.</span><span class="sxs-lookup"><span data-stu-id="d7478-136">The Application Id does not exist in the tenant.</span></span> <span data-ttu-id="d7478-137">Make sure it is correct.</span><span class="sxs-lookup"><span data-stu-id="d7478-137">Make sure it is correct.</span></span>
 * <span data-ttu-id="d7478-138">The Application Id exists, but no data was found in the reporting period.</span><span class="sxs-lookup"><span data-stu-id="d7478-138">The Application Id exists, but no data was found in the reporting period.</span></span> <span data-ttu-id="d7478-139">Review your date time parameters.</span><span class="sxs-lookup"><span data-stu-id="d7478-139">Review your date time parameters.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d7478-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="d7478-140">Next steps</span></span>
### <a name="estimating-your-azure-ad-monthly-bill"></a><span data-ttu-id="d7478-141">Estimating your Azure AD monthly bill.</span><span class="sxs-lookup"><span data-stu-id="d7478-141">Estimating your Azure AD monthly bill.</span></span>
<span data-ttu-id="d7478-142">When combined with [the most current Azure AD B2C pricing available](https://azure.microsoft.com/pricing/details/active-directory-b2c/), you can estimate daily, weekly, and monthly Azure consumption.</span><span class="sxs-lookup"><span data-stu-id="d7478-142">When combined with [the most current Azure AD B2C pricing available](https://azure.microsoft.com/pricing/details/active-directory-b2c/), you can estimate daily, weekly, and monthly Azure consumption.</span></span>  <span data-ttu-id="d7478-143">An estimate is especially useful as you plan changes in tenant behavior which may impact overall cost.</span><span class="sxs-lookup"><span data-stu-id="d7478-143">An estimate is especially useful as you plan changes in tenant behavior which may impact overall cost.</span></span>  <span data-ttu-id="d7478-144">Actual costs can be reviewed under your [linked Azure Subscription.](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-how-to-enable-billing)</span><span class="sxs-lookup"><span data-stu-id="d7478-144">Actual costs can be reviewed under your [linked Azure Subscription.](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-how-to-enable-billing)</span></span>

### <a name="options-for-other-output-formats"></a><span data-ttu-id="d7478-145">Options for other output formats</span><span class="sxs-lookup"><span data-stu-id="d7478-145">Options for other output formats</span></span>
```
# to output to JSON use following line in the PowerShell sample
$myReport.Content | Out-File -FilePath b2cUserJourneySummaryEvents.json -Force

# to output the content to a name value list
($myReport.Content | ConvertFrom-Json).value | Out-File -FilePath name-your-file.txt -Force

# to output the content in XML use the following line
(($myReport.Content | ConvertFrom-Json).value | ConvertTo-Xml).InnerXml | Out-File -FilePath name-your-file.xml -Force
```


<!--Reference style links - using these makes the source content way more readable than using inline links-->
[gog]: http://google.com/        
[yah]: http://search.yahoo.com/  
[msn]: http://search.msn.com/    
