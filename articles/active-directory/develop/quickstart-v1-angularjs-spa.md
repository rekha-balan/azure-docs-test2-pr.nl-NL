---
title: Azure AD AngularJS Getting Started | Microsoft Docs
description: How to build an AngularJS single-page application that integrates with Azure AD for sign-in and calls Azure AD-protected APIs by using OAuth.
services: active-directory
documentationcenter: ''
author: CelesteDG
manager: mtillman
editor: ''
ms.assetid: f2991054-8146-4718-a5f7-59b892230ad7
ms.service: active-directory
ms.component: develop
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 11/30/2017
ms.author: celested
ms.reviewer: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 0c7f6a0e447e3b48cdd1df684dc105ece1e98f66
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856771"
---
# <a name="azure-ad-angularjs-getting-started"></a><span data-ttu-id="43db0-103">Azure AD AngularJS getting started</span><span class="sxs-lookup"><span data-stu-id="43db0-103">Azure AD AngularJS getting started</span></span>

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="43db0-104">Azure Active Directory (Azure AD) makes it simple and straightforward for you to add sign-in, sign-out, and secure OAuth API calls to your single-page apps.</span><span class="sxs-lookup"><span data-stu-id="43db0-104">Azure Active Directory (Azure AD) makes it simple and straightforward for you to add sign-in, sign-out, and secure OAuth API calls to your single-page apps.</span></span> <span data-ttu-id="43db0-105">It enables your apps to authenticate users with their Windows Server Active Directory accounts and consume any web API that Azure AD helps protect, such as the Office 365 APIs or the Azure API.</span><span class="sxs-lookup"><span data-stu-id="43db0-105">It enables your apps to authenticate users with their Windows Server Active Directory accounts and consume any web API that Azure AD helps protect, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="43db0-106">For JavaScript applications running in a browser, Azure AD provides the Active Directory Authentication Library (ADAL), or adal.js.</span><span class="sxs-lookup"><span data-stu-id="43db0-106">For JavaScript applications running in a browser, Azure AD provides the Active Directory Authentication Library (ADAL), or adal.js.</span></span> <span data-ttu-id="43db0-107">The sole purpose of adal.js is to make it easy for your app to get access tokens.</span><span class="sxs-lookup"><span data-stu-id="43db0-107">The sole purpose of adal.js is to make it easy for your app to get access tokens.</span></span> <span data-ttu-id="43db0-108">To demonstrate just how easy it is, here we'll build an AngularJS To Do List application that:</span><span class="sxs-lookup"><span data-stu-id="43db0-108">To demonstrate just how easy it is, here we'll build an AngularJS To Do List application that:</span></span>

* <span data-ttu-id="43db0-109">Signs the user in to the app by using Azure AD as the identity provider.</span><span class="sxs-lookup"><span data-stu-id="43db0-109">Signs the user in to the app by using Azure AD as the identity provider.</span></span>

* <span data-ttu-id="43db0-110">Displays some information about the user.</span><span class="sxs-lookup"><span data-stu-id="43db0-110">Displays some information about the user.</span></span>
* <span data-ttu-id="43db0-111">Securely calls the app's To Do List API by using bearer tokens from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="43db0-111">Securely calls the app's To Do List API by using bearer tokens from Azure AD.</span></span>
* <span data-ttu-id="43db0-112">Signs the user out of the app.</span><span class="sxs-lookup"><span data-stu-id="43db0-112">Signs the user out of the app.</span></span>

<span data-ttu-id="43db0-113">To build the complete, working application, you need to:</span><span class="sxs-lookup"><span data-stu-id="43db0-113">To build the complete, working application, you need to:</span></span>

1. <span data-ttu-id="43db0-114">Register your app with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="43db0-114">Register your app with Azure AD.</span></span>
2. <span data-ttu-id="43db0-115">Install ADAL and configure the single-page app.</span><span class="sxs-lookup"><span data-stu-id="43db0-115">Install ADAL and configure the single-page app.</span></span>
3. <span data-ttu-id="43db0-116">Use ADAL to help secure pages in the single-page app.</span><span class="sxs-lookup"><span data-stu-id="43db0-116">Use ADAL to help secure pages in the single-page app.</span></span>

<span data-ttu-id="43db0-117">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="43db0-117">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="43db0-118">You also need an Azure AD tenant in which you can create users and register an application.</span><span class="sxs-lookup"><span data-stu-id="43db0-118">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="43db0-119">If you don't already have a tenant, [learn how to get one](quickstart-create-new-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="43db0-119">If you don't already have a tenant, [learn how to get one](quickstart-create-new-tenant.md).</span></span>

## <a name="step-1-register-the-directorysearcher-application"></a><span data-ttu-id="43db0-120">Step 1: Register the DirectorySearcher application</span><span class="sxs-lookup"><span data-stu-id="43db0-120">Step 1: Register the DirectorySearcher application</span></span>
<span data-ttu-id="43db0-121">To enable your app to authenticate users and get tokens, you first need to register it in your Azure AD tenant:</span><span class="sxs-lookup"><span data-stu-id="43db0-121">To enable your app to authenticate users and get tokens, you first need to register it in your Azure AD tenant:</span></span>

1. <span data-ttu-id="43db0-122">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="43db0-122">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="43db0-123">If you are signed in to multiple directories, you may need to ensure you are viewing the correct directory.</span><span class="sxs-lookup"><span data-stu-id="43db0-123">If you are signed in to multiple directories, you may need to ensure you are viewing the correct directory.</span></span> <span data-ttu-id="43db0-124">To do so, on the top bar, click your account.</span><span class="sxs-lookup"><span data-stu-id="43db0-124">To do so, on the top bar, click your account.</span></span> <span data-ttu-id="43db0-125">Under the **Directory** list, choose the Azure AD tenant where you want to register your application.</span><span class="sxs-lookup"><span data-stu-id="43db0-125">Under the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="43db0-126">Click **All services** in the left pane, and then select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="43db0-126">Click **All services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="43db0-127">Click **App registrations**, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="43db0-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="43db0-128">Follow the prompts and create a new web application and/or web API:</span><span class="sxs-lookup"><span data-stu-id="43db0-128">Follow the prompts and create a new web application and/or web API:</span></span>
  * <span data-ttu-id="43db0-129">**Name** describes your application to users.</span><span class="sxs-lookup"><span data-stu-id="43db0-129">**Name** describes your application to users.</span></span>
  * <span data-ttu-id="43db0-130">**Sign-on URL** is the location to which Azure AD will return tokens.</span><span class="sxs-lookup"><span data-stu-id="43db0-130">**Sign-on URL** is the location to which Azure AD will return tokens.</span></span> <span data-ttu-id="43db0-131">The default location for this sample is `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="43db0-131">The default location for this sample is `https://localhost:44326/`.</span></span>
6. <span data-ttu-id="43db0-132">After you finish registration, Azure AD assigns a unique application ID to your app.</span><span class="sxs-lookup"><span data-stu-id="43db0-132">After you finish registration, Azure AD assigns a unique application ID to your app.</span></span> <span data-ttu-id="43db0-133">You'll need this value in the next sections, so copy it from the application tab.</span><span class="sxs-lookup"><span data-stu-id="43db0-133">You'll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="43db0-134">Adal.js uses the OAuth implicit flow to communicate with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="43db0-134">Adal.js uses the OAuth implicit flow to communicate with Azure AD.</span></span> <span data-ttu-id="43db0-135">You must enable the implicit flow for your application:</span><span class="sxs-lookup"><span data-stu-id="43db0-135">You must enable the implicit flow for your application:</span></span>
  1. <span data-ttu-id="43db0-136">Click the application and select **Manifest** to open the inline manifest editor.</span><span class="sxs-lookup"><span data-stu-id="43db0-136">Click the application and select **Manifest** to open the inline manifest editor.</span></span>
  2. <span data-ttu-id="43db0-137">Locate the `oauth2AllowImplicitFlow` property.</span><span class="sxs-lookup"><span data-stu-id="43db0-137">Locate the `oauth2AllowImplicitFlow` property.</span></span> <span data-ttu-id="43db0-138">Set its value to `true`.</span><span class="sxs-lookup"><span data-stu-id="43db0-138">Set its value to `true`.</span></span>
  3. <span data-ttu-id="43db0-139">Click **Save** to save the manifest.</span><span class="sxs-lookup"><span data-stu-id="43db0-139">Click **Save** to save the manifest.</span></span>
8. <span data-ttu-id="43db0-140">Grant permissions across your tenant for your application.</span><span class="sxs-lookup"><span data-stu-id="43db0-140">Grant permissions across your tenant for your application.</span></span> <span data-ttu-id="43db0-141">Go to **Settings** > **Required Permissions**, and click the **Grant Permissions** button on the top bar.</span><span class="sxs-lookup"><span data-stu-id="43db0-141">Go to **Settings** > **Required Permissions**, and click the **Grant Permissions** button on the top bar.</span></span> <span data-ttu-id="43db0-142">Click **Yes** to confirm.</span><span class="sxs-lookup"><span data-stu-id="43db0-142">Click **Yes** to confirm.</span></span>

## <a name="step-2-install-adal-and-configure-the-single-page-app"></a><span data-ttu-id="43db0-143">Step 2: Install ADAL and configure the single-page app</span><span class="sxs-lookup"><span data-stu-id="43db0-143">Step 2: Install ADAL and configure the single-page app</span></span>
<span data-ttu-id="43db0-144">Now that you have an application in Azure AD, you can install adal.js and write your identity-related code.</span><span class="sxs-lookup"><span data-stu-id="43db0-144">Now that you have an application in Azure AD, you can install adal.js and write your identity-related code.</span></span>

### <a name="configure-the-javascript-client"></a><span data-ttu-id="43db0-145">Configure the JavaScript client</span><span class="sxs-lookup"><span data-stu-id="43db0-145">Configure the JavaScript client</span></span>
<span data-ttu-id="43db0-146">Begin by adding adal.js to the TodoSPA project by using the Package Manager Console:</span><span class="sxs-lookup"><span data-stu-id="43db0-146">Begin by adding adal.js to the TodoSPA project by using the Package Manager Console:</span></span>
  1. <span data-ttu-id="43db0-147">Download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) and add it to the `App/Scripts/` project directory.</span><span class="sxs-lookup"><span data-stu-id="43db0-147">Download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) and add it to the `App/Scripts/` project directory.</span></span>
  2. <span data-ttu-id="43db0-148">Download [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) and add it to the `App/Scripts/` project directory.</span><span class="sxs-lookup"><span data-stu-id="43db0-148">Download [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) and add it to the `App/Scripts/` project directory.</span></span>
  3. <span data-ttu-id="43db0-149">Load each script before the end of the `</body>` in `index.html`:</span><span class="sxs-lookup"><span data-stu-id="43db0-149">Load each script before the end of the `</body>` in `index.html`:</span></span>

    ```js
    ...
    <script src="App/Scripts/adal.js"></script>
    <script src="App/Scripts/adal-angular.js"></script>
    ...
    ```

### <a name="configure-the-back-end-server"></a><span data-ttu-id="43db0-150">Configure the back end server</span><span class="sxs-lookup"><span data-stu-id="43db0-150">Configure the back end server</span></span>
<span data-ttu-id="43db0-151">For the single-page app's back-end To Do List API to accept tokens from the browser, the back end needs configuration information about the app registration.</span><span class="sxs-lookup"><span data-stu-id="43db0-151">For the single-page app's back-end To Do List API to accept tokens from the browser, the back end needs configuration information about the app registration.</span></span> <span data-ttu-id="43db0-152">In the TodoSPA project, open `web.config`.</span><span class="sxs-lookup"><span data-stu-id="43db0-152">In the TodoSPA project, open `web.config`.</span></span> <span data-ttu-id="43db0-153">Replace the values of the elements in the `<appSettings>` section to reflect the values that you used in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="43db0-153">Replace the values of the elements in the `<appSettings>` section to reflect the values that you used in the Azure portal.</span></span> <span data-ttu-id="43db0-154">Your code will reference these values whenever it uses ADAL.</span><span class="sxs-lookup"><span data-stu-id="43db0-154">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="43db0-155">`ida:Tenant` is the domain of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="43db0-155">`ida:Tenant` is the domain of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="43db0-156">`ida:Audience` is the client ID of your application that you copied from the portal.</span><span class="sxs-lookup"><span data-stu-id="43db0-156">`ida:Audience` is the client ID of your application that you copied from the portal.</span></span>

## <a name="step-3-use-adal-to-help-secure-pages-in-the-single-page-app"></a><span data-ttu-id="43db0-157">Step 3: Use ADAL to help secure pages in the single-page app</span><span class="sxs-lookup"><span data-stu-id="43db0-157">Step 3: Use ADAL to help secure pages in the single-page app</span></span>
<span data-ttu-id="43db0-158">Adal.js integrates with AngularJS route and HTTP providers, so you can help secure individual views in your single-page app.</span><span class="sxs-lookup"><span data-stu-id="43db0-158">Adal.js integrates with AngularJS route and HTTP providers, so you can help secure individual views in your single-page app.</span></span>

1. <span data-ttu-id="43db0-159">In `App/Scripts/app.js`, bring in the adal.js module:</span><span class="sxs-lookup"><span data-stu-id="43db0-159">In `App/Scripts/app.js`, bring in the adal.js module:</span></span>

    ```js
    angular.module('todoApp', ['ngRoute','AdalAngular'])
    .config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
     function ($routeProvider, $httpProvider, adalProvider) {
    ...
    ```
2. <span data-ttu-id="43db0-160">Initialize `adalProvider` by using the configuration values of your application registration, also in `App/Scripts/app.js`:</span><span class="sxs-lookup"><span data-stu-id="43db0-160">Initialize `adalProvider` by using the configuration values of your application registration, also in `App/Scripts/app.js`:</span></span>

    ```js
    adalProvider.init(
      {
          instance: 'https://login.microsoftonline.com/',
          tenant: 'Enter your tenant name here e.g. contoso.onmicrosoft.com',
          clientId: 'Enter your client ID here e.g. e9a5a8b6-8af7-4719-9821-0deef255f68e',
          extraQueryParameter: 'nux=1',
          //cacheLocation: 'localStorage', // enable this for IE, as sessionStorage does not work for localhost.
      },
      $httpProvider
    );
    ```
3. <span data-ttu-id="43db0-161">Help secure the `TodoList` view in the app by using only one line of code: `requireADLogin`.</span><span class="sxs-lookup"><span data-stu-id="43db0-161">Help secure the `TodoList` view in the app by using only one line of code: `requireADLogin`.</span></span>

    ```js
    ...
    }).when("/TodoList", {
            controller: "todoListCtrl",
            templateUrl: "/App/Views/TodoList.html",
            requireADLogin: true,
    ...
    ```

## <a name="summary"></a><span data-ttu-id="43db0-162">Summary</span><span class="sxs-lookup"><span data-stu-id="43db0-162">Summary</span></span>
<span data-ttu-id="43db0-163">You now have a secure single-page app that can sign in users and issue bearer-token-protected requests to its back-end API.</span><span class="sxs-lookup"><span data-stu-id="43db0-163">You now have a secure single-page app that can sign in users and issue bearer-token-protected requests to its back-end API.</span></span> <span data-ttu-id="43db0-164">When a user clicks the **TodoList** link, adal.js will automatically redirect to Azure AD for sign-in if necessary.</span><span class="sxs-lookup"><span data-stu-id="43db0-164">When a user clicks the **TodoList** link, adal.js will automatically redirect to Azure AD for sign-in if necessary.</span></span> <span data-ttu-id="43db0-165">In addition, adal.js will automatically attach an access token to any Ajax requests that are sent to the app's back end.</span><span class="sxs-lookup"><span data-stu-id="43db0-165">In addition, adal.js will automatically attach an access token to any Ajax requests that are sent to the app's back end.</span></span> 

<span data-ttu-id="43db0-166">The preceding steps are the bare minimum necessary to build a single-page app by using adal.js.</span><span class="sxs-lookup"><span data-stu-id="43db0-166">The preceding steps are the bare minimum necessary to build a single-page app by using adal.js.</span></span> <span data-ttu-id="43db0-167">But a few other features are useful in single-page app:</span><span class="sxs-lookup"><span data-stu-id="43db0-167">But a few other features are useful in single-page app:</span></span>

* <span data-ttu-id="43db0-168">To explicitly issue sign-in and sign-out requests, you can define functions in your controllers that invoke adal.js.</span><span class="sxs-lookup"><span data-stu-id="43db0-168">To explicitly issue sign-in and sign-out requests, you can define functions in your controllers that invoke adal.js.</span></span> <span data-ttu-id="43db0-169">In `App/Scripts/homeCtrl.js`:</span><span class="sxs-lookup"><span data-stu-id="43db0-169">In `App/Scripts/homeCtrl.js`:</span></span>

    ```js
    ...
    $scope.login = function () {
        adalService.login();
    };
    $scope.logout = function () {
        adalService.logOut();
    };
    ...
    ```
* <span data-ttu-id="43db0-170">You might want to present user information in the app's UI.</span><span class="sxs-lookup"><span data-stu-id="43db0-170">You might want to present user information in the app's UI.</span></span> <span data-ttu-id="43db0-171">The ADAL service has already been added to the `userDataCtrl` controller, so you can access the `userInfo` object in the associated view, `App/Views/UserData.html`:</span><span class="sxs-lookup"><span data-stu-id="43db0-171">The ADAL service has already been added to the `userDataCtrl` controller, so you can access the `userInfo` object in the associated view, `App/Views/UserData.html`:</span></span>

    ```js
    <p>{{userInfo.userName}}</p>
    <p>aud:{{userInfo.profile.aud}}</p>
    <p>iss:{{userInfo.profile.iss}}</p>
    ...
    ```

* <span data-ttu-id="43db0-172">There are many scenarios in which you'll want to know if the user is signed in or not.</span><span class="sxs-lookup"><span data-stu-id="43db0-172">There are many scenarios in which you'll want to know if the user is signed in or not.</span></span> <span data-ttu-id="43db0-173">You can also use the `userInfo` object to gather this information.</span><span class="sxs-lookup"><span data-stu-id="43db0-173">You can also use the `userInfo` object to gather this information.</span></span> <span data-ttu-id="43db0-174">For instance, in `index.html`, you can show either the **Login** or **Logout** button based on authentication status:</span><span class="sxs-lookup"><span data-stu-id="43db0-174">For instance, in `index.html`, you can show either the **Login** or **Logout** button based on authentication status:</span></span>

    ```js
    <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
    <li><a class="btn btn-link" ng-hide=" userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    ```

<span data-ttu-id="43db0-175">Your Azure AD-integrated single-page app can authenticate users, securely call its back end by using OAuth 2.0, and get basic information about the user.</span><span class="sxs-lookup"><span data-stu-id="43db0-175">Your Azure AD-integrated single-page app can authenticate users, securely call its back end by using OAuth 2.0, and get basic information about the user.</span></span> <span data-ttu-id="43db0-176">If you haven't already, now is the time to populate your tenant with some users.</span><span class="sxs-lookup"><span data-stu-id="43db0-176">If you haven't already, now is the time to populate your tenant with some users.</span></span> <span data-ttu-id="43db0-177">Run your To Do List single-page app, and sign in with one of those users.</span><span class="sxs-lookup"><span data-stu-id="43db0-177">Run your To Do List single-page app, and sign in with one of those users.</span></span> <span data-ttu-id="43db0-178">Add tasks to the user's to-do list, sign out, and sign back in.</span><span class="sxs-lookup"><span data-stu-id="43db0-178">Add tasks to the user's to-do list, sign out, and sign back in.</span></span>

<span data-ttu-id="43db0-179">Adal.js makes it easy to incorporate common identity features into your application.</span><span class="sxs-lookup"><span data-stu-id="43db0-179">Adal.js makes it easy to incorporate common identity features into your application.</span></span> <span data-ttu-id="43db0-180">It takes care of all the dirty work for you: cache management, OAuth protocol support, presenting the user with a sign-in UI, refreshing expired tokens, and more.</span><span class="sxs-lookup"><span data-stu-id="43db0-180">It takes care of all the dirty work for you: cache management, OAuth protocol support, presenting the user with a sign-in UI, refreshing expired tokens, and more.</span></span>

<span data-ttu-id="43db0-181">For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="43db0-181">For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span>

## <a name="next-steps"></a><span data-ttu-id="43db0-182">Next steps</span><span class="sxs-lookup"><span data-stu-id="43db0-182">Next steps</span></span>
<span data-ttu-id="43db0-183">You can now move on to additional scenarios.</span><span class="sxs-lookup"><span data-stu-id="43db0-183">You can now move on to additional scenarios.</span></span> <span data-ttu-id="43db0-184">You might want to try: [Call a CORS web API from a single-page app](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span><span class="sxs-lookup"><span data-stu-id="43db0-184">You might want to try: [Call a CORS web API from a single-page app](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
