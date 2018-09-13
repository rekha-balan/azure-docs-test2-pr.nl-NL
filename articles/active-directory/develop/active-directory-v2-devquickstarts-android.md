---
title: Azure Active Directory v2.0 Android app | Microsoft Docs
description: How to build an Android app that signs in users with both personal Microsoft account and work or school accounts and calls the Graph API by using third party libraries.
services: active-directory
documentationcenter: ''
author: xerners
manager: mbaldwin
editor: ''
ms.assetid: 16294c07-f27d-45c9-833f-7dbb12083794
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: xerners
ms.openlocfilehash: 135b8d5a931215130a411842dab0964f77ee1dd0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563744"
---
# <a name="add-sign-in-to-an-android-app-using-a-third-party-library-with-graph-api-using-the-v20-endpoint"></a><span data-ttu-id="40f48-103">Add sign-in to an Android app using a third-party library with Graph API using the v2.0 endpoint</span><span class="sxs-lookup"><span data-stu-id="40f48-103">Add sign-in to an Android app using a third-party library with Graph API using the v2.0 endpoint</span></span>
<span data-ttu-id="40f48-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="40f48-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="40f48-105">Developers can use any library they want to integrate with our services.</span><span class="sxs-lookup"><span data-stu-id="40f48-105">Developers can use any library they want to integrate with our services.</span></span> <span data-ttu-id="40f48-106">To help developers use our platform with other libraries, we've written a few walkthroughs like this one to demonstrate how to configure third-party libraries to connect to the Microsoft identity platform.</span><span class="sxs-lookup"><span data-stu-id="40f48-106">To help developers use our platform with other libraries, we've written a few walkthroughs like this one to demonstrate how to configure third-party libraries to connect to the Microsoft identity platform.</span></span> <span data-ttu-id="40f48-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect to the Microsoft identity platform.</span><span class="sxs-lookup"><span data-stu-id="40f48-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect to the Microsoft identity platform.</span></span>

<span data-ttu-id="40f48-108">With the application that this walkthrough creates, users can sign in to their organization and then search for themselves in their organization by using the Graph API.</span><span class="sxs-lookup"><span data-stu-id="40f48-108">With the application that this walkthrough creates, users can sign in to their organization and then search for themselves in their organization by using the Graph API.</span></span>

<span data-ttu-id="40f48-109">If you're new to OAuth2 or OpenID Connect, much of this sample configuration may not make sense to you.</span><span class="sxs-lookup"><span data-stu-id="40f48-109">If you're new to OAuth2 or OpenID Connect, much of this sample configuration may not make sense to you.</span></span> <span data-ttu-id="40f48-110">We recommend that you read [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span><span class="sxs-lookup"><span data-stu-id="40f48-110">We recommend that you read [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="40f48-111">Some features of our platform that do have an expression in the OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you to use our open source Microsoft Azure Identity Libraries.</span><span class="sxs-lookup"><span data-stu-id="40f48-111">Some features of our platform that do have an expression in the OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you to use our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="40f48-112">The v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span><span class="sxs-lookup"><span data-stu-id="40f48-112">The v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="40f48-113">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="40f48-113">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-the-code-from-github"></a><span data-ttu-id="40f48-114">Download the code from GitHub</span><span class="sxs-lookup"><span data-stu-id="40f48-114">Download the code from GitHub</span></span>
<span data-ttu-id="40f48-115">The code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span><span class="sxs-lookup"><span data-stu-id="40f48-115">The code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span></span>  <span data-ttu-id="40f48-116">To follow along, you can  [download the app's skeleton as a .zip](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) or clone the skeleton:</span><span class="sxs-lookup"><span data-stu-id="40f48-116">To follow along, you can  [download the app's skeleton as a .zip](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) or clone the skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

<span data-ttu-id="40f48-117">You can also just download the sample and get started right away:</span><span class="sxs-lookup"><span data-stu-id="40f48-117">You can also just download the sample and get started right away:</span></span>

```
git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="40f48-118">Register an app</span><span class="sxs-lookup"><span data-stu-id="40f48-118">Register an app</span></span>
<span data-ttu-id="40f48-119">Create a new app at the [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow the detailed steps at [How to register an app with the v2.0 endpoint](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="40f48-119">Create a new app at the [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow the detailed steps at [How to register an app with the v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="40f48-120">Make sure to:</span><span class="sxs-lookup"><span data-stu-id="40f48-120">Make sure to:</span></span>

* <span data-ttu-id="40f48-121">Copy the **Application Id** that's assigned to your app because you'll need it soon.</span><span class="sxs-lookup"><span data-stu-id="40f48-121">Copy the **Application Id** that's assigned to your app because you'll need it soon.</span></span>
* <span data-ttu-id="40f48-122">Add the **Mobile** platform for your app.</span><span class="sxs-lookup"><span data-stu-id="40f48-122">Add the **Mobile** platform for your app.</span></span>

> <span data-ttu-id="40f48-123">Note: The Application registration portal provides a **Redirect URI** value.</span><span class="sxs-lookup"><span data-stu-id="40f48-123">Note: The Application registration portal provides a **Redirect URI** value.</span></span> <span data-ttu-id="40f48-124">However, in this example you must use the default value of `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span><span class="sxs-lookup"><span data-stu-id="40f48-124">However, in this example you must use the default value of `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span></span>
> 
> 

## <a name="download-the-nxoauth2-third-party-library-and-create-a-workspace"></a><span data-ttu-id="40f48-125">Download the NXOAuth2 third-party library and create a workspace</span><span class="sxs-lookup"><span data-stu-id="40f48-125">Download the NXOAuth2 third-party library and create a workspace</span></span>
<span data-ttu-id="40f48-126">For this walkthrough, you will use the OIDCAndroidLib from GitHub, which is an OAuth2 library based on the OpenID Connect code of Google.</span><span class="sxs-lookup"><span data-stu-id="40f48-126">For this walkthrough, you will use the OIDCAndroidLib from GitHub, which is an OAuth2 library based on the OpenID Connect code of Google.</span></span> <span data-ttu-id="40f48-127">It implements the native application profile and supports the authorization endpoint of the user.</span><span class="sxs-lookup"><span data-stu-id="40f48-127">It implements the native application profile and supports the authorization endpoint of the user.</span></span> <span data-ttu-id="40f48-128">These are all the things that you'll need to integrate with the Microsoft identity platform.</span><span class="sxs-lookup"><span data-stu-id="40f48-128">These are all the things that you'll need to integrate with the Microsoft identity platform.</span></span>

<span data-ttu-id="40f48-129">Clone the OIDCAndroidLib repo to your computer.</span><span class="sxs-lookup"><span data-stu-id="40f48-129">Clone the OIDCAndroidLib repo to your computer.</span></span>

```
git@github.com:kalemontes/OIDCAndroidLib.git
```

![androidStudio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-android-native-oidcandroidlib-v2/emotes-url.png)

## <a name="set-up-your-android-studio-environment"></a><span data-ttu-id="40f48-131">Set up your Android Studio environment</span><span class="sxs-lookup"><span data-stu-id="40f48-131">Set up your Android Studio environment</span></span>
1. <span data-ttu-id="40f48-132">Create a new Android Studio project and accept the defaults in the wizard.</span><span class="sxs-lookup"><span data-stu-id="40f48-132">Create a new Android Studio project and accept the defaults in the wizard.</span></span>
   
    ![Create new project in Android Studio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-android-native-oidcandroidlib-v2/SetUpSample1.PNG)
   
    ![Target Android devices](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-android-native-oidcandroidlib-v2/SetUpSample2.PNG)
   
    ![Add an activity to mobile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-android-native-oidcandroidlib-v2/SetUpSample3.PNG)
2. <span data-ttu-id="40f48-136">To set up your project modules, move the cloned repo to the project location.</span><span class="sxs-lookup"><span data-stu-id="40f48-136">To set up your project modules, move the cloned repo to the project location.</span></span> <span data-ttu-id="40f48-137">You can also create the project and then clone it directly to the project location.</span><span class="sxs-lookup"><span data-stu-id="40f48-137">You can also create the project and then clone it directly to the project location.</span></span>
   
    ![Project modules](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4_1.PNG)
3. <span data-ttu-id="40f48-139">Open the project modules settings by using the context menu or by using the Ctrl+Alt+Maj+S shortcut.</span><span class="sxs-lookup"><span data-stu-id="40f48-139">Open the project modules settings by using the context menu or by using the Ctrl+Alt+Maj+S shortcut.</span></span>
   
    ![Project modules settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4.PNG)
4. <span data-ttu-id="40f48-141">Remove the default app module because you only want the project container settings.</span><span class="sxs-lookup"><span data-stu-id="40f48-141">Remove the default app module because you only want the project container settings.</span></span>
   
    ![The default app module](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-android-native-oidcandroidlib-v2/SetUpSample5.PNG)
5. <span data-ttu-id="40f48-143">Import modules from the cloned repo to the current project.</span><span class="sxs-lookup"><span data-stu-id="40f48-143">Import modules from the cloned repo to the current project.</span></span>
   
    <span data-ttu-id="40f48-144">![Import gradle project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![Create new module page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span><span class="sxs-lookup"><span data-stu-id="40f48-144">![Import gradle project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![Create new module page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span></span>
6. <span data-ttu-id="40f48-145">Repeat these steps for the `oidlib-sample` module.</span><span class="sxs-lookup"><span data-stu-id="40f48-145">Repeat these steps for the `oidlib-sample` module.</span></span>
7. <span data-ttu-id="40f48-146">Check the oidclib dependencies on the `oidlib-sample` module.</span><span class="sxs-lookup"><span data-stu-id="40f48-146">Check the oidclib dependencies on the `oidlib-sample` module.</span></span>
   
    ![oidclib dependencies on the oidlib-sample module](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8.PNG)
8. <span data-ttu-id="40f48-148">Click **OK** and wait for gradle sync.</span><span class="sxs-lookup"><span data-stu-id="40f48-148">Click **OK** and wait for gradle sync.</span></span>
   
    <span data-ttu-id="40f48-149">Your settings.gradle should look like:</span><span class="sxs-lookup"><span data-stu-id="40f48-149">Your settings.gradle should look like:</span></span>
   
    ![Screenshot of settings.gradle](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8_1.PNG)
9. <span data-ttu-id="40f48-151">Build the sample app to make sure that the sample running correctly.</span><span class="sxs-lookup"><span data-stu-id="40f48-151">Build the sample app to make sure that the sample running correctly.</span></span>
   
    <span data-ttu-id="40f48-152">You won't be able to use this with Azure Active Directory yet.</span><span class="sxs-lookup"><span data-stu-id="40f48-152">You won't be able to use this with Azure Active Directory yet.</span></span> <span data-ttu-id="40f48-153">We'll need to configure some endpoints first.</span><span class="sxs-lookup"><span data-stu-id="40f48-153">We'll need to configure some endpoints first.</span></span> <span data-ttu-id="40f48-154">This is to ensure you don't have an Android Studio issues before we start customizing the sample app.</span><span class="sxs-lookup"><span data-stu-id="40f48-154">This is to ensure you don't have an Android Studio issues before we start customizing the sample app.</span></span>
10. <span data-ttu-id="40f48-155">Build and run `oidlib-sample` as the target in Android Studio.</span><span class="sxs-lookup"><span data-stu-id="40f48-155">Build and run `oidlib-sample` as the target in Android Studio.</span></span>
    
    ![Progress of oidlib-sample build](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-android-native-oidcandroidlib-v2/SetUpSample9.png)
11. <span data-ttu-id="40f48-157">Delete the `app ` directory that was left when you removed the module from the project because Android Studio doesn't delete it for safety.</span><span class="sxs-lookup"><span data-stu-id="40f48-157">Delete the `app ` directory that was left when you removed the module from the project because Android Studio doesn't delete it for safety.</span></span>
    
    ![File structure that includes the app directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-android-native-oidcandroidlib-v2/SetUpSample12.PNG)
12. <span data-ttu-id="40f48-159">Open the **Edit Configurations** menu to remove the run configuration that was also left when you removed the module from the project.</span><span class="sxs-lookup"><span data-stu-id="40f48-159">Open the **Edit Configurations** menu to remove the run configuration that was also left when you removed the module from the project.</span></span>
    
    <span data-ttu-id="40f48-160">![Edit configurations menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
    ![Run configuration of app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span><span class="sxs-lookup"><span data-stu-id="40f48-160">![Edit configurations menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
![Run configuration of app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span></span>

## <a name="configure-the-endpoints-of-the-sample"></a><span data-ttu-id="40f48-161">Configure the endpoints of the sample</span><span class="sxs-lookup"><span data-stu-id="40f48-161">Configure the endpoints of the sample</span></span>
<span data-ttu-id="40f48-162">Now that you have the `oidlib-sample` running successfully, let's edit some endpoints to get this working with Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="40f48-162">Now that you have the `oidlib-sample` running successfully, let's edit some endpoints to get this working with Azure Active Directory.</span></span>

### <a name="configure-your-client-by-editing-the-oidcclientconfxml-file"></a><span data-ttu-id="40f48-163">Configure your client by editing the oidc_clientconf.xml file</span><span class="sxs-lookup"><span data-stu-id="40f48-163">Configure your client by editing the oidc_clientconf.xml file</span></span>
1. <span data-ttu-id="40f48-164">Because you are using OAuth2 flows only to get a token and call the Graph API, set the client to do OAuth2 only.</span><span class="sxs-lookup"><span data-stu-id="40f48-164">Because you are using OAuth2 flows only to get a token and call the Graph API, set the client to do OAuth2 only.</span></span> <span data-ttu-id="40f48-165">OIDC will come in a later example.</span><span class="sxs-lookup"><span data-stu-id="40f48-165">OIDC will come in a later example.</span></span>
   
    ```xml
        <bool name="oidc_oauth2only">true</bool>
    ```
2. <span data-ttu-id="40f48-166">Configure your client ID that you received from the registration portal.</span><span class="sxs-lookup"><span data-stu-id="40f48-166">Configure your client ID that you received from the registration portal.</span></span>
   
    ```xml
        <string name="oidc_clientId">86172f9d-a1ae-4348-aafa-7b3e5d1b36f5</string>
        <string name="oidc_clientSecret"></string>
    ```
3. <span data-ttu-id="40f48-167">Configure your redirect URI with the one below.</span><span class="sxs-lookup"><span data-stu-id="40f48-167">Configure your redirect URI with the one below.</span></span>
   
    ```xml
        <string name="oidc_redirectUrl">https://login.microsoftonline.com/common/oauth2/nativeclient</string>
    ```
4. <span data-ttu-id="40f48-168">Configure your scopes that you need in order to access the Graph API.</span><span class="sxs-lookup"><span data-stu-id="40f48-168">Configure your scopes that you need in order to access the Graph API.</span></span>
   
    ```xml
        <string-array name="oidc_scopes">
            <item>openid</item>
            <item>https://graph.microsoft.com/User.Read</item>
            <item>offline_access</item>
        </string-array>
    ```

<span data-ttu-id="40f48-169">The `User.Read` value in `oidc_scopes` allows you to read the basic profile the signed in user.</span><span class="sxs-lookup"><span data-stu-id="40f48-169">The `User.Read` value in `oidc_scopes` allows you to read the basic profile the signed in user.</span></span>
<span data-ttu-id="40f48-170">You can learn more about all the available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span><span class="sxs-lookup"><span data-stu-id="40f48-170">You can learn more about all the available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="40f48-171">If you'd like explanations about `openid` or `offline_access` as scopes in OpenID Connect, see [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="40f48-171">If you'd like explanations about `openid` or `offline_access` as scopes in OpenID Connect, see [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md).</span></span>

### <a name="configure-your-client-endpoints-by-editing-the-oidcendpointsxml-file"></a><span data-ttu-id="40f48-172">Configure your client endpoints by editing the oidc_endpoints.xml file</span><span class="sxs-lookup"><span data-stu-id="40f48-172">Configure your client endpoints by editing the oidc_endpoints.xml file</span></span>
* <span data-ttu-id="40f48-173">Open the `oidc_endpoints.xml` file and make the following changes:</span><span class="sxs-lookup"><span data-stu-id="40f48-173">Open the `oidc_endpoints.xml` file and make the following changes:</span></span>
  
    ```xml
    <!-- Stores OpenID Connect provider endpoints. -->
    <resources>
        <string name="op_authorizationEnpoint">https://login.microsoftonline.com/common/oauth2/v2.0/authorize</string>
        <string name="op_tokenEndpoint">https://login.microsoftonline.com/common/oauth2/v2.0/token</string>
        <string name="op_userInfoEndpoint">https://www.example.com/oauth2/userinfo</string>
        <string name="op_revocationEndpoint">https://www.example.com/oauth2/revoketoken</string>
    </resources>
    ```

<span data-ttu-id="40f48-174">These endpoints should never change if you are using OAuth2 as your protocol.</span><span class="sxs-lookup"><span data-stu-id="40f48-174">These endpoints should never change if you are using OAuth2 as your protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="40f48-175">The endpoints for `userInfoEndpoint` and `revocationEndpoint` are currently not supported by Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="40f48-175">The endpoints for `userInfoEndpoint` and `revocationEndpoint` are currently not supported by Azure Active Directory.</span></span> <span data-ttu-id="40f48-176">If you leave these with the default example.com value, you will be reminded that they are not available in the sample :-)</span><span class="sxs-lookup"><span data-stu-id="40f48-176">If you leave these with the default example.com value, you will be reminded that they are not available in the sample :-)</span></span>
> 
> 

## <a name="configure-a-graph-api-call"></a><span data-ttu-id="40f48-177">Configure a Graph API call</span><span class="sxs-lookup"><span data-stu-id="40f48-177">Configure a Graph API call</span></span>
* <span data-ttu-id="40f48-178">Open the `HomeActivity.java` file and make the following changes:</span><span class="sxs-lookup"><span data-stu-id="40f48-178">Open the `HomeActivity.java` file and make the following changes:</span></span>
  
    ```Java
       //TODO: set your protected resource url
        private static final String protectedResUrl = "https://graph.microsoft.com/v1.0/me/";
    ```

<span data-ttu-id="40f48-179">Here a simple Graph API call returns our information.</span><span class="sxs-lookup"><span data-stu-id="40f48-179">Here a simple Graph API call returns our information.</span></span>

<span data-ttu-id="40f48-180">Those are all the changes that you need to do.</span><span class="sxs-lookup"><span data-stu-id="40f48-180">Those are all the changes that you need to do.</span></span> <span data-ttu-id="40f48-181">Run the `oidlib-sample` application, and click **Sign in**.</span><span class="sxs-lookup"><span data-stu-id="40f48-181">Run the `oidlib-sample` application, and click **Sign in**.</span></span>

<span data-ttu-id="40f48-182">After you've successfully authenticated, select the **Request Protected Resource** button to test your call to the Graph API.</span><span class="sxs-lookup"><span data-stu-id="40f48-182">After you've successfully authenticated, select the **Request Protected Resource** button to test your call to the Graph API.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="40f48-183">Get security updates for our product</span><span class="sxs-lookup"><span data-stu-id="40f48-183">Get security updates for our product</span></span>
<span data-ttu-id="40f48-184">We encourage you to get notifications about security incidents by visiting the [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span><span class="sxs-lookup"><span data-stu-id="40f48-184">We encourage you to get notifications about security incidents by visiting the [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>
















