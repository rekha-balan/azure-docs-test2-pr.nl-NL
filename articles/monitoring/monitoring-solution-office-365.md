---
title: Office 365 management solution in Azure | Microsoft Docs
description: This article provides details on configuration and use of the Office 365 solution in Azure.  It includes detailed description of the Office 365 records created in Log Analytics.
services: operations-management-suite
documentationcenter: ''
author: bwren
manager: carmonm
editor: ''
ms.service: operations-management-suite
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2018
ms.author: bwren
ms.openlocfilehash: 3772b03d9a9d688b9d0eac42d51af7a2f2e0c5bd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867349"
---
# <a name="office-365-management-solution-in-azure-preview"></a><span data-ttu-id="d7c5e-104">Office 365 management solution in Azure (Preview)</span><span class="sxs-lookup"><span data-stu-id="d7c5e-104">Office 365 management solution in Azure (Preview)</span></span>

![Office 365 logo](media/monitoring-solution-office-365/icon.png)

<span data-ttu-id="d7c5e-106">The Office 365 management solution allows you to monitor your Office 365 environment in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-106">The Office 365 management solution allows you to monitor your Office 365 environment in Log Analytics.</span></span>

- <span data-ttu-id="d7c5e-107">Monitor user activities on your Office 365 accounts to analyze usage patterns as well as identify behavioral trends.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-107">Monitor user activities on your Office 365 accounts to analyze usage patterns as well as identify behavioral trends.</span></span> <span data-ttu-id="d7c5e-108">For example, you can extract specific usage scenarios, such as files that are shared outside your organization or the most popular SharePoint sites.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-108">For example, you can extract specific usage scenarios, such as files that are shared outside your organization or the most popular SharePoint sites.</span></span>
- <span data-ttu-id="d7c5e-109">Monitor administrator activities to track configuration changes or high privilege operations.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-109">Monitor administrator activities to track configuration changes or high privilege operations.</span></span>
- <span data-ttu-id="d7c5e-110">Detect and investigate unwanted user behavior, which can be customized for your organizational needs.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-110">Detect and investigate unwanted user behavior, which can be customized for your organizational needs.</span></span>
- <span data-ttu-id="d7c5e-111">Demonstrate audit and compliance.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-111">Demonstrate audit and compliance.</span></span> <span data-ttu-id="d7c5e-112">For example, you can monitor file access operations on confidential files, which can help you with the audit and compliance process.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-112">For example, you can monitor file access operations on confidential files, which can help you with the audit and compliance process.</span></span>
- <span data-ttu-id="d7c5e-113">Perform operational troubleshooting by using [log searches](../log-analytics/log-analytics-log-search.md) on top of Office 365 activity data of your organization.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-113">Perform operational troubleshooting by using [log searches](../log-analytics/log-analytics-log-search.md) on top of Office 365 activity data of your organization.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7c5e-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d7c5e-114">Prerequisites</span></span>
<span data-ttu-id="d7c5e-115">The following is required prior to this solution being installed and configured.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-115">The following is required prior to this solution being installed and configured.</span></span>

- <span data-ttu-id="d7c5e-116">Organizational Office 365 subscription.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-116">Organizational Office 365 subscription.</span></span>
- <span data-ttu-id="d7c5e-117">Credentials for a user account that is a Global Administrator.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-117">Credentials for a user account that is a Global Administrator.</span></span>
- <span data-ttu-id="d7c5e-118">To receive audit data, you must [configure auditing](https://support.office.com/en-us/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c?ui=en-US&rs=en-US&ad=US#PickTab=Before_you_begin) in your Office 365 subscription.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-118">To receive audit data, you must [configure auditing](https://support.office.com/en-us/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c?ui=en-US&rs=en-US&ad=US#PickTab=Before_you_begin) in your Office 365 subscription.</span></span>  <span data-ttu-id="d7c5e-119">Note that [mailbox auditing](https://technet.microsoft.com/library/dn879651.aspx) is configured separately.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-119">Note that [mailbox auditing](https://technet.microsoft.com/library/dn879651.aspx) is configured separately.</span></span>  <span data-ttu-id="d7c5e-120">You can still install the solution and collect other data if auditing is not configured.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-120">You can still install the solution and collect other data if auditing is not configured.</span></span>
 

## <a name="management-packs"></a><span data-ttu-id="d7c5e-121">Management packs</span><span class="sxs-lookup"><span data-stu-id="d7c5e-121">Management packs</span></span>
<span data-ttu-id="d7c5e-122">This solution does not install any management packs in [connected management groups](../log-analytics/log-analytics-om-agents.md).</span><span class="sxs-lookup"><span data-stu-id="d7c5e-122">This solution does not install any management packs in [connected management groups](../log-analytics/log-analytics-om-agents.md).</span></span>
  
## <a name="install-and-configure"></a><span data-ttu-id="d7c5e-123">Install and configure</span><span class="sxs-lookup"><span data-stu-id="d7c5e-123">Install and configure</span></span>
<span data-ttu-id="d7c5e-124">Start by adding the [Office 365 solution to your subscription](monitoring-solutions.md#install-a-management-solution).</span><span class="sxs-lookup"><span data-stu-id="d7c5e-124">Start by adding the [Office 365 solution to your subscription](monitoring-solutions.md#install-a-management-solution).</span></span> <span data-ttu-id="d7c5e-125">Once it's added, you must perform the configuration steps in this section to give it access to your Office 365 subscription.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-125">Once it's added, you must perform the configuration steps in this section to give it access to your Office 365 subscription.</span></span>

### <a name="required-information"></a><span data-ttu-id="d7c5e-126">Required information</span><span class="sxs-lookup"><span data-stu-id="d7c5e-126">Required information</span></span>
<span data-ttu-id="d7c5e-127">Before you start this procedure, gather the following information.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-127">Before you start this procedure, gather the following information.</span></span>

<span data-ttu-id="d7c5e-128">From your Log Analytics workspace:</span><span class="sxs-lookup"><span data-stu-id="d7c5e-128">From your Log Analytics workspace:</span></span>

- <span data-ttu-id="d7c5e-129">Workspace name: The workspace where the Office 365 data will be collected.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-129">Workspace name: The workspace where the Office 365 data will be collected.</span></span>
- <span data-ttu-id="d7c5e-130">Resource group name: The resource group that contains the workspace.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-130">Resource group name: The resource group that contains the workspace.</span></span>
- <span data-ttu-id="d7c5e-131">Azure subscription ID: The subscription that contains the workspace.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-131">Azure subscription ID: The subscription that contains the workspace.</span></span>

<span data-ttu-id="d7c5e-132">From your Office 365 subscription:</span><span class="sxs-lookup"><span data-stu-id="d7c5e-132">From your Office 365 subscription:</span></span>

- <span data-ttu-id="d7c5e-133">Username: Email address of an administrative account.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-133">Username: Email address of an administrative account.</span></span>
- <span data-ttu-id="d7c5e-134">Tenant ID: Unique ID for Office 365 subscription.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-134">Tenant ID: Unique ID for Office 365 subscription.</span></span>
- <span data-ttu-id="d7c5e-135">Client ID: 16-character string that represents Office 365 client.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-135">Client ID: 16-character string that represents Office 365 client.</span></span>
- <span data-ttu-id="d7c5e-136">Client Secret: Encrypted string necessary for authentication.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-136">Client Secret: Encrypted string necessary for authentication.</span></span>

### <a name="create-an-office-365-application-in-azure-active-directory"></a><span data-ttu-id="d7c5e-137">Create an Office 365 application in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d7c5e-137">Create an Office 365 application in Azure Active Directory</span></span>
<span data-ttu-id="d7c5e-138">The first step is to create an application in Azure Active Directory that the management solution will use to access your Office 365 solution.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-138">The first step is to create an application in Azure Active Directory that the management solution will use to access your Office 365 solution.</span></span>

1. <span data-ttu-id="d7c5e-139">Log in to the Azure portal at [https://portal.azure.com](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d7c5e-139">Log in to the Azure portal at [https://portal.azure.com](https://portal.azure.com/).</span></span>
1. <span data-ttu-id="d7c5e-140">Select **Azure Active Directory** and then **App registrations**.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-140">Select **Azure Active Directory** and then **App registrations**.</span></span>
1. <span data-ttu-id="d7c5e-141">Click **New application registration**.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-141">Click **New application registration**.</span></span>

    ![Add app registration](media/monitoring-solution-office-365/add-app-registration.png)
1. <span data-ttu-id="d7c5e-143">Enter an application **Name** and **Sign-on URL**.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-143">Enter an application **Name** and **Sign-on URL**.</span></span>  <span data-ttu-id="d7c5e-144">The name should be descriptive.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-144">The name should be descriptive.</span></span>  <span data-ttu-id="d7c5e-145">Use _http://localhost_ for the URL, and keep _Web app / API_ for the **Application type**</span><span class="sxs-lookup"><span data-stu-id="d7c5e-145">Use _http://localhost_ for the URL, and keep _Web app / API_ for the **Application type**</span></span>
    
    ![Create application](media/monitoring-solution-office-365/create-application.png)
1. <span data-ttu-id="d7c5e-147">Click **Create** and validate the application information.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-147">Click **Create** and validate the application information.</span></span>

    ![Registered app](media/monitoring-solution-office-365/registered-app.png)

### <a name="configure-application-for-office-365"></a><span data-ttu-id="d7c5e-149">Configure application for Office 365</span><span class="sxs-lookup"><span data-stu-id="d7c5e-149">Configure application for Office 365</span></span>

1. <span data-ttu-id="d7c5e-150">Click **Settings** to open the **Settings** menu.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-150">Click **Settings** to open the **Settings** menu.</span></span>
1. <span data-ttu-id="d7c5e-151">Select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-151">Select **Properties**.</span></span> <span data-ttu-id="d7c5e-152">Change **Multi-tenanted** to _Yes_.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-152">Change **Multi-tenanted** to _Yes_.</span></span>

    ![Settings multitenant](media/monitoring-solution-office-365/settings-multitenant.png)

1. <span data-ttu-id="d7c5e-154">Select **Required permissions** in the **Settings** menu and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-154">Select **Required permissions** in the **Settings** menu and then click **Add**.</span></span>
1. <span data-ttu-id="d7c5e-155">Click **Select an API** and then **Office 365 Management APIs**.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-155">Click **Select an API** and then **Office 365 Management APIs**.</span></span> <span data-ttu-id="d7c5e-156">click **Office 365 Management APIs**.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-156">click **Office 365 Management APIs**.</span></span> <span data-ttu-id="d7c5e-157">Click **Select**.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-157">Click **Select**.</span></span>

    ![Select API](media/monitoring-solution-office-365/select-api.png)

1. <span data-ttu-id="d7c5e-159">Under **Select permissions** select the following options for both **Application permissions** and **Delegated permissions**:</span><span class="sxs-lookup"><span data-stu-id="d7c5e-159">Under **Select permissions** select the following options for both **Application permissions** and **Delegated permissions**:</span></span>
    - <span data-ttu-id="d7c5e-160">Read service health information for your organization</span><span class="sxs-lookup"><span data-stu-id="d7c5e-160">Read service health information for your organization</span></span>
    - <span data-ttu-id="d7c5e-161">Read activity data for your organization</span><span class="sxs-lookup"><span data-stu-id="d7c5e-161">Read activity data for your organization</span></span>
    - <span data-ttu-id="d7c5e-162">Read activity reports for your organization</span><span class="sxs-lookup"><span data-stu-id="d7c5e-162">Read activity reports for your organization</span></span>

    ![Select API](media/monitoring-solution-office-365/select-permissions.png)

1. <span data-ttu-id="d7c5e-164">Click **Select** and then **Done**.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-164">Click **Select** and then **Done**.</span></span>
1. <span data-ttu-id="d7c5e-165">Click **Grant permissions** and then click **Yes** when asked for verification.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-165">Click **Grant permissions** and then click **Yes** when asked for verification.</span></span>

    ![Grant permissions](media/monitoring-solution-office-365/grant-permissions.png)

### <a name="add-a-key-for-the-application"></a><span data-ttu-id="d7c5e-167">Add a key for the application</span><span class="sxs-lookup"><span data-stu-id="d7c5e-167">Add a key for the application</span></span>

1. <span data-ttu-id="d7c5e-168">Select **Keys** in the **Settings** menu.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-168">Select **Keys** in the **Settings** menu.</span></span>
1. <span data-ttu-id="d7c5e-169">Type in a **Description** and **Duration** for the new key.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-169">Type in a **Description** and **Duration** for the new key.</span></span>
1. <span data-ttu-id="d7c5e-170">Click **Save** and then copy the **Value** that's generated.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-170">Click **Save** and then copy the **Value** that's generated.</span></span>

    ![Keys](media/monitoring-solution-office-365/keys.png)

### <a name="add-admin-consent"></a><span data-ttu-id="d7c5e-172">Add admin consent</span><span class="sxs-lookup"><span data-stu-id="d7c5e-172">Add admin consent</span></span>
<span data-ttu-id="d7c5e-173">To enable the administrative account for the first time, you must provide administrative consent for the application.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-173">To enable the administrative account for the first time, you must provide administrative consent for the application.</span></span> <span data-ttu-id="d7c5e-174">You can do this with a PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-174">You can do this with a PowerShell script.</span></span> 

1. <span data-ttu-id="d7c5e-175">Save the following script as *office365_consent.ps1*.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-175">Save the following script as *office365_consent.ps1*.</span></span>

    ```
    param (
        [Parameter(Mandatory=$True)][string]$WorkspaceName,     
        [Parameter(Mandatory=$True)][string]$ResourceGroupName,
        [Parameter(Mandatory=$True)][string]$SubscriptionId
    )
    
    $option = [System.StringSplitOptions]::RemoveEmptyEntries 
    
    IF ($Subscription -eq $null)
        {Login-AzureRmAccount -ErrorAction Stop}
    $Subscription = (Select-AzureRmSubscription -SubscriptionId $($SubscriptionId) -ErrorAction Stop)
    $Subscription
    $Workspace = (Set-AzureRMOperationalInsightsWorkspace -Name $($WorkspaceName) -ResourceGroupName $($ResourceGroupName) -ErrorAction Stop)
    $WorkspaceLocation= $Workspace.Location
    $WorkspaceLocation
    
    Function AdminConsent{
    
    $domain='login.microsoftonline.com'
    switch ($WorkspaceLocation.Replace(" ","").ToLower()) {
           "eastus"   {$OfficeAppClientId="d7eb65b0-8167-4b5d-b371-719a2e5e30cc"; break}
           "westeurope"   {$OfficeAppClientId="c9005da2-023d-40f1-a17a-2b7d91af4ede"; break}
           "southeastasia"   {$OfficeAppClientId="09c5b521-648d-4e29-81ff-7f3a71b27270"; break}
           "australiasoutheast"  {$OfficeAppClientId="f553e464-612b-480f-adb9-14fd8b6cbff8"; break}   
           "westcentralus"  {$OfficeAppClientId="98a2a546-84b4-49c0-88b8-11b011dc8c4e"; break}
           "japaneast"   {$OfficeAppClientId="b07d97d3-731b-4247-93d1-755b5dae91cb"; break}
           "uksouth"   {$OfficeAppClientId="f232cf9b-e7a9-4ebb-a143-be00850cd22a"; break}
           "centralindia"   {$OfficeAppClientId="ffbd6cf4-cba8-4bea-8b08-4fb5ee2a60bd"; break}
           "canadacentral"  {$OfficeAppClientId="c2d686db-f759-43c9-ade5-9d7aeec19455"; break}
           "eastus2"  {$OfficeAppClientId="7eb65b0-8167-4b5d-b371-719a2e5e30cc"; break}
           "westus2"  {$OfficeAppClientId="98a2a546-84b4-49c0-88b8-11b011dc8c4e"; break} #Need to check
           "usgovvirginia" {$OfficeAppClientId="c8b41a87-f8c5-4d10-98a4-f8c11c3933fe"; 
                             $domain='login.microsoftonline.us'; break}
           default {$OfficeAppClientId="55b65fb5-b825-43b5-8972-c8b6875867c1";
                    $domain='login.windows-ppe.net'; break} #Int
        }
    
        $domain
        Start-Process -FilePath  "https://$($domain)/common/adminconsent?client_id=$($OfficeAppClientId)&state=12345"
    }
    
    AdminConsent -ErrorAction Stop
    ```

2. <span data-ttu-id="d7c5e-176">Run the script with the following command.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-176">Run the script with the following command.</span></span>
    ```
    .\office365_consent.ps1 -WorkspaceName <Workspace name> -ResourceGroupName <Resource group name> -SubscriptionId <Subscription ID>
    ```
    <span data-ttu-id="d7c5e-177">Example:</span><span class="sxs-lookup"><span data-stu-id="d7c5e-177">Example:</span></span>

    ```
    .\office365_consent.ps1 -WorkspaceName MyWorkspace -ResourceGroupName MyResourceGroup -SubscriptionId '60b79d74-f4e4-4867-b631- yyyyyyyyyyyy'
    ```

1. <span data-ttu-id="d7c5e-178">You will be presented with a window similar to the one below.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-178">You will be presented with a window similar to the one below.</span></span> <span data-ttu-id="d7c5e-179">Click **Accept**.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-179">Click **Accept**.</span></span>
    
    ![Admin consent](media/monitoring-solution-office-365/admin-consent.png)

### <a name="subscribe-to-log-analytics-workspace"></a><span data-ttu-id="d7c5e-181">Subscribe to Log Analytics workspace</span><span class="sxs-lookup"><span data-stu-id="d7c5e-181">Subscribe to Log Analytics workspace</span></span>
<span data-ttu-id="d7c5e-182">The last step is to subscribe the application to your Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-182">The last step is to subscribe the application to your Log Analytics workspace.</span></span> <span data-ttu-id="d7c5e-183">You also do this with a PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-183">You also do this with a PowerShell script.</span></span>

1. <span data-ttu-id="d7c5e-184">Save the following script as *office365_subscription.ps1*.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-184">Save the following script as *office365_subscription.ps1*.</span></span>

    ```
    param (
        [Parameter(Mandatory=$True)][string]$WorkspaceName,
        [Parameter(Mandatory=$True)][string]$ResourceGroupName,
        [Parameter(Mandatory=$True)][string]$SubscriptionId,
        [Parameter(Mandatory=$True)][string]$OfficeUsername,
        [Parameter(Mandatory=$True)][string]$OfficeTennantId,
        [Parameter(Mandatory=$True)][string]$OfficeClientId,
        [Parameter(Mandatory=$True)][string]$OfficeClientSecret
    )
    $line='#-------------------------------------------------------------------------------------------------------------------------------------------------------------------------'
    $line
    IF ($Subscription -eq $null)
        {Login-AzureRmAccount -ErrorAction Stop}
    $Subscription = (Select-AzureRmSubscription -SubscriptionId $($SubscriptionId) -ErrorAction Stop)
    $Subscription
    $option = [System.StringSplitOptions]::RemoveEmptyEntries 
    $Workspace = (Set-AzureRMOperationalInsightsWorkspace -Name $($WorkspaceName) -ResourceGroupName $($ResourceGroupName) -ErrorAction Stop)
    $Workspace
    $WorkspaceLocation= $Workspace.Location
    $OfficeClientSecret =[uri]::EscapeDataString($OfficeClientSecret)
    
    # Client ID for Azure PowerShell
    $clientId = "1950a258-227b-4e31-a9cf-717495945fc2"
    # Set redirect URI for Azure PowerShell
    $redirectUri = "urn:ietf:wg:oauth:2.0:oob"
    $domain='login.microsoftonline.com'
    $adTenant = $Subscription[0].Tenant.Id
    $authority = "https://login.windows.net/$adTenant";
    $ARMResource ="https://management.azure.com/";
    $xms_client_tenant_Id ='55b65fb5-b825-43b5-8972-c8b6875867c1'
    
    switch ($WorkspaceLocation) {
           "USGov Virginia" { 
                             $domain='login.microsoftonline.us';
                              $authority = "https://login.microsoftonline.us/$adTenant";
                              $ARMResource ="https://management.usgovcloudapi.net/"; break} # US Gov Virginia
           default {
                    $domain='login.microsoftonline.com'; 
                    $authority = "https://login.windows.net/$adTenant";
                    $ARMResource ="https://management.azure.com/";break} 
                    }
    
    Function RESTAPI-Auth { 
    
    $global:SubscriptionID = $Subscription.SubscriptionId
    # Set Resource URI to Azure Service Management API
    $resourceAppIdURIARM=$ARMResource;
    # Authenticate and Acquire Token 
    # Create Authentication Context tied to Azure AD Tenant
    $authContext = New-Object "Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext" -ArgumentList $authority
    # Acquire token
    $global:authResultARM = $authContext.AcquireToken($resourceAppIdURIARM, $clientId, $redirectUri, "Auto")
    $authHeader = $global:authResultARM.CreateAuthorizationHeader()
    $authHeader
    }
    
    Function Failure {
    $line
    $formatstring = "{0} : {1}`n{2}`n" +
                    "    + CategoryInfo          : {3}`n" +
                    "    + FullyQualifiedErrorId : {4}`n"
    $fields = $_.InvocationInfo.MyCommand.Name,
              $_.ErrorDetails.Message,
              $_.InvocationInfo.PositionMessage,
              $_.CategoryInfo.ToString(),
              $_.FullyQualifiedErrorId
    
    $formatstring -f $fields
    $_.Exception.Response
    
    $line
    break
    }
    
    Function Connection-API
    {
    $authHeader = $global:authResultARM.CreateAuthorizationHeader()
    $ResourceName = "https://manage.office.com"
    $SubscriptionId   =  $Subscription[0].Subscription.Id
    
    $line
    $connectionAPIUrl = $ARMResource + 'subscriptions/' + $SubscriptionId + '/resourceGroups/' + $ResourceGroupName + '/providers/Microsoft.OperationalInsights/workspaces/' + $WorkspaceName + '/connections/office365connection_' + $SubscriptionId + $OfficeTennantId + '?api-version=2017-04-26-preview'
    $connectionAPIUrl
    $line
    
    $xms_client_tenant_Id ='1da8f770-27f4-4351-8cb3-43ee54f14759'
    
    $BodyString = "{
                    'properties': {
                                    'AuthProvider':'Office365',
                                    'clientId': '" + $OfficeClientId + "',
                                    'clientSecret': '" + $OfficeClientSecret + "',
                                    'Username': '" + $OfficeUsername   + "',
                                    'Url': 'https://$($domain)/" + $OfficeTennantId + "/oauth2/token',
                                  },
                    'etag': '*',
                    'kind': 'Connection',
                    'solution': 'Connection',
                   }"
    
    $params = @{
        ContentType = 'application/json'
        Headers = @{
        'Authorization'="$($authHeader)"
        'x-ms-client-tenant-id'=$xms_client_tenant_Id #Prod-'1da8f770-27f4-4351-8cb3-43ee54f14759'
        'Content-Type' = 'application/json'
        }
        Body = $BodyString
        Method = 'Put'
        URI = $connectionAPIUrl
    }
    $response = Invoke-WebRequest @params 
    $response
    $line
    
    }
    
    Function Office-Subscribe-Call{
    try{
    #----------------------------------------------------------------------------------------------------------------------------------------------
    $authHeader = $global:authResultARM.CreateAuthorizationHeader()
    $SubscriptionId   =  $Subscription[0].Subscription.Id
    $OfficeAPIUrl = $ARMResource + 'subscriptions/' + $SubscriptionId + '/resourceGroups/' + $ResourceGroupName + '/providers/Microsoft.OperationalInsights/workspaces/' + $WorkspaceName + '/datasources/office365datasources_' + $SubscriptionId + $OfficeTennantId + '?api-version=2015-11-01-preview'
    
    $OfficeBodyString = "{
                    'properties': {
                                    'AuthProvider':'Office365',
                                    'office365TenantID': '" + $OfficeTennantId + "',
                                    'connectionID': 'office365connection_" + $SubscriptionId + $OfficeTennantId + "',
                                    'office365AdminUsername': '" + $OfficeUsername + "',
                                    'contentTypes':'Audit.Exchange,Audit.AzureActiveDirectory,Audit.Sharepoint'
                                  },
                    'etag': '*',
                    'kind': 'Office365',
                    'solution': 'Office365',
                   }"
    
    $Officeparams = @{
        ContentType = 'application/json'
        Headers = @{
        'Authorization'="$($authHeader)"
        'x-ms-client-tenant-id'=$xms_client_tenant_Id
        'Content-Type' = 'application/json'
        }
        Body = $OfficeBodyString
        Method = 'Put'
        URI = $OfficeAPIUrl
      }
    
    $officeresponse = Invoke-WebRequest @Officeparams 
    $officeresponse
    }
    catch{ Failure }
    }
    
    #GetDetails 
    RESTAPI-Auth -ErrorAction Stop
    Connection-API -ErrorAction Stop
    Office-Subscribe-Call -ErrorAction Stop
    ```

2. <span data-ttu-id="d7c5e-185">Run the script with the following command:</span><span class="sxs-lookup"><span data-stu-id="d7c5e-185">Run the script with the following command:</span></span>
    ```
    .\office365_subscription.ps1 -WorkspaceName <Log Analytics workspace name> -ResourceGroupName <Resource Group name> -SubscriptionId <Subscription ID> -OfficeUsername <OfficeUsername> -OfficeTennantID <Tenant ID> -OfficeClientId <Client ID> -OfficeClientSecret <Client secret>
    ```
    <span data-ttu-id="d7c5e-186">Example:</span><span class="sxs-lookup"><span data-stu-id="d7c5e-186">Example:</span></span>

    ```
    .\office365_subscription.ps1 -WorkspaceName MyWorkspace -ResourceGroupName MyResourceGroup -SubscriptionId '60b79d74-f4e4-4867-b631-yyyyyyyyyyyy' -OfficeUsername 'admin@contoso.com' -OfficeTennantID 'ce4464f8-a172-4dcf-b675-xxxxxxxxxxxx' -OfficeClientId 'f8f14c50-5438-4c51-8956-zzzzzzzzzzzz' -OfficeClientSecret 'y5Lrwthu6n5QgLOWlqhvKqtVUZXX0exrA2KRHmtHgQb='
    ```

### <a name="troubleshooting"></a><span data-ttu-id="d7c5e-187">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="d7c5e-187">Troubleshooting</span></span>

<span data-ttu-id="d7c5e-188">You may see the following error if you attempt to create a subscription after the subscription already exists.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-188">You may see the following error if you attempt to create a subscription after the subscription already exists.</span></span>

```
Invoke-WebRequest : {"Message":"An error has occurred."}
At C:\Users\v-tanmah\Desktop\ps scripts\office365_subscription.ps1:161 char:19
+ $officeresponse = Invoke-WebRequest @Officeparams
+                   ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (System.Net.HttpWebRequest:HttpWebRequest) [Invoke-WebRequest], WebException
    + FullyQualifiedErrorId : WebCmdletWebResponseException,Microsoft.PowerShell.Commands.InvokeWebRequestCommand 
```

<span data-ttu-id="d7c5e-189">You may see the following error if invalid parameter values are provided.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-189">You may see the following error if invalid parameter values are provided.</span></span>

```
Select-AzureRmSubscription : Please provide a valid tenant or a valid subscription.
At line:12 char:18
+ ... cription = (Select-AzureRmSubscription -SubscriptionId $($Subscriptio ...
+                 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureRmContext], ArgumentException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.Profile.SetAzureRMContextCommand

```

## <a name="uninstall"></a><span data-ttu-id="d7c5e-190">Uninstall</span><span class="sxs-lookup"><span data-stu-id="d7c5e-190">Uninstall</span></span>
<span data-ttu-id="d7c5e-191">You can remove the Office 365 management solution using the process in [Remove a management solution](../monitoring/monitoring-solutions.md#remove-a-management-solution).</span><span class="sxs-lookup"><span data-stu-id="d7c5e-191">You can remove the Office 365 management solution using the process in [Remove a management solution](../monitoring/monitoring-solutions.md#remove-a-management-solution).</span></span> <span data-ttu-id="d7c5e-192">This will not stop data being collected from Office 365 into Log Analytics though.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-192">This will not stop data being collected from Office 365 into Log Analytics though.</span></span> <span data-ttu-id="d7c5e-193">Follow the procedure below to unsubscribe from Office 365 and stop collecting data.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-193">Follow the procedure below to unsubscribe from Office 365 and stop collecting data.</span></span>

1. <span data-ttu-id="d7c5e-194">Save the following script as *office365_unsubscribe.ps1*.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-194">Save the following script as *office365_unsubscribe.ps1*.</span></span>

    ```
    param (
        [Parameter(Mandatory=$True)][string]$WorkspaceName,
        [Parameter(Mandatory=$True)][string]$ResourceGroupName,
        [Parameter(Mandatory=$True)][string]$SubscriptionId,
        [Parameter(Mandatory=$True)][string]$OfficeTennantId
    )
    $line='#-------------------------------------------------------------------------------------------------------------------------------------------------------------------------'
    
    $line
    IF ($Subscription -eq $null)
        {Login-AzureRmAccount -ErrorAction Stop}
    $Subscription = (Select-AzureRmSubscription -SubscriptionId $($SubscriptionId) -ErrorAction Stop)
    $Subscription
    $option = [System.StringSplitOptions]::RemoveEmptyEntries 
    $Workspace = (Set-AzureRMOperationalInsightsWorkspace -Name $($WorkspaceName) -ResourceGroupName $($ResourceGroupName) -ErrorAction Stop)
    $Workspace
    $WorkspaceLocation= $Workspace.Location
    
    # Client ID for Azure PowerShell
    $clientId = "1950a258-227b-4e31-a9cf-717495945fc2"
    # Set redirect URI for Azure PowerShell
    $redirectUri = "urn:ietf:wg:oauth:2.0:oob"
    $domain='login.microsoftonline.com'
    $adTenant =  $Subscription[0].Tenant.Id
    $authority = "https://login.windows.net/$adTenant";
    $ARMResource ="https://management.azure.com/";
    $xms_client_tenant_Id ='55b65fb5-b825-43b5-8972-c8b6875867c1'
    
    switch ($WorkspaceLocation) {
           "USGov Virginia" { 
                             $domain='login.microsoftonline.us';
                              $authority = "https://login.microsoftonline.us/$adTenant";
                              $ARMResource ="https://management.usgovcloudapi.net/"; break} # US Gov Virginia
           default {
                    $domain='login.microsoftonline.com'; 
                    $authority = "https://login.windows.net/$adTenant";
                    $ARMResource ="https://management.azure.com/";break} 
                    }
    
    Function RESTAPI-Auth { 
    
    $global:SubscriptionID = $Subscription.SubscriptionId
    # Set Resource URI to Azure Service Management API
    $resourceAppIdURIARM=$ARMResource;
    # Authenticate and Acquire Token 
    # Create Authentication Context tied to Azure AD Tenant
    $authContext = New-Object "Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext" -ArgumentList $authority
    # Acquire token
    $global:authResultARM = $authContext.AcquireToken($resourceAppIdURIARM, $clientId, $redirectUri, "Auto")
    $authHeader = $global:authResultARM.CreateAuthorizationHeader()
    $authHeader
    }
    
    Function Office-UnSubscribe-Call{
    
    #----------------------------------------------------------------------------------------------------------------------------------------------
    $authHeader = $global:authResultARM.CreateAuthorizationHeader()
    $ResourceName = "https://manage.office.com"
    $SubscriptionId   = $Subscription[0].Subscription.Id
    $OfficeAPIUrl = $ARMResource + 'subscriptions/' + $SubscriptionId + '/resourceGroups/' + $ResourceGroupName + '/providers/Microsoft.OperationalInsights/workspaces/' + $WorkspaceName + '/datasources/office365datasources_'  + $SubscriptionId + $OfficeTennantId + '?api-version=2015-11-01-preview'
    
    $Officeparams = @{
        ContentType = 'application/json'
        Headers = @{
        'Authorization'="$($authHeader)"
        'x-ms-client-tenant-id'=$xms_client_tenant_Id
        'Content-Type' = 'application/json'
        }
        Method = 'Delete'
        URI = $OfficeAPIUrl
      }
    
    $officeresponse = Invoke-WebRequest @Officeparams 
    $officeresponse
    
    }
    
    #GetDetails 
    RESTAPI-Auth -ErrorAction Stop
    Office-UnSubscribe-Call -ErrorAction Stop
    ```

2. <span data-ttu-id="d7c5e-195">Run the script with the following command:</span><span class="sxs-lookup"><span data-stu-id="d7c5e-195">Run the script with the following command:</span></span>

    ```
    .\office365_unsubscribe.ps1 -WorkspaceName <Log Analytics workspace name> -ResourceGroupName <Resource Group name> -SubscriptionId <Subscription ID> -OfficeTennantID <Tenant ID> 
    ```

    <span data-ttu-id="d7c5e-196">Example:</span><span class="sxs-lookup"><span data-stu-id="d7c5e-196">Example:</span></span>

    ```
    .\office365_unsubscribe.ps1 -WorkspaceName MyWorkspace -ResourceGroupName MyResourceGroup -SubscriptionId '60b79d74-f4e4-4867-b631-yyyyyyyyyyyy' -OfficeTennantID 'ce4464f8-a172-4dcf-b675-xxxxxxxxxxxx'
    ```

## <a name="data-collection"></a><span data-ttu-id="d7c5e-197">Data collection</span><span class="sxs-lookup"><span data-stu-id="d7c5e-197">Data collection</span></span>
### <a name="supported-agents"></a><span data-ttu-id="d7c5e-198">Supported agents</span><span class="sxs-lookup"><span data-stu-id="d7c5e-198">Supported agents</span></span>
<span data-ttu-id="d7c5e-199">The Office 365 solution doesn't retrieve data from any of the [OMS agents](../log-analytics/log-analytics-data-sources.md).</span><span class="sxs-lookup"><span data-stu-id="d7c5e-199">The Office 365 solution doesn't retrieve data from any of the [OMS agents](../log-analytics/log-analytics-data-sources.md).</span></span>  <span data-ttu-id="d7c5e-200">It retrieves data directly from Office 365.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-200">It retrieves data directly from Office 365.</span></span>

### <a name="collection-frequency"></a><span data-ttu-id="d7c5e-201">Collection frequency</span><span class="sxs-lookup"><span data-stu-id="d7c5e-201">Collection frequency</span></span>
<span data-ttu-id="d7c5e-202">It may take a few hours for data to initially be collected.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-202">It may take a few hours for data to initially be collected.</span></span> <span data-ttu-id="d7c5e-203">Once it starts collecting, Office 365 sends a [webhook notification](https://msdn.microsoft.com/office-365/office-365-management-activity-api-reference#receiving-notifications) with detailed data to Log Analytics each time a record is created.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-203">Once it starts collecting, Office 365 sends a [webhook notification](https://msdn.microsoft.com/office-365/office-365-management-activity-api-reference#receiving-notifications) with detailed data to Log Analytics each time a record is created.</span></span> <span data-ttu-id="d7c5e-204">This record is available in Log Analytics within a few minutes after being received.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-204">This record is available in Log Analytics within a few minutes after being received.</span></span>

## <a name="using-the-solution"></a><span data-ttu-id="d7c5e-205">Using the solution</span><span class="sxs-lookup"><span data-stu-id="d7c5e-205">Using the solution</span></span>
<span data-ttu-id="d7c5e-206">When you add the Office 365 solution to your Log Analytics workspace, the **Office 365** tile will be added to your dashboard.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-206">When you add the Office 365 solution to your Log Analytics workspace, the **Office 365** tile will be added to your dashboard.</span></span> <span data-ttu-id="d7c5e-207">This tile displays a count and graphical representation of the number of computers in your environment and their update compliance.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-207">This tile displays a count and graphical representation of the number of computers in your environment and their update compliance.</span></span><br><br>
<span data-ttu-id="d7c5e-208">![Office 365 Summary Tile](media/monitoring-solution-office-365/tile.png)</span><span class="sxs-lookup"><span data-stu-id="d7c5e-208">![Office 365 Summary Tile](media/monitoring-solution-office-365/tile.png)</span></span>  

<span data-ttu-id="d7c5e-209">Click on the **Office 365** tile to open the **Office 365** dashboard.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-209">Click on the **Office 365** tile to open the **Office 365** dashboard.</span></span>

![Office 365 Dashboard](media/monitoring-solution-office-365/dashboard.png)  

<span data-ttu-id="d7c5e-211">The dashboard includes the columns in the following table.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-211">The dashboard includes the columns in the following table.</span></span> <span data-ttu-id="d7c5e-212">Each column lists the top ten alerts by count matching that column's criteria for the specified scope and time range.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-212">Each column lists the top ten alerts by count matching that column's criteria for the specified scope and time range.</span></span> <span data-ttu-id="d7c5e-213">You can run a log search that provides the entire list by clicking See all at the bottom of the column or by clicking the column header.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-213">You can run a log search that provides the entire list by clicking See all at the bottom of the column or by clicking the column header.</span></span>

| <span data-ttu-id="d7c5e-214">Column</span><span class="sxs-lookup"><span data-stu-id="d7c5e-214">Column</span></span> | <span data-ttu-id="d7c5e-215">Description</span><span class="sxs-lookup"><span data-stu-id="d7c5e-215">Description</span></span> |
|:--|:--|
| <span data-ttu-id="d7c5e-216">Operations</span><span class="sxs-lookup"><span data-stu-id="d7c5e-216">Operations</span></span> | <span data-ttu-id="d7c5e-217">Provides information about the active users from your all monitored Office 365 subscriptions.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-217">Provides information about the active users from your all monitored Office 365 subscriptions.</span></span> <span data-ttu-id="d7c5e-218">You will also be able to see the number of activities that happen over time.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-218">You will also be able to see the number of activities that happen over time.</span></span>
| <span data-ttu-id="d7c5e-219">Exchange</span><span class="sxs-lookup"><span data-stu-id="d7c5e-219">Exchange</span></span> | <span data-ttu-id="d7c5e-220">Shows the breakdown of Exchange Server activities such as Add-Mailbox Permission, or Set-Mailbox.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-220">Shows the breakdown of Exchange Server activities such as Add-Mailbox Permission, or Set-Mailbox.</span></span> |
| <span data-ttu-id="d7c5e-221">SharePoint</span><span class="sxs-lookup"><span data-stu-id="d7c5e-221">SharePoint</span></span> | <span data-ttu-id="d7c5e-222">Shows the top activities that users perform on SharePoint documents.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-222">Shows the top activities that users perform on SharePoint documents.</span></span> <span data-ttu-id="d7c5e-223">When you drill down from this tile, the search page shows the details of these activities, such as the target document and the location of this activity.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-223">When you drill down from this tile, the search page shows the details of these activities, such as the target document and the location of this activity.</span></span> <span data-ttu-id="d7c5e-224">For example, for a File Accessed event, you will be able to see the document that’s being accessed, its associated account name, and IP address.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-224">For example, for a File Accessed event, you will be able to see the document that’s being accessed, its associated account name, and IP address.</span></span> |
| <span data-ttu-id="d7c5e-225">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d7c5e-225">Azure Active Directory</span></span> | <span data-ttu-id="d7c5e-226">Includes top user activities, such as Reset User Password and Login Attempts.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-226">Includes top user activities, such as Reset User Password and Login Attempts.</span></span> <span data-ttu-id="d7c5e-227">When you drill down, you will be able to see the details of these activities like the Result Status.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-227">When you drill down, you will be able to see the details of these activities like the Result Status.</span></span> <span data-ttu-id="d7c5e-228">This is mostly helpful if you want to monitor suspicious activities on your Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-228">This is mostly helpful if you want to monitor suspicious activities on your Azure Active Directory.</span></span> |




## <a name="log-analytics-records"></a><span data-ttu-id="d7c5e-229">Log Analytics records</span><span class="sxs-lookup"><span data-stu-id="d7c5e-229">Log Analytics records</span></span>

<span data-ttu-id="d7c5e-230">All records created in the Log Analytics workspace by the Office 365 solution have a **Type** of **OfficeActivity**.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-230">All records created in the Log Analytics workspace by the Office 365 solution have a **Type** of **OfficeActivity**.</span></span>  <span data-ttu-id="d7c5e-231">The **OfficeWorkload** property determines which Office 365 service the record refers to - Exchange, AzureActiveDirectory, SharePoint, or OneDrive.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-231">The **OfficeWorkload** property determines which Office 365 service the record refers to - Exchange, AzureActiveDirectory, SharePoint, or OneDrive.</span></span>  <span data-ttu-id="d7c5e-232">The **RecordType** property specifies the type of operation.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-232">The **RecordType** property specifies the type of operation.</span></span>  <span data-ttu-id="d7c5e-233">The properties will vary for each operation type and are shown in the tables below.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-233">The properties will vary for each operation type and are shown in the tables below.</span></span>

### <a name="common-properties"></a><span data-ttu-id="d7c5e-234">Common properties</span><span class="sxs-lookup"><span data-stu-id="d7c5e-234">Common properties</span></span>
<span data-ttu-id="d7c5e-235">The following properties are common to all Office 365 records.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-235">The following properties are common to all Office 365 records.</span></span>

| <span data-ttu-id="d7c5e-236">Property</span><span class="sxs-lookup"><span data-stu-id="d7c5e-236">Property</span></span> | <span data-ttu-id="d7c5e-237">Description</span><span class="sxs-lookup"><span data-stu-id="d7c5e-237">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d7c5e-238">Type</span><span class="sxs-lookup"><span data-stu-id="d7c5e-238">Type</span></span> | <span data-ttu-id="d7c5e-239">*OfficeActivity*</span><span class="sxs-lookup"><span data-stu-id="d7c5e-239">*OfficeActivity*</span></span> |
| <span data-ttu-id="d7c5e-240">ClientIP</span><span class="sxs-lookup"><span data-stu-id="d7c5e-240">ClientIP</span></span> | <span data-ttu-id="d7c5e-241">The IP address of the device that was used when the activity was logged.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-241">The IP address of the device that was used when the activity was logged.</span></span> <span data-ttu-id="d7c5e-242">The IP address is displayed in either an IPv4 or IPv6 address format.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-242">The IP address is displayed in either an IPv4 or IPv6 address format.</span></span> |
| <span data-ttu-id="d7c5e-243">OfficeWorkload</span><span class="sxs-lookup"><span data-stu-id="d7c5e-243">OfficeWorkload</span></span> | <span data-ttu-id="d7c5e-244">Office 365 service that the record refers to.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-244">Office 365 service that the record refers to.</span></span><br><br><span data-ttu-id="d7c5e-245">AzureActiveDirectory</span><span class="sxs-lookup"><span data-stu-id="d7c5e-245">AzureActiveDirectory</span></span><br><span data-ttu-id="d7c5e-246">Exchange</span><span class="sxs-lookup"><span data-stu-id="d7c5e-246">Exchange</span></span><br><span data-ttu-id="d7c5e-247">SharePoint</span><span class="sxs-lookup"><span data-stu-id="d7c5e-247">SharePoint</span></span>|
| <span data-ttu-id="d7c5e-248">Operation</span><span class="sxs-lookup"><span data-stu-id="d7c5e-248">Operation</span></span> | <span data-ttu-id="d7c5e-249">The name of the user or admin activity.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-249">The name of the user or admin activity.</span></span>  |
| <span data-ttu-id="d7c5e-250">OrganizationId</span><span class="sxs-lookup"><span data-stu-id="d7c5e-250">OrganizationId</span></span> | <span data-ttu-id="d7c5e-251">The GUID for your organization's Office 365 tenant.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-251">The GUID for your organization's Office 365 tenant.</span></span> <span data-ttu-id="d7c5e-252">This value will always be the same for your organization, regardless of the Office 365 service in which it occurs.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-252">This value will always be the same for your organization, regardless of the Office 365 service in which it occurs.</span></span> |
| <span data-ttu-id="d7c5e-253">RecordType</span><span class="sxs-lookup"><span data-stu-id="d7c5e-253">RecordType</span></span> | <span data-ttu-id="d7c5e-254">Type of of operation performed.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-254">Type of of operation performed.</span></span> |
| <span data-ttu-id="d7c5e-255">ResultStatus</span><span class="sxs-lookup"><span data-stu-id="d7c5e-255">ResultStatus</span></span> | <span data-ttu-id="d7c5e-256">Indicates whether the action (specified in the Operation property) was successful or not.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-256">Indicates whether the action (specified in the Operation property) was successful or not.</span></span> <span data-ttu-id="d7c5e-257">Possible values are Succeeded, PartiallySucceded, or Failed.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-257">Possible values are Succeeded, PartiallySucceded, or Failed.</span></span> <span data-ttu-id="d7c5e-258">For Exchange admin activity, the value is either True or False.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-258">For Exchange admin activity, the value is either True or False.</span></span> |
| <span data-ttu-id="d7c5e-259">UserId</span><span class="sxs-lookup"><span data-stu-id="d7c5e-259">UserId</span></span> | <span data-ttu-id="d7c5e-260">The UPN (User Principal Name) of the user who performed the action that resulted in the record being logged; for example, my_name@my_domain_name.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-260">The UPN (User Principal Name) of the user who performed the action that resulted in the record being logged; for example, my_name@my_domain_name.</span></span> <span data-ttu-id="d7c5e-261">Note that records for activity performed by system accounts (such as SHAREPOINT\system or NTAUTHORITY\SYSTEM) are also included.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-261">Note that records for activity performed by system accounts (such as SHAREPOINT\system or NTAUTHORITY\SYSTEM) are also included.</span></span> | 
| <span data-ttu-id="d7c5e-262">UserKey</span><span class="sxs-lookup"><span data-stu-id="d7c5e-262">UserKey</span></span> | <span data-ttu-id="d7c5e-263">An alternative ID for the user identified in the UserId property.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-263">An alternative ID for the user identified in the UserId property.</span></span>  <span data-ttu-id="d7c5e-264">For example, this property is populated with the passport unique ID (PUID) for events performed by users in SharePoint, OneDrive for Business, and Exchange.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-264">For example, this property is populated with the passport unique ID (PUID) for events performed by users in SharePoint, OneDrive for Business, and Exchange.</span></span> <span data-ttu-id="d7c5e-265">This property may also specify the same value as the UserID property for events occurring in other services and events performed by system accounts</span><span class="sxs-lookup"><span data-stu-id="d7c5e-265">This property may also specify the same value as the UserID property for events occurring in other services and events performed by system accounts</span></span>|
| <span data-ttu-id="d7c5e-266">UserType</span><span class="sxs-lookup"><span data-stu-id="d7c5e-266">UserType</span></span> | <span data-ttu-id="d7c5e-267">The type of user that performed the operation.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-267">The type of user that performed the operation.</span></span><br><br><span data-ttu-id="d7c5e-268">Admin</span><span class="sxs-lookup"><span data-stu-id="d7c5e-268">Admin</span></span><br><span data-ttu-id="d7c5e-269">Application</span><span class="sxs-lookup"><span data-stu-id="d7c5e-269">Application</span></span><br><span data-ttu-id="d7c5e-270">DcAdmin</span><span class="sxs-lookup"><span data-stu-id="d7c5e-270">DcAdmin</span></span><br><span data-ttu-id="d7c5e-271">Regular</span><span class="sxs-lookup"><span data-stu-id="d7c5e-271">Regular</span></span><br><span data-ttu-id="d7c5e-272">Reserved</span><span class="sxs-lookup"><span data-stu-id="d7c5e-272">Reserved</span></span><br><span data-ttu-id="d7c5e-273">ServicePrincipal</span><span class="sxs-lookup"><span data-stu-id="d7c5e-273">ServicePrincipal</span></span><br><span data-ttu-id="d7c5e-274">System</span><span class="sxs-lookup"><span data-stu-id="d7c5e-274">System</span></span> |


### <a name="azure-active-directory-base"></a><span data-ttu-id="d7c5e-275">Azure Active Directory base</span><span class="sxs-lookup"><span data-stu-id="d7c5e-275">Azure Active Directory base</span></span>
<span data-ttu-id="d7c5e-276">The following properties are common to all Azure Active Directory records.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-276">The following properties are common to all Azure Active Directory records.</span></span>

| <span data-ttu-id="d7c5e-277">Property</span><span class="sxs-lookup"><span data-stu-id="d7c5e-277">Property</span></span> | <span data-ttu-id="d7c5e-278">Description</span><span class="sxs-lookup"><span data-stu-id="d7c5e-278">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d7c5e-279">OfficeWorkload</span><span class="sxs-lookup"><span data-stu-id="d7c5e-279">OfficeWorkload</span></span> | <span data-ttu-id="d7c5e-280">AzureActiveDirectory</span><span class="sxs-lookup"><span data-stu-id="d7c5e-280">AzureActiveDirectory</span></span> |
| <span data-ttu-id="d7c5e-281">RecordType</span><span class="sxs-lookup"><span data-stu-id="d7c5e-281">RecordType</span></span>     | <span data-ttu-id="d7c5e-282">AzureActiveDirectory</span><span class="sxs-lookup"><span data-stu-id="d7c5e-282">AzureActiveDirectory</span></span> |
| <span data-ttu-id="d7c5e-283">AzureActiveDirectory_EventType</span><span class="sxs-lookup"><span data-stu-id="d7c5e-283">AzureActiveDirectory_EventType</span></span> | <span data-ttu-id="d7c5e-284">The type of Azure AD event.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-284">The type of Azure AD event.</span></span> |
| <span data-ttu-id="d7c5e-285">ExtendedProperties</span><span class="sxs-lookup"><span data-stu-id="d7c5e-285">ExtendedProperties</span></span> | <span data-ttu-id="d7c5e-286">The extended properties of the Azure AD event.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-286">The extended properties of the Azure AD event.</span></span> |


### <a name="azure-active-directory-account-logon"></a><span data-ttu-id="d7c5e-287">Azure Active Directory Account logon</span><span class="sxs-lookup"><span data-stu-id="d7c5e-287">Azure Active Directory Account logon</span></span>
<span data-ttu-id="d7c5e-288">These records are created when an Active Directory user attempts to log on.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-288">These records are created when an Active Directory user attempts to log on.</span></span>

| <span data-ttu-id="d7c5e-289">Property</span><span class="sxs-lookup"><span data-stu-id="d7c5e-289">Property</span></span> | <span data-ttu-id="d7c5e-290">Description</span><span class="sxs-lookup"><span data-stu-id="d7c5e-290">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d7c5e-291">OfficeWorkload</span><span class="sxs-lookup"><span data-stu-id="d7c5e-291">OfficeWorkload</span></span> | <span data-ttu-id="d7c5e-292">AzureActiveDirectory</span><span class="sxs-lookup"><span data-stu-id="d7c5e-292">AzureActiveDirectory</span></span> |
| <span data-ttu-id="d7c5e-293">RecordType</span><span class="sxs-lookup"><span data-stu-id="d7c5e-293">RecordType</span></span>     | <span data-ttu-id="d7c5e-294">AzureActiveDirectoryAccountLogon</span><span class="sxs-lookup"><span data-stu-id="d7c5e-294">AzureActiveDirectoryAccountLogon</span></span> |
| <span data-ttu-id="d7c5e-295">Application</span><span class="sxs-lookup"><span data-stu-id="d7c5e-295">Application</span></span> | <span data-ttu-id="d7c5e-296">The application that triggers the account login event, such as Office 15.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-296">The application that triggers the account login event, such as Office 15.</span></span> |
| <span data-ttu-id="d7c5e-297">Client</span><span class="sxs-lookup"><span data-stu-id="d7c5e-297">Client</span></span> | <span data-ttu-id="d7c5e-298">Details about the client device, device OS, and device browser that was used for the of the account login event.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-298">Details about the client device, device OS, and device browser that was used for the of the account login event.</span></span> |
| <span data-ttu-id="d7c5e-299">LoginStatus</span><span class="sxs-lookup"><span data-stu-id="d7c5e-299">LoginStatus</span></span> | <span data-ttu-id="d7c5e-300">This property is from OrgIdLogon.LoginStatus directly.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-300">This property is from OrgIdLogon.LoginStatus directly.</span></span> <span data-ttu-id="d7c5e-301">The mapping of various interesting logon failures could be done by alerting algorithms.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-301">The mapping of various interesting logon failures could be done by alerting algorithms.</span></span> |
| <span data-ttu-id="d7c5e-302">UserDomain</span><span class="sxs-lookup"><span data-stu-id="d7c5e-302">UserDomain</span></span> | <span data-ttu-id="d7c5e-303">The Tenant Identity Information (TII).</span><span class="sxs-lookup"><span data-stu-id="d7c5e-303">The Tenant Identity Information (TII).</span></span> | 


### <a name="azure-active-directory"></a><span data-ttu-id="d7c5e-304">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d7c5e-304">Azure Active Directory</span></span>
<span data-ttu-id="d7c5e-305">These records are created when change or additions are made to Azure Active Directory objects.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-305">These records are created when change or additions are made to Azure Active Directory objects.</span></span>

| <span data-ttu-id="d7c5e-306">Property</span><span class="sxs-lookup"><span data-stu-id="d7c5e-306">Property</span></span> | <span data-ttu-id="d7c5e-307">Description</span><span class="sxs-lookup"><span data-stu-id="d7c5e-307">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d7c5e-308">OfficeWorkload</span><span class="sxs-lookup"><span data-stu-id="d7c5e-308">OfficeWorkload</span></span> | <span data-ttu-id="d7c5e-309">AzureActiveDirectory</span><span class="sxs-lookup"><span data-stu-id="d7c5e-309">AzureActiveDirectory</span></span> |
| <span data-ttu-id="d7c5e-310">RecordType</span><span class="sxs-lookup"><span data-stu-id="d7c5e-310">RecordType</span></span>     | <span data-ttu-id="d7c5e-311">AzureActiveDirectory</span><span class="sxs-lookup"><span data-stu-id="d7c5e-311">AzureActiveDirectory</span></span> |
| <span data-ttu-id="d7c5e-312">AADTarget</span><span class="sxs-lookup"><span data-stu-id="d7c5e-312">AADTarget</span></span> | <span data-ttu-id="d7c5e-313">The user that the action (identified by the Operation property) was performed on.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-313">The user that the action (identified by the Operation property) was performed on.</span></span> |
| <span data-ttu-id="d7c5e-314">Actor</span><span class="sxs-lookup"><span data-stu-id="d7c5e-314">Actor</span></span> | <span data-ttu-id="d7c5e-315">The user or service principal that performed the action.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-315">The user or service principal that performed the action.</span></span> |
| <span data-ttu-id="d7c5e-316">ActorContextId</span><span class="sxs-lookup"><span data-stu-id="d7c5e-316">ActorContextId</span></span> | <span data-ttu-id="d7c5e-317">The GUID of the organization that the actor belongs to.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-317">The GUID of the organization that the actor belongs to.</span></span> |
| <span data-ttu-id="d7c5e-318">ActorIpAddress</span><span class="sxs-lookup"><span data-stu-id="d7c5e-318">ActorIpAddress</span></span> | <span data-ttu-id="d7c5e-319">The actor's IP address in IPV4 or IPV6 address format.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-319">The actor's IP address in IPV4 or IPV6 address format.</span></span> |
| <span data-ttu-id="d7c5e-320">InterSystemsId</span><span class="sxs-lookup"><span data-stu-id="d7c5e-320">InterSystemsId</span></span> | <span data-ttu-id="d7c5e-321">The GUID that track the actions across components within the Office 365 service.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-321">The GUID that track the actions across components within the Office 365 service.</span></span> |
| <span data-ttu-id="d7c5e-322">IntraSystemId</span><span class="sxs-lookup"><span data-stu-id="d7c5e-322">IntraSystemId</span></span> |   <span data-ttu-id="d7c5e-323">The GUID that's generated by Azure Active Directory to track the action.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-323">The GUID that's generated by Azure Active Directory to track the action.</span></span> |
| <span data-ttu-id="d7c5e-324">SupportTicketId</span><span class="sxs-lookup"><span data-stu-id="d7c5e-324">SupportTicketId</span></span> | <span data-ttu-id="d7c5e-325">The customer support ticket ID for the action in "act-on-behalf-of" situations.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-325">The customer support ticket ID for the action in "act-on-behalf-of" situations.</span></span> |
| <span data-ttu-id="d7c5e-326">TargetContextId</span><span class="sxs-lookup"><span data-stu-id="d7c5e-326">TargetContextId</span></span> | <span data-ttu-id="d7c5e-327">The GUID of the organization that the targeted user belongs to.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-327">The GUID of the organization that the targeted user belongs to.</span></span> |


### <a name="data-center-security"></a><span data-ttu-id="d7c5e-328">Data Center Security</span><span class="sxs-lookup"><span data-stu-id="d7c5e-328">Data Center Security</span></span>
<span data-ttu-id="d7c5e-329">These records are created from Data Center Security audit data.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-329">These records are created from Data Center Security audit data.</span></span>  

| <span data-ttu-id="d7c5e-330">Property</span><span class="sxs-lookup"><span data-stu-id="d7c5e-330">Property</span></span> | <span data-ttu-id="d7c5e-331">Description</span><span class="sxs-lookup"><span data-stu-id="d7c5e-331">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d7c5e-332">EffectiveOrganization</span><span class="sxs-lookup"><span data-stu-id="d7c5e-332">EffectiveOrganization</span></span> | <span data-ttu-id="d7c5e-333">The name of the tenant that the elevation/cmdlet was targeted at.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-333">The name of the tenant that the elevation/cmdlet was targeted at.</span></span> |
| <span data-ttu-id="d7c5e-334">ElevationApprovedTime</span><span class="sxs-lookup"><span data-stu-id="d7c5e-334">ElevationApprovedTime</span></span> | <span data-ttu-id="d7c5e-335">The timestamp for when the elevation was approved.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-335">The timestamp for when the elevation was approved.</span></span> |
| <span data-ttu-id="d7c5e-336">ElevationApprover</span><span class="sxs-lookup"><span data-stu-id="d7c5e-336">ElevationApprover</span></span> | <span data-ttu-id="d7c5e-337">The name of a Microsoft manager.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-337">The name of a Microsoft manager.</span></span> |
| <span data-ttu-id="d7c5e-338">ElevationDuration</span><span class="sxs-lookup"><span data-stu-id="d7c5e-338">ElevationDuration</span></span> | <span data-ttu-id="d7c5e-339">The duration for which the elevation was active.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-339">The duration for which the elevation was active.</span></span> |
| <span data-ttu-id="d7c5e-340">ElevationRequestId</span><span class="sxs-lookup"><span data-stu-id="d7c5e-340">ElevationRequestId</span></span> |  <span data-ttu-id="d7c5e-341">A unique identifier for the elevation request.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-341">A unique identifier for the elevation request.</span></span> |
| <span data-ttu-id="d7c5e-342">ElevationRole</span><span class="sxs-lookup"><span data-stu-id="d7c5e-342">ElevationRole</span></span> | <span data-ttu-id="d7c5e-343">The role the elevation was requested for.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-343">The role the elevation was requested for.</span></span> |
| <span data-ttu-id="d7c5e-344">ElevationTime</span><span class="sxs-lookup"><span data-stu-id="d7c5e-344">ElevationTime</span></span> | <span data-ttu-id="d7c5e-345">The start time of the elevation.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-345">The start time of the elevation.</span></span> |
| <span data-ttu-id="d7c5e-346">Start_Time</span><span class="sxs-lookup"><span data-stu-id="d7c5e-346">Start_Time</span></span> | <span data-ttu-id="d7c5e-347">The start time of the cmdlet execution.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-347">The start time of the cmdlet execution.</span></span> |


### <a name="exchange-admin"></a><span data-ttu-id="d7c5e-348">Exchange Admin</span><span class="sxs-lookup"><span data-stu-id="d7c5e-348">Exchange Admin</span></span>
<span data-ttu-id="d7c5e-349">These records are created when changes are made to Exchange configuration.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-349">These records are created when changes are made to Exchange configuration.</span></span>

| <span data-ttu-id="d7c5e-350">Property</span><span class="sxs-lookup"><span data-stu-id="d7c5e-350">Property</span></span> | <span data-ttu-id="d7c5e-351">Description</span><span class="sxs-lookup"><span data-stu-id="d7c5e-351">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d7c5e-352">OfficeWorkload</span><span class="sxs-lookup"><span data-stu-id="d7c5e-352">OfficeWorkload</span></span> | <span data-ttu-id="d7c5e-353">Exchange</span><span class="sxs-lookup"><span data-stu-id="d7c5e-353">Exchange</span></span> |
| <span data-ttu-id="d7c5e-354">RecordType</span><span class="sxs-lookup"><span data-stu-id="d7c5e-354">RecordType</span></span>     | <span data-ttu-id="d7c5e-355">ExchangeAdmin</span><span class="sxs-lookup"><span data-stu-id="d7c5e-355">ExchangeAdmin</span></span> |
| <span data-ttu-id="d7c5e-356">ExternalAccess</span><span class="sxs-lookup"><span data-stu-id="d7c5e-356">ExternalAccess</span></span> |  <span data-ttu-id="d7c5e-357">Specifies whether the cmdlet was run by a user in your organization, by Microsoft datacenter personnel or a datacenter service account, or by a delegated administrator.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-357">Specifies whether the cmdlet was run by a user in your organization, by Microsoft datacenter personnel or a datacenter service account, or by a delegated administrator.</span></span> <span data-ttu-id="d7c5e-358">The value False indicates that the cmdlet was run by someone in your organization.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-358">The value False indicates that the cmdlet was run by someone in your organization.</span></span> <span data-ttu-id="d7c5e-359">The value True indicates that the cmdlet was run by datacenter personnel, a datacenter service account, or a delegated administrator.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-359">The value True indicates that the cmdlet was run by datacenter personnel, a datacenter service account, or a delegated administrator.</span></span> |
| <span data-ttu-id="d7c5e-360">ModifiedObjectResolvedName</span><span class="sxs-lookup"><span data-stu-id="d7c5e-360">ModifiedObjectResolvedName</span></span> |  <span data-ttu-id="d7c5e-361">This is the user friendly name of the object that was modified by the cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-361">This is the user friendly name of the object that was modified by the cmdlet.</span></span> <span data-ttu-id="d7c5e-362">This is logged only if the cmdlet modifies the object.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-362">This is logged only if the cmdlet modifies the object.</span></span> |
| <span data-ttu-id="d7c5e-363">OrganizationName</span><span class="sxs-lookup"><span data-stu-id="d7c5e-363">OrganizationName</span></span> | <span data-ttu-id="d7c5e-364">The name of the tenant.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-364">The name of the tenant.</span></span> |
| <span data-ttu-id="d7c5e-365">OriginatingServer</span><span class="sxs-lookup"><span data-stu-id="d7c5e-365">OriginatingServer</span></span> | <span data-ttu-id="d7c5e-366">The name of the server from which the cmdlet was executed.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-366">The name of the server from which the cmdlet was executed.</span></span> |
| <span data-ttu-id="d7c5e-367">Parameters</span><span class="sxs-lookup"><span data-stu-id="d7c5e-367">Parameters</span></span> | <span data-ttu-id="d7c5e-368">The name and value for all parameters that were used with the cmdlet that is identified in the Operations property.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-368">The name and value for all parameters that were used with the cmdlet that is identified in the Operations property.</span></span> |


### <a name="exchange-mailbox"></a><span data-ttu-id="d7c5e-369">Exchange Mailbox</span><span class="sxs-lookup"><span data-stu-id="d7c5e-369">Exchange Mailbox</span></span>
<span data-ttu-id="d7c5e-370">These records are created when changes or additions are made to Exchange mailboxes.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-370">These records are created when changes or additions are made to Exchange mailboxes.</span></span>

| <span data-ttu-id="d7c5e-371">Property</span><span class="sxs-lookup"><span data-stu-id="d7c5e-371">Property</span></span> | <span data-ttu-id="d7c5e-372">Description</span><span class="sxs-lookup"><span data-stu-id="d7c5e-372">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d7c5e-373">OfficeWorkload</span><span class="sxs-lookup"><span data-stu-id="d7c5e-373">OfficeWorkload</span></span> | <span data-ttu-id="d7c5e-374">Exchange</span><span class="sxs-lookup"><span data-stu-id="d7c5e-374">Exchange</span></span> |
| <span data-ttu-id="d7c5e-375">RecordType</span><span class="sxs-lookup"><span data-stu-id="d7c5e-375">RecordType</span></span>     | <span data-ttu-id="d7c5e-376">ExchangeItem</span><span class="sxs-lookup"><span data-stu-id="d7c5e-376">ExchangeItem</span></span> |
| <span data-ttu-id="d7c5e-377">ClientInfoString</span><span class="sxs-lookup"><span data-stu-id="d7c5e-377">ClientInfoString</span></span> | <span data-ttu-id="d7c5e-378">Information about the email client that was used to perform the operation, such as a browser version, Outlook version, and mobile device information.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-378">Information about the email client that was used to perform the operation, such as a browser version, Outlook version, and mobile device information.</span></span> |
| <span data-ttu-id="d7c5e-379">Client_IPAddress</span><span class="sxs-lookup"><span data-stu-id="d7c5e-379">Client_IPAddress</span></span> | <span data-ttu-id="d7c5e-380">The IP address of the device that was used when the operation was logged.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-380">The IP address of the device that was used when the operation was logged.</span></span> <span data-ttu-id="d7c5e-381">The IP address is displayed in either an IPv4 or IPv6 address format.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-381">The IP address is displayed in either an IPv4 or IPv6 address format.</span></span> |
| <span data-ttu-id="d7c5e-382">ClientMachineName</span><span class="sxs-lookup"><span data-stu-id="d7c5e-382">ClientMachineName</span></span> | <span data-ttu-id="d7c5e-383">The machine name that hosts the Outlook client.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-383">The machine name that hosts the Outlook client.</span></span> |
| <span data-ttu-id="d7c5e-384">ClientProcessName</span><span class="sxs-lookup"><span data-stu-id="d7c5e-384">ClientProcessName</span></span> | <span data-ttu-id="d7c5e-385">The email client that was used to access the mailbox.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-385">The email client that was used to access the mailbox.</span></span> |
| <span data-ttu-id="d7c5e-386">ClientVersion</span><span class="sxs-lookup"><span data-stu-id="d7c5e-386">ClientVersion</span></span> | <span data-ttu-id="d7c5e-387">The version of the email client .</span><span class="sxs-lookup"><span data-stu-id="d7c5e-387">The version of the email client .</span></span> |
| <span data-ttu-id="d7c5e-388">InternalLogonType</span><span class="sxs-lookup"><span data-stu-id="d7c5e-388">InternalLogonType</span></span> | <span data-ttu-id="d7c5e-389">Reserved for internal use.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-389">Reserved for internal use.</span></span> |
| <span data-ttu-id="d7c5e-390">Logon_Type</span><span class="sxs-lookup"><span data-stu-id="d7c5e-390">Logon_Type</span></span> | <span data-ttu-id="d7c5e-391">Indicates the type of user who accessed the mailbox and performed the operation that was logged.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-391">Indicates the type of user who accessed the mailbox and performed the operation that was logged.</span></span> |
| <span data-ttu-id="d7c5e-392">LogonUserDisplayName</span><span class="sxs-lookup"><span data-stu-id="d7c5e-392">LogonUserDisplayName</span></span> |    <span data-ttu-id="d7c5e-393">The user-friendly name of the user who performed the operation.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-393">The user-friendly name of the user who performed the operation.</span></span> |
| <span data-ttu-id="d7c5e-394">LogonUserSid</span><span class="sxs-lookup"><span data-stu-id="d7c5e-394">LogonUserSid</span></span> | <span data-ttu-id="d7c5e-395">The SID of the user who performed the operation.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-395">The SID of the user who performed the operation.</span></span> |
| <span data-ttu-id="d7c5e-396">MailboxGuid</span><span class="sxs-lookup"><span data-stu-id="d7c5e-396">MailboxGuid</span></span> | <span data-ttu-id="d7c5e-397">The Exchange GUID of the mailbox that was accessed.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-397">The Exchange GUID of the mailbox that was accessed.</span></span> |
| <span data-ttu-id="d7c5e-398">MailboxOwnerMasterAccountSid</span><span class="sxs-lookup"><span data-stu-id="d7c5e-398">MailboxOwnerMasterAccountSid</span></span> | <span data-ttu-id="d7c5e-399">Mailbox owner account's master account SID.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-399">Mailbox owner account's master account SID.</span></span> |
| <span data-ttu-id="d7c5e-400">MailboxOwnerSid</span><span class="sxs-lookup"><span data-stu-id="d7c5e-400">MailboxOwnerSid</span></span> | <span data-ttu-id="d7c5e-401">The SID of the mailbox owner.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-401">The SID of the mailbox owner.</span></span> |
| <span data-ttu-id="d7c5e-402">MailboxOwnerUPN</span><span class="sxs-lookup"><span data-stu-id="d7c5e-402">MailboxOwnerUPN</span></span> | <span data-ttu-id="d7c5e-403">The email address of the person who owns the mailbox that was accessed.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-403">The email address of the person who owns the mailbox that was accessed.</span></span> |


### <a name="exchange-mailbox-audit"></a><span data-ttu-id="d7c5e-404">Exchange Mailbox Audit</span><span class="sxs-lookup"><span data-stu-id="d7c5e-404">Exchange Mailbox Audit</span></span>
<span data-ttu-id="d7c5e-405">These records are created when a mailbox audit entry is created.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-405">These records are created when a mailbox audit entry is created.</span></span>

| <span data-ttu-id="d7c5e-406">Property</span><span class="sxs-lookup"><span data-stu-id="d7c5e-406">Property</span></span> | <span data-ttu-id="d7c5e-407">Description</span><span class="sxs-lookup"><span data-stu-id="d7c5e-407">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d7c5e-408">OfficeWorkload</span><span class="sxs-lookup"><span data-stu-id="d7c5e-408">OfficeWorkload</span></span> | <span data-ttu-id="d7c5e-409">Exchange</span><span class="sxs-lookup"><span data-stu-id="d7c5e-409">Exchange</span></span> |
| <span data-ttu-id="d7c5e-410">RecordType</span><span class="sxs-lookup"><span data-stu-id="d7c5e-410">RecordType</span></span>     | <span data-ttu-id="d7c5e-411">ExchangeItem</span><span class="sxs-lookup"><span data-stu-id="d7c5e-411">ExchangeItem</span></span> |
| <span data-ttu-id="d7c5e-412">Item</span><span class="sxs-lookup"><span data-stu-id="d7c5e-412">Item</span></span> | <span data-ttu-id="d7c5e-413">Represents the item upon which the operation was performed</span><span class="sxs-lookup"><span data-stu-id="d7c5e-413">Represents the item upon which the operation was performed</span></span> | 
| <span data-ttu-id="d7c5e-414">SendAsUserMailboxGuid</span><span class="sxs-lookup"><span data-stu-id="d7c5e-414">SendAsUserMailboxGuid</span></span> | <span data-ttu-id="d7c5e-415">The Exchange GUID of the mailbox that was accessed to send email as.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-415">The Exchange GUID of the mailbox that was accessed to send email as.</span></span> |
| <span data-ttu-id="d7c5e-416">SendAsUserSmtp</span><span class="sxs-lookup"><span data-stu-id="d7c5e-416">SendAsUserSmtp</span></span> | <span data-ttu-id="d7c5e-417">SMTP address of the user who is being impersonated.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-417">SMTP address of the user who is being impersonated.</span></span> |
| <span data-ttu-id="d7c5e-418">SendonBehalfOfUserMailboxGuid</span><span class="sxs-lookup"><span data-stu-id="d7c5e-418">SendonBehalfOfUserMailboxGuid</span></span> | <span data-ttu-id="d7c5e-419">The Exchange GUID of the mailbox that was accessed to send mail on behalf of.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-419">The Exchange GUID of the mailbox that was accessed to send mail on behalf of.</span></span> |
| <span data-ttu-id="d7c5e-420">SendOnBehalfOfUserSmtp</span><span class="sxs-lookup"><span data-stu-id="d7c5e-420">SendOnBehalfOfUserSmtp</span></span> | <span data-ttu-id="d7c5e-421">SMTP address of the user on whose behalf the email is sent.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-421">SMTP address of the user on whose behalf the email is sent.</span></span> |


### <a name="exchange-mailbox-audit-group"></a><span data-ttu-id="d7c5e-422">Exchange Mailbox Audit Group</span><span class="sxs-lookup"><span data-stu-id="d7c5e-422">Exchange Mailbox Audit Group</span></span>
<span data-ttu-id="d7c5e-423">These records are created when changes or additions are made to Exchange groups.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-423">These records are created when changes or additions are made to Exchange groups.</span></span>

| <span data-ttu-id="d7c5e-424">Property</span><span class="sxs-lookup"><span data-stu-id="d7c5e-424">Property</span></span> | <span data-ttu-id="d7c5e-425">Description</span><span class="sxs-lookup"><span data-stu-id="d7c5e-425">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d7c5e-426">OfficeWorkload</span><span class="sxs-lookup"><span data-stu-id="d7c5e-426">OfficeWorkload</span></span> | <span data-ttu-id="d7c5e-427">Exchange</span><span class="sxs-lookup"><span data-stu-id="d7c5e-427">Exchange</span></span> |
| <span data-ttu-id="d7c5e-428">OfficeWorkload</span><span class="sxs-lookup"><span data-stu-id="d7c5e-428">OfficeWorkload</span></span> | <span data-ttu-id="d7c5e-429">ExchangeItemGroup</span><span class="sxs-lookup"><span data-stu-id="d7c5e-429">ExchangeItemGroup</span></span> |
| <span data-ttu-id="d7c5e-430">AffectedItems</span><span class="sxs-lookup"><span data-stu-id="d7c5e-430">AffectedItems</span></span> | <span data-ttu-id="d7c5e-431">Information about each item in the group.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-431">Information about each item in the group.</span></span> |
| <span data-ttu-id="d7c5e-432">CrossMailboxOperations</span><span class="sxs-lookup"><span data-stu-id="d7c5e-432">CrossMailboxOperations</span></span> | <span data-ttu-id="d7c5e-433">Indicates if the operation involved more than one mailbox.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-433">Indicates if the operation involved more than one mailbox.</span></span> |
| <span data-ttu-id="d7c5e-434">DestMailboxId</span><span class="sxs-lookup"><span data-stu-id="d7c5e-434">DestMailboxId</span></span> | <span data-ttu-id="d7c5e-435">Set only if the CrossMailboxOperations parameter is True.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-435">Set only if the CrossMailboxOperations parameter is True.</span></span> <span data-ttu-id="d7c5e-436">Specifies the target mailbox GUID.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-436">Specifies the target mailbox GUID.</span></span> |
| <span data-ttu-id="d7c5e-437">DestMailboxOwnerMasterAccountSid</span><span class="sxs-lookup"><span data-stu-id="d7c5e-437">DestMailboxOwnerMasterAccountSid</span></span> | <span data-ttu-id="d7c5e-438">Set only if the CrossMailboxOperations parameter is True.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-438">Set only if the CrossMailboxOperations parameter is True.</span></span> <span data-ttu-id="d7c5e-439">Specifies the SID for the master account SID of the target mailbox owner.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-439">Specifies the SID for the master account SID of the target mailbox owner.</span></span> |
| <span data-ttu-id="d7c5e-440">DestMailboxOwnerSid</span><span class="sxs-lookup"><span data-stu-id="d7c5e-440">DestMailboxOwnerSid</span></span> | <span data-ttu-id="d7c5e-441">Set only if the CrossMailboxOperations parameter is True.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-441">Set only if the CrossMailboxOperations parameter is True.</span></span> <span data-ttu-id="d7c5e-442">Specifies the SID of the target mailbox.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-442">Specifies the SID of the target mailbox.</span></span> |
| <span data-ttu-id="d7c5e-443">DestMailboxOwnerUPN</span><span class="sxs-lookup"><span data-stu-id="d7c5e-443">DestMailboxOwnerUPN</span></span> | <span data-ttu-id="d7c5e-444">Set only if the CrossMailboxOperations parameter is True.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-444">Set only if the CrossMailboxOperations parameter is True.</span></span> <span data-ttu-id="d7c5e-445">Specifies the UPN of the owner of the target mailbox.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-445">Specifies the UPN of the owner of the target mailbox.</span></span> |
| <span data-ttu-id="d7c5e-446">DestFolder</span><span class="sxs-lookup"><span data-stu-id="d7c5e-446">DestFolder</span></span> | <span data-ttu-id="d7c5e-447">The destination folder, for operations such as Move.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-447">The destination folder, for operations such as Move.</span></span> |
| <span data-ttu-id="d7c5e-448">Folder</span><span class="sxs-lookup"><span data-stu-id="d7c5e-448">Folder</span></span> | <span data-ttu-id="d7c5e-449">The folder where a group of items is located.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-449">The folder where a group of items is located.</span></span> |
| <span data-ttu-id="d7c5e-450">Folders</span><span class="sxs-lookup"><span data-stu-id="d7c5e-450">Folders</span></span> |     <span data-ttu-id="d7c5e-451">Information about the source folders involved in an operation; for example, if folders are selected and then deleted.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-451">Information about the source folders involved in an operation; for example, if folders are selected and then deleted.</span></span> |


### <a name="sharepoint-base"></a><span data-ttu-id="d7c5e-452">SharePoint Base</span><span class="sxs-lookup"><span data-stu-id="d7c5e-452">SharePoint Base</span></span>
<span data-ttu-id="d7c5e-453">These properties are common to all SharePoint records.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-453">These properties are common to all SharePoint records.</span></span>

| <span data-ttu-id="d7c5e-454">Property</span><span class="sxs-lookup"><span data-stu-id="d7c5e-454">Property</span></span> | <span data-ttu-id="d7c5e-455">Description</span><span class="sxs-lookup"><span data-stu-id="d7c5e-455">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d7c5e-456">OfficeWorkload</span><span class="sxs-lookup"><span data-stu-id="d7c5e-456">OfficeWorkload</span></span> | <span data-ttu-id="d7c5e-457">SharePoint</span><span class="sxs-lookup"><span data-stu-id="d7c5e-457">SharePoint</span></span> |
| <span data-ttu-id="d7c5e-458">OfficeWorkload</span><span class="sxs-lookup"><span data-stu-id="d7c5e-458">OfficeWorkload</span></span> | <span data-ttu-id="d7c5e-459">SharePoint</span><span class="sxs-lookup"><span data-stu-id="d7c5e-459">SharePoint</span></span> |
| <span data-ttu-id="d7c5e-460">EventSource</span><span class="sxs-lookup"><span data-stu-id="d7c5e-460">EventSource</span></span> | <span data-ttu-id="d7c5e-461">Identifies that an event occurred in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-461">Identifies that an event occurred in SharePoint.</span></span> <span data-ttu-id="d7c5e-462">Possible values are SharePoint or ObjectModel.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-462">Possible values are SharePoint or ObjectModel.</span></span> |
| <span data-ttu-id="d7c5e-463">ItemType</span><span class="sxs-lookup"><span data-stu-id="d7c5e-463">ItemType</span></span> | <span data-ttu-id="d7c5e-464">The type of object that was accessed or modified.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-464">The type of object that was accessed or modified.</span></span> <span data-ttu-id="d7c5e-465">See the ItemType table for details on the types of objects.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-465">See the ItemType table for details on the types of objects.</span></span> |
| <span data-ttu-id="d7c5e-466">MachineDomainInfo</span><span class="sxs-lookup"><span data-stu-id="d7c5e-466">MachineDomainInfo</span></span> | <span data-ttu-id="d7c5e-467">Information about device sync operations.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-467">Information about device sync operations.</span></span> <span data-ttu-id="d7c5e-468">This information is reported only if it's present in the request.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-468">This information is reported only if it's present in the request.</span></span> |
| <span data-ttu-id="d7c5e-469">MachineId</span><span class="sxs-lookup"><span data-stu-id="d7c5e-469">MachineId</span></span> |   <span data-ttu-id="d7c5e-470">Information about device sync operations.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-470">Information about device sync operations.</span></span> <span data-ttu-id="d7c5e-471">This information is reported only if it's present in the request.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-471">This information is reported only if it's present in the request.</span></span> |
| <span data-ttu-id="d7c5e-472">Site_</span><span class="sxs-lookup"><span data-stu-id="d7c5e-472">Site_</span></span> | <span data-ttu-id="d7c5e-473">The GUID of the site where the file or folder accessed by the user is located.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-473">The GUID of the site where the file or folder accessed by the user is located.</span></span> |
| <span data-ttu-id="d7c5e-474">Source_Name</span><span class="sxs-lookup"><span data-stu-id="d7c5e-474">Source_Name</span></span> | <span data-ttu-id="d7c5e-475">The entity that triggered the audited operation.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-475">The entity that triggered the audited operation.</span></span> <span data-ttu-id="d7c5e-476">Possible values are SharePoint or ObjectModel.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-476">Possible values are SharePoint or ObjectModel.</span></span> |
| <span data-ttu-id="d7c5e-477">UserAgent</span><span class="sxs-lookup"><span data-stu-id="d7c5e-477">UserAgent</span></span> | <span data-ttu-id="d7c5e-478">Information about the user's client or browser.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-478">Information about the user's client or browser.</span></span> <span data-ttu-id="d7c5e-479">This information is provided by the client or browser.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-479">This information is provided by the client or browser.</span></span> |


### <a name="sharepoint-schema"></a><span data-ttu-id="d7c5e-480">SharePoint Schema</span><span class="sxs-lookup"><span data-stu-id="d7c5e-480">SharePoint Schema</span></span>
<span data-ttu-id="d7c5e-481">These records are created when configuration changes are made to SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-481">These records are created when configuration changes are made to SharePoint.</span></span>

| <span data-ttu-id="d7c5e-482">Property</span><span class="sxs-lookup"><span data-stu-id="d7c5e-482">Property</span></span> | <span data-ttu-id="d7c5e-483">Description</span><span class="sxs-lookup"><span data-stu-id="d7c5e-483">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d7c5e-484">OfficeWorkload</span><span class="sxs-lookup"><span data-stu-id="d7c5e-484">OfficeWorkload</span></span> | <span data-ttu-id="d7c5e-485">SharePoint</span><span class="sxs-lookup"><span data-stu-id="d7c5e-485">SharePoint</span></span> |
| <span data-ttu-id="d7c5e-486">OfficeWorkload</span><span class="sxs-lookup"><span data-stu-id="d7c5e-486">OfficeWorkload</span></span> | <span data-ttu-id="d7c5e-487">SharePoint</span><span class="sxs-lookup"><span data-stu-id="d7c5e-487">SharePoint</span></span> |
| <span data-ttu-id="d7c5e-488">CustomEvent</span><span class="sxs-lookup"><span data-stu-id="d7c5e-488">CustomEvent</span></span> | <span data-ttu-id="d7c5e-489">Optional string for custom events.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-489">Optional string for custom events.</span></span> |
| <span data-ttu-id="d7c5e-490">Event_Data</span><span class="sxs-lookup"><span data-stu-id="d7c5e-490">Event_Data</span></span> |  <span data-ttu-id="d7c5e-491">Optional payload for custom events.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-491">Optional payload for custom events.</span></span> |
| <span data-ttu-id="d7c5e-492">ModifiedProperties</span><span class="sxs-lookup"><span data-stu-id="d7c5e-492">ModifiedProperties</span></span> | <span data-ttu-id="d7c5e-493">The property is included for admin events, such as adding a user as a member of a site or a site collection admin group.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-493">The property is included for admin events, such as adding a user as a member of a site or a site collection admin group.</span></span> <span data-ttu-id="d7c5e-494">The property includes the name of the property that was modified (for example, the Site Admin group), the new value of the modified property (such the user who was added as a site admin), and the previous value of the modified object.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-494">The property includes the name of the property that was modified (for example, the Site Admin group), the new value of the modified property (such the user who was added as a site admin), and the previous value of the modified object.</span></span> |


### <a name="sharepoint-file-operations"></a><span data-ttu-id="d7c5e-495">SharePoint File Operations</span><span class="sxs-lookup"><span data-stu-id="d7c5e-495">SharePoint File Operations</span></span>
<span data-ttu-id="d7c5e-496">These records are created in response to file operations in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-496">These records are created in response to file operations in SharePoint.</span></span>

| <span data-ttu-id="d7c5e-497">Property</span><span class="sxs-lookup"><span data-stu-id="d7c5e-497">Property</span></span> | <span data-ttu-id="d7c5e-498">Description</span><span class="sxs-lookup"><span data-stu-id="d7c5e-498">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d7c5e-499">OfficeWorkload</span><span class="sxs-lookup"><span data-stu-id="d7c5e-499">OfficeWorkload</span></span> | <span data-ttu-id="d7c5e-500">SharePoint</span><span class="sxs-lookup"><span data-stu-id="d7c5e-500">SharePoint</span></span> |
| <span data-ttu-id="d7c5e-501">OfficeWorkload</span><span class="sxs-lookup"><span data-stu-id="d7c5e-501">OfficeWorkload</span></span> | <span data-ttu-id="d7c5e-502">SharePointFileOperation</span><span class="sxs-lookup"><span data-stu-id="d7c5e-502">SharePointFileOperation</span></span> |
| <span data-ttu-id="d7c5e-503">DestinationFileExtension</span><span class="sxs-lookup"><span data-stu-id="d7c5e-503">DestinationFileExtension</span></span> | <span data-ttu-id="d7c5e-504">The file extension of a file that is copied or moved.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-504">The file extension of a file that is copied or moved.</span></span> <span data-ttu-id="d7c5e-505">This property is displayed only for FileCopied and FileMoved events.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-505">This property is displayed only for FileCopied and FileMoved events.</span></span> |
| <span data-ttu-id="d7c5e-506">DestinationFileName</span><span class="sxs-lookup"><span data-stu-id="d7c5e-506">DestinationFileName</span></span> | <span data-ttu-id="d7c5e-507">The name of the file that is copied or moved.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-507">The name of the file that is copied or moved.</span></span> <span data-ttu-id="d7c5e-508">This property is displayed only for FileCopied and FileMoved events.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-508">This property is displayed only for FileCopied and FileMoved events.</span></span> |
| <span data-ttu-id="d7c5e-509">DestinationRelativeUrl</span><span class="sxs-lookup"><span data-stu-id="d7c5e-509">DestinationRelativeUrl</span></span> | <span data-ttu-id="d7c5e-510">The URL of the destination folder where a file is copied or moved.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-510">The URL of the destination folder where a file is copied or moved.</span></span> <span data-ttu-id="d7c5e-511">The combination of the values for SiteURL, DestinationRelativeURL, and DestinationFileName parameters is the same as the value for the ObjectID property, which is the full path name for the file that was copied.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-511">The combination of the values for SiteURL, DestinationRelativeURL, and DestinationFileName parameters is the same as the value for the ObjectID property, which is the full path name for the file that was copied.</span></span> <span data-ttu-id="d7c5e-512">This property is displayed only for FileCopied and FileMoved events.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-512">This property is displayed only for FileCopied and FileMoved events.</span></span> |
| <span data-ttu-id="d7c5e-513">SharingType</span><span class="sxs-lookup"><span data-stu-id="d7c5e-513">SharingType</span></span> | <span data-ttu-id="d7c5e-514">The type of sharing permissions that were assigned to the user that the resource was shared with.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-514">The type of sharing permissions that were assigned to the user that the resource was shared with.</span></span> <span data-ttu-id="d7c5e-515">This user is identified by the UserSharedWith parameter.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-515">This user is identified by the UserSharedWith parameter.</span></span> |
| <span data-ttu-id="d7c5e-516">Site_Url</span><span class="sxs-lookup"><span data-stu-id="d7c5e-516">Site_Url</span></span> | <span data-ttu-id="d7c5e-517">The URL of the site where the file or folder accessed by the user is located.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-517">The URL of the site where the file or folder accessed by the user is located.</span></span> |
| <span data-ttu-id="d7c5e-518">SourceFileExtension</span><span class="sxs-lookup"><span data-stu-id="d7c5e-518">SourceFileExtension</span></span> | <span data-ttu-id="d7c5e-519">The file extension of the file that was accessed by the user.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-519">The file extension of the file that was accessed by the user.</span></span> <span data-ttu-id="d7c5e-520">This property is blank if the object that was accessed is a folder.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-520">This property is blank if the object that was accessed is a folder.</span></span> |
| <span data-ttu-id="d7c5e-521">SourceFileName</span><span class="sxs-lookup"><span data-stu-id="d7c5e-521">SourceFileName</span></span> |  <span data-ttu-id="d7c5e-522">The name of the file or folder accessed by the user.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-522">The name of the file or folder accessed by the user.</span></span> |
| <span data-ttu-id="d7c5e-523">SourceRelativeUrl</span><span class="sxs-lookup"><span data-stu-id="d7c5e-523">SourceRelativeUrl</span></span> | <span data-ttu-id="d7c5e-524">The URL of the folder that contains the file accessed by the user.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-524">The URL of the folder that contains the file accessed by the user.</span></span> <span data-ttu-id="d7c5e-525">The combination of the values for the SiteURL, SourceRelativeURL, and SourceFileName parameters is the same as the value for the ObjectID property, which is the full path name for the file accessed by the user.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-525">The combination of the values for the SiteURL, SourceRelativeURL, and SourceFileName parameters is the same as the value for the ObjectID property, which is the full path name for the file accessed by the user.</span></span> |
| <span data-ttu-id="d7c5e-526">UserSharedWith</span><span class="sxs-lookup"><span data-stu-id="d7c5e-526">UserSharedWith</span></span> |  <span data-ttu-id="d7c5e-527">The user that a resource was shared with.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-527">The user that a resource was shared with.</span></span> |




## <a name="sample-log-searches"></a><span data-ttu-id="d7c5e-528">Sample log searches</span><span class="sxs-lookup"><span data-stu-id="d7c5e-528">Sample log searches</span></span>
<span data-ttu-id="d7c5e-529">The following table provides sample log searches for update records collected by this solution.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-529">The following table provides sample log searches for update records collected by this solution.</span></span>

| <span data-ttu-id="d7c5e-530">Query</span><span class="sxs-lookup"><span data-stu-id="d7c5e-530">Query</span></span> | <span data-ttu-id="d7c5e-531">Description</span><span class="sxs-lookup"><span data-stu-id="d7c5e-531">Description</span></span> |
| --- | --- |
|<span data-ttu-id="d7c5e-532">Count of all the operations on your Office 365 subscription</span><span class="sxs-lookup"><span data-stu-id="d7c5e-532">Count of all the operations on your Office 365 subscription</span></span> |<span data-ttu-id="d7c5e-533">OfficeActivity &#124; summarize count() by Operation</span><span class="sxs-lookup"><span data-stu-id="d7c5e-533">OfficeActivity &#124; summarize count() by Operation</span></span> |
|<span data-ttu-id="d7c5e-534">Usage of SharePoint sites</span><span class="sxs-lookup"><span data-stu-id="d7c5e-534">Usage of SharePoint sites</span></span>|<span data-ttu-id="d7c5e-535">OfficeActivity &#124; where OfficeWorkload =~ "sharepoint" &#124; summarize count() by SiteUrl</span><span class="sxs-lookup"><span data-stu-id="d7c5e-535">OfficeActivity &#124; where OfficeWorkload =~ "sharepoint" &#124; summarize count() by SiteUrl</span></span> | <span data-ttu-id="d7c5e-536">sort by Count asc</span><span class="sxs-lookup"><span data-stu-id="d7c5e-536">sort by Count asc</span></span>|
|<span data-ttu-id="d7c5e-537">File access operations by user type</span><span class="sxs-lookup"><span data-stu-id="d7c5e-537">File access operations by user type</span></span>|<span data-ttu-id="d7c5e-538">search in (OfficeActivity) OfficeWorkload =~ "azureactivedirectory" and "MyTest"</span><span class="sxs-lookup"><span data-stu-id="d7c5e-538">search in (OfficeActivity) OfficeWorkload =~ "azureactivedirectory" and "MyTest"</span></span>|
|<span data-ttu-id="d7c5e-539">Search with a specific keyword</span><span class="sxs-lookup"><span data-stu-id="d7c5e-539">Search with a specific keyword</span></span>|<span data-ttu-id="d7c5e-540">Type=OfficeActivity OfficeWorkload=azureactivedirectory "MyTest"</span><span class="sxs-lookup"><span data-stu-id="d7c5e-540">Type=OfficeActivity OfficeWorkload=azureactivedirectory "MyTest"</span></span>|
|<span data-ttu-id="d7c5e-541">Monitor external actions on Exchange</span><span class="sxs-lookup"><span data-stu-id="d7c5e-541">Monitor external actions on Exchange</span></span>|<span data-ttu-id="d7c5e-542">OfficeActivity &#124; where OfficeWorkload =~ "exchange" and ExternalAccess == true</span><span class="sxs-lookup"><span data-stu-id="d7c5e-542">OfficeActivity &#124; where OfficeWorkload =~ "exchange" and ExternalAccess == true</span></span>|



## <a name="next-steps"></a><span data-ttu-id="d7c5e-543">Next steps</span><span class="sxs-lookup"><span data-stu-id="d7c5e-543">Next steps</span></span>
* <span data-ttu-id="d7c5e-544">Use Log Searches in [Log Analytics](../log-analytics/log-analytics-log-searches.md) to view detailed update data.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-544">Use Log Searches in [Log Analytics](../log-analytics/log-analytics-log-searches.md) to view detailed update data.</span></span>
* <span data-ttu-id="d7c5e-545">[Create your own dashboards](../log-analytics/log-analytics-dashboards.md) to display your favorite Office 365 search queries.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-545">[Create your own dashboards](../log-analytics/log-analytics-dashboards.md) to display your favorite Office 365 search queries.</span></span>
* <span data-ttu-id="d7c5e-546">[Create alerts](../log-analytics/log-analytics-alerts.md) to be proactively notified of important Office 365 activities.</span><span class="sxs-lookup"><span data-stu-id="d7c5e-546">[Create alerts](../log-analytics/log-analytics-alerts.md) to be proactively notified of important Office 365 activities.</span></span>  
