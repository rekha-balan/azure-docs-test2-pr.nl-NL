---
title: Azure Active Directory B2C | Microsoft Docs
description: How to build a .NET Web app and call a web api using Azure Active Directory B2C and OAuth 2.0 access tokens.
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: ''
ms.assetid: d3888556-2647-4a42-b068-027f9374aa61
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 02ec1b7a58aff6ae0788e341e8987b9d32cb5a7b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540989"
---
# <a name="azure-ad-b2c-call-a-net-web-api-from-a-net-web-app"></a><span data-ttu-id="bcb52-103">Azure AD B2C: Call a .NET web API from a .NET web app</span><span class="sxs-lookup"><span data-stu-id="bcb52-103">Azure AD B2C: Call a .NET web API from a .NET web app</span></span>

<span data-ttu-id="bcb52-104">By using Azure AD B2C, you can add powerful identity management features to your web apps and web APIs.</span><span class="sxs-lookup"><span data-stu-id="bcb52-104">By using Azure AD B2C, you can add powerful identity management features to your web apps and web APIs.</span></span> <span data-ttu-id="bcb52-105">This article discusses how to request access tokens and make calls from a .NET "to-do list" web app to a .NET web api.</span><span class="sxs-lookup"><span data-stu-id="bcb52-105">This article discusses how to request access tokens and make calls from a .NET "to-do list" web app to a .NET web api.</span></span>

<span data-ttu-id="bcb52-106">This article does not cover how to implement sign-in, sign-up and profile management with Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="bcb52-106">This article does not cover how to implement sign-in, sign-up and profile management with Azure AD B2C.</span></span> <span data-ttu-id="bcb52-107">It focuses on calling web APIs after the user is already authenticated.</span><span class="sxs-lookup"><span data-stu-id="bcb52-107">It focuses on calling web APIs after the user is already authenticated.</span></span> <span data-ttu-id="bcb52-108">If you haven't already, you should:</span><span class="sxs-lookup"><span data-stu-id="bcb52-108">If you haven't already, you should:</span></span>

* <span data-ttu-id="bcb52-109">Get started with a [.NET web app](active-directory-b2c-devquickstarts-web-dotnet-susi.md)</span><span class="sxs-lookup"><span data-stu-id="bcb52-109">Get started with a [.NET web app](active-directory-b2c-devquickstarts-web-dotnet-susi.md)</span></span>
* <span data-ttu-id="bcb52-110">Get started with a [.NET web api](active-directory-b2c-devquickstarts-api-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="bcb52-110">Get started with a [.NET web api](active-directory-b2c-devquickstarts-api-dotnet.md)</span></span>

## <a name="prerequisite"></a><span data-ttu-id="bcb52-111">Prerequisite</span><span class="sxs-lookup"><span data-stu-id="bcb52-111">Prerequisite</span></span>

<span data-ttu-id="bcb52-112">To build a web application that calls a web api, you need to:</span><span class="sxs-lookup"><span data-stu-id="bcb52-112">To build a web application that calls a web api, you need to:</span></span>

1. <span data-ttu-id="bcb52-113">[Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bcb52-113">[Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>
2. <span data-ttu-id="bcb52-114">[Register a web api](active-directory-b2c-app-registration.md#register-a-web-api).</span><span class="sxs-lookup"><span data-stu-id="bcb52-114">[Register a web api](active-directory-b2c-app-registration.md#register-a-web-api).</span></span>
3. <span data-ttu-id="bcb52-115">[Register a web app](active-directory-b2c-app-registration.md#register-a-web-application).</span><span class="sxs-lookup"><span data-stu-id="bcb52-115">[Register a web app](active-directory-b2c-app-registration.md#register-a-web-application).</span></span>
4. <span data-ttu-id="bcb52-116">[Set up policies](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="bcb52-116">[Set up policies](active-directory-b2c-reference-policies.md).</span></span>
5. <span data-ttu-id="bcb52-117">[Grant the web app permissions to use the web api](active-directory-b2c-access-tokens.md#granting-permissions-to-a-web-api).</span><span class="sxs-lookup"><span data-stu-id="bcb52-117">[Grant the web app permissions to use the web api](active-directory-b2c-access-tokens.md#granting-permissions-to-a-web-api).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bcb52-118">The client application and web API must use the same Azure AD B2C directory.</span><span class="sxs-lookup"><span data-stu-id="bcb52-118">The client application and web API must use the same Azure AD B2C directory.</span></span>
>

## <a name="download-the-code"></a><span data-ttu-id="bcb52-119">Download the code</span><span class="sxs-lookup"><span data-stu-id="bcb52-119">Download the code</span></span>

<span data-ttu-id="bcb52-120">The code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="bcb52-120">The code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="bcb52-121">You can clone the sample by running:</span><span class="sxs-lookup"><span data-stu-id="bcb52-121">You can clone the sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="bcb52-122">After you download the sample code, open the Visual Studio .sln file to get started.</span><span class="sxs-lookup"><span data-stu-id="bcb52-122">After you download the sample code, open the Visual Studio .sln file to get started.</span></span> <span data-ttu-id="bcb52-123">The solution file contains two projects: `TaskWebApp` and `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="bcb52-123">The solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="bcb52-124">`TaskWebApp` is a MVC web application that the user interacts with.</span><span class="sxs-lookup"><span data-stu-id="bcb52-124">`TaskWebApp` is a MVC web application that the user interacts with.</span></span> <span data-ttu-id="bcb52-125">`TaskService` is the app's back-end web API that stores each user's to-do list.</span><span class="sxs-lookup"><span data-stu-id="bcb52-125">`TaskService` is the app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="bcb52-126">This article does not cover building the `TaskWebApp` web app or the `TaskService` web api.</span><span class="sxs-lookup"><span data-stu-id="bcb52-126">This article does not cover building the `TaskWebApp` web app or the `TaskService` web api.</span></span> <span data-ttu-id="bcb52-127">To learn how to build the .NET web app using Azure AD B2C, see our [.NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="bcb52-127">To learn how to build the .NET web app using Azure AD B2C, see our [.NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span> <span data-ttu-id="bcb52-128">To learn how to build the .NET web API secured using Azure AD B2C, see our [.NET web API tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="bcb52-128">To learn how to build the .NET web API secured using Azure AD B2C, see our [.NET web API tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

### <a name="update-the-azure-ad-b2c-configuration"></a><span data-ttu-id="bcb52-129">Update the Azure AD B2C configuration</span><span class="sxs-lookup"><span data-stu-id="bcb52-129">Update the Azure AD B2C configuration</span></span>

<span data-ttu-id="bcb52-130">Our sample is configured to use the policies and client ID of our demo tenant.</span><span class="sxs-lookup"><span data-stu-id="bcb52-130">Our sample is configured to use the policies and client ID of our demo tenant.</span></span> <span data-ttu-id="bcb52-131">If you would like to use your own tenant:</span><span class="sxs-lookup"><span data-stu-id="bcb52-131">If you would like to use your own tenant:</span></span>

1. <span data-ttu-id="bcb52-132">Open `web.config` in the `TaskService` project and replace the values for</span><span class="sxs-lookup"><span data-stu-id="bcb52-132">Open `web.config` in the `TaskService` project and replace the values for</span></span>

    * <span data-ttu-id="bcb52-133">`ida:Tenant` with your tenant name</span><span class="sxs-lookup"><span data-stu-id="bcb52-133">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="bcb52-134">`ida:ClientId` with your web api application ID</span><span class="sxs-lookup"><span data-stu-id="bcb52-134">`ida:ClientId` with your web api application ID</span></span>
    * <span data-ttu-id="bcb52-135">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span><span class="sxs-lookup"><span data-stu-id="bcb52-135">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="bcb52-136">Open `web.config` in the `TaskWebApp` project and replace the values for</span><span class="sxs-lookup"><span data-stu-id="bcb52-136">Open `web.config` in the `TaskWebApp` project and replace the values for</span></span>

    * <span data-ttu-id="bcb52-137">`ida:Tenant` with your tenant name</span><span class="sxs-lookup"><span data-stu-id="bcb52-137">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="bcb52-138">`ida:ClientId` with your web app application ID</span><span class="sxs-lookup"><span data-stu-id="bcb52-138">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="bcb52-139">`ida:ClientSecret` with your web app secret key</span><span class="sxs-lookup"><span data-stu-id="bcb52-139">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="bcb52-140">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span><span class="sxs-lookup"><span data-stu-id="bcb52-140">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="bcb52-141">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span><span class="sxs-lookup"><span data-stu-id="bcb52-141">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="bcb52-142">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span><span class="sxs-lookup"><span data-stu-id="bcb52-142">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>



## <a name="requesting-and-saving-an-access-token"></a><span data-ttu-id="bcb52-143">Requesting and saving an access token</span><span class="sxs-lookup"><span data-stu-id="bcb52-143">Requesting and saving an access token</span></span>

### <a name="specify-the-permissions"></a><span data-ttu-id="bcb52-144">Specify the permissions</span><span class="sxs-lookup"><span data-stu-id="bcb52-144">Specify the permissions</span></span>

<span data-ttu-id="bcb52-145">In order to make the call to the web API, you need to authenticate the user (using your sign-up/sign-in policy) and [receive an access token](active-directory-b2c-access-tokens.md) from Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="bcb52-145">In order to make the call to the web API, you need to authenticate the user (using your sign-up/sign-in policy) and [receive an access token](active-directory-b2c-access-tokens.md) from Azure AD B2C.</span></span> <span data-ttu-id="bcb52-146">In order to receive an access token, you first must specify the permissions you would like the access token to grant.</span><span class="sxs-lookup"><span data-stu-id="bcb52-146">In order to receive an access token, you first must specify the permissions you would like the access token to grant.</span></span> <span data-ttu-id="bcb52-147">The permissions are specified in the `scope` parameter when you make the request to the `/authorize` endpoint.</span><span class="sxs-lookup"><span data-stu-id="bcb52-147">The permissions are specified in the `scope` parameter when you make the request to the `/authorize` endpoint.</span></span> <span data-ttu-id="bcb52-148">For example, to acquire an access token with the “read” permission to the resource application that has the App ID URI of `https://contoso.onmicrosoft.com/tasks`, the scope would be `https://contoso.onmicrosoft.com/tasks/read`.</span><span class="sxs-lookup"><span data-stu-id="bcb52-148">For example, to acquire an access token with the “read” permission to the resource application that has the App ID URI of `https://contoso.onmicrosoft.com/tasks`, the scope would be `https://contoso.onmicrosoft.com/tasks/read`.</span></span>

<span data-ttu-id="bcb52-149">To specify the scope in our sample, open the file `App_Start\Startup.Auth.cs` and define the `Scope` variable in OpenIdConnectAuthenticationOptions.</span><span class="sxs-lookup"><span data-stu-id="bcb52-149">To specify the scope in our sample, open the file `App_Start\Startup.Auth.cs` and define the `Scope` variable in OpenIdConnectAuthenticationOptions.</span></span>

```CSharp
// App_Start\Startup.Auth.cs

    app.UseOpenIdConnectAuthentication(
        new OpenIdConnectAuthenticationOptions
        {
            ...

            // Specify the scope by appending all of the scopes requested into one string (seperated by a blank space)
            Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
        }
    );
}
```

### <a name="exchange-the-authorization-code-for-an-access-token"></a><span data-ttu-id="bcb52-150">Exchange the authorization code for an access token</span><span class="sxs-lookup"><span data-stu-id="bcb52-150">Exchange the authorization code for an access token</span></span>

<span data-ttu-id="bcb52-151">After an user completes the sign-up or sign-in experience, your app will receive an authorization code from Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="bcb52-151">After an user completes the sign-up or sign-in experience, your app will receive an authorization code from Azure AD B2C.</span></span> <span data-ttu-id="bcb52-152">The OWIN OpenID Connect middleware will store the code, but will not exchange it for an access token.</span><span class="sxs-lookup"><span data-stu-id="bcb52-152">The OWIN OpenID Connect middleware will store the code, but will not exchange it for an access token.</span></span> <span data-ttu-id="bcb52-153">You can use the [MSAL library](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) to make the exchange.</span><span class="sxs-lookup"><span data-stu-id="bcb52-153">You can use the [MSAL library](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) to make the exchange.</span></span> <span data-ttu-id="bcb52-154">In our sample, we configured a notification callback into the OpenID Connect middleware whenever an authorization code is received.</span><span class="sxs-lookup"><span data-stu-id="bcb52-154">In our sample, we configured a notification callback into the OpenID Connect middleware whenever an authorization code is received.</span></span> <span data-ttu-id="bcb52-155">In the callback, we use MSAL to exchange the code for a token and save the token into the cache.</span><span class="sxs-lookup"><span data-stu-id="bcb52-155">In the callback, we use MSAL to exchange the code for a token and save the token into the cache.</span></span>

```CSharp
/*
* Callback function when an authorization code is received
*/
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
    // Extract the code from the response notification
    var code = notification.Code;

    var userObjectId = notification.AuthenticationTicket.Identity.FindFirst(ObjectIdElement).Value;
    var authority = String.Format(AadInstance, Tenant, DefaultPolicy);
    var httpContext = notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase;

    // Exchange the code for a token. Make sure to specify the necessary scopes
    ClientCredential cred = new ClientCredential(ClientSecret);
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                            RedirectUri, cred, new NaiveSessionCache(userObjectId, httpContext));
    var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { ReadTasksScope, WriteTasksScope }, code, DefaultPolicy);
}
```

## <a name="calling-the-web-api"></a><span data-ttu-id="bcb52-156">Calling the web API</span><span class="sxs-lookup"><span data-stu-id="bcb52-156">Calling the web API</span></span>

<span data-ttu-id="bcb52-157">This section discusses how to use the token received during sign-up/sign-in with Azure AD B2C in order to access the web API.</span><span class="sxs-lookup"><span data-stu-id="bcb52-157">This section discusses how to use the token received during sign-up/sign-in with Azure AD B2C in order to access the web API.</span></span>

### <a name="retrieve-the-saved-token-in-the-controllers"></a><span data-ttu-id="bcb52-158">Retrieve the saved token in the controllers</span><span class="sxs-lookup"><span data-stu-id="bcb52-158">Retrieve the saved token in the controllers</span></span>

<span data-ttu-id="bcb52-159">The `TasksController` is responsible for communicating with the web API and for sending HTTP requests to the API to read, create, and delete tasks.</span><span class="sxs-lookup"><span data-stu-id="bcb52-159">The `TasksController` is responsible for communicating with the web API and for sending HTTP requests to the API to read, create, and delete tasks.</span></span> <span data-ttu-id="bcb52-160">Because the API is secured by Azure AD B2C, you need to first retrieve the token you saved in the above step.</span><span class="sxs-lookup"><span data-stu-id="bcb52-160">Because the API is secured by Azure AD B2C, you need to first retrieve the token you saved in the above step.</span></span>

```CSharp
// Controllers\TasksController.cs

/*
* Uses MSAL to retrieve the token from the cache
*/
private async void acquireToken(String[] scope)
{
    string userObjectID = ClaimsPrincipal.Current.FindFirst(Startup.ObjectIdElement).Value;
    string authority = String.Format(Startup.AadInstance, Startup.Tenant, Startup.DefaultPolicy);

    ClientCredential credential = new ClientCredential(Startup.ClientSecret);

    // Retrieve the token using the provided scopes
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                        Startup.RedirectUri, credential,
                                        new NaiveSessionCache(userObjectID, this.HttpContext));
    AuthenticationResult result = await app.AcquireTokenSilentAsync(scope);

    accessToken = result.Token;
}
```

### <a name="read-tasks-from-the-web-api"></a><span data-ttu-id="bcb52-161">Read tasks from the web API</span><span class="sxs-lookup"><span data-stu-id="bcb52-161">Read tasks from the web API</span></span>

<span data-ttu-id="bcb52-162">When you have a token, you can attach it to the HTTP `GET` request in the `Authorization` header to securely call `TaskService`:</span><span class="sxs-lookup"><span data-stu-id="bcb52-162">When you have a token, you can attach it to the HTTP `GET` request in the `Authorization` header to securely call `TaskService`:</span></span>

```CSharp
// Controllers\TasksController.cs

public async Task<ActionResult> Index()
{
    try {

        // Retrieve the token with the specified scopes
        acquireToken(new string[] { Startup.ReadTasksScope });

        HttpClient client = new HttpClient();
        HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, apiEndpoint);

        // Add token to the Authorization header and make the request
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", accessToken);
        HttpResponseMessage response = await client.SendAsync(request);

        // Handle response ...
}

```

### <a name="create-and-delete-tasks-on-the-web-api"></a><span data-ttu-id="bcb52-163">Create and delete tasks on the web API</span><span class="sxs-lookup"><span data-stu-id="bcb52-163">Create and delete tasks on the web API</span></span>

<span data-ttu-id="bcb52-164">Follow the same pattern when you send `POST` and `DELETE` requests to the web API, using MSAL to retrieve the access token from the cache.</span><span class="sxs-lookup"><span data-stu-id="bcb52-164">Follow the same pattern when you send `POST` and `DELETE` requests to the web API, using MSAL to retrieve the access token from the cache.</span></span>

## <a name="run-the-sample-app"></a><span data-ttu-id="bcb52-165">Run the sample app</span><span class="sxs-lookup"><span data-stu-id="bcb52-165">Run the sample app</span></span>

<span data-ttu-id="bcb52-166">Finally, build and run both the apps.</span><span class="sxs-lookup"><span data-stu-id="bcb52-166">Finally, build and run both the apps.</span></span> <span data-ttu-id="bcb52-167">Sign up and sign in, and create tasks for the signed-in user.</span><span class="sxs-lookup"><span data-stu-id="bcb52-167">Sign up and sign in, and create tasks for the signed-in user.</span></span> <span data-ttu-id="bcb52-168">Sign out and sign in as a different user.</span><span class="sxs-lookup"><span data-stu-id="bcb52-168">Sign out and sign in as a different user.</span></span> <span data-ttu-id="bcb52-169">Create tasks for that user.</span><span class="sxs-lookup"><span data-stu-id="bcb52-169">Create tasks for that user.</span></span> <span data-ttu-id="bcb52-170">Notice how the tasks are stored per-user on the API, because the API extracts the user's identity from the token it receives.</span><span class="sxs-lookup"><span data-stu-id="bcb52-170">Notice how the tasks are stored per-user on the API, because the API extracts the user's identity from the token it receives.</span></span> <span data-ttu-id="bcb52-171">Also try playing with the scopes.</span><span class="sxs-lookup"><span data-stu-id="bcb52-171">Also try playing with the scopes.</span></span> <span data-ttu-id="bcb52-172">Remove the permission to "write" and then try adding a task.</span><span class="sxs-lookup"><span data-stu-id="bcb52-172">Remove the permission to "write" and then try adding a task.</span></span> <span data-ttu-id="bcb52-173">Just make sure to sign out each time you change the scope.</span><span class="sxs-lookup"><span data-stu-id="bcb52-173">Just make sure to sign out each time you change the scope.</span></span>

