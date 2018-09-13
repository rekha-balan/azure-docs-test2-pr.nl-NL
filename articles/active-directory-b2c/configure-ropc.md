---
title: Configure the resource owner password credentials flow in Azure Active Directory B2C | Microsoft Docs
description: Learn how to configure the resource owner password credentials flow in Azure AD B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 08/07/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 519f13d668f09fb2d83e8f64767e195e2544fc1e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857447"
---
# <a name="configure-the-resource-owner-password-credentials-flow-in-azure-ad-b2c"></a><span data-ttu-id="2decb-103">Configure the resource owner password credentials flow in Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="2decb-103">Configure the resource owner password credentials flow in Azure AD B2C</span></span>

<span data-ttu-id="2decb-104">The resource owner password credentials (ROPC) flow is an OAuth standard authentication flow where the application, also known as the relying party, exchanges valid credentials such as userid and password for an ID token, access token, and a refresh token.</span><span class="sxs-lookup"><span data-stu-id="2decb-104">The resource owner password credentials (ROPC) flow is an OAuth standard authentication flow where the application, also known as the relying party, exchanges valid credentials such as userid and password for an ID token, access token, and a refresh token.</span></span> 

> [!NOTE]
> <span data-ttu-id="2decb-105">This feature is in preview.</span><span class="sxs-lookup"><span data-stu-id="2decb-105">This feature is in preview.</span></span>

<span data-ttu-id="2decb-106">In Azure Active Directory (Azure AD) B2C, the following options are supported:</span><span class="sxs-lookup"><span data-stu-id="2decb-106">In Azure Active Directory (Azure AD) B2C, the following options are supported:</span></span>

- <span data-ttu-id="2decb-107">**Native Client**: User interaction during authentication happens when code runs on a user-side device.</span><span class="sxs-lookup"><span data-stu-id="2decb-107">**Native Client**: User interaction during authentication happens when code runs on a user-side device.</span></span> <span data-ttu-id="2decb-108">The device can be a mobile application that's running in a native operating system, such as Android, or running in a browser, such as JavaScript.</span><span class="sxs-lookup"><span data-stu-id="2decb-108">The device can be a mobile application that's running in a native operating system, such as Android, or running in a browser, such as JavaScript.</span></span>
- <span data-ttu-id="2decb-109">**Public client flow**: Only user credentials, gathered by an application, are sent in the API call.</span><span class="sxs-lookup"><span data-stu-id="2decb-109">**Public client flow**: Only user credentials, gathered by an application, are sent in the API call.</span></span> <span data-ttu-id="2decb-110">The credentials of the application are not sent.</span><span class="sxs-lookup"><span data-stu-id="2decb-110">The credentials of the application are not sent.</span></span>
- <span data-ttu-id="2decb-111">**Add new claims**: The ID token contents can be changed to add new claims.</span><span class="sxs-lookup"><span data-stu-id="2decb-111">**Add new claims**: The ID token contents can be changed to add new claims.</span></span> 

<span data-ttu-id="2decb-112">The following flows are not supported:</span><span class="sxs-lookup"><span data-stu-id="2decb-112">The following flows are not supported:</span></span>

- <span data-ttu-id="2decb-113">**Server-to-server**: The identity protection system needs a reliable IP address gathered from the caller (the native client) as part of the interaction.</span><span class="sxs-lookup"><span data-stu-id="2decb-113">**Server-to-server**: The identity protection system needs a reliable IP address gathered from the caller (the native client) as part of the interaction.</span></span> <span data-ttu-id="2decb-114">In a server-side API call, only the server’s IP address is used.</span><span class="sxs-lookup"><span data-stu-id="2decb-114">In a server-side API call, only the server’s IP address is used.</span></span> <span data-ttu-id="2decb-115">If a dynamic threshold of failed authentications is exceeded, the identity protection system may identify a repeated IP address as an attacker.</span><span class="sxs-lookup"><span data-stu-id="2decb-115">If a dynamic threshold of failed authentications is exceeded, the identity protection system may identify a repeated IP address as an attacker.</span></span>
- <span data-ttu-id="2decb-116">**Confidential client flow**: The application client ID is validated, but the application secret is not validated.</span><span class="sxs-lookup"><span data-stu-id="2decb-116">**Confidential client flow**: The application client ID is validated, but the application secret is not validated.</span></span>

##  <a name="create-a-resource-owner-policy"></a><span data-ttu-id="2decb-117">Create a resource owner policy</span><span class="sxs-lookup"><span data-stu-id="2decb-117">Create a resource owner policy</span></span>

1. <span data-ttu-id="2decb-118">Sign in to the Azure portal as the global administrator of your Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="2decb-118">Sign in to the Azure portal as the global administrator of your Azure AD B2C tenant.</span></span>
2. <span data-ttu-id="2decb-119">To switch to your Azure AD B2C tenant, select the B2C directory in the upper-right corner of the portal.</span><span class="sxs-lookup"><span data-stu-id="2decb-119">To switch to your Azure AD B2C tenant, select the B2C directory in the upper-right corner of the portal.</span></span>
3. <span data-ttu-id="2decb-120">Under **Policies**, select **Resource Owner policies**.</span><span class="sxs-lookup"><span data-stu-id="2decb-120">Under **Policies**, select **Resource Owner policies**.</span></span>
4. <span data-ttu-id="2decb-121">Provide a name for the policy, such as *ROPC_Auth*, and then select **Application claims**.</span><span class="sxs-lookup"><span data-stu-id="2decb-121">Provide a name for the policy, such as *ROPC_Auth*, and then select **Application claims**.</span></span>
5. <span data-ttu-id="2decb-122">Select the application claims that you need for your application, such as *Display Name*, *Email Address*, and *Identity Provider*.</span><span class="sxs-lookup"><span data-stu-id="2decb-122">Select the application claims that you need for your application, such as *Display Name*, *Email Address*, and *Identity Provider*.</span></span>
6. <span data-ttu-id="2decb-123">Select **OK**, and then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="2decb-123">Select **OK**, and then select **Create**.</span></span>

   <span data-ttu-id="2decb-124">You'll then see an endpoint such as this example:</span><span class="sxs-lookup"><span data-stu-id="2decb-124">You'll then see an endpoint such as this example:</span></span>

   `https://yourtenant.b2clogin.com/yourtenant.onmicrosoft.com/v2.0/.well-known/openid-configuration?p=B2C_1_ROPC_Auth`


## <a name="register-an-application"></a><span data-ttu-id="2decb-125">Register an application</span><span class="sxs-lookup"><span data-stu-id="2decb-125">Register an application</span></span>

1. <span data-ttu-id="2decb-126">In the B2C settings, select **Applications**, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="2decb-126">In the B2C settings, select **Applications**, and then select **Add**.</span></span>
2. <span data-ttu-id="2decb-127">Enter a name for the application, such as *ROPC_Auth_app*.</span><span class="sxs-lookup"><span data-stu-id="2decb-127">Enter a name for the application, such as *ROPC_Auth_app*.</span></span>
3. <span data-ttu-id="2decb-128">Select **No** for **Web App/Web API**, and then select **Yes** for **Native client**.</span><span class="sxs-lookup"><span data-stu-id="2decb-128">Select **No** for **Web App/Web API**, and then select **Yes** for **Native client**.</span></span>
4. <span data-ttu-id="2decb-129">Leave all other values as they are, and then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="2decb-129">Leave all other values as they are, and then select **Create**.</span></span>
5. <span data-ttu-id="2decb-130">Select the new application, and note the Application ID for later use.</span><span class="sxs-lookup"><span data-stu-id="2decb-130">Select the new application, and note the Application ID for later use.</span></span>

## <a name="test-the-policy"></a><span data-ttu-id="2decb-131">Test the policy</span><span class="sxs-lookup"><span data-stu-id="2decb-131">Test the policy</span></span>

<span data-ttu-id="2decb-132">Use your favorite API development application to generate an API call, and review the response to debug your policy.</span><span class="sxs-lookup"><span data-stu-id="2decb-132">Use your favorite API development application to generate an API call, and review the response to debug your policy.</span></span> <span data-ttu-id="2decb-133">Construct a call like this with the information in the following table as the body of the POST request:</span><span class="sxs-lookup"><span data-stu-id="2decb-133">Construct a call like this with the information in the following table as the body of the POST request:</span></span>
- <span data-ttu-id="2decb-134">Replace *\<yourtenant.onmicrosoft.com>* with the name of your B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="2decb-134">Replace *\<yourtenant.onmicrosoft.com>* with the name of your B2C tenant.</span></span>
- <span data-ttu-id="2decb-135">Replace *\<B2C_1A_ROPC_Auth>* with the full name of your resource owner password credentials policy.</span><span class="sxs-lookup"><span data-stu-id="2decb-135">Replace *\<B2C_1A_ROPC_Auth>* with the full name of your resource owner password credentials policy.</span></span>
- <span data-ttu-id="2decb-136">Replace *\<bef2222d56-552f-4a5b-b90a-1988a7d634c3>* with the Application ID from your registration.</span><span class="sxs-lookup"><span data-stu-id="2decb-136">Replace *\<bef2222d56-552f-4a5b-b90a-1988a7d634c3>* with the Application ID from your registration.</span></span>

`https://yourtenant.b2clogin.com/<yourtenant.onmicrosoft.com>/oauth2/v2.0/token?p=B2C_1_ROPC_Auth`

| <span data-ttu-id="2decb-137">Key</span><span class="sxs-lookup"><span data-stu-id="2decb-137">Key</span></span> | <span data-ttu-id="2decb-138">Value</span><span class="sxs-lookup"><span data-stu-id="2decb-138">Value</span></span> |
| --- | ----- |
| <span data-ttu-id="2decb-139">username</span><span class="sxs-lookup"><span data-stu-id="2decb-139">username</span></span> | leadiocl@outlook.com |
| <span data-ttu-id="2decb-140">password</span><span class="sxs-lookup"><span data-stu-id="2decb-140">password</span></span> | <span data-ttu-id="2decb-141">Passxword1</span><span class="sxs-lookup"><span data-stu-id="2decb-141">Passxword1</span></span> |
| <span data-ttu-id="2decb-142">grant_type</span><span class="sxs-lookup"><span data-stu-id="2decb-142">grant_type</span></span> | <span data-ttu-id="2decb-143">password</span><span class="sxs-lookup"><span data-stu-id="2decb-143">password</span></span> |
| <span data-ttu-id="2decb-144">scope</span><span class="sxs-lookup"><span data-stu-id="2decb-144">scope</span></span> | <span data-ttu-id="2decb-145">openid \<bef2222d56-552f-4a5b-b90a-1988a7d634c3> offline_access</span><span class="sxs-lookup"><span data-stu-id="2decb-145">openid \<bef2222d56-552f-4a5b-b90a-1988a7d634c3> offline_access</span></span> |
| <span data-ttu-id="2decb-146">client_id</span><span class="sxs-lookup"><span data-stu-id="2decb-146">client_id</span></span> | <span data-ttu-id="2decb-147">\<bef2222d56-552f-4a5b-b90a-1988a7d634c3></span><span class="sxs-lookup"><span data-stu-id="2decb-147">\<bef2222d56-552f-4a5b-b90a-1988a7d634c3></span></span> |
| <span data-ttu-id="2decb-148">response_type</span><span class="sxs-lookup"><span data-stu-id="2decb-148">response_type</span></span> | <span data-ttu-id="2decb-149">token id_token</span><span class="sxs-lookup"><span data-stu-id="2decb-149">token id_token</span></span> |

<span data-ttu-id="2decb-150">*Client_id* is the value that you previously noted as the application ID.</span><span class="sxs-lookup"><span data-stu-id="2decb-150">*Client_id* is the value that you previously noted as the application ID.</span></span> <span data-ttu-id="2decb-151">*Offline_access* is optional if you want to receive a refresh token.</span><span class="sxs-lookup"><span data-stu-id="2decb-151">*Offline_access* is optional if you want to receive a refresh token.</span></span> <span data-ttu-id="2decb-152">The username and password that you use must be credentials from an existing user in your Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="2decb-152">The username and password that you use must be credentials from an existing user in your Azure AD B2C tenant.</span></span>

<span data-ttu-id="2decb-153">The actual POST request looks like the following:</span><span class="sxs-lookup"><span data-stu-id="2decb-153">The actual POST request looks like the following:</span></span>

```
POST /yourtenant.onmicrosoft.com/oauth2/v2.0/token?B2C_1_ROPC_Auth HTTP/1.1
Host: yourtenant.b2clogin.com
Content-Type: application/x-www-form-urlencoded

username=leadiocl%40trashmail.ws&password=Passxword1&grant_type=password&scope=openid+bef22d56-552f-4a5b-b90a-1988a7d634ce+offline_access&client_id=bef22d56-552f-4a5b-b90a-1988a7d634ce&response_type=token+id_token
```


<span data-ttu-id="2decb-154">A successful response with offline-access looks like the following example:</span><span class="sxs-lookup"><span data-stu-id="2decb-154">A successful response with offline-access looks like the following example:</span></span>

```
{ 
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6Ik9YQjNhdTNScWhUQWN6R0RWZDM5djNpTmlyTWhqN2wxMjIySnh6TmgwRlkifQ.eyJpc3MiOiJodHRwczovL3RlLmNwaW0ud2luZG93cy5uZXQvZjA2YzJmZTgtNzA5Zi00MDMwLTg1ZGMtMzhhNGJmZDllODJkL3YyLjAvIiwiZXhwIjoxNTEzMTMwMDc4LCJuYmYiOjE1MTMxMjY0NzgsImF1ZCI6ImJlZjIyZDU2LTU1MmYtNGE1Yi1iOTBhLTE5ODhhN2Q2MzRjZSIsIm9pZCI6IjNjM2I5NjljLThjNDktNGUxMS1hNGVmLWZkYjJmMzkyZjA0OSIsInN1YiI6Ik5vdCBzdXBwb3J0ZWQgY3VycmVudGx5LiBVc2Ugb2lkIGNsYWltLiIsImF6cCI6ImJlZjIyZDU2LTU1MmYtNGE1Yi1iOTBhLTE5ODhhN2Q2MzRjZSIsInZlciI6IjEuMCIsImlhdCI6MTUxMzEyNjQ3OH0.MSEThYZxCS4SevBw3-3ecnVLUkucFkehH-gH-P7SFcJ-MhsBeQEpMF1Rzu_R9kUqV3qEWKAPYCNdZ3_P4Dd3a63iG6m9TnO1Vt5SKTETuhVx3Xl5LYeA1i3Slt9Y7LIicn59hGKRZ8ddrQzkqj69j723ooy01amrXvF6zNOudh0acseszt7fbzzofyagKPerxaeTH0NgyOinLwXu0eNj_6RtF9gBfgwVidRy9OzXUJnqm1GdrS61XUqiIUtv4H04jYxDem7ek6E4jsH809uSXT0iD5_4C5bDHrpO1N6pXSasmVR9GM1XgfXA_IRLFU4Nd26CzGl1NjbhLnvli2qY4A", 
    "token_type": "Bearer", 
    "expires_in": "3600", 
    "refresh_token": "eyJraWQiOiJacW9pQlp2TW5pYVc2MUY0TnlfR3REVk1EVFBLbUJLb0FUcWQ1ZWFja1hBIiwidmVyIjoiMS4wIiwiemlwIjoiRGVmbGF0ZSIsInNlciI6IjEuMCJ9.aJ_2UW14dh4saWTQ0jLJ7ByQs5JzIeW_AU9Q_RVFgrrnYiPhikEc68ilvWWo8B20KTRB_s7oy_Eoh5LACsqU6Oz0Mjnh0-DxgrMblUOTAQ9dbfAT5WoLZiCBJIz4YT5OUA_RAGjhBUkqGwdWEumDExQnXIjRSeaUBmWCQHPPguV1_5wSj8aW2zIzYIMbofvpjwIATlbIZwJ7ufnLypRuq_MDbZhJkegDw10KI4MHJlJ40Ip8mCOe0XeJIDpfefiJ6WQpUq4zl06NO7j8kvDoVq9WALJIao7LYk_x9UIT-3d0W0eDBHGSRcNgtMYpymaN9ltx6djcEesXNn4CFnWG3g.y6KKeA9EcsW9zW-g.TrTSgn4WBt18gezegxihBla9SLSTC3YfDROQsL9K4yX4400FKlTlf-2l9CnpGTEdWXVi7sIMHCl8S4oUiXd-rvY2mn_NfDrbbVJfgKp1j7Nnq9FFyeJEFcP_FtUXgsNTG9iwfzWox04B1d845qNRWiS9N8BhAAAIdz5N0ChHuOxsVOC0Y_Ly3DNe-JQyXcq964M6-jp3cgi4UqMxT837L6pLY5Ih_iPsSfyHzstsFeqyUIktnzt1MpTlyW-_GDyFK1S-SyV8PPQ7phgFouw2jho1iboHX70RlDGYyVmP1CfQzKE_zWxj3rgaCZvYMWN8fUenoiatzhvWkUM7dhqKGjofPeL8rOMkhl6afLLjObzhUg3PZFcMR6guLjQdEwQFufWxGjfpvaHycZSKeWu6-7dF8Hy_nyMLLdBpUkdrXPob_5gRiaH72KvncSIFvJLqhY3NgXO05Fy87PORjggXwYkhWh4FgQZBIYD6h0CSk2nfFjR9uD9EKiBBWSBZj814S_Jdw6HESFtn91thpvU3hi3qNOi1m41gg1vt5Kh35A5AyDY1J7a9i_lN4B7e_pknXlVX6Z-Z2BYZvwAU7KLKsy5a99p9FX0lg6QweDzhukXrB4wgfKvVRTo.mjk92wMk-zUSrzuuuXPVeg", 
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6Ik9YQjNhdTNScWhUQWN6R0RWZDM5djNpTmlyTWhqN2wxMjIySnh6TmgwRlkifQ.eyJleHAiOjE1MTMxMzAwNzgsIm5iZiI6MTUxMzEyNjQ3OCwidmVyIjoiMS4wIiwiaXNzIjoiaHR0cHM6Ly90ZS5jcGltLndpbmRvd3MubmV0L2YwNmMyZmU4LTcwOWYtNDAzMC04NWRjLTM4YTRiZmQ5ZTgyZC92Mi4wLyIsInN1YiI6Ik5vdCBzdXBwb3J0ZWQgY3VycmVudGx5LiBVc2Ugb2lkIGNsYWltLiIsImF1ZCI6ImJlZjIyZDU2LTU1MmYtNGE1Yi1iOTBhLTE5ODhhN2Q2MzRjZSIsImFjciI6ImIyY18xYV9yZXNvdXJjZW93bmVydjIiLCJpYXQiOjE1MTMxMjY0NzgsImF1dGhfdGltZSI6MTUxMzEyNjQ3OCwib2lkIjoiM2MzYjk2OWMtOGM0OS00ZTExLWE0ZWYtZmRiMmYzOTJmMDQ5IiwiYXRfaGFzaCI6Ikd6QUNCTVJtcklwYm9OdkFtNHhMWEEifQ.iAJg13cgySsdH3cmoEPGZB_g-4O8KWvGr6W5VzRXtkrlLoKB1pl4hL6f_0xOrxnQwj2sUgW-wjsCVzMc_dkHSwd9QFZ4EYJEJbi1LMGk2lW-PgjsbwHPDU1mz-SR1PeqqJgvOqrzXo0YHXr-e07M4v4Tko-i_OYcrdJzj4Bkv7ZZilsSj62lNig4HkxTIWi5Ec2gD79bPKzgCtIww1KRnwmrlnCOrMFYNj-0T3lTDcXAQog63MOacf7OuRVUC5k_IdseigeMSscrYrNrH28s3r0JoqDhNUTewuw1jx0X6gdqQWZKOLJ7OF_EJMP-BkRTixBGK5eW2YeUUEVQxsFlUg" 
} 
```

## <a name="redeem-a-refresh-token"></a><span data-ttu-id="2decb-155">Redeem a refresh token</span><span class="sxs-lookup"><span data-stu-id="2decb-155">Redeem a refresh token</span></span>

<span data-ttu-id="2decb-156">Construct a POST call like the one shown here with the information in the following table as the body of the request:</span><span class="sxs-lookup"><span data-stu-id="2decb-156">Construct a POST call like the one shown here with the information in the following table as the body of the request:</span></span>

`https://yourtenant.b2clogin.com/<yourtenant.onmicrosoft.com>/oauth2/v2.0/token?p=B2C_1_ROPC_Auth`

| <span data-ttu-id="2decb-157">Key</span><span class="sxs-lookup"><span data-stu-id="2decb-157">Key</span></span> | <span data-ttu-id="2decb-158">Value</span><span class="sxs-lookup"><span data-stu-id="2decb-158">Value</span></span> |
| --- | ----- |
| <span data-ttu-id="2decb-159">grant_type</span><span class="sxs-lookup"><span data-stu-id="2decb-159">grant_type</span></span> | <span data-ttu-id="2decb-160">refresh_token</span><span class="sxs-lookup"><span data-stu-id="2decb-160">refresh_token</span></span> |
| <span data-ttu-id="2decb-161">response_type</span><span class="sxs-lookup"><span data-stu-id="2decb-161">response_type</span></span> | <span data-ttu-id="2decb-162">id_token</span><span class="sxs-lookup"><span data-stu-id="2decb-162">id_token</span></span> |
| <span data-ttu-id="2decb-163">client_id</span><span class="sxs-lookup"><span data-stu-id="2decb-163">client_id</span></span> | <span data-ttu-id="2decb-164">\<bef2222d56-552f-4a5b-b90a-1988a7d634c3></span><span class="sxs-lookup"><span data-stu-id="2decb-164">\<bef2222d56-552f-4a5b-b90a-1988a7d634c3></span></span> |
| <span data-ttu-id="2decb-165">resource</span><span class="sxs-lookup"><span data-stu-id="2decb-165">resource</span></span> | <span data-ttu-id="2decb-166">\<bef2222d56-552f-4a5b-b90a-1988a7d634c3></span><span class="sxs-lookup"><span data-stu-id="2decb-166">\<bef2222d56-552f-4a5b-b90a-1988a7d634c3></span></span> |
| <span data-ttu-id="2decb-167">refresh_token</span><span class="sxs-lookup"><span data-stu-id="2decb-167">refresh_token</span></span> | <span data-ttu-id="2decb-168">eyJraWQiOiJacW9pQlp2TW5pYVc2MUY0TnlfR3...</span><span class="sxs-lookup"><span data-stu-id="2decb-168">eyJraWQiOiJacW9pQlp2TW5pYVc2MUY0TnlfR3...</span></span> |

<span data-ttu-id="2decb-169">*Client_id* and *resource* are the values that you previously noted as the application ID.</span><span class="sxs-lookup"><span data-stu-id="2decb-169">*Client_id* and *resource* are the values that you previously noted as the application ID.</span></span> <span data-ttu-id="2decb-170">*Refresh_token* is the token that you received in the authentication call mentioned previously.</span><span class="sxs-lookup"><span data-stu-id="2decb-170">*Refresh_token* is the token that you received in the authentication call mentioned previously.</span></span>

<span data-ttu-id="2decb-171">A successful response looks like the following example:</span><span class="sxs-lookup"><span data-stu-id="2decb-171">A successful response looks like the following example:</span></span>

```
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6Ilg1ZVhrNHh5b2pORnVtMWtsMll0djhkbE5QNC1jNTdkTzZRR1RWQndhTmsifQ.eyJpc3MiOiJodHRwczovL2xvZ2luLm1pY3Jvc29mdG9ubGluZS5jb20vNTE2ZmMwNjUtZmYzNi00YjkzLWFhNWEtZDZlZWRhN2NiYWM4L3YyLjAvIiwiZXhwIjoxNTMzNjc2NTkwLCJuYmYiOjE1MzM2NzI5OTAsImF1ZCI6IjljNTA2MThjLWY5NTEtNDlhNS1iZmU1LWQ3ODA4NTEyMWMzYSIsImlkcCI6IkxvY2FsQWNjb3VudCIsInN1YiI6ImJmZDgwODBjLTBjNDAtNDNjYS05ZTI3LTUyZTAyNzIyNWYyMSIsIm5hbWUiOiJEYXZpZE11IiwiZW1haWxzIjpbImRhdmlkd20xMDMwQGhvdG1haWwuY29tIl0sInRmcCI6IkIyQ18xX1JPUENfQXV0aCIsImF6cCI6IjljNTA2MThjLWY5NTEtNDlhNS1iZmU1LWQ3ODA4NTEyMWMzYSIsInZlciI6IjEuMCIsImlhdCI6MTUzMzY3Mjk5MH0.RULWeBR8--s5cCGG6XOi8m-AGyCaASx9W5B3tNUQjbVkHnGdo2_OUrnVoOZ1PTcrc1b0PQM2kVWi7NpYn57ifnqL_feTJPDbj9FJ8BmyxULdoECWxSM6KHsOPWZOIg5y1lNwN_IQ2HNF6UaDyYf1ZIM-jHr-uSfUnQXyWRnGDwNKX7TQbFmFk4oFMbPxTE7ioWAmxSnroiiB4__P9D0rUM1vf_qfzemf2ErIWSF9rGtCNBG-BvJlr3ZMCxIhRiIWNM2bVY0i3Nprzj0V8_FM6q8U19bvg9yDEzUcbe_1PMqzP3IrXW9N1XvQHupsOj8Keb7SmpgY1GG091X6wBCypw",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6Ilg1ZVhrNHh5b2pORnVtMWtsMll0djhkbE5QNC1jNTdkTzZRR1RWQndhTmsifQ.eyJleHAiOjE1MzM2NzY1OTAsIm5iZiI6MTUzMzY3Mjk5MCwidmVyIjoiMS4wIiwiaXNzIjoiaHR0cHM6Ly9sb2dpbi5taWNyb3NvZnRvbmxpbmUuY29tLzUxNmZjMDY1LWZmMzYtNGI5My1hYTVhLWQ2ZWVkYTdjYmFjOC92Mi4wLyIsInN1YiI6ImJmZDgwODBjLTBjNDAtNDNjYS05ZTI3LTUyZTAyNzIyNWYyMSIsImF1ZCI6IjljNTA2MThjLWY5NTEtNDlhNS1iZmU1LWQ3ODA4NTEyMWMzYSIsImlhdCI6MTUzMzY3Mjk5MCwiYXV0aF90aW1lIjoxNTMzNjcyOTkwLCJpZHAiOiJMb2NhbEFjY291bnQiLCJuYW1lIjoiRGF2aWRNdSIsImVtYWlscyI6WyJkYXZpZHdtMTAzMEBob3RtYWlsLmNvbSJdLCJ0ZnAiOiJCMkNfMV9ST1BDX0F1dGgiLCJhdF9oYXNoIjoiYW5hZ3QtX1NveUtBQV9UNFBLaHN4dyJ9.bPzpUFh94XFHXC_yR6qH_Unf6_hN-9-BjDXOzrdb1AuoU6-owQ3fWDxNBUbYEPALid3sgm4qhJ6BROFKryD8aWfrNyaErnYZwZ6rliHk4foa3JsbDgM3yNGPL0hzOFpC4Y9QhUjNgQOxvnQLtqbHVNonSvBc7VVPAjBDza44GowmvLORfJ1qkTjdrFM75HlLVeQch8cUNf-Ova77JdG5WHgYgqRhAq1OhV68YgEpQkARyz77zbAz9zZEHZZlgsli8UV6C-CPcmoHbwS-85mLzF9nLxhzjgIXJwckB6I7lvTpfuRtaqZIb3pMYeHZJaxaNLDvq9Qe4N-danXABg1B2w",
    "token_type": "Bearer",
    "not_before": 1533672990,
    "expires_in": 3600,
    "expires_on": 1533676590,
    "resource": "bef2222d56-552f-4a5b-b90a-1988a7d634c3",
    "id_token_expires_in": 3600,
    "profile_info": "eyJ2ZXIiOiIxLjAiLCJ0aWQiOiI1MTZmYzA2NS1mZjM2LTRiOTMtYWE1YS1kNmVlZGE3Y2JhYzgiLCJzdWIiOm51bGwsIm5hbWUiOiJEYXZpZE11IiwicHJlZmVycmVkX3VzZXJuYW1lIjpudWxsLCJpZHAiOiJMb2NhbEFjY291bnQifQ",
    "refresh_token": "eyJraWQiOiJjcGltY29yZV8wOTI1MjAxNSIsInZlciI6IjEuMCIsInppcCI6IkRlZmxhdGUiLCJzZXIiOiIxLjAifQ..8oC4Q6aKdr35yMWm.p43lns-cfWNFbtmrhvtssQXCItb3E9aSLafZJ6nKnnpXGQ-ZapOOyH7hPK7AN_RT7NMsQwNdy0Fyv_hOMrFbMPZNvHSa91RsQIvBZ73-CVy0HNF0grSezjCATg4NVHfricuQVegEmZKFOoNP6TaMC2kIlEi3rhrrO8VE3ZFQ3Jjo6j91BJaE9ybb02HWOoKqlzHiazwQyUHujw_R0TyXaQCI_gtLARr5QUXm7hlAfHhxR9uewQKlRbeuMH8nCMLSMASCJyzfeSJTjXmA0F0VrXozrqzOJdyy0EETPR7oA48MJ9l6C2sy2ZELkqpOM3xhbhV-Re7nM09b8DeWuCw7VNTcQc9DKnIHDR-H5U2Tc-lMJQadgUNZv7KGSRGTyprWb7wF7FEPnRNID5PCDV_N_yoQpI7VvJO_NotXEgHFo7OHs5Gsgwpl5mrDtymYzIMM7onTflOlu46em_qltji7xcWNOuHq4AeOlcY9ZythZgJH7livljReTwyX8QuUwpomXVEUGDc5pAnvgSozxnUbM7AlwfUeJZRT45P7L7683RSqChdNxiQk0sXUECqxnFxMAz4VUzld2yFe-pzvxFF4_feQjBEmSCAvekpvJUrEticEs4QzByV5UZ2ZCKccijFTg4doACiCo_z13JTm47mxm-5jUhXOQqiL69oxztk.KqI-z2LlC77lvwqmeFtdGQ",
    "refresh_token_expires_in": 1209600
}
```

## <a name="implement-with-your-preferred-native-sdk-or-use-app-auth"></a><span data-ttu-id="2decb-172">Implement with your preferred native SDK or use App-Auth</span><span class="sxs-lookup"><span data-stu-id="2decb-172">Implement with your preferred native SDK or use App-Auth</span></span>

<span data-ttu-id="2decb-173">The Azure AD B2C implementation meets OAuth 2.0 standards for public client resource owner password credentials and should be compatible with most client SDKs.</span><span class="sxs-lookup"><span data-stu-id="2decb-173">The Azure AD B2C implementation meets OAuth 2.0 standards for public client resource owner password credentials and should be compatible with most client SDKs.</span></span> <span data-ttu-id="2decb-174">We have tested this flow extensively, in production, with AppAuth for iOS and AppAuth for Android.</span><span class="sxs-lookup"><span data-stu-id="2decb-174">We have tested this flow extensively, in production, with AppAuth for iOS and AppAuth for Android.</span></span> <span data-ttu-id="2decb-175">For the latest information, see [Native App SDK for OAuth 2.0 and OpenID Connect implementing modern best practices](https://appauth.io/).</span><span class="sxs-lookup"><span data-stu-id="2decb-175">For the latest information, see [Native App SDK for OAuth 2.0 and OpenID Connect implementing modern best practices](https://appauth.io/).</span></span>

<span data-ttu-id="2decb-176">Download working samples that have been configured for use with Azure AD B2C from GitHub, [for Android](https://aka.ms/aadb2cappauthropc) and [for iOS](https://aka.ms/aadb2ciosappauthropc).</span><span class="sxs-lookup"><span data-stu-id="2decb-176">Download working samples that have been configured for use with Azure AD B2C from GitHub, [for Android](https://aka.ms/aadb2cappauthropc) and [for iOS](https://aka.ms/aadb2ciosappauthropc).</span></span>




