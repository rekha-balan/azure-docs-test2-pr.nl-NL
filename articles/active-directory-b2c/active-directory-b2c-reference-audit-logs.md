---
title: Audit logs samples and definitions in Azure Active Directory B2C | Microsoft Docs
description: Guide and samples on accessing the Azure AD B2C Audit logs.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.topic: conceptual
ms.workload: identity
ms.date: 08/04/2017
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 1697830f699c9cd50548bcfcdd038348db314020
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857227"
---
# <a name="accessing-azure-ad-b2c-audit-logs"></a><span data-ttu-id="2d9e0-103">Accessing Azure AD B2C audit logs</span><span class="sxs-lookup"><span data-stu-id="2d9e0-103">Accessing Azure AD B2C audit logs</span></span>

<span data-ttu-id="2d9e0-104">Azure Active Directory B2C (Azure AD B2C) emits audit logs containing activity information about B2C resources, issued tokens, and administrator access.</span><span class="sxs-lookup"><span data-stu-id="2d9e0-104">Azure Active Directory B2C (Azure AD B2C) emits audit logs containing activity information about B2C resources, issued tokens, and administrator access.</span></span> <span data-ttu-id="2d9e0-105">This article provides a brief overview of the information available through audit logs and instructions on how to access this data for your Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="2d9e0-105">This article provides a brief overview of the information available through audit logs and instructions on how to access this data for your Azure AD B2C tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2d9e0-106">Audit logs are only retained for seven days.</span><span class="sxs-lookup"><span data-stu-id="2d9e0-106">Audit logs are only retained for seven days.</span></span> <span data-ttu-id="2d9e0-107">Plan to download and store your logs using one of the methods shown below if you require a longer retention period.</span><span class="sxs-lookup"><span data-stu-id="2d9e0-107">Plan to download and store your logs using one of the methods shown below if you require a longer retention period.</span></span> 

##<a name="overview-of-activities-available-in-the-b2c-category-of-audit-logs"></a><span data-ttu-id="2d9e0-108">Overview of activities available in the B2C category of audit logs</span><span class="sxs-lookup"><span data-stu-id="2d9e0-108">Overview of activities available in the B2C category of audit logs</span></span>
<span data-ttu-id="2d9e0-109">The **B2C** category in audit logs contains the following types of activities:</span><span class="sxs-lookup"><span data-stu-id="2d9e0-109">The **B2C** category in audit logs contains the following types of activities:</span></span>
|<span data-ttu-id="2d9e0-110">Activity type</span><span class="sxs-lookup"><span data-stu-id="2d9e0-110">Activity type</span></span> |<span data-ttu-id="2d9e0-111">Description</span><span class="sxs-lookup"><span data-stu-id="2d9e0-111">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="2d9e0-112">Authorization</span><span class="sxs-lookup"><span data-stu-id="2d9e0-112">Authorization</span></span> |<span data-ttu-id="2d9e0-113">Activities concerning the authorization of a user to access B2C resources (for example, an administrator accessing a list of B2C policies)</span><span class="sxs-lookup"><span data-stu-id="2d9e0-113">Activities concerning the authorization of a user to access B2C resources (for example, an administrator accessing a list of B2C policies)</span></span>         |
|<span data-ttu-id="2d9e0-114">Directory</span><span class="sxs-lookup"><span data-stu-id="2d9e0-114">Directory</span></span> |<span data-ttu-id="2d9e0-115">Activities related to directory attributes retrieved when an administrator signs in using the Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2d9e0-115">Activities related to directory attributes retrieved when an administrator signs in using the Azure Portal</span></span> |
|<span data-ttu-id="2d9e0-116">Application</span><span class="sxs-lookup"><span data-stu-id="2d9e0-116">Application</span></span> | <span data-ttu-id="2d9e0-117">CRUD operations on B2C applications</span><span class="sxs-lookup"><span data-stu-id="2d9e0-117">CRUD operations on B2C applications</span></span> |
|<span data-ttu-id="2d9e0-118">Key</span><span class="sxs-lookup"><span data-stu-id="2d9e0-118">Key</span></span> |<span data-ttu-id="2d9e0-119">CRUD operations on keys stored in B2C key container</span><span class="sxs-lookup"><span data-stu-id="2d9e0-119">CRUD operations on keys stored in B2C key container</span></span> |
|<span data-ttu-id="2d9e0-120">Resource</span><span class="sxs-lookup"><span data-stu-id="2d9e0-120">Resource</span></span> |<span data-ttu-id="2d9e0-121">CRUD operations on B2C resources (for example, policies and identity providers)</span><span class="sxs-lookup"><span data-stu-id="2d9e0-121">CRUD operations on B2C resources (for example, policies and identity providers)</span></span>
|<span data-ttu-id="2d9e0-122">Authentication</span><span class="sxs-lookup"><span data-stu-id="2d9e0-122">Authentication</span></span> |<span data-ttu-id="2d9e0-123">Validation of user credentials and token issuance</span><span class="sxs-lookup"><span data-stu-id="2d9e0-123">Validation of user credentials and token issuance</span></span>|

> [!NOTE]
> <span data-ttu-id="2d9e0-124">For user object CRUD activities, refer to the **Core Directory** category.</span><span class="sxs-lookup"><span data-stu-id="2d9e0-124">For user object CRUD activities, refer to the **Core Directory** category.</span></span>

##<a name="example-activity"></a><span data-ttu-id="2d9e0-125">Example activity</span><span class="sxs-lookup"><span data-stu-id="2d9e0-125">Example activity</span></span>
<span data-ttu-id="2d9e0-126">The example below shows the data captured when a user signs in with an external identity provider: ![Audit Logs - Example](./media/active-directory-b2c-reference-audit-logs/audit-logs-example.png)</span><span class="sxs-lookup"><span data-stu-id="2d9e0-126">The example below shows the data captured when a user signs in with an external identity provider: ![Audit Logs - Example](./media/active-directory-b2c-reference-audit-logs/audit-logs-example.png)</span></span>

##<a name="accessing-audit-logs-through-the-azure-portal"></a><span data-ttu-id="2d9e0-127">Accessing audit logs through the Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2d9e0-127">Accessing audit logs through the Azure Portal</span></span>
1. <span data-ttu-id="2d9e0-128">Go to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2d9e0-128">Go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="2d9e0-129">Make sure you are in your B2C directory.</span><span class="sxs-lookup"><span data-stu-id="2d9e0-129">Make sure you are in your B2C directory.</span></span>
2. <span data-ttu-id="2d9e0-130">Click on **Azure Active Directory** in the favorites bar on the left</span><span class="sxs-lookup"><span data-stu-id="2d9e0-130">Click on **Azure Active Directory** in the favorites bar on the left</span></span> 
    
    ![Audit Logs - AAD button](./media/active-directory-b2c-reference-audit-logs/audit-logs-portal-aad.png)

1. <span data-ttu-id="2d9e0-132">Under **Activity**, click on **Audit Logs**</span><span class="sxs-lookup"><span data-stu-id="2d9e0-132">Under **Activity**, click on **Audit Logs**</span></span>

    ![Audit Logs - Logs section](./media/active-directory-b2c-reference-audit-logs/audit-logs-portal-section.png)

2. <span data-ttu-id="2d9e0-134">In the **Category** dropbox, select **B2C**</span><span class="sxs-lookup"><span data-stu-id="2d9e0-134">In the **Category** dropbox, select **B2C**</span></span>
3. <span data-ttu-id="2d9e0-135">Click on **Apply**</span><span class="sxs-lookup"><span data-stu-id="2d9e0-135">Click on **Apply**</span></span>

    ![Audit Logs - Category](./media/active-directory-b2c-reference-audit-logs/audit-logs-portal-category.png)

<span data-ttu-id="2d9e0-137">You will see a list of activities logged over the last seven days.</span><span class="sxs-lookup"><span data-stu-id="2d9e0-137">You will see a list of activities logged over the last seven days.</span></span> 
- <span data-ttu-id="2d9e0-138">Use the **Activity Resource Type** dropdown to filter by the activity types outlined above</span><span class="sxs-lookup"><span data-stu-id="2d9e0-138">Use the **Activity Resource Type** dropdown to filter by the activity types outlined above</span></span>
- <span data-ttu-id="2d9e0-139">Use the **Date Range** dropdown to filter the date range of the activities shown</span><span class="sxs-lookup"><span data-stu-id="2d9e0-139">Use the **Date Range** dropdown to filter the date range of the activities shown</span></span>
- <span data-ttu-id="2d9e0-140">If you click on a specific row in the list, a contextual box on the right will show you additional attributes associated with the activity</span><span class="sxs-lookup"><span data-stu-id="2d9e0-140">If you click on a specific row in the list, a contextual box on the right will show you additional attributes associated with the activity</span></span>
- <span data-ttu-id="2d9e0-141">Click on **Download** to download the activities as a csv file</span><span class="sxs-lookup"><span data-stu-id="2d9e0-141">Click on **Download** to download the activities as a csv file</span></span>

##<a name="accessing-audit-logs-through-the-azure-ad-reporting-api"></a><span data-ttu-id="2d9e0-142">Accessing audit logs through the Azure AD reporting API</span><span class="sxs-lookup"><span data-stu-id="2d9e0-142">Accessing audit logs through the Azure AD reporting API</span></span>
<span data-ttu-id="2d9e0-143">Audit logs are published to the same pipeline as other activities for Azure Active Directory, so they can be accessed through the [Azure Active Directory reporting API](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-audit-reference).</span><span class="sxs-lookup"><span data-stu-id="2d9e0-143">Audit logs are published to the same pipeline as other activities for Azure Active Directory, so they can be accessed through the [Azure Active Directory reporting API](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-audit-reference).</span></span> 

###<a name="prerequisites"></a><span data-ttu-id="2d9e0-144">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2d9e0-144">Prerequisites</span></span>
<span data-ttu-id="2d9e0-145">To authenticate to the Azure AD reporting API you first need to register an application.</span><span class="sxs-lookup"><span data-stu-id="2d9e0-145">To authenticate to the Azure AD reporting API you first need to register an application.</span></span> <span data-ttu-id="2d9e0-146">Make sure to follow the steps in [Prerequisites to access the Azure AD reporting APIs](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="2d9e0-146">Make sure to follow the steps in [Prerequisites to access the Azure AD reporting APIs](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span></span>

###<a name="accesing-the-api"></a><span data-ttu-id="2d9e0-147">Accesing the API</span><span class="sxs-lookup"><span data-stu-id="2d9e0-147">Accesing the API</span></span>
<span data-ttu-id="2d9e0-148">To download the Azure AD B2C audit logs via the API, you'll want to filter the logs to the **B2C** category.</span><span class="sxs-lookup"><span data-stu-id="2d9e0-148">To download the Azure AD B2C audit logs via the API, you'll want to filter the logs to the **B2C** category.</span></span> <span data-ttu-id="2d9e0-149">To filter by category, use the query string parameter when calling the Azure AD reporting API endpoint, as shown below:</span><span class="sxs-lookup"><span data-stu-id="2d9e0-149">To filter by category, use the query string parameter when calling the Azure AD reporting API endpoint, as shown below:</span></span>

`https://graph.windows.net/your-b2c-tentant.onmicrosoft.com/activities/audit?api-version=beta&$filter=category eq 'B2C'`

###<a name="powershell-script"></a><span data-ttu-id="2d9e0-150">PowerShell script</span><span class="sxs-lookup"><span data-stu-id="2d9e0-150">PowerShell script</span></span>
<span data-ttu-id="2d9e0-151">The following script provides an example of using PowerShell to query the Azure AD reporting API and store the results as a JSON file:</span><span class="sxs-lookup"><span data-stu-id="2d9e0-151">The following script provides an example of using PowerShell to query the Azure AD reporting API and store the results as a JSON file:</span></span>

```powershell
# This script will require registration of a Web Application in Azure Active Directory (see https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/)

# Constants
$ClientID       = "your-client-application-id-here"       # Insert your application's Client ID, a Globally Unique ID (registered by Global Admin)
$ClientSecret   = "your-client-application-secret-here"   # Insert your application's Client Key/Secret string
$loginURL       = "https://login.microsoftonline.com"     
$tenantdomain   = "your-b2c-tenant.onmicrosoft.com"       # AAD B2C Tenant; for example, contoso.onmicrosoft.com
$resource       = "https://graph.windows.net"             # Azure AD Graph API resource URI
$7daysago       = "{0:s}" -f (get-date).AddDays(-7) + "Z" # Use 'AddMinutes(-5)' to decrement minutes, for example
Write-Output "Searching for events starting $7daysago"

# Create HTTP header, get an OAuth2 access token based on client id, secret and tenant domain
$body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
$oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

# Parse audit report items, save output to file(s): auditX.json, where X = 0 thru n for number of nextLink pages
if ($oauth.access_token -ne $null) {   
    $i=0
    $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}
    $url = 'https://graph.windows.net/' + $tenantdomain + '/activities/audit?api-version=beta&$filter=category eq ''B2C''and activityDate gt ' + $7daysago 

    # loop through each query page (1 through n)
    Do{
        # display each event on the console window
        Write-Output "Fetching data using Uri: $url"
        $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)
        foreach ($event in ($myReport.Content | ConvertFrom-Json).value) {
            Write-Output ($event | ConvertTo-Json)
        }

        # save the query page to an output file
        Write-Output "Save the output to a file audit$i.json"
        $myReport.Content | Out-File -FilePath audit$i.json -Force
        $url = ($myReport.Content | ConvertFrom-Json).'@odata.nextLink'
        $i = $i+1
    } while($url -ne $null)
} else {
    Write-Host "ERROR: No Access Token"
}
```

