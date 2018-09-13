---
title: Use Azure AD v2.0 to access secure resources without user interaction | Microsoft Docs
description: Build web applications by using the Azure AD implementation of the OAuth 2.0 authentication protocol.
services: active-directory
documentationcenter: ''
author: dstrockis
manager: mbaldwin
editor: ''
ms.assetid: 9b7cfbd7-f89f-4e33-aff2-414edd584b07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.openlocfilehash: c232212e1e10ee6ce965d06edac764059b3cf08d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550482"
---
# <a name="azure-active-directory-v20-and-the-oauth-20-client-credentials-flow"></a><span data-ttu-id="ae280-103">Azure Active Directory v2.0 and the OAuth 2.0 client credentials flow</span><span class="sxs-lookup"><span data-stu-id="ae280-103">Azure Active Directory v2.0 and the OAuth 2.0 client credentials flow</span></span>
<span data-ttu-id="ae280-104">You can use the [OAuth 2.0 client credentials grant](http://tools.ietf.org/html/rfc6749#section-4.4), sometimes called *two-legged OAuth*, to access web-hosted resources by using the identity of an application.</span><span class="sxs-lookup"><span data-stu-id="ae280-104">You can use the [OAuth 2.0 client credentials grant](http://tools.ietf.org/html/rfc6749#section-4.4), sometimes called *two-legged OAuth*, to access web-hosted resources by using the identity of an application.</span></span> <span data-ttu-id="ae280-105">This type of grant commonly is used for server-to-server interactions that must run in the background, without immediate interaction with a user.</span><span class="sxs-lookup"><span data-stu-id="ae280-105">This type of grant commonly is used for server-to-server interactions that must run in the background, without immediate interaction with a user.</span></span> <span data-ttu-id="ae280-106">These types of applications often are referred to as *daemons* or *service accounts*.</span><span class="sxs-lookup"><span data-stu-id="ae280-106">These types of applications often are referred to as *daemons* or *service accounts*.</span></span>

> [!NOTE]
> <span data-ttu-id="ae280-107">The v2.0 endpoint doesn't support all Azure Active Directory scenarios and features.</span><span class="sxs-lookup"><span data-stu-id="ae280-107">The v2.0 endpoint doesn't support all Azure Active Directory scenarios and features.</span></span> <span data-ttu-id="ae280-108">To determine whether you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="ae280-108">To determine whether you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="ae280-109">In the more typical *three-legged OAuth*, a client application is granted permission to access a resource on behalf of a specific user.</span><span class="sxs-lookup"><span data-stu-id="ae280-109">In the more typical *three-legged OAuth*, a client application is granted permission to access a resource on behalf of a specific user.</span></span> <span data-ttu-id="ae280-110">The permission is delegated from the user to the application, usually during the [consent](active-directory-v2-scopes.md) process.</span><span class="sxs-lookup"><span data-stu-id="ae280-110">The permission is delegated from the user to the application, usually during the [consent](active-directory-v2-scopes.md) process.</span></span> <span data-ttu-id="ae280-111">However, in the client credentials flow, permissions are granted directly to the application itself.</span><span class="sxs-lookup"><span data-stu-id="ae280-111">However, in the client credentials flow, permissions are granted directly to the application itself.</span></span> <span data-ttu-id="ae280-112">When the app presents a token to a resource, the resource enforces that the app itself has authorization to perform an action, and not that the user has authorization.</span><span class="sxs-lookup"><span data-stu-id="ae280-112">When the app presents a token to a resource, the resource enforces that the app itself has authorization to perform an action, and not that the user has authorization.</span></span>

## <a name="protocol-diagram"></a><span data-ttu-id="ae280-113">Protocol diagram</span><span class="sxs-lookup"><span data-stu-id="ae280-113">Protocol diagram</span></span>
<span data-ttu-id="ae280-114">The entire client credentials flow looks similar to the next diagram.</span><span class="sxs-lookup"><span data-stu-id="ae280-114">The entire client credentials flow looks similar to the next diagram.</span></span> <span data-ttu-id="ae280-115">We describe each of the steps later in this article.</span><span class="sxs-lookup"><span data-stu-id="ae280-115">We describe each of the steps later in this article.</span></span>

![Client credentials flow](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/active-directory-v2-flows/convergence_scenarios_client_creds.png)

## <a name="get-direct-authorization"></a><span data-ttu-id="ae280-117">Get direct authorization</span><span class="sxs-lookup"><span data-stu-id="ae280-117">Get direct authorization</span></span>
<span data-ttu-id="ae280-118">An app typically receives direct authorization to access a resource in one of two ways: through an access control list (ACL) at the resource, or through application permission assignment in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ae280-118">An app typically receives direct authorization to access a resource in one of two ways: through an access control list (ACL) at the resource, or through application permission assignment in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="ae280-119">These two methods are the most common in Azure AD, and we recommend them for clients and resources that perform the client credentials flow.</span><span class="sxs-lookup"><span data-stu-id="ae280-119">These two methods are the most common in Azure AD, and we recommend them for clients and resources that perform the client credentials flow.</span></span> <span data-ttu-id="ae280-120">A resource can choose to authorize its clients in other ways, however.</span><span class="sxs-lookup"><span data-stu-id="ae280-120">A resource can choose to authorize its clients in other ways, however.</span></span> <span data-ttu-id="ae280-121">Each resource server can choose the method that makes the most sense for its application.</span><span class="sxs-lookup"><span data-stu-id="ae280-121">Each resource server can choose the method that makes the most sense for its application.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="ae280-122">Access control lists</span><span class="sxs-lookup"><span data-stu-id="ae280-122">Access control lists</span></span>
<span data-ttu-id="ae280-123">A resource provider might enforce an authorization check based on a list of Application IDs that it knows and grants a specific level of access to.</span><span class="sxs-lookup"><span data-stu-id="ae280-123">A resource provider might enforce an authorization check based on a list of Application IDs that it knows and grants a specific level of access to.</span></span> <span data-ttu-id="ae280-124">When the resource receives a token from the v2.0 endpoint, it can decode the token and extract the client's Application ID from the `appid` and `iss` claims.</span><span class="sxs-lookup"><span data-stu-id="ae280-124">When the resource receives a token from the v2.0 endpoint, it can decode the token and extract the client's Application ID from the `appid` and `iss` claims.</span></span> <span data-ttu-id="ae280-125">Then it compares the application against an ACL that it maintains.</span><span class="sxs-lookup"><span data-stu-id="ae280-125">Then it compares the application against an ACL that it maintains.</span></span> <span data-ttu-id="ae280-126">The ACL's granularity and method might vary substantially between resources.</span><span class="sxs-lookup"><span data-stu-id="ae280-126">The ACL's granularity and method might vary substantially between resources.</span></span>

<span data-ttu-id="ae280-127">A common use case is to use an ACL to run tests for a web application or for a Web API.</span><span class="sxs-lookup"><span data-stu-id="ae280-127">A common use case is to use an ACL to run tests for a web application or for a Web API.</span></span> <span data-ttu-id="ae280-128">The Web API might grant only a subset of full permissions to a specific client.</span><span class="sxs-lookup"><span data-stu-id="ae280-128">The Web API might grant only a subset of full permissions to a specific client.</span></span> <span data-ttu-id="ae280-129">To run end-to-end tests on the API, create a test client that acquires tokens from the v2.0 endpoint and then sends them to the API.</span><span class="sxs-lookup"><span data-stu-id="ae280-129">To run end-to-end tests on the API, create a test client that acquires tokens from the v2.0 endpoint and then sends them to the API.</span></span> <span data-ttu-id="ae280-130">The API then checks the ACL for the test client's Application ID for full access to the API's entire functionality.</span><span class="sxs-lookup"><span data-stu-id="ae280-130">The API then checks the ACL for the test client's Application ID for full access to the API's entire functionality.</span></span> <span data-ttu-id="ae280-131">If you use this kind of ACL, be sure to validate not only the caller's `appid` value.</span><span class="sxs-lookup"><span data-stu-id="ae280-131">If you use this kind of ACL, be sure to validate not only the caller's `appid` value.</span></span> <span data-ttu-id="ae280-132">Also validate that the `iss` value of the token is trusted.</span><span class="sxs-lookup"><span data-stu-id="ae280-132">Also validate that the `iss` value of the token is trusted.</span></span>

<span data-ttu-id="ae280-133">This type of authorization is common for daemons and service accounts that need to access data owned by consumer users who have personal Microsoft accounts.</span><span class="sxs-lookup"><span data-stu-id="ae280-133">This type of authorization is common for daemons and service accounts that need to access data owned by consumer users who have personal Microsoft accounts.</span></span> <span data-ttu-id="ae280-134">For data owned by organizations, we recommend that you get the necessary authorization through application permissions.</span><span class="sxs-lookup"><span data-stu-id="ae280-134">For data owned by organizations, we recommend that you get the necessary authorization through application permissions.</span></span>

### <a name="application-permissions"></a><span data-ttu-id="ae280-135">Application permissions</span><span class="sxs-lookup"><span data-stu-id="ae280-135">Application permissions</span></span>
<span data-ttu-id="ae280-136">Instead of using ACLs, you can use APIs to expose a set of application permissions.</span><span class="sxs-lookup"><span data-stu-id="ae280-136">Instead of using ACLs, you can use APIs to expose a set of application permissions.</span></span> <span data-ttu-id="ae280-137">An application permission is granted to an application by an organization's administrator, and can be used only to access data owned by that organization and its employees.</span><span class="sxs-lookup"><span data-stu-id="ae280-137">An application permission is granted to an application by an organization's administrator, and can be used only to access data owned by that organization and its employees.</span></span> <span data-ttu-id="ae280-138">For example, Microsoft Graph exposes several application permissions to do the following:</span><span class="sxs-lookup"><span data-stu-id="ae280-138">For example, Microsoft Graph exposes several application permissions to do the following:</span></span>

* <span data-ttu-id="ae280-139">Read mail in all mailboxes</span><span class="sxs-lookup"><span data-stu-id="ae280-139">Read mail in all mailboxes</span></span>
* <span data-ttu-id="ae280-140">Read and write mail in all mailboxes</span><span class="sxs-lookup"><span data-stu-id="ae280-140">Read and write mail in all mailboxes</span></span>
* <span data-ttu-id="ae280-141">Send mail as any user</span><span class="sxs-lookup"><span data-stu-id="ae280-141">Send mail as any user</span></span>
* <span data-ttu-id="ae280-142">Read directory data</span><span class="sxs-lookup"><span data-stu-id="ae280-142">Read directory data</span></span>

<span data-ttu-id="ae280-143">For more information about application permissions, go to [Microsoft Graph](https://graph.microsoft.io).</span><span class="sxs-lookup"><span data-stu-id="ae280-143">For more information about application permissions, go to [Microsoft Graph](https://graph.microsoft.io).</span></span>

<span data-ttu-id="ae280-144">To use application permissions in your app, do the steps we discuss in the next sections.</span><span class="sxs-lookup"><span data-stu-id="ae280-144">To use application permissions in your app, do the steps we discuss in the next sections.</span></span>

#### <a name="request-the-permissions-in-the-app-registration-portal"></a><span data-ttu-id="ae280-145">Request the permissions in the app registration portal</span><span class="sxs-lookup"><span data-stu-id="ae280-145">Request the permissions in the app registration portal</span></span>
1. <span data-ttu-id="ae280-146">Go to your application in the [Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or [create an app](active-directory-v2-app-registration.md), if you haven't already.</span><span class="sxs-lookup"><span data-stu-id="ae280-146">Go to your application in the [Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or [create an app](active-directory-v2-app-registration.md), if you haven't already.</span></span> <span data-ttu-id="ae280-147">You'll need to use at least one Application Secret when you create your app.</span><span class="sxs-lookup"><span data-stu-id="ae280-147">You'll need to use at least one Application Secret when you create your app.</span></span>
2. <span data-ttu-id="ae280-148">Locate the **Direct Application Permissions** section, and then add the permissions that your app requires.</span><span class="sxs-lookup"><span data-stu-id="ae280-148">Locate the **Direct Application Permissions** section, and then add the permissions that your app requires.</span></span>
3. <span data-ttu-id="ae280-149">**Save** the app registration.</span><span class="sxs-lookup"><span data-stu-id="ae280-149">**Save** the app registration.</span></span>

#### <a name="recommended-sign-the-user-in-to-your-app"></a><span data-ttu-id="ae280-150">Recommended: Sign the user in to your app</span><span class="sxs-lookup"><span data-stu-id="ae280-150">Recommended: Sign the user in to your app</span></span>
<span data-ttu-id="ae280-151">Typically, when you build an application that uses application permissions, the app requires a page or view on which the admin approves the app's permissions.</span><span class="sxs-lookup"><span data-stu-id="ae280-151">Typically, when you build an application that uses application permissions, the app requires a page or view on which the admin approves the app's permissions.</span></span> <span data-ttu-id="ae280-152">This page can be part of the app's sign-in flow, part of the app's settings, or it can be a dedicated "connect" flow.</span><span class="sxs-lookup"><span data-stu-id="ae280-152">This page can be part of the app's sign-in flow, part of the app's settings, or it can be a dedicated "connect" flow.</span></span> <span data-ttu-id="ae280-153">In many cases, it makes sense for the app to show this "connect" view only after a user has signed in with a work or school Microsoft account.</span><span class="sxs-lookup"><span data-stu-id="ae280-153">In many cases, it makes sense for the app to show this "connect" view only after a user has signed in with a work or school Microsoft account.</span></span>

<span data-ttu-id="ae280-154">If you sign the user in to your app, you can identify the organization to which the user belongs before you ask the user to approve the application permissions.</span><span class="sxs-lookup"><span data-stu-id="ae280-154">If you sign the user in to your app, you can identify the organization to which the user belongs before you ask the user to approve the application permissions.</span></span> <span data-ttu-id="ae280-155">Although not strictly necessary, it can help you create a more intuitive experience for your users.</span><span class="sxs-lookup"><span data-stu-id="ae280-155">Although not strictly necessary, it can help you create a more intuitive experience for your users.</span></span> <span data-ttu-id="ae280-156">To sign the user in, follow our [v2.0 protocol tutorials](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="ae280-156">To sign the user in, follow our [v2.0 protocol tutorials](active-directory-v2-protocols.md).</span></span>

#### <a name="request-the-permissions-from-a-directory-admin"></a><span data-ttu-id="ae280-157">Request the permissions from a directory admin</span><span class="sxs-lookup"><span data-stu-id="ae280-157">Request the permissions from a directory admin</span></span>
<span data-ttu-id="ae280-158">When you're ready to request permissions from the organization's admin, you can redirect the user to the v2.0 *admin consent endpoint*.</span><span class="sxs-lookup"><span data-stu-id="ae280-158">When you're ready to request permissions from the organization's admin, you can redirect the user to the v2.0 *admin consent endpoint*.</span></span>

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/adminconsent?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&state=12345
&redirect_uri=http://localhost/myapp/permissions
```

```
// Pro tip: Try pasting the following request in a browser!
```

```
https://login.microsoftonline.com/common/adminconsent?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&state=12345&redirect_uri=http://localhost/myapp/permissions
```

| <span data-ttu-id="ae280-159">Parameter</span><span class="sxs-lookup"><span data-stu-id="ae280-159">Parameter</span></span> | <span data-ttu-id="ae280-160">Condition</span><span class="sxs-lookup"><span data-stu-id="ae280-160">Condition</span></span> | <span data-ttu-id="ae280-161">Description</span><span class="sxs-lookup"><span data-stu-id="ae280-161">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ae280-162">tenant</span><span class="sxs-lookup"><span data-stu-id="ae280-162">tenant</span></span> |<span data-ttu-id="ae280-163">Required</span><span class="sxs-lookup"><span data-stu-id="ae280-163">Required</span></span> |<span data-ttu-id="ae280-164">The directory tenant that you want to request permission from.</span><span class="sxs-lookup"><span data-stu-id="ae280-164">The directory tenant that you want to request permission from.</span></span> <span data-ttu-id="ae280-165">This can be in GUID or friendly name format.</span><span class="sxs-lookup"><span data-stu-id="ae280-165">This can be in GUID or friendly name format.</span></span> <span data-ttu-id="ae280-166">If you don't know which tenant the user belongs to and you want to let them sign in with any tenant, use `common`.</span><span class="sxs-lookup"><span data-stu-id="ae280-166">If you don't know which tenant the user belongs to and you want to let them sign in with any tenant, use `common`.</span></span> |
| <span data-ttu-id="ae280-167">client_id</span><span class="sxs-lookup"><span data-stu-id="ae280-167">client_id</span></span> |<span data-ttu-id="ae280-168">Required</span><span class="sxs-lookup"><span data-stu-id="ae280-168">Required</span></span> |<span data-ttu-id="ae280-169">The Application ID that the [Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) assigned to your app.</span><span class="sxs-lookup"><span data-stu-id="ae280-169">The Application ID that the [Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) assigned to your app.</span></span> |
| <span data-ttu-id="ae280-170">redirect_uri</span><span class="sxs-lookup"><span data-stu-id="ae280-170">redirect_uri</span></span> |<span data-ttu-id="ae280-171">Required</span><span class="sxs-lookup"><span data-stu-id="ae280-171">Required</span></span> |<span data-ttu-id="ae280-172">The redirect URI where you want the response to be sent for your app to handle.</span><span class="sxs-lookup"><span data-stu-id="ae280-172">The redirect URI where you want the response to be sent for your app to handle.</span></span> <span data-ttu-id="ae280-173">It must exactly match one of the redirect URIs that you registered in the portal, except that it must be URL encoded, and it can have additional path segments.</span><span class="sxs-lookup"><span data-stu-id="ae280-173">It must exactly match one of the redirect URIs that you registered in the portal, except that it must be URL encoded, and it can have additional path segments.</span></span> |
| <span data-ttu-id="ae280-174">state</span><span class="sxs-lookup"><span data-stu-id="ae280-174">state</span></span> |<span data-ttu-id="ae280-175">Recommended</span><span class="sxs-lookup"><span data-stu-id="ae280-175">Recommended</span></span> |<span data-ttu-id="ae280-176">A value that is included in the request that also is returned in the token response.</span><span class="sxs-lookup"><span data-stu-id="ae280-176">A value that is included in the request that also is returned in the token response.</span></span> <span data-ttu-id="ae280-177">It can be a string of any content that you want.</span><span class="sxs-lookup"><span data-stu-id="ae280-177">It can be a string of any content that you want.</span></span> <span data-ttu-id="ae280-178">The state is used to encode information about the user's state in the app before the authentication request occurred, such as the page or view they were on.</span><span class="sxs-lookup"><span data-stu-id="ae280-178">The state is used to encode information about the user's state in the app before the authentication request occurred, such as the page or view they were on.</span></span> |

<span data-ttu-id="ae280-179">At this point, Azure AD enforces that only a tenant administrator can sign in to complete the request.</span><span class="sxs-lookup"><span data-stu-id="ae280-179">At this point, Azure AD enforces that only a tenant administrator can sign in to complete the request.</span></span> <span data-ttu-id="ae280-180">The administrator will be asked to approve all the direct application permissions that you have requested for your app in the app registration portal.</span><span class="sxs-lookup"><span data-stu-id="ae280-180">The administrator will be asked to approve all the direct application permissions that you have requested for your app in the app registration portal.</span></span>

##### <a name="successful-response"></a><span data-ttu-id="ae280-181">Successful response</span><span class="sxs-lookup"><span data-stu-id="ae280-181">Successful response</span></span>
<span data-ttu-id="ae280-182">If the admin approves the permissions for your application, the successful response looks like this:</span><span class="sxs-lookup"><span data-stu-id="ae280-182">If the admin approves the permissions for your application, the successful response looks like this:</span></span>

```
GET http://localhost/myapp/permissions?tenant=a8990e1f-ff32-408a-9f8e-78d3b9139b95&state=state=12345&admin_consent=True
```

| <span data-ttu-id="ae280-183">Parameter</span><span class="sxs-lookup"><span data-stu-id="ae280-183">Parameter</span></span> | <span data-ttu-id="ae280-184">Description</span><span class="sxs-lookup"><span data-stu-id="ae280-184">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ae280-185">tenant</span><span class="sxs-lookup"><span data-stu-id="ae280-185">tenant</span></span> |<span data-ttu-id="ae280-186">The directory tenant that granted your application the permissions that it requested, in GUID format.</span><span class="sxs-lookup"><span data-stu-id="ae280-186">The directory tenant that granted your application the permissions that it requested, in GUID format.</span></span> |
| <span data-ttu-id="ae280-187">state</span><span class="sxs-lookup"><span data-stu-id="ae280-187">state</span></span> |<span data-ttu-id="ae280-188">A value that is included in the request that also is returned in the token response.</span><span class="sxs-lookup"><span data-stu-id="ae280-188">A value that is included in the request that also is returned in the token response.</span></span> <span data-ttu-id="ae280-189">It can be a string of any content that you want.</span><span class="sxs-lookup"><span data-stu-id="ae280-189">It can be a string of any content that you want.</span></span> <span data-ttu-id="ae280-190">The state is used to encode information about the user's state in the app before the authentication request occurred, such as the page or view they were on.</span><span class="sxs-lookup"><span data-stu-id="ae280-190">The state is used to encode information about the user's state in the app before the authentication request occurred, such as the page or view they were on.</span></span> |
| <span data-ttu-id="ae280-191">admin_consent</span><span class="sxs-lookup"><span data-stu-id="ae280-191">admin_consent</span></span> |<span data-ttu-id="ae280-192">Set to **true**.</span><span class="sxs-lookup"><span data-stu-id="ae280-192">Set to **true**.</span></span> |

##### <a name="error-response"></a><span data-ttu-id="ae280-193">Error response</span><span class="sxs-lookup"><span data-stu-id="ae280-193">Error response</span></span>
<span data-ttu-id="ae280-194">If the admin does not approve the permissions for your application, the failed response looks like this:</span><span class="sxs-lookup"><span data-stu-id="ae280-194">If the admin does not approve the permissions for your application, the failed response looks like this:</span></span>

```
GET http://localhost/myapp/permissions?error=permission_denied&error_description=The+admin+canceled+the+request
```

| <span data-ttu-id="ae280-195">Parameter</span><span class="sxs-lookup"><span data-stu-id="ae280-195">Parameter</span></span> | <span data-ttu-id="ae280-196">Description</span><span class="sxs-lookup"><span data-stu-id="ae280-196">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ae280-197">error</span><span class="sxs-lookup"><span data-stu-id="ae280-197">error</span></span> |<span data-ttu-id="ae280-198">An error code string that you can use to classify types of errors, and which you can use to react to errors.</span><span class="sxs-lookup"><span data-stu-id="ae280-198">An error code string that you can use to classify types of errors, and which you can use to react to errors.</span></span> |
| <span data-ttu-id="ae280-199">error_description</span><span class="sxs-lookup"><span data-stu-id="ae280-199">error_description</span></span> |<span data-ttu-id="ae280-200">A specific error message that can help you identify the root cause of an error.</span><span class="sxs-lookup"><span data-stu-id="ae280-200">A specific error message that can help you identify the root cause of an error.</span></span> |

<span data-ttu-id="ae280-201">After you've received a successful response from the app provisioning endpoint, your app has gained the direct application permissions that it requested.</span><span class="sxs-lookup"><span data-stu-id="ae280-201">After you've received a successful response from the app provisioning endpoint, your app has gained the direct application permissions that it requested.</span></span> <span data-ttu-id="ae280-202">Now you can request a token for the resource that you want.</span><span class="sxs-lookup"><span data-stu-id="ae280-202">Now you can request a token for the resource that you want.</span></span>

## <a name="get-a-token"></a><span data-ttu-id="ae280-203">Get a token</span><span class="sxs-lookup"><span data-stu-id="ae280-203">Get a token</span></span>
<span data-ttu-id="ae280-204">After you've acquired the necessary authorization for your application, proceed with acquiring access tokens for APIs.</span><span class="sxs-lookup"><span data-stu-id="ae280-204">After you've acquired the necessary authorization for your application, proceed with acquiring access tokens for APIs.</span></span> <span data-ttu-id="ae280-205">To get a token by using the client credentials grant, send a POST request to the `/token` v2.0 endpoint:</span><span class="sxs-lookup"><span data-stu-id="ae280-205">To get a token by using the client credentials grant, send a POST request to the `/token` v2.0 endpoint:</span></span>

```
POST /common/oauth2/v2.0/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=535fb089-9ff3-47b6-9bfb-4f1264799865&scope=https%3A%2F%2Fgraph.microsoft.com%2F.default&client_secret=qWgdYAmab0YSkuL1qKv5bPX&grant_type=client_credentials
```

```
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d 'client_id=535fb089-9ff3-47b6-9bfb-4f1264799865&scope=https%3A%2F%2Fgraph.microsoft.com%2F.default&client_secret=qWgdYAmab0YSkuL1qKv5bPX&grant_type=client_credentials' 'https://login.microsoftonline.com/common/oauth2/v2.0/token'
```

| <span data-ttu-id="ae280-206">Parameter</span><span class="sxs-lookup"><span data-stu-id="ae280-206">Parameter</span></span> | <span data-ttu-id="ae280-207">Condition</span><span class="sxs-lookup"><span data-stu-id="ae280-207">Condition</span></span> | <span data-ttu-id="ae280-208">Description</span><span class="sxs-lookup"><span data-stu-id="ae280-208">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ae280-209">client_id</span><span class="sxs-lookup"><span data-stu-id="ae280-209">client_id</span></span> |<span data-ttu-id="ae280-210">Required</span><span class="sxs-lookup"><span data-stu-id="ae280-210">Required</span></span> |<span data-ttu-id="ae280-211">The Application ID that the [Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) assigned to your app.</span><span class="sxs-lookup"><span data-stu-id="ae280-211">The Application ID that the [Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) assigned to your app.</span></span> |
| <span data-ttu-id="ae280-212">scope</span><span class="sxs-lookup"><span data-stu-id="ae280-212">scope</span></span> |<span data-ttu-id="ae280-213">Required</span><span class="sxs-lookup"><span data-stu-id="ae280-213">Required</span></span> |<span data-ttu-id="ae280-214">The value passed for the `scope` parameter in this request should be the resource identifier (Application ID URI) of the resource you want, affixed with the `.default` suffix.</span><span class="sxs-lookup"><span data-stu-id="ae280-214">The value passed for the `scope` parameter in this request should be the resource identifier (Application ID URI) of the resource you want, affixed with the `.default` suffix.</span></span> <span data-ttu-id="ae280-215">For the Microsoft Graph example, the value is `https://graph.microsoft.com/.default`.</span><span class="sxs-lookup"><span data-stu-id="ae280-215">For the Microsoft Graph example, the value is `https://graph.microsoft.com/.default`.</span></span> <span data-ttu-id="ae280-216">This value informs the v2.0 endpoint that of all the direct application permissions you have configured for your app, it should issue a token for the ones associated with the resource you want to use.</span><span class="sxs-lookup"><span data-stu-id="ae280-216">This value informs the v2.0 endpoint that of all the direct application permissions you have configured for your app, it should issue a token for the ones associated with the resource you want to use.</span></span> |
| <span data-ttu-id="ae280-217">client_secret</span><span class="sxs-lookup"><span data-stu-id="ae280-217">client_secret</span></span> |<span data-ttu-id="ae280-218">Required</span><span class="sxs-lookup"><span data-stu-id="ae280-218">Required</span></span> |<span data-ttu-id="ae280-219">The Application Secret that you generated for your app in the app registration portal.</span><span class="sxs-lookup"><span data-stu-id="ae280-219">The Application Secret that you generated for your app in the app registration portal.</span></span> |
| <span data-ttu-id="ae280-220">grant_type</span><span class="sxs-lookup"><span data-stu-id="ae280-220">grant_type</span></span> |<span data-ttu-id="ae280-221">Required</span><span class="sxs-lookup"><span data-stu-id="ae280-221">Required</span></span> |<span data-ttu-id="ae280-222">Must be `client_credentials`.</span><span class="sxs-lookup"><span data-stu-id="ae280-222">Must be `client_credentials`.</span></span> |

##### <a name="successful-response"></a><span data-ttu-id="ae280-223">Successful response</span><span class="sxs-lookup"><span data-stu-id="ae280-223">Successful response</span></span>
<span data-ttu-id="ae280-224">A successful response looks like this:</span><span class="sxs-lookup"><span data-stu-id="ae280-224">A successful response looks like this:</span></span>

```
{
  "token_type": "Bearer",
  "expires_in": 3599,
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBP..."
}
```

| <span data-ttu-id="ae280-225">Parameter</span><span class="sxs-lookup"><span data-stu-id="ae280-225">Parameter</span></span> | <span data-ttu-id="ae280-226">Description</span><span class="sxs-lookup"><span data-stu-id="ae280-226">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ae280-227">access_token</span><span class="sxs-lookup"><span data-stu-id="ae280-227">access_token</span></span> |<span data-ttu-id="ae280-228">The requested access token.</span><span class="sxs-lookup"><span data-stu-id="ae280-228">The requested access token.</span></span> <span data-ttu-id="ae280-229">The app can use this token to authenticate to the secured resource, such as to a Web API.</span><span class="sxs-lookup"><span data-stu-id="ae280-229">The app can use this token to authenticate to the secured resource, such as to a Web API.</span></span> |
| <span data-ttu-id="ae280-230">token_type</span><span class="sxs-lookup"><span data-stu-id="ae280-230">token_type</span></span> |<span data-ttu-id="ae280-231">Indicates the token type value.</span><span class="sxs-lookup"><span data-stu-id="ae280-231">Indicates the token type value.</span></span> <span data-ttu-id="ae280-232">The only type that Azure AD supports is `bearer`.</span><span class="sxs-lookup"><span data-stu-id="ae280-232">The only type that Azure AD supports is `bearer`.</span></span> |
| <span data-ttu-id="ae280-233">expires_in</span><span class="sxs-lookup"><span data-stu-id="ae280-233">expires_in</span></span> |<span data-ttu-id="ae280-234">How long the access token is valid (in seconds).</span><span class="sxs-lookup"><span data-stu-id="ae280-234">How long the access token is valid (in seconds).</span></span> |

##### <a name="error-response"></a><span data-ttu-id="ae280-235">Error response</span><span class="sxs-lookup"><span data-stu-id="ae280-235">Error response</span></span>
<span data-ttu-id="ae280-236">An error response looks like this:</span><span class="sxs-lookup"><span data-stu-id="ae280-236">An error response looks like this:</span></span>

```
{
  "error": "invalid_scope",
  "error_description": "AADSTS70011: The provided value for the input parameter 'scope' is not valid. The scope https://foo.microsoft.com/.default is not valid.\r\nTrace ID: 255d1aef-8c98-452f-ac51-23d051240864\r\nCorrelation ID: fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7\r\nTimestamp: 2016-01-09 02:02:12Z",
  "error_codes": [
    70011
  ],
  "timestamp": "2016-01-09 02:02:12Z",
  "trace_id": "255d1aef-8c98-452f-ac51-23d051240864",
  "correlation_id": "fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7"
}
```

| <span data-ttu-id="ae280-237">Parameter</span><span class="sxs-lookup"><span data-stu-id="ae280-237">Parameter</span></span> | <span data-ttu-id="ae280-238">Description</span><span class="sxs-lookup"><span data-stu-id="ae280-238">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ae280-239">error</span><span class="sxs-lookup"><span data-stu-id="ae280-239">error</span></span> |<span data-ttu-id="ae280-240">An error code string that you can use to classify types of errors that occur, and to react to errors.</span><span class="sxs-lookup"><span data-stu-id="ae280-240">An error code string that you can use to classify types of errors that occur, and to react to errors.</span></span> |
| <span data-ttu-id="ae280-241">error_description</span><span class="sxs-lookup"><span data-stu-id="ae280-241">error_description</span></span> |<span data-ttu-id="ae280-242">A specific error message that might help you identify the root cause of an authentication error.</span><span class="sxs-lookup"><span data-stu-id="ae280-242">A specific error message that might help you identify the root cause of an authentication error.</span></span> |
| <span data-ttu-id="ae280-243">error_codes</span><span class="sxs-lookup"><span data-stu-id="ae280-243">error_codes</span></span> |<span data-ttu-id="ae280-244">A list of STS-specific error codes that might help with diagnostics.</span><span class="sxs-lookup"><span data-stu-id="ae280-244">A list of STS-specific error codes that might help with diagnostics.</span></span> |
| <span data-ttu-id="ae280-245">timestamp</span><span class="sxs-lookup"><span data-stu-id="ae280-245">timestamp</span></span> |<span data-ttu-id="ae280-246">The time at which the error occurred.</span><span class="sxs-lookup"><span data-stu-id="ae280-246">The time at which the error occurred.</span></span> |
| <span data-ttu-id="ae280-247">trace_id</span><span class="sxs-lookup"><span data-stu-id="ae280-247">trace_id</span></span> |<span data-ttu-id="ae280-248">A unique identifier for the request that might help with diagnostics.</span><span class="sxs-lookup"><span data-stu-id="ae280-248">A unique identifier for the request that might help with diagnostics.</span></span> |
| <span data-ttu-id="ae280-249">correlation_id</span><span class="sxs-lookup"><span data-stu-id="ae280-249">correlation_id</span></span> |<span data-ttu-id="ae280-250">A unique identifier for the request that might help with diagnostics across components.</span><span class="sxs-lookup"><span data-stu-id="ae280-250">A unique identifier for the request that might help with diagnostics across components.</span></span> |

## <a name="use-a-token"></a><span data-ttu-id="ae280-251">Use a token</span><span class="sxs-lookup"><span data-stu-id="ae280-251">Use a token</span></span>
<span data-ttu-id="ae280-252">Now that you've acquired a token, use the token to make requests to the resource.</span><span class="sxs-lookup"><span data-stu-id="ae280-252">Now that you've acquired a token, use the token to make requests to the resource.</span></span> <span data-ttu-id="ae280-253">When the token expires, repeat the request to the `/token` endpoint to acquire a fresh access token.</span><span class="sxs-lookup"><span data-stu-id="ae280-253">When the token expires, repeat the request to the `/token` endpoint to acquire a fresh access token.</span></span>

```
GET /v1.0/me/messages
Host: https://graph.microsoft.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

```
// Pro tip: Try the following command! (Replace the token with your own.)
```

```
curl -X GET -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q" 'https://graph.microsoft.com/v1.0/me/messages'
```

## <a name="code-sample"></a><span data-ttu-id="ae280-254">Code sample</span><span class="sxs-lookup"><span data-stu-id="ae280-254">Code sample</span></span>
<span data-ttu-id="ae280-255">To see an example of an application that implements the client credentials grant by using the admin consent endpoint, see our [v2.0 daemon code sample](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).</span><span class="sxs-lookup"><span data-stu-id="ae280-255">To see an example of an application that implements the client credentials grant by using the admin consent endpoint, see our [v2.0 daemon code sample](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).</span></span>


