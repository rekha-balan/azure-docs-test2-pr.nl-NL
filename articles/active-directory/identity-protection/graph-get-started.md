---
title: Microsoft Graph for Azure Active Directory Identity Protection | Microsoft Docs
description: Learn how to query Microsoft Graph for a list of risk events and associated information from Azure Active Directory.
services: active-directory
keywords: azure active directory identity protection, risk event, vulnerability, security policy, Microsoft Graph
documentationcenter: ''
author: MarkusVi
manager: mtillman
ms.assetid: fa109ba7-a914-437b-821d-2bd98e681386
ms.service: active-directory
ms.component: conditional-access
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2017
ms.author: markvi
ms.reviewer: nigu
ms.custom: seohack1
ms.openlocfilehash: 3bdf44e0a1cf0ccda6d015fa3683964f3530d4af
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965860"
---
# <a name="get-started-with-azure-active-directory-identity-protection-and-microsoft-graph"></a><span data-ttu-id="f8a26-104">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="f8a26-104">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>
<span data-ttu-id="f8a26-105">Microsoft Graph is the Microsoft unified API endpoint and the home of [Azure Active Directory Identity Protection](../active-directory-identityprotection.md) APIs.</span><span class="sxs-lookup"><span data-stu-id="f8a26-105">Microsoft Graph is the Microsoft unified API endpoint and the home of [Azure Active Directory Identity Protection](../active-directory-identityprotection.md) APIs.</span></span> <span data-ttu-id="f8a26-106">The first API, **identityRiskEvents**, allows you to query Microsoft Graph for a list of [risk events](../reports-monitoring/concept-risk-events.md) and associated information.</span><span class="sxs-lookup"><span data-stu-id="f8a26-106">The first API, **identityRiskEvents**, allows you to query Microsoft Graph for a list of [risk events](../reports-monitoring/concept-risk-events.md) and associated information.</span></span> <span data-ttu-id="f8a26-107">This article gets you started querying this API.</span><span class="sxs-lookup"><span data-stu-id="f8a26-107">This article gets you started querying this API.</span></span> <span data-ttu-id="f8a26-108">For an in-depth introduction, full documentation, and access to the Graph Explorer, see the [Microsoft Graph site](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="f8a26-108">For an in-depth introduction, full documentation, and access to the Graph Explorer, see the [Microsoft Graph site](https://graph.microsoft.io/).</span></span>


<span data-ttu-id="f8a26-109">There are four steps to accessing Identity Protection data through Microsoft Graph:</span><span class="sxs-lookup"><span data-stu-id="f8a26-109">There are four steps to accessing Identity Protection data through Microsoft Graph:</span></span>

1. <span data-ttu-id="f8a26-110">Retrieve your domain name.</span><span class="sxs-lookup"><span data-stu-id="f8a26-110">Retrieve your domain name.</span></span>
2. <span data-ttu-id="f8a26-111">Create a new app registration.</span><span class="sxs-lookup"><span data-stu-id="f8a26-111">Create a new app registration.</span></span> 
2. <span data-ttu-id="f8a26-112">Use this secret and a few other pieces of information to authenticate to Microsoft Graph, where you receive an authentication token.</span><span class="sxs-lookup"><span data-stu-id="f8a26-112">Use this secret and a few other pieces of information to authenticate to Microsoft Graph, where you receive an authentication token.</span></span> 
3. <span data-ttu-id="f8a26-113">Use this token to make requests to the API endpoint and get Identity Protection data back.</span><span class="sxs-lookup"><span data-stu-id="f8a26-113">Use this token to make requests to the API endpoint and get Identity Protection data back.</span></span>

<span data-ttu-id="f8a26-114">Before you get started, you’ll need:</span><span class="sxs-lookup"><span data-stu-id="f8a26-114">Before you get started, you’ll need:</span></span>

* <span data-ttu-id="f8a26-115">Administrator privileges to create the application in Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8a26-115">Administrator privileges to create the application in Azure AD</span></span>
* <span data-ttu-id="f8a26-116">The name of your tenant's domain (for example, contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="f8a26-116">The name of your tenant's domain (for example, contoso.onmicrosoft.com)</span></span>


## <a name="retrieve-your-domain-name"></a><span data-ttu-id="f8a26-117">Retrieve your domain name</span><span class="sxs-lookup"><span data-stu-id="f8a26-117">Retrieve your domain name</span></span> 

1. <span data-ttu-id="f8a26-118">[Sign in](https://portal.azure.com) to your Azure portal as an administrator.</span><span class="sxs-lookup"><span data-stu-id="f8a26-118">[Sign in](https://portal.azure.com) to your Azure portal as an administrator.</span></span> 

2. <span data-ttu-id="f8a26-119">On the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f8a26-119">On the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Creating an application](./media/graph-get-started/41.png)


3. <span data-ttu-id="f8a26-121">In the **Manage** section, click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="f8a26-121">In the **Manage** section, click **Properties**.</span></span>

    ![Creating an application](./media/graph-get-started/42.png)

4. <span data-ttu-id="f8a26-123">Copy your domain name.</span><span class="sxs-lookup"><span data-stu-id="f8a26-123">Copy your domain name.</span></span>


## <a name="create-a-new-app-registration"></a><span data-ttu-id="f8a26-124">Create a new app registration</span><span class="sxs-lookup"><span data-stu-id="f8a26-124">Create a new app registration</span></span>

1. <span data-ttu-id="f8a26-125">On the **Active Directory** page, in the **Manage** section, click **App registrations**.</span><span class="sxs-lookup"><span data-stu-id="f8a26-125">On the **Active Directory** page, in the **Manage** section, click **App registrations**.</span></span>

    ![Creating an application](./media/graph-get-started/42.png)


2. <span data-ttu-id="f8a26-127">In the menu on the top, click **New application registration**.</span><span class="sxs-lookup"><span data-stu-id="f8a26-127">In the menu on the top, click **New application registration**.</span></span>
   
    ![Creating an application](./media/graph-get-started/43.png)

3. <span data-ttu-id="f8a26-129">On the **Create** page,  perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f8a26-129">On the **Create** page,  perform the following steps:</span></span>
   
    ![Creating an application](./media/graph-get-started/44.png)

    <span data-ttu-id="f8a26-131">a.</span><span class="sxs-lookup"><span data-stu-id="f8a26-131">a.</span></span> <span data-ttu-id="f8a26-132">In the **Name** textbox, type a name for your application (e.g.: AADIP Risk Event API Application).</span><span class="sxs-lookup"><span data-stu-id="f8a26-132">In the **Name** textbox, type a name for your application (e.g.: AADIP Risk Event API Application).</span></span>
   
    <span data-ttu-id="f8a26-133">b.</span><span class="sxs-lookup"><span data-stu-id="f8a26-133">b.</span></span> <span data-ttu-id="f8a26-134">As **Type**, select **Web Application And / Or Web API**.</span><span class="sxs-lookup"><span data-stu-id="f8a26-134">As **Type**, select **Web Application And / Or Web API**.</span></span>
   
    <span data-ttu-id="f8a26-135">c.</span><span class="sxs-lookup"><span data-stu-id="f8a26-135">c.</span></span> <span data-ttu-id="f8a26-136">In the **Sign-on URL** textbox, type `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="f8a26-136">In the **Sign-on URL** textbox, type `http://localhost`.</span></span>

    <span data-ttu-id="f8a26-137">d.</span><span class="sxs-lookup"><span data-stu-id="f8a26-137">d.</span></span> <span data-ttu-id="f8a26-138">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="f8a26-138">Click **Create**.</span></span>

4. <span data-ttu-id="f8a26-139">To open the **Settings** page, in the applications list, click your newly created app registration.</span><span class="sxs-lookup"><span data-stu-id="f8a26-139">To open the **Settings** page, in the applications list, click your newly created app registration.</span></span> 

5. <span data-ttu-id="f8a26-140">Copy the **Application ID**.</span><span class="sxs-lookup"><span data-stu-id="f8a26-140">Copy the **Application ID**.</span></span>


## <a name="grant-your-application-permission-to-use-the-api"></a><span data-ttu-id="f8a26-141">Grant your application permission to use the API</span><span class="sxs-lookup"><span data-stu-id="f8a26-141">Grant your application permission to use the API</span></span>

1. <span data-ttu-id="f8a26-142">On the **Settings** page, click **Required permissions**.</span><span class="sxs-lookup"><span data-stu-id="f8a26-142">On the **Settings** page, click **Required permissions**.</span></span>
   
    ![Creating an application](./media/graph-get-started/15.png)

2. <span data-ttu-id="f8a26-144">On the **Required permissions** page, in the toolbar on the top, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="f8a26-144">On the **Required permissions** page, in the toolbar on the top, click **Add**.</span></span>
   
    ![Creating an application](./media/graph-get-started/16.png)
   
3. <span data-ttu-id="f8a26-146">On the **Add API access** page, click **Select an API**.</span><span class="sxs-lookup"><span data-stu-id="f8a26-146">On the **Add API access** page, click **Select an API**.</span></span>
   
    ![Creating an application](./media/graph-get-started/17.png)

4. <span data-ttu-id="f8a26-148">On the **Select an API** page, select **Microsoft Graph**, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="f8a26-148">On the **Select an API** page, select **Microsoft Graph**, and then click **Select**.</span></span>
   
    ![Creating an application](./media/graph-get-started/18.png)

5. <span data-ttu-id="f8a26-150">On the **Add API access** page, click **Select permissions**.</span><span class="sxs-lookup"><span data-stu-id="f8a26-150">On the **Add API access** page, click **Select permissions**.</span></span>
   
    ![Creating an application](./media/graph-get-started/19.png)

6. <span data-ttu-id="f8a26-152">On the **Enable Access** page, click **Read all identity risk information**, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="f8a26-152">On the **Enable Access** page, click **Read all identity risk information**, and then click **Select**.</span></span>
   
    ![Creating an application](./media/graph-get-started/20.png)

7. <span data-ttu-id="f8a26-154">On the **Add API access** page, click **Done**.</span><span class="sxs-lookup"><span data-stu-id="f8a26-154">On the **Add API access** page, click **Done**.</span></span>
   
    ![Creating an application](./media/graph-get-started/21.png)

8. <span data-ttu-id="f8a26-156">On the **Required Permissions** page, click **Grant Permissions**, and then click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="f8a26-156">On the **Required Permissions** page, click **Grant Permissions**, and then click **Yes**.</span></span>
   
    ![Creating an application](./media/graph-get-started/22.png)



## <a name="get-an-access-key"></a><span data-ttu-id="f8a26-158">Get an access key</span><span class="sxs-lookup"><span data-stu-id="f8a26-158">Get an access key</span></span>

1. <span data-ttu-id="f8a26-159">On the **Settings** page, click **Keys**.</span><span class="sxs-lookup"><span data-stu-id="f8a26-159">On the **Settings** page, click **Keys**.</span></span>
   
    ![Creating an application](./media/graph-get-started/23.png)

2. <span data-ttu-id="f8a26-161">On the **Keys** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f8a26-161">On the **Keys** page, perform the following steps:</span></span>
   
    ![Creating an application](./media/graph-get-started/24.png)

    <span data-ttu-id="f8a26-163">a.</span><span class="sxs-lookup"><span data-stu-id="f8a26-163">a.</span></span> <span data-ttu-id="f8a26-164">In the **Key description** textbox, type a description (for example, *AADIP Risk Event*).</span><span class="sxs-lookup"><span data-stu-id="f8a26-164">In the **Key description** textbox, type a description (for example, *AADIP Risk Event*).</span></span>
    
    <span data-ttu-id="f8a26-165">b.</span><span class="sxs-lookup"><span data-stu-id="f8a26-165">b.</span></span> <span data-ttu-id="f8a26-166">As **Duration**, select **In 1 year**.</span><span class="sxs-lookup"><span data-stu-id="f8a26-166">As **Duration**, select **In 1 year**.</span></span>

    <span data-ttu-id="f8a26-167">c.</span><span class="sxs-lookup"><span data-stu-id="f8a26-167">c.</span></span> <span data-ttu-id="f8a26-168">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="f8a26-168">Click **Save**.</span></span>
   
    <span data-ttu-id="f8a26-169">d.</span><span class="sxs-lookup"><span data-stu-id="f8a26-169">d.</span></span> <span data-ttu-id="f8a26-170">Copy the key value, and then paste it into a safe location.</span><span class="sxs-lookup"><span data-stu-id="f8a26-170">Copy the key value, and then paste it into a safe location.</span></span>   
   
   > [!NOTE]
   > <span data-ttu-id="f8a26-171">If you lose this key, you will have to return to this section and create a new key.</span><span class="sxs-lookup"><span data-stu-id="f8a26-171">If you lose this key, you will have to return to this section and create a new key.</span></span> <span data-ttu-id="f8a26-172">Keep this key a secret: anyone who has it can access your data.</span><span class="sxs-lookup"><span data-stu-id="f8a26-172">Keep this key a secret: anyone who has it can access your data.</span></span>
   > 
   > 

## <a name="authenticate-to-microsoft-graph-and-query-the-identity-risk-events-api"></a><span data-ttu-id="f8a26-173">Authenticate to Microsoft Graph and query the Identity Risk Events API</span><span class="sxs-lookup"><span data-stu-id="f8a26-173">Authenticate to Microsoft Graph and query the Identity Risk Events API</span></span>
<span data-ttu-id="f8a26-174">At this point, you should have:</span><span class="sxs-lookup"><span data-stu-id="f8a26-174">At this point, you should have:</span></span>

- <span data-ttu-id="f8a26-175">The name of your tenant's domain</span><span class="sxs-lookup"><span data-stu-id="f8a26-175">The name of your tenant's domain</span></span>

- <span data-ttu-id="f8a26-176">The client ID</span><span class="sxs-lookup"><span data-stu-id="f8a26-176">The client ID</span></span> 

- <span data-ttu-id="f8a26-177">The key</span><span class="sxs-lookup"><span data-stu-id="f8a26-177">The key</span></span> 


<span data-ttu-id="f8a26-178">To authenticate, send a post request to `https://login.microsoft.com` with the following parameters in the body:</span><span class="sxs-lookup"><span data-stu-id="f8a26-178">To authenticate, send a post request to `https://login.microsoft.com` with the following parameters in the body:</span></span>

- <span data-ttu-id="f8a26-179">grant_type: “**client_credentials**”</span><span class="sxs-lookup"><span data-stu-id="f8a26-179">grant_type: “**client_credentials**”</span></span>

-  <span data-ttu-id="f8a26-180">resource: “**https://graph.microsoft.com**”</span><span class="sxs-lookup"><span data-stu-id="f8a26-180">resource: “**https://graph.microsoft.com**”</span></span>

- <span data-ttu-id="f8a26-181">client_id: \<your client ID\></span><span class="sxs-lookup"><span data-stu-id="f8a26-181">client_id: \<your client ID\></span></span>

- <span data-ttu-id="f8a26-182">client_secret: \<your key\></span><span class="sxs-lookup"><span data-stu-id="f8a26-182">client_secret: \<your key\></span></span>


<span data-ttu-id="f8a26-183">If successful, this returns an authentication token.</span><span class="sxs-lookup"><span data-stu-id="f8a26-183">If successful, this returns an authentication token.</span></span>  
<span data-ttu-id="f8a26-184">To call the API, create a header with the following parameter:</span><span class="sxs-lookup"><span data-stu-id="f8a26-184">To call the API, create a header with the following parameter:</span></span>

    `Authorization`=”<token_type> <access_token>"


<span data-ttu-id="f8a26-185">When authenticating, you can find the token type and access token in the returned token.</span><span class="sxs-lookup"><span data-stu-id="f8a26-185">When authenticating, you can find the token type and access token in the returned token.</span></span>

<span data-ttu-id="f8a26-186">Send this header as a request to the following API URL: `https://graph.microsoft.com/beta/identityRiskEvents`</span><span class="sxs-lookup"><span data-stu-id="f8a26-186">Send this header as a request to the following API URL: `https://graph.microsoft.com/beta/identityRiskEvents`</span></span>

<span data-ttu-id="f8a26-187">The response, if successful, is a collection of identity risk events and associated data in the OData JSON format, which can be parsed and handled as you see fit.</span><span class="sxs-lookup"><span data-stu-id="f8a26-187">The response, if successful, is a collection of identity risk events and associated data in the OData JSON format, which can be parsed and handled as you see fit.</span></span>

<span data-ttu-id="f8a26-188">Here’s sample code for authenticating and calling the API using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f8a26-188">Here’s sample code for authenticating and calling the API using PowerShell.</span></span>  
<span data-ttu-id="f8a26-189">Just add your client ID, the secret key, and the tenant domain.</span><span class="sxs-lookup"><span data-stu-id="f8a26-189">Just add your client ID, the secret key, and the tenant domain.</span></span>

    $ClientID       = "<your client ID here>"        # Should be a ~36 hex character string; insert your info here
    $ClientSecret   = "<your client secret here>"    # Should be a ~44 character string; insert your info here
    $tenantdomain   = "<your tenant domain here>"    # For example, contoso.onmicrosoft.com

    $loginURL       = "https://login.microsoft.com"
    $resource       = "https://graph.microsoft.com"

    $body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
    $oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

    Write-Output $oauth

    if ($oauth.access_token -ne $null) {
        $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

        $url = "https://graph.microsoft.com/beta/identityRiskEvents"
        Write-Output $url

        $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)

        foreach ($event in ($myReport.Content | ConvertFrom-Json).value) {
            Write-Output $event
        }

    } else {
        Write-Host "ERROR: No Access Token"
    } 


## <a name="next-steps"></a><span data-ttu-id="f8a26-190">Next steps</span><span class="sxs-lookup"><span data-stu-id="f8a26-190">Next steps</span></span>

<span data-ttu-id="f8a26-191">Congratulations, you just made your first call to Microsoft Graph!</span><span class="sxs-lookup"><span data-stu-id="f8a26-191">Congratulations, you just made your first call to Microsoft Graph!</span></span>  
<span data-ttu-id="f8a26-192">Now you can query identity risk events and use the data however you see fit.</span><span class="sxs-lookup"><span data-stu-id="f8a26-192">Now you can query identity risk events and use the data however you see fit.</span></span>

<span data-ttu-id="f8a26-193">To learn more about Microsoft Graph and how to build applications using the Graph API, check out the [documentation](https://graph.microsoft.io/docs) and much more on the [Microsoft Graph site](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="f8a26-193">To learn more about Microsoft Graph and how to build applications using the Graph API, check out the [documentation](https://graph.microsoft.io/docs) and much more on the [Microsoft Graph site](https://graph.microsoft.io/).</span></span> <span data-ttu-id="f8a26-194">Also, make sure to bookmark the [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) page that lists all of the Identity Protection APIs available in Graph.</span><span class="sxs-lookup"><span data-stu-id="f8a26-194">Also, make sure to bookmark the [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) page that lists all of the Identity Protection APIs available in Graph.</span></span> <span data-ttu-id="f8a26-195">As we add new ways to work with Identity Protection via API, you’ll see them on that page.</span><span class="sxs-lookup"><span data-stu-id="f8a26-195">As we add new ways to work with Identity Protection via API, you’ll see them on that page.</span></span>

<span data-ttu-id="f8a26-196">For related information, see:</span><span class="sxs-lookup"><span data-stu-id="f8a26-196">For related information, see:</span></span>

-  [<span data-ttu-id="f8a26-197">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="f8a26-197">Azure Active Directory Identity Protection</span></span>](../active-directory-identityprotection.md)

-  [<span data-ttu-id="f8a26-198">Types of risk events detected by Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="f8a26-198">Types of risk events detected by Azure Active Directory Identity Protection</span></span>](../reports-monitoring/concept-risk-events.md)

- [<span data-ttu-id="f8a26-199">Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="f8a26-199">Microsoft Graph</span></span>](https://graph.microsoft.io/)

- [<span data-ttu-id="f8a26-200">Overview of Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="f8a26-200">Overview of Microsoft Graph</span></span>](https://graph.microsoft.io/docs)

- [<span data-ttu-id="f8a26-201">Azure AD Identity Protection Service Root</span><span class="sxs-lookup"><span data-stu-id="f8a26-201">Azure AD Identity Protection Service Root</span></span>](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root)

