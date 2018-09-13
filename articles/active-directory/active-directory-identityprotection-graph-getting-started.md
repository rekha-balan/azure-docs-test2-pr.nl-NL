---
title: Get started with Azure Active Directory Identity Protection and Microsoft Graph | Microsoft Docs
description: Provides an introduction to query Microsoft Graph for a list of risk events and associated information from Azure Active Directory.
services: active-directory
keywords: azure active directory identity protection, risk event, vulnerability, security policy, Microsoft Graph
documentationcenter: ''
author: MarkusVi
manager: femila
ms.assetid: fa109ba7-a914-437b-821d-2bd98e681386
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: markvi
ms.openlocfilehash: 5472ecffb297b6ddd345fa83cf9e793a374f36c9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563351"
---
# <a name="get-started-with-azure-active-directory-identity-protection-and-microsoft-graph"></a><span data-ttu-id="e495f-104">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="e495f-104">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>
<span data-ttu-id="e495f-105">Microsoft Graph is Microsoft’s unified API endpoint and the home of [Azure Active Directory Identity Protection’s](active-directory-identityprotection.md) APIs.</span><span class="sxs-lookup"><span data-stu-id="e495f-105">Microsoft Graph is Microsoft’s unified API endpoint and the home of [Azure Active Directory Identity Protection’s](active-directory-identityprotection.md) APIs.</span></span> <span data-ttu-id="e495f-106">Our first API, **identityRiskEvents**, allows you to query Microsoft Graph for a list of [risk events](active-directory-identityprotection-risk-events-types.md) and associated information.</span><span class="sxs-lookup"><span data-stu-id="e495f-106">Our first API, **identityRiskEvents**, allows you to query Microsoft Graph for a list of [risk events](active-directory-identityprotection-risk-events-types.md) and associated information.</span></span> <span data-ttu-id="e495f-107">This article gets you started querying this API.</span><span class="sxs-lookup"><span data-stu-id="e495f-107">This article gets you started querying this API.</span></span> <span data-ttu-id="e495f-108">For an in depth introduction, full documentation, and access to the Graph Explorer, see the [Microsoft Graph site](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="e495f-108">For an in depth introduction, full documentation, and access to the Graph Explorer, see the [Microsoft Graph site](https://graph.microsoft.io/).</span></span>


<span data-ttu-id="e495f-109">There are three steps to accessing Identity Protection data through Microsoft Graph:</span><span class="sxs-lookup"><span data-stu-id="e495f-109">There are three steps to accessing Identity Protection data through Microsoft Graph:</span></span>

1. <span data-ttu-id="e495f-110">Add an application with a client secret.</span><span class="sxs-lookup"><span data-stu-id="e495f-110">Add an application with a client secret.</span></span> 
2. <span data-ttu-id="e495f-111">Use this secret and a few other pieces of information to authenticate to Microsoft Graph, where you receive an authentication token.</span><span class="sxs-lookup"><span data-stu-id="e495f-111">Use this secret and a few other pieces of information to authenticate to Microsoft Graph, where you receive an authentication token.</span></span> 
3. <span data-ttu-id="e495f-112">Use this token to make requests to the API endpoint and get Identity Protection data back.</span><span class="sxs-lookup"><span data-stu-id="e495f-112">Use this token to make requests to the API endpoint and get Identity Protection data back.</span></span>

<span data-ttu-id="e495f-113">Before you get started, you’ll need:</span><span class="sxs-lookup"><span data-stu-id="e495f-113">Before you get started, you’ll need:</span></span>

* <span data-ttu-id="e495f-114">Administrator privileges to create the application in Azure AD</span><span class="sxs-lookup"><span data-stu-id="e495f-114">Administrator privileges to create the application in Azure AD</span></span>
* <span data-ttu-id="e495f-115">The name of your tenant's domain (for example, contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="e495f-115">The name of your tenant's domain (for example, contoso.onmicrosoft.com)</span></span>

## <a name="add-an-application-with-a-client-secret"></a><span data-ttu-id="e495f-116">Add an application with a client secret</span><span class="sxs-lookup"><span data-stu-id="e495f-116">Add an application with a client secret</span></span>
1. <span data-ttu-id="e495f-117">[Sign in](https://manage.windowsazure.com) to your Azure classic portal as an administrator.</span><span class="sxs-lookup"><span data-stu-id="e495f-117">[Sign in](https://manage.windowsazure.com) to your Azure classic portal as an administrator.</span></span> 
2. <span data-ttu-id="e495f-118">On on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e495f-118">On on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Creating an application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection-graph-getting-started/tutorial_general_01.png)
3. <span data-ttu-id="e495f-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="e495f-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
4. <span data-ttu-id="e495f-121">In the menu on the top, click **Applications**.</span><span class="sxs-lookup"><span data-stu-id="e495f-121">In the menu on the top, click **Applications**.</span></span>
   
    ![Creating an application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection-graph-getting-started/tutorial_general_02.png)
5. <span data-ttu-id="e495f-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="e495f-123">Click **Add** at the bottom of the page.</span></span>
   
    ![Creating an application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection-graph-getting-started/tutorial_general_03.png)
6. <span data-ttu-id="e495f-125">On the **What do you want to do** dialog, click **Add an application my organization is developing**.</span><span class="sxs-lookup"><span data-stu-id="e495f-125">On the **What do you want to do** dialog, click **Add an application my organization is developing**.</span></span>
   
    ![Creating an application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection-graph-getting-started/tutorial_general_04.png)
7. <span data-ttu-id="e495f-127">On the **Tell us about your application** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e495f-127">On the **Tell us about your application** dialog, perform the following steps:</span></span>
   
    ![Creating an application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection-graph-getting-started/tutorial_general_05.png)
   
    <span data-ttu-id="e495f-129">a.</span><span class="sxs-lookup"><span data-stu-id="e495f-129">a.</span></span> <span data-ttu-id="e495f-130">In the **Name** textbox, type a name for your application (e.g.: AADIP Risk Event API Application).</span><span class="sxs-lookup"><span data-stu-id="e495f-130">In the **Name** textbox, type a name for your application (e.g.: AADIP Risk Event API Application).</span></span>
   
    <span data-ttu-id="e495f-131">b.</span><span class="sxs-lookup"><span data-stu-id="e495f-131">b.</span></span> <span data-ttu-id="e495f-132">As **Type**, select **Web Application And / Or Web API**.</span><span class="sxs-lookup"><span data-stu-id="e495f-132">As **Type**, select **Web Application And / Or Web API**.</span></span>
   
    <span data-ttu-id="e495f-133">c.</span><span class="sxs-lookup"><span data-stu-id="e495f-133">c.</span></span> <span data-ttu-id="e495f-134">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e495f-134">Click **Next**.</span></span>
8. <span data-ttu-id="e495f-135">On the **App properties** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e495f-135">On the **App properties** dialog, perform the following steps:</span></span>
   
    ![Creating an application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection-graph-getting-started/tutorial_general_06.png)
   
    <span data-ttu-id="e495f-137">a.</span><span class="sxs-lookup"><span data-stu-id="e495f-137">a.</span></span> <span data-ttu-id="e495f-138">In the **Sign-On URL** textbox, type `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="e495f-138">In the **Sign-On URL** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="e495f-139">b.</span><span class="sxs-lookup"><span data-stu-id="e495f-139">b.</span></span> <span data-ttu-id="e495f-140">In the **App ID URI** textbox, type `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="e495f-140">In the **App ID URI** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="e495f-141">c.</span><span class="sxs-lookup"><span data-stu-id="e495f-141">c.</span></span> <span data-ttu-id="e495f-142">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="e495f-142">Click **Complete**.</span></span>

<span data-ttu-id="e495f-143">Your can now configure your application.</span><span class="sxs-lookup"><span data-stu-id="e495f-143">Your can now configure your application.</span></span>

![Creating an application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection-graph-getting-started/tutorial_general_07.png)

## <a name="grant-your-application-permission-to-use-the-api"></a><span data-ttu-id="e495f-145">Grant your application permission to use the API</span><span class="sxs-lookup"><span data-stu-id="e495f-145">Grant your application permission to use the API</span></span>
1. <span data-ttu-id="e495f-146">On your application's page, in the menu on the top, click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="e495f-146">On your application's page, in the menu on the top, click **Configure**.</span></span> 
   
    ![Creating an application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection-graph-getting-started/tutorial_general_08.png)
2. <span data-ttu-id="e495f-148">In the **permissions to other applications** section, click **Add application**.</span><span class="sxs-lookup"><span data-stu-id="e495f-148">In the **permissions to other applications** section, click **Add application**.</span></span>
   
    ![Creating an application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection-graph-getting-started/tutorial_general_09.png)
3. <span data-ttu-id="e495f-150">On the **permissions to other applications** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e495f-150">On the **permissions to other applications** dialog, perform the following steps:</span></span>
   
    ![Creating an application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection-graph-getting-started/tutorial_general_10.png)
   
    <span data-ttu-id="e495f-152">a.</span><span class="sxs-lookup"><span data-stu-id="e495f-152">a.</span></span> <span data-ttu-id="e495f-153">Select **Microsoft Graph**.</span><span class="sxs-lookup"><span data-stu-id="e495f-153">Select **Microsoft Graph**.</span></span>
   
    <span data-ttu-id="e495f-154">b.</span><span class="sxs-lookup"><span data-stu-id="e495f-154">b.</span></span> <span data-ttu-id="e495f-155">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="e495f-155">Click **Complete**.</span></span>
4. <span data-ttu-id="e495f-156">Click **Application Permissions: 0**, and then select **Read all identity risk event information**.</span><span class="sxs-lookup"><span data-stu-id="e495f-156">Click **Application Permissions: 0**, and then select **Read all identity risk event information**.</span></span>
   
    ![Creating an application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection-graph-getting-started/tutorial_general_11.png)
5. <span data-ttu-id="e495f-158">Click **Save** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="e495f-158">Click **Save** at the bottom of the page.</span></span>
   
    ![Creating an application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)

## <a name="get-an-access-key"></a><span data-ttu-id="e495f-160">Get an access key</span><span class="sxs-lookup"><span data-stu-id="e495f-160">Get an access key</span></span>
1. <span data-ttu-id="e495f-161">On your application's page, in the **keys** section, select 1 year as duration.</span><span class="sxs-lookup"><span data-stu-id="e495f-161">On your application's page, in the **keys** section, select 1 year as duration.</span></span>
   
    ![Creating an application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection-graph-getting-started/tutorial_general_13.png)
2. <span data-ttu-id="e495f-163">Click **Save** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="e495f-163">Click **Save** at the bottom of the page.</span></span>
   
    ![Creating an application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)
3. <span data-ttu-id="e495f-165">in the keys section, copy the value of your newly created key, and then paste it into a safe location.</span><span class="sxs-lookup"><span data-stu-id="e495f-165">in the keys section, copy the value of your newly created key, and then paste it into a safe location.</span></span>
   
    ![Creating an application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection-graph-getting-started/tutorial_general_14.png)
   
   > [!NOTE]
   > <span data-ttu-id="e495f-167">If you lose this key, you will have to return to this section and create a new key.</span><span class="sxs-lookup"><span data-stu-id="e495f-167">If you lose this key, you will have to return to this section and create a new key.</span></span> <span data-ttu-id="e495f-168">Keep this key a secret: anyone who has it can access your data.</span><span class="sxs-lookup"><span data-stu-id="e495f-168">Keep this key a secret: anyone who has it can access your data.</span></span>
   > 
   > 
4. <span data-ttu-id="e495f-169">In the **properties** section, copy the **Client ID**, and then paste it into a safe location.</span><span class="sxs-lookup"><span data-stu-id="e495f-169">In the **properties** section, copy the **Client ID**, and then paste it into a safe location.</span></span> 

## <a name="authenticate-to-microsoft-graph-and-query-the-identity-risk-events-api"></a><span data-ttu-id="e495f-170">Authenticate to Microsoft Graph and query the Identity Risk Events API</span><span class="sxs-lookup"><span data-stu-id="e495f-170">Authenticate to Microsoft Graph and query the Identity Risk Events API</span></span>
<span data-ttu-id="e495f-171">At this point, you should have:</span><span class="sxs-lookup"><span data-stu-id="e495f-171">At this point, you should have:</span></span>

* <span data-ttu-id="e495f-172">The client ID you copied above</span><span class="sxs-lookup"><span data-stu-id="e495f-172">The client ID you copied above</span></span>
* <span data-ttu-id="e495f-173">The key you copied above</span><span class="sxs-lookup"><span data-stu-id="e495f-173">The key you copied above</span></span>
* <span data-ttu-id="e495f-174">The name of your tenant's domain</span><span class="sxs-lookup"><span data-stu-id="e495f-174">The name of your tenant's domain</span></span>

<span data-ttu-id="e495f-175">To authenticate, send a post request to `https://login.microsoft.com` with the following parameters in the body:</span><span class="sxs-lookup"><span data-stu-id="e495f-175">To authenticate, send a post request to `https://login.microsoft.com` with the following parameters in the body:</span></span>

* <span data-ttu-id="e495f-176">grant_type: “**client_credentials**”</span><span class="sxs-lookup"><span data-stu-id="e495f-176">grant_type: “**client_credentials**”</span></span>
* <span data-ttu-id="e495f-177">resource: “**https://graph.microsoft.com**”</span><span class="sxs-lookup"><span data-stu-id="e495f-177">resource: “**https://graph.microsoft.com**”</span></span>
* <span data-ttu-id="e495f-178">client_id: <your client ID></span><span class="sxs-lookup"><span data-stu-id="e495f-178">client_id: <your client ID></span></span>
* <span data-ttu-id="e495f-179">client_secret: <your key></span><span class="sxs-lookup"><span data-stu-id="e495f-179">client_secret: <your key></span></span>

> [!NOTE]
> <span data-ttu-id="e495f-180">You need to provide values for the **client_id** and the **client_secret** parameter.</span><span class="sxs-lookup"><span data-stu-id="e495f-180">You need to provide values for the **client_id** and the **client_secret** parameter.</span></span>
> 
> 

<span data-ttu-id="e495f-181">If successful, this returns an authentication token.</span><span class="sxs-lookup"><span data-stu-id="e495f-181">If successful, this returns an authentication token.</span></span>  
<span data-ttu-id="e495f-182">To call the API, create a header with the following parameter:</span><span class="sxs-lookup"><span data-stu-id="e495f-182">To call the API, create a header with the following parameter:</span></span>

    `Authorization`=”<token_type> <access_token>"


<span data-ttu-id="e495f-183">When authenticating, you can find the token type and access token in the returned token.</span><span class="sxs-lookup"><span data-stu-id="e495f-183">When authenticating, you can find the token type and access token in the returned token.</span></span>

<span data-ttu-id="e495f-184">Send this header as a request to the following API URL: `https://graph.microsoft.com/beta/identityRiskEvents`</span><span class="sxs-lookup"><span data-stu-id="e495f-184">Send this header as a request to the following API URL: `https://graph.microsoft.com/beta/identityRiskEvents`</span></span>

<span data-ttu-id="e495f-185">The response, if successful, is a collection of identity risk events and associated data in the OData JSON format, which can be parsed and handled as see fit.</span><span class="sxs-lookup"><span data-stu-id="e495f-185">The response, if successful, is a collection of identity risk events and associated data in the OData JSON format, which can be parsed and handled as see fit.</span></span>

<span data-ttu-id="e495f-186">Here’s sample code for authenticating and calling the API using Powershell.</span><span class="sxs-lookup"><span data-stu-id="e495f-186">Here’s sample code for authenticating and calling the API using Powershell.</span></span>  
<span data-ttu-id="e495f-187">Just add your client ID, key, and tenant domain.</span><span class="sxs-lookup"><span data-stu-id="e495f-187">Just add your client ID, key, and tenant domain.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="e495f-188">Next steps</span><span class="sxs-lookup"><span data-stu-id="e495f-188">Next steps</span></span>
<span data-ttu-id="e495f-189">Congratulations, you just made your first call to Microsoft Graph!</span><span class="sxs-lookup"><span data-stu-id="e495f-189">Congratulations, you just made your first call to Microsoft Graph!</span></span>  
<span data-ttu-id="e495f-190">Now you can query identity risk events and use the data however you see fit.</span><span class="sxs-lookup"><span data-stu-id="e495f-190">Now you can query identity risk events and use the data however you see fit.</span></span>

<span data-ttu-id="e495f-191">To learn more about Microsoft Graph and how to build applications using the Graph API, check out the [documentation](https://graph.microsoft.io/docs) and much more on the [Microsoft Graph site](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="e495f-191">To learn more about Microsoft Graph and how to build applications using the Graph API, check out the [documentation](https://graph.microsoft.io/docs) and much more on the [Microsoft Graph site](https://graph.microsoft.io/).</span></span> <span data-ttu-id="e495f-192">Also, make sure to bookmark the [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) page that lists all of the Identity Protection APIs available in Graph.</span><span class="sxs-lookup"><span data-stu-id="e495f-192">Also, make sure to bookmark the [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) page that lists all of the Identity Protection APIs available in Graph.</span></span> <span data-ttu-id="e495f-193">As we add new ways to work with Identity Protection via API, you’ll see them on that page.</span><span class="sxs-lookup"><span data-stu-id="e495f-193">As we add new ways to work with Identity Protection via API, you’ll see them on that page.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e495f-194">Additional resources</span><span class="sxs-lookup"><span data-stu-id="e495f-194">Additional resources</span></span>
* [<span data-ttu-id="e495f-195">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="e495f-195">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)
* [<span data-ttu-id="e495f-196">Types of risk events detected by Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="e495f-196">Types of risk events detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-risk-events-types.md)
* [<span data-ttu-id="e495f-197">Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="e495f-197">Microsoft Graph</span></span>](https://graph.microsoft.io/)
* [<span data-ttu-id="e495f-198">Overview of Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="e495f-198">Overview of Microsoft Graph</span></span>](https://graph.microsoft.io/docs)
* [<span data-ttu-id="e495f-199">Azure AD Identity Protection Service Root</span><span class="sxs-lookup"><span data-stu-id="e495f-199">Azure AD Identity Protection Service Root</span></span>](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root)
















