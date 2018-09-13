---
title: Protect an API by using OAuth 2.0 with Azure Active Directory and API Management | Microsoft Docs
description: Learn how to protect a web API backend with Azure Active Directory and API Management.
services: api-management
documentationcenter: ''
author: miaojiang
manager: cfowler
editor: ''
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/18/2018
ms.author: apimpm
ms.openlocfilehash: 06350d30999cb056babbd001f98a6c3a5fdbac6c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44805537"
---
# <a name="protect-an-api-by-using-oauth-20-with-azure-active-directory-and-api-management"></a><span data-ttu-id="d41ca-103">Protect an API by using OAuth 2.0 with Azure Active Directory and API Management</span><span class="sxs-lookup"><span data-stu-id="d41ca-103">Protect an API by using OAuth 2.0 with Azure Active Directory and API Management</span></span>

<span data-ttu-id="d41ca-104">This guide shows you how to configure your Azure API Management instance to protect an API, by using the OAuth 2.0 protocol with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d41ca-104">This guide shows you how to configure your Azure API Management instance to protect an API, by using the OAuth 2.0 protocol with Azure Active Directory (Azure AD).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d41ca-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d41ca-105">Prerequisites</span></span>
<span data-ttu-id="d41ca-106">To follow the steps in this article, you must have:</span><span class="sxs-lookup"><span data-stu-id="d41ca-106">To follow the steps in this article, you must have:</span></span>
* <span data-ttu-id="d41ca-107">An API Management instance</span><span class="sxs-lookup"><span data-stu-id="d41ca-107">An API Management instance</span></span>
* <span data-ttu-id="d41ca-108">An API being published that uses the API Management instance</span><span class="sxs-lookup"><span data-stu-id="d41ca-108">An API being published that uses the API Management instance</span></span>
* <span data-ttu-id="d41ca-109">An Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="d41ca-109">An Azure AD tenant</span></span>

## <a name="overview"></a><span data-ttu-id="d41ca-110">Overview</span><span class="sxs-lookup"><span data-stu-id="d41ca-110">Overview</span></span>

<span data-ttu-id="d41ca-111">Here is a quick overview of the steps:</span><span class="sxs-lookup"><span data-stu-id="d41ca-111">Here is a quick overview of the steps:</span></span>

1. <span data-ttu-id="d41ca-112">Register an application (backend-app) in Azure AD to represent the API.</span><span class="sxs-lookup"><span data-stu-id="d41ca-112">Register an application (backend-app) in Azure AD to represent the API.</span></span>
2. <span data-ttu-id="d41ca-113">Register another application (client-app) in Azure AD to represent a client application that needs to call the API.</span><span class="sxs-lookup"><span data-stu-id="d41ca-113">Register another application (client-app) in Azure AD to represent a client application that needs to call the API.</span></span>
3. <span data-ttu-id="d41ca-114">In Azure AD, grant permissions to allow the client-app to call the backend-app.</span><span class="sxs-lookup"><span data-stu-id="d41ca-114">In Azure AD, grant permissions to allow the client-app to call the backend-app.</span></span>
4. <span data-ttu-id="d41ca-115">Configure the Developer Console to use OAuth 2.0 user authorization.</span><span class="sxs-lookup"><span data-stu-id="d41ca-115">Configure the Developer Console to use OAuth 2.0 user authorization.</span></span>
5. <span data-ttu-id="d41ca-116">Add the **validate-jwt** policy to validate the OAuth token for every incoming request.</span><span class="sxs-lookup"><span data-stu-id="d41ca-116">Add the **validate-jwt** policy to validate the OAuth token for every incoming request.</span></span>

## <a name="register-an-application-in-azure-ad-to-represent-the-api"></a><span data-ttu-id="d41ca-117">Register an application in Azure AD to represent the API</span><span class="sxs-lookup"><span data-stu-id="d41ca-117">Register an application in Azure AD to represent the API</span></span>

<span data-ttu-id="d41ca-118">To protect an API with Azure AD, the first step is to register an application in Azure AD that represents the API.</span><span class="sxs-lookup"><span data-stu-id="d41ca-118">To protect an API with Azure AD, the first step is to register an application in Azure AD that represents the API.</span></span> 

1. <span data-ttu-id="d41ca-119">Browse to your Azure AD tenant, and then browse to **App registrations**.</span><span class="sxs-lookup"><span data-stu-id="d41ca-119">Browse to your Azure AD tenant, and then browse to **App registrations**.</span></span>

2. <span data-ttu-id="d41ca-120">Select **New application registration**.</span><span class="sxs-lookup"><span data-stu-id="d41ca-120">Select **New application registration**.</span></span> 

3. <span data-ttu-id="d41ca-121">Provide a name of the application.</span><span class="sxs-lookup"><span data-stu-id="d41ca-121">Provide a name of the application.</span></span> <span data-ttu-id="d41ca-122">(For this example, the name is `backend-app`.)</span><span class="sxs-lookup"><span data-stu-id="d41ca-122">(For this example, the name is `backend-app`.)</span></span>  

4. <span data-ttu-id="d41ca-123">Choose **Web app / API** as the **Application type**.</span><span class="sxs-lookup"><span data-stu-id="d41ca-123">Choose **Web app / API** as the **Application type**.</span></span> 

5. <span data-ttu-id="d41ca-124">For **Sign-on URL**, you can use `https://localhost` as a placeholder.</span><span class="sxs-lookup"><span data-stu-id="d41ca-124">For **Sign-on URL**, you can use `https://localhost` as a placeholder.</span></span>

6. <span data-ttu-id="d41ca-125">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="d41ca-125">Select **Create**.</span></span>

<span data-ttu-id="d41ca-126">When the application is created, make a note of the **Application ID**, for use in a subsequent step.</span><span class="sxs-lookup"><span data-stu-id="d41ca-126">When the application is created, make a note of the **Application ID**, for use in a subsequent step.</span></span> 

## <a name="register-another-application-in-azure-ad-to-represent-a-client-application"></a><span data-ttu-id="d41ca-127">Register another application in Azure AD to represent a client application</span><span class="sxs-lookup"><span data-stu-id="d41ca-127">Register another application in Azure AD to represent a client application</span></span>

<span data-ttu-id="d41ca-128">Every client application that calls the API needs to be registered as an application in Azure AD as well.</span><span class="sxs-lookup"><span data-stu-id="d41ca-128">Every client application that calls the API needs to be registered as an application in Azure AD as well.</span></span> <span data-ttu-id="d41ca-129">For this example, the sample client application is the Developer Console in the API Management developer portal.</span><span class="sxs-lookup"><span data-stu-id="d41ca-129">For this example, the sample client application is the Developer Console in the API Management developer portal.</span></span> <span data-ttu-id="d41ca-130">Here's how to register another application in Azure AD to represent the Developer Console.</span><span class="sxs-lookup"><span data-stu-id="d41ca-130">Here's how to register another application in Azure AD to represent the Developer Console.</span></span>

1. <span data-ttu-id="d41ca-131">Select **New application registration**.</span><span class="sxs-lookup"><span data-stu-id="d41ca-131">Select **New application registration**.</span></span> 

2. <span data-ttu-id="d41ca-132">Provide a name of the application.</span><span class="sxs-lookup"><span data-stu-id="d41ca-132">Provide a name of the application.</span></span> <span data-ttu-id="d41ca-133">(For this example, the name is `client-app`.)</span><span class="sxs-lookup"><span data-stu-id="d41ca-133">(For this example, the name is `client-app`.)</span></span>

3. <span data-ttu-id="d41ca-134">Choose **Web app / API** as the **Application type**.</span><span class="sxs-lookup"><span data-stu-id="d41ca-134">Choose **Web app / API** as the **Application type**.</span></span>  

4. <span data-ttu-id="d41ca-135">For **Sign-on URL**, you can use `https://localhost` as a placeholder, or use the sign-in URL of your API Management instance.</span><span class="sxs-lookup"><span data-stu-id="d41ca-135">For **Sign-on URL**, you can use `https://localhost` as a placeholder, or use the sign-in URL of your API Management instance.</span></span> <span data-ttu-id="d41ca-136">(For this example, the URL is `https://contoso5.portal.azure-api.net/signin`.)</span><span class="sxs-lookup"><span data-stu-id="d41ca-136">(For this example, the URL is `https://contoso5.portal.azure-api.net/signin`.)</span></span>

5. <span data-ttu-id="d41ca-137">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="d41ca-137">Select **Create**.</span></span>

<span data-ttu-id="d41ca-138">When the application is created, make a note of the **Application ID**, for use in a subsequent step.</span><span class="sxs-lookup"><span data-stu-id="d41ca-138">When the application is created, make a note of the **Application ID**, for use in a subsequent step.</span></span> 

<span data-ttu-id="d41ca-139">Now, create a client secret for this application, for use in a subsequent step.</span><span class="sxs-lookup"><span data-stu-id="d41ca-139">Now, create a client secret for this application, for use in a subsequent step.</span></span>

1. <span data-ttu-id="d41ca-140">Select **Settings** again, and go to **Keys**.</span><span class="sxs-lookup"><span data-stu-id="d41ca-140">Select **Settings** again, and go to **Keys**.</span></span>

2. <span data-ttu-id="d41ca-141">Under **Passwords**, provide a **Key description**.</span><span class="sxs-lookup"><span data-stu-id="d41ca-141">Under **Passwords**, provide a **Key description**.</span></span> <span data-ttu-id="d41ca-142">Choose when the key should expire, and select **Save**.</span><span class="sxs-lookup"><span data-stu-id="d41ca-142">Choose when the key should expire, and select **Save**.</span></span>

<span data-ttu-id="d41ca-143">Make a note of the key value.</span><span class="sxs-lookup"><span data-stu-id="d41ca-143">Make a note of the key value.</span></span> 

## <a name="grant-permissions-in-azure-ad"></a><span data-ttu-id="d41ca-144">Grant permissions in Azure AD</span><span class="sxs-lookup"><span data-stu-id="d41ca-144">Grant permissions in Azure AD</span></span>

<span data-ttu-id="d41ca-145">Now that you have registered two applications to represent the API and the Developer Console, you need to grant permissions to allow the client-app to call the backend-app.</span><span class="sxs-lookup"><span data-stu-id="d41ca-145">Now that you have registered two applications to represent the API and the Developer Console, you need to grant permissions to allow the client-app to call the backend-app.</span></span>  

1. <span data-ttu-id="d41ca-146">Browse to **Application registrations**.</span><span class="sxs-lookup"><span data-stu-id="d41ca-146">Browse to **Application registrations**.</span></span> 

2. <span data-ttu-id="d41ca-147">Select `client-app`, and go to **Settings**.</span><span class="sxs-lookup"><span data-stu-id="d41ca-147">Select `client-app`, and go to **Settings**.</span></span>

3. <span data-ttu-id="d41ca-148">Select **Required permissions** > **Add**.</span><span class="sxs-lookup"><span data-stu-id="d41ca-148">Select **Required permissions** > **Add**.</span></span>

4. <span data-ttu-id="d41ca-149">Select **Select an API**, and search for `backend-app`.</span><span class="sxs-lookup"><span data-stu-id="d41ca-149">Select **Select an API**, and search for `backend-app`.</span></span>

5. <span data-ttu-id="d41ca-150">Under **Delegated Permissions**, select `Access backend-app`.</span><span class="sxs-lookup"><span data-stu-id="d41ca-150">Under **Delegated Permissions**, select `Access backend-app`.</span></span> 

6. <span data-ttu-id="d41ca-151">Select **Select**, and then select **Done**.</span><span class="sxs-lookup"><span data-stu-id="d41ca-151">Select **Select**, and then select **Done**.</span></span> 

> [!NOTE]
> <span data-ttu-id="d41ca-152">If **Azure Active Directory** is not listed under permissions to other applications, select **Add** to add it from the list.</span><span class="sxs-lookup"><span data-stu-id="d41ca-152">If **Azure Active Directory** is not listed under permissions to other applications, select **Add** to add it from the list.</span></span>
> 
> 

## <a name="enable-oauth-20-user-authorization-in-the-developer-console"></a><span data-ttu-id="d41ca-153">Enable OAuth 2.0 user authorization in the Developer Console</span><span class="sxs-lookup"><span data-stu-id="d41ca-153">Enable OAuth 2.0 user authorization in the Developer Console</span></span>

<span data-ttu-id="d41ca-154">At this point, you have created your applications in Azure AD, and have granted proper permissions to allow the client-app to call the backend-app.</span><span class="sxs-lookup"><span data-stu-id="d41ca-154">At this point, you have created your applications in Azure AD, and have granted proper permissions to allow the client-app to call the backend-app.</span></span> 

<span data-ttu-id="d41ca-155">In this example, the Developer Console is the client-app.</span><span class="sxs-lookup"><span data-stu-id="d41ca-155">In this example, the Developer Console is the client-app.</span></span> <span data-ttu-id="d41ca-156">The following steps describe how to enable OAuth 2.0 user authorization in the Developer Console.</span><span class="sxs-lookup"><span data-stu-id="d41ca-156">The following steps describe how to enable OAuth 2.0 user authorization in the Developer Console.</span></span> 

1. <span data-ttu-id="d41ca-157">Browse to your API Management instance.</span><span class="sxs-lookup"><span data-stu-id="d41ca-157">Browse to your API Management instance.</span></span>

2. <span data-ttu-id="d41ca-158">Select **OAuth 2.0** > **Add**.</span><span class="sxs-lookup"><span data-stu-id="d41ca-158">Select **OAuth 2.0** > **Add**.</span></span>

3. <span data-ttu-id="d41ca-159">Provide a **Display name** and **Description**.</span><span class="sxs-lookup"><span data-stu-id="d41ca-159">Provide a **Display name** and **Description**.</span></span>

4. <span data-ttu-id="d41ca-160">For the **Client registration page URL**, enter a placeholder value, such as `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="d41ca-160">For the **Client registration page URL**, enter a placeholder value, such as `http://localhost`.</span></span> <span data-ttu-id="d41ca-161">The **Client registration page URL** points to the page that users can use to create and configure their own accounts for OAuth 2.0 providers that support this.</span><span class="sxs-lookup"><span data-stu-id="d41ca-161">The **Client registration page URL** points to the page that users can use to create and configure their own accounts for OAuth 2.0 providers that support this.</span></span> <span data-ttu-id="d41ca-162">In this example, users do not create and configure their own accounts, so you use a placeholder instead.</span><span class="sxs-lookup"><span data-stu-id="d41ca-162">In this example, users do not create and configure their own accounts, so you use a placeholder instead.</span></span>

5. <span data-ttu-id="d41ca-163">For **Authorization grant types**, select **Authorization code**.</span><span class="sxs-lookup"><span data-stu-id="d41ca-163">For **Authorization grant types**, select **Authorization code**.</span></span>

6. <span data-ttu-id="d41ca-164">Specify the **Authorization endpoint URL** and **Token endpoint URL**.</span><span class="sxs-lookup"><span data-stu-id="d41ca-164">Specify the **Authorization endpoint URL** and **Token endpoint URL**.</span></span> <span data-ttu-id="d41ca-165">Retrieve these values from the **Endpoints** page in your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="d41ca-165">Retrieve these values from the **Endpoints** page in your Azure AD tenant.</span></span> <span data-ttu-id="d41ca-166">Browse to the **App registrations** page again, and select **Endpoints**.</span><span class="sxs-lookup"><span data-stu-id="d41ca-166">Browse to the **App registrations** page again, and select **Endpoints**.</span></span>

7. <span data-ttu-id="d41ca-167">Copy the **OAuth 2.0 Authorization Endpoint**, and paste it into the **Authorization endpoint URL** text box.</span><span class="sxs-lookup"><span data-stu-id="d41ca-167">Copy the **OAuth 2.0 Authorization Endpoint**, and paste it into the **Authorization endpoint URL** text box.</span></span>

8. <span data-ttu-id="d41ca-168">Copy the **OAuth 2.0 Token Endpoint**, and paste it into the **Token endpoint URL** text box.</span><span class="sxs-lookup"><span data-stu-id="d41ca-168">Copy the **OAuth 2.0 Token Endpoint**, and paste it into the **Token endpoint URL** text box.</span></span> <span data-ttu-id="d41ca-169">In addition to pasting in the token endpoint, add a body parameter named **resource**.</span><span class="sxs-lookup"><span data-stu-id="d41ca-169">In addition to pasting in the token endpoint, add a body parameter named **resource**.</span></span> <span data-ttu-id="d41ca-170">For the value of this parameter, use the **Application ID** for the back-end app.</span><span class="sxs-lookup"><span data-stu-id="d41ca-170">For the value of this parameter, use the **Application ID** for the back-end app.</span></span>

9. <span data-ttu-id="d41ca-171">Next, specify the client credentials.</span><span class="sxs-lookup"><span data-stu-id="d41ca-171">Next, specify the client credentials.</span></span> <span data-ttu-id="d41ca-172">These are the credentials for the client-app.</span><span class="sxs-lookup"><span data-stu-id="d41ca-172">These are the credentials for the client-app.</span></span>

10. <span data-ttu-id="d41ca-173">For **Client ID**, use the **Application ID** for the client-app.</span><span class="sxs-lookup"><span data-stu-id="d41ca-173">For **Client ID**, use the **Application ID** for the client-app.</span></span>

11. <span data-ttu-id="d41ca-174">For **Client secret**, use the key you created for the client-app earlier.</span><span class="sxs-lookup"><span data-stu-id="d41ca-174">For **Client secret**, use the key you created for the client-app earlier.</span></span> 

12. <span data-ttu-id="d41ca-175">Immediately following the client secret is the **redirect_url** for the authorization code grant type.</span><span class="sxs-lookup"><span data-stu-id="d41ca-175">Immediately following the client secret is the **redirect_url** for the authorization code grant type.</span></span> <span data-ttu-id="d41ca-176">Make a note of this URL.</span><span class="sxs-lookup"><span data-stu-id="d41ca-176">Make a note of this URL.</span></span>

13. <span data-ttu-id="d41ca-177">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="d41ca-177">Select **Create**.</span></span>

14. <span data-ttu-id="d41ca-178">Go back to the **Settings** page of your client-app.</span><span class="sxs-lookup"><span data-stu-id="d41ca-178">Go back to the **Settings** page of your client-app.</span></span>

15. <span data-ttu-id="d41ca-179">Select **Reply URLs**, and paste the **redirect_url** in the first row.</span><span class="sxs-lookup"><span data-stu-id="d41ca-179">Select **Reply URLs**, and paste the **redirect_url** in the first row.</span></span> <span data-ttu-id="d41ca-180">In this example, you replaced `https://localhost` with the URL in the first row.</span><span class="sxs-lookup"><span data-stu-id="d41ca-180">In this example, you replaced `https://localhost` with the URL in the first row.</span></span>  

<span data-ttu-id="d41ca-181">Now that you have configured an OAuth 2.0 authorization server, the Developer Console can obtain access tokens from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d41ca-181">Now that you have configured an OAuth 2.0 authorization server, the Developer Console can obtain access tokens from Azure AD.</span></span> 

<span data-ttu-id="d41ca-182">The next step is to enable OAuth 2.0 user authorization for your API.</span><span class="sxs-lookup"><span data-stu-id="d41ca-182">The next step is to enable OAuth 2.0 user authorization for your API.</span></span> <span data-ttu-id="d41ca-183">This enables the Developer Console to know that it needs to obtain an access token on behalf of the user, before making calls to your API.</span><span class="sxs-lookup"><span data-stu-id="d41ca-183">This enables the Developer Console to know that it needs to obtain an access token on behalf of the user, before making calls to your API.</span></span>

1. <span data-ttu-id="d41ca-184">Browse to your API Management instance, and go to **APIs**.</span><span class="sxs-lookup"><span data-stu-id="d41ca-184">Browse to your API Management instance, and go to **APIs**.</span></span>

2. <span data-ttu-id="d41ca-185">Select the API you want to protect.</span><span class="sxs-lookup"><span data-stu-id="d41ca-185">Select the API you want to protect.</span></span> <span data-ttu-id="d41ca-186">In this example, you use the `Echo API`.</span><span class="sxs-lookup"><span data-stu-id="d41ca-186">In this example, you use the `Echo API`.</span></span>

3. <span data-ttu-id="d41ca-187">Go to **Settings**.</span><span class="sxs-lookup"><span data-stu-id="d41ca-187">Go to **Settings**.</span></span>

4. <span data-ttu-id="d41ca-188">Under **Security**, choose **OAuth 2.0**, and select the OAuth 2.0 server you configured earlier.</span><span class="sxs-lookup"><span data-stu-id="d41ca-188">Under **Security**, choose **OAuth 2.0**, and select the OAuth 2.0 server you configured earlier.</span></span> 

5. <span data-ttu-id="d41ca-189">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="d41ca-189">Select **Save**.</span></span>

## <a name="successfully-call-the-api-from-the-developer-portal"></a><span data-ttu-id="d41ca-190">Successfully call the API from the developer portal</span><span class="sxs-lookup"><span data-stu-id="d41ca-190">Successfully call the API from the developer portal</span></span>

<span data-ttu-id="d41ca-191">Now that the OAuth 2.0 user authorization is enabled on the `Echo API`, the Developer Console obtains an access token on behalf of the user, before calling the API.</span><span class="sxs-lookup"><span data-stu-id="d41ca-191">Now that the OAuth 2.0 user authorization is enabled on the `Echo API`, the Developer Console obtains an access token on behalf of the user, before calling the API.</span></span>

1. <span data-ttu-id="d41ca-192">Browse to any operation under the `Echo API` in the developer portal, and select **Try it**.</span><span class="sxs-lookup"><span data-stu-id="d41ca-192">Browse to any operation under the `Echo API` in the developer portal, and select **Try it**.</span></span> <span data-ttu-id="d41ca-193">This brings you to the Developer Console.</span><span class="sxs-lookup"><span data-stu-id="d41ca-193">This brings you to the Developer Console.</span></span>

2. <span data-ttu-id="d41ca-194">Note a new item in the **Authorization** section, corresponding to the authorization server you just added.</span><span class="sxs-lookup"><span data-stu-id="d41ca-194">Note a new item in the **Authorization** section, corresponding to the authorization server you just added.</span></span>

3. <span data-ttu-id="d41ca-195">Select **Authorization code** from the authorization drop-down list, and you are prompted to sign in to the Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="d41ca-195">Select **Authorization code** from the authorization drop-down list, and you are prompted to sign in to the Azure AD tenant.</span></span> <span data-ttu-id="d41ca-196">If you are already signed in with the account, you might not be prompted.</span><span class="sxs-lookup"><span data-stu-id="d41ca-196">If you are already signed in with the account, you might not be prompted.</span></span>

4. <span data-ttu-id="d41ca-197">After successful sign-in, an `Authorization` header is added to the request, with an access token from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d41ca-197">After successful sign-in, an `Authorization` header is added to the request, with an access token from Azure AD.</span></span> <span data-ttu-id="d41ca-198">The following is a sample token (Base64 encoded):</span><span class="sxs-lookup"><span data-stu-id="d41ca-198">The following is a sample token (Base64 encoded):</span></span>

   ```
   Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6IlNTUWRoSTFjS3ZoUUVEU0p4RTJnR1lzNDBRMCIsImtpZCI6IlNTUWRoSTFjS3ZoUUVEU0p4RTJnR1lzNDBRMCJ9.eyJhdWQiOiIxYzg2ZWVmNC1jMjZkLTRiNGUtODEzNy0wYjBiZTEyM2NhMGMiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC80NDc4ODkyMC05Yjk3LTRmOGItODIwYS0yMTFiMTMzZDk1MzgvIiwiaWF0IjoxNTIxMTUyNjMzLCJuYmYiOjE1MjExNTI2MzMsImV4cCI6MTUyMTE1NjUzMywiYWNyIjoiMSIsImFpbyI6IkFWUUFxLzhHQUFBQUptVzkzTFd6dVArcGF4ZzJPeGE1cGp2V1NXV1ZSVnd1ZXZ5QU5yMlNkc0tkQmFWNnNjcHZsbUpmT1dDOThscUJJMDhXdlB6cDdlenpJdzJLai9MdWdXWWdydHhkM1lmaDlYSGpXeFVaWk9JPSIsImFtciI6WyJyc2EiXSwiYXBwaWQiOiJhYTY5ODM1OC0yMWEzLTRhYTQtYjI3OC1mMzI2NTMzMDUzZTkiLCJhcHBpZGFjciI6IjEiLCJlbWFpbCI6Im1pamlhbmdAbWljcm9zb2Z0LmNvbSIsImZhbWlseV9uYW1lIjoiSmlhbmciLCJnaXZlbl9uYW1lIjoiTWlhbyIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI0Ny8iLCJpcGFkZHIiOiIxMzEuMTA3LjE3NC4xNDAiLCJuYW1lIjoiTWlhbyBKaWFuZyIsIm9pZCI6IjhiMTU4ZDEwLWVmZGItNDUxMS1iOTQzLTczOWZkYjMxNzAyZSIsInNjcCI6InVzZXJfaW1wZXJzb25hdGlvbiIsInN1YiI6IkFGaWtvWFk1TEV1LTNkbk1pa3Z3MUJzQUx4SGIybV9IaVJjaHVfSEM1aGciLCJ0aWQiOiI0NDc4ODkyMC05Yjk3LTRmOGItODIwYS0yMTFiMTMzZDk1MzgiLCJ1bmlxdWVfbmFtZSI6Im1pamlhbmdAbWljcm9zb2Z0LmNvbSIsInV0aSI6ImFQaTJxOVZ6ODBXdHNsYjRBMzBCQUEiLCJ2ZXIiOiIxLjAifQ.agGfaegYRnGj6DM_-N_eYulnQdXHhrsus45QDuApirETDR2P2aMRxRioOCR2YVwn8pmpQ1LoAhddcYMWisrw_qhaQr0AYsDPWRtJ6x0hDk5teUgbix3gazb7F-TVcC1gXpc9y7j77Ujxcq9z0r5lF65Y9bpNSefn9Te6GZYG7BgKEixqC4W6LqjtcjuOuW-ouy6LSSox71Fj4Ni3zkGfxX1T_jiOvQTd6BBltSrShDm0bTMefoyX8oqfMEA2ziKjwvBFrOjO0uK4rJLgLYH4qvkR0bdF9etdstqKMo5gecarWHNzWi_tghQu9aE3Z3EZdYNI_ZGM-Bbe3pkCfvEOyA
   ```

5. <span data-ttu-id="d41ca-199">Select **Send**, and you can call the API successfully.</span><span class="sxs-lookup"><span data-stu-id="d41ca-199">Select **Send**, and you can call the API successfully.</span></span>


## <a name="configure-a-jwt-validation-policy-to-pre-authorize-requests"></a><span data-ttu-id="d41ca-200">Configure a JWT validation policy to pre-authorize requests</span><span class="sxs-lookup"><span data-stu-id="d41ca-200">Configure a JWT validation policy to pre-authorize requests</span></span>

<span data-ttu-id="d41ca-201">At this point, when a user tries to make a call from the Developer Console, the user is prompted to sign in.</span><span class="sxs-lookup"><span data-stu-id="d41ca-201">At this point, when a user tries to make a call from the Developer Console, the user is prompted to sign in.</span></span> <span data-ttu-id="d41ca-202">The Developer Console obtains an access token on behalf of the user.</span><span class="sxs-lookup"><span data-stu-id="d41ca-202">The Developer Console obtains an access token on behalf of the user.</span></span>

<span data-ttu-id="d41ca-203">But what if someone calls your API without a token or with an invalid token?</span><span class="sxs-lookup"><span data-stu-id="d41ca-203">But what if someone calls your API without a token or with an invalid token?</span></span> <span data-ttu-id="d41ca-204">For example, you can still call the API even if you delete the `Authorization` header.</span><span class="sxs-lookup"><span data-stu-id="d41ca-204">For example, you can still call the API even if you delete the `Authorization` header.</span></span> <span data-ttu-id="d41ca-205">The reason is that API Management does not validate the access token at this point.</span><span class="sxs-lookup"><span data-stu-id="d41ca-205">The reason is that API Management does not validate the access token at this point.</span></span> <span data-ttu-id="d41ca-206">It simply passes the `Authorization` header to the back-end API.</span><span class="sxs-lookup"><span data-stu-id="d41ca-206">It simply passes the `Authorization` header to the back-end API.</span></span>

<span data-ttu-id="d41ca-207">You can use the [Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) policy to pre-authorize requests in API Management, by validating the access tokens of each incoming request.</span><span class="sxs-lookup"><span data-stu-id="d41ca-207">You can use the [Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) policy to pre-authorize requests in API Management, by validating the access tokens of each incoming request.</span></span> <span data-ttu-id="d41ca-208">If a request does not have a valid token, API Management blocks it.</span><span class="sxs-lookup"><span data-stu-id="d41ca-208">If a request does not have a valid token, API Management blocks it.</span></span> <span data-ttu-id="d41ca-209">For example, you can add the following policy to the `<inbound>` policy section of the `Echo API`.</span><span class="sxs-lookup"><span data-stu-id="d41ca-209">For example, you can add the following policy to the `<inbound>` policy section of the `Echo API`.</span></span> <span data-ttu-id="d41ca-210">It checks the audience claim in an access token, and returns an error message if the token is not valid.</span><span class="sxs-lookup"><span data-stu-id="d41ca-210">It checks the audience claim in an access token, and returns an error message if the token is not valid.</span></span> <span data-ttu-id="d41ca-211">For information on how to configure policies, see [Set or edit policies](set-edit-policies.md).</span><span class="sxs-lookup"><span data-stu-id="d41ca-211">For information on how to configure policies, see [Set or edit policies](set-edit-policies.md).</span></span>

```xml
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">
    <openid-config url="https://login.microsoftonline.com/{aad-tenant}/.well-known/openid-configuration" />
    <required-claims>
        <claim name="aud">
            <value>{Application ID of backend-app}</value>
        </claim>
    </required-claims>
</validate-jwt>
```

## <a name="build-an-application-to-call-the-api"></a><span data-ttu-id="d41ca-212">Build an application to call the API</span><span class="sxs-lookup"><span data-stu-id="d41ca-212">Build an application to call the API</span></span>

<span data-ttu-id="d41ca-213">In this guide, you used the Developer Console in API Management as the sample client application to call the `Echo API` protected by OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="d41ca-213">In this guide, you used the Developer Console in API Management as the sample client application to call the `Echo API` protected by OAuth 2.0.</span></span> <span data-ttu-id="d41ca-214">To learn more about how to build an application and implement OAuth 2.0, see [Azure Active Directory code samples](../active-directory/develop/sample-v1-code.md).</span><span class="sxs-lookup"><span data-stu-id="d41ca-214">To learn more about how to build an application and implement OAuth 2.0, see [Azure Active Directory code samples](../active-directory/develop/sample-v1-code.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d41ca-215">Next steps</span><span class="sxs-lookup"><span data-stu-id="d41ca-215">Next steps</span></span>
* <span data-ttu-id="d41ca-216">Learn more about [Azure Active Directory and OAuth2.0](../active-directory/develop/authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="d41ca-216">Learn more about [Azure Active Directory and OAuth2.0](../active-directory/develop/authentication-scenarios.md).</span></span>
* <span data-ttu-id="d41ca-217">Check out more [videos](https://azure.microsoft.com/documentation/videos/index/?services=api-management) about API Management.</span><span class="sxs-lookup"><span data-stu-id="d41ca-217">Check out more [videos](https://azure.microsoft.com/documentation/videos/index/?services=api-management) about API Management.</span></span>
* <span data-ttu-id="d41ca-218">For other ways to secure your back-end service, see [Mutual Certificate authentication](api-management-howto-mutual-certificates.md).</span><span class="sxs-lookup"><span data-stu-id="d41ca-218">For other ways to secure your back-end service, see [Mutual Certificate authentication](api-management-howto-mutual-certificates.md).</span></span>

* <span data-ttu-id="d41ca-219">[Create an API Management service instance](get-started-create-service-instance.md).</span><span class="sxs-lookup"><span data-stu-id="d41ca-219">[Create an API Management service instance](get-started-create-service-instance.md).</span></span>

* <span data-ttu-id="d41ca-220">[Manage your first API](import-and-publish.md).</span><span class="sxs-lookup"><span data-stu-id="d41ca-220">[Manage your first API](import-and-publish.md).</span></span>
