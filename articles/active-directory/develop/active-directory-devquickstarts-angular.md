---
title: Azure AD AngularJS Getting Started | Microsoft Docs
description: How to build an AngularJS single-page application that integrates with Azure AD for sign-in and calls Azure AD-protected APIs by using OAuth.
services: active-directory
documentationcenter: ''
author: dstrockis
manager: mbaldwin
editor: ''
ms.assetid: f2991054-8146-4718-a5f7-59b892230ad7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.openlocfilehash: 0ace1ee96d9266db9310ba73c36788a787a9dd15
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551248"
---
# <a name="help-secure-angularjs-single-page-apps-by-using-azure-ad"></a><span data-ttu-id="f4b84-103">Help secure AngularJS single-page apps by using Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4b84-103">Help secure AngularJS single-page apps by using Azure AD</span></span>

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="f4b84-104">Azure Active Directory (Azure AD) makes it simple and straightforward for you to add sign-in, sign-out, and secure OAuth API calls to your single-page apps.</span><span class="sxs-lookup"><span data-stu-id="f4b84-104">Azure Active Directory (Azure AD) makes it simple and straightforward for you to add sign-in, sign-out, and secure OAuth API calls to your single-page apps.</span></span>  <span data-ttu-id="f4b84-105">It enables your apps to authenticate users with their Windows Server Active Directory accounts and consume any web API that Azure AD helps protect, such as the Office 365 APIs or the Azure API.</span><span class="sxs-lookup"><span data-stu-id="f4b84-105">It enables your apps to authenticate users with their Windows Server Active Directory accounts and consume any web API that Azure AD helps protect, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="f4b84-106">For JavaScript applications running in a browser, Azure AD provides the Active Directory Authentication Library (ADAL), or adal.js.</span><span class="sxs-lookup"><span data-stu-id="f4b84-106">For JavaScript applications running in a browser, Azure AD provides the Active Directory Authentication Library (ADAL), or adal.js.</span></span> <span data-ttu-id="f4b84-107">The sole purpose of adal.js is to make it easy for your app to get access tokens.</span><span class="sxs-lookup"><span data-stu-id="f4b84-107">The sole purpose of adal.js is to make it easy for your app to get access tokens.</span></span> <span data-ttu-id="f4b84-108">To demonstrate just how easy it is, here we'll build an AngularJS To Do List application that:</span><span class="sxs-lookup"><span data-stu-id="f4b84-108">To demonstrate just how easy it is, here we'll build an AngularJS To Do List application that:</span></span>

* <span data-ttu-id="f4b84-109">Signs the user in to the app by using Azure AD as the identity provider.</span><span class="sxs-lookup"><span data-stu-id="f4b84-109">Signs the user in to the app by using Azure AD as the identity provider.</span></span>
* <span data-ttu-id="f4b84-110">Displays some information about the user.</span><span class="sxs-lookup"><span data-stu-id="f4b84-110">Displays some information about the user.</span></span>
* <span data-ttu-id="f4b84-111">Securely calls the app's To Do List API by using bearer tokens from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4b84-111">Securely calls the app's To Do List API by using bearer tokens from Azure AD.</span></span>
* <span data-ttu-id="f4b84-112">Signs the user out of the app.</span><span class="sxs-lookup"><span data-stu-id="f4b84-112">Signs the user out of the app.</span></span>

<span data-ttu-id="f4b84-113">To build the complete, working application, you need to:</span><span class="sxs-lookup"><span data-stu-id="f4b84-113">To build the complete, working application, you need to:</span></span>

1. <span data-ttu-id="f4b84-114">Register your app with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4b84-114">Register your app with Azure AD.</span></span>
2. <span data-ttu-id="f4b84-115">Install ADAL and configure the single-page app.</span><span class="sxs-lookup"><span data-stu-id="f4b84-115">Install ADAL and configure the single-page app.</span></span>
3. <span data-ttu-id="f4b84-116">Use ADAL to help secure pages in the single-page app.</span><span class="sxs-lookup"><span data-stu-id="f4b84-116">Use ADAL to help secure pages in the single-page app.</span></span>

<span data-ttu-id="f4b84-117">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="f4b84-117">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="f4b84-118">You also need an Azure AD tenant in which you can create users and register an application.</span><span class="sxs-lookup"><span data-stu-id="f4b84-118">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="f4b84-119">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="f4b84-119">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-the-directorysearcher-application"></a><span data-ttu-id="f4b84-120">Step 1: Register the DirectorySearcher application</span><span class="sxs-lookup"><span data-stu-id="f4b84-120">Step 1: Register the DirectorySearcher application</span></span>
<span data-ttu-id="f4b84-121">To enable your app to authenticate users and get tokens, you first need to register it in your Azure AD tenant:</span><span class="sxs-lookup"><span data-stu-id="f4b84-121">To enable your app to authenticate users and get tokens, you first need to register it in your Azure AD tenant:</span></span>

1. <span data-ttu-id="f4b84-122">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f4b84-122">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f4b84-123">On the top bar, click your account.</span><span class="sxs-lookup"><span data-stu-id="f4b84-123">On the top bar, click your account.</span></span> <span data-ttu-id="f4b84-124">Under the **Directory** list, choose the Azure AD tenant where you want to register your application.</span><span class="sxs-lookup"><span data-stu-id="f4b84-124">Under the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="f4b84-125">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f4b84-125">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="f4b84-126">Click **App registrations**, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="f4b84-126">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="f4b84-127">Follow the prompts and create a new web application and/or web API:</span><span class="sxs-lookup"><span data-stu-id="f4b84-127">Follow the prompts and create a new web application and/or web API:</span></span>
  * <span data-ttu-id="f4b84-128">**Name** describes your application to users.</span><span class="sxs-lookup"><span data-stu-id="f4b84-128">**Name** describes your application to users.</span></span>
  * <span data-ttu-id="f4b84-129">**Redirect Uri** is the location to which Azure AD will return tokens.</span><span class="sxs-lookup"><span data-stu-id="f4b84-129">**Redirect Uri** is the location to which Azure AD will return tokens.</span></span> <span data-ttu-id="f4b84-130">The default location for this sample is `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="f4b84-130">The default location for this sample is `https://localhost:44326/`.</span></span>
6. <span data-ttu-id="f4b84-131">After you finish registration, Azure AD assigns a unique application ID to your app.</span><span class="sxs-lookup"><span data-stu-id="f4b84-131">After you finish registration, Azure AD assigns a unique application ID to your app.</span></span>  <span data-ttu-id="f4b84-132">You'll need this value in the next sections, so copy it from the application tab.</span><span class="sxs-lookup"><span data-stu-id="f4b84-132">You'll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="f4b84-133">Adal.js uses the OAuth implicit flow to communicate with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4b84-133">Adal.js uses the OAuth implicit flow to communicate with Azure AD.</span></span> <span data-ttu-id="f4b84-134">You must enable the implicit flow for your application:</span><span class="sxs-lookup"><span data-stu-id="f4b84-134">You must enable the implicit flow for your application:</span></span>
  1. <span data-ttu-id="f4b84-135">Click the application and select **Manifest** to open the inline manifest editor.</span><span class="sxs-lookup"><span data-stu-id="f4b84-135">Click the application and select **Manifest** to open the inline manifest editor.</span></span>
  2. <span data-ttu-id="f4b84-136">Locate the `oauth2AllowImplicitFlow` property.</span><span class="sxs-lookup"><span data-stu-id="f4b84-136">Locate the `oauth2AllowImplicitFlow` property.</span></span> <span data-ttu-id="f4b84-137">Set its value to `true`.</span><span class="sxs-lookup"><span data-stu-id="f4b84-137">Set its value to `true`.</span></span>
  3. <span data-ttu-id="f4b84-138">Click **Save** to save the manifest.</span><span class="sxs-lookup"><span data-stu-id="f4b84-138">Click **Save** to save the manifest.</span></span>
8. <span data-ttu-id="f4b84-139">Grant permissions across your tenant for your application.</span><span class="sxs-lookup"><span data-stu-id="f4b84-139">Grant permissions across your tenant for your application.</span></span> <span data-ttu-id="f4b84-140">Go to **Settings** > **Properties** > **Required Permissions**, and click the **Grant Permissions** button on the top bar.</span><span class="sxs-lookup"><span data-stu-id="f4b84-140">Go to **Settings** > **Properties** > **Required Permissions**, and click the **Grant Permissions** button on the top bar.</span></span> <span data-ttu-id="f4b84-141">Click **Yes** to confirm.</span><span class="sxs-lookup"><span data-stu-id="f4b84-141">Click **Yes** to confirm.</span></span>

## <a name="step-2-install-adal-and-configure-the-single-page-app"></a><span data-ttu-id="f4b84-142">Step 2: Install ADAL and configure the single-page app</span><span class="sxs-lookup"><span data-stu-id="f4b84-142">Step 2: Install ADAL and configure the single-page app</span></span>
<span data-ttu-id="f4b84-143">Now that you have an application in Azure AD, you can install adal.js and write your identity-related code.</span><span class="sxs-lookup"><span data-stu-id="f4b84-143">Now that you have an application in Azure AD, you can install adal.js and write your identity-related code.</span></span>

<span data-ttu-id="f4b84-144">Begin by adding adal.js to the TodoSPA project by using the Package Manager Console:</span><span class="sxs-lookup"><span data-stu-id="f4b84-144">Begin by adding adal.js to the TodoSPA project by using the Package Manager Console:</span></span>
  1. <span data-ttu-id="f4b84-145">Download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) and add it to the `App/Scripts/` project directory.</span><span class="sxs-lookup"><span data-stu-id="f4b84-145">Download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) and add it to the `App/Scripts/` project directory.</span></span>
  2. <span data-ttu-id="f4b84-146">Download [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) and add it to the `App/Scripts/` project directory.</span><span class="sxs-lookup"><span data-stu-id="f4b84-146">Download [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) and add it to the `App/Scripts/` project directory.</span></span>
  3. <span data-ttu-id="f4b84-147">Load each script before the end of the `</body>` in `index.html`:</span><span class="sxs-lookup"><span data-stu-id="f4b84-147">Load each script before the end of the `</body>` in `index.html`:</span></span>

    ```js
    ...
    <script src="App/Scripts/adal.js"></script>
    <script src="App/Scripts/adal-angular.js"></script>
    ...
    ```

<span data-ttu-id="f4b84-148">For the single-page app's back-end To Do List API to accept tokens from the browser, the back end needs configuration information about the app registration.</span><span class="sxs-lookup"><span data-stu-id="f4b84-148">For the single-page app's back-end To Do List API to accept tokens from the browser, the back end needs configuration information about the app registration.</span></span> <span data-ttu-id="f4b84-149">In the TodoSPA project, open `web.config`.</span><span class="sxs-lookup"><span data-stu-id="f4b84-149">In the TodoSPA project, open `web.config`.</span></span> <span data-ttu-id="f4b84-150">Replace the values of the elements in the `<appSettings>` section to reflect the values that you used in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f4b84-150">Replace the values of the elements in the `<appSettings>` section to reflect the values that you used in the Azure portal.</span></span> <span data-ttu-id="f4b84-151">Your code will reference these values whenever it uses ADAL.</span><span class="sxs-lookup"><span data-stu-id="f4b84-151">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="f4b84-152">`ida:Tenant` is the domain of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="f4b84-152">`ida:Tenant` is the domain of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="f4b84-153">`ida:Audience` is the client ID of your application that you copied from the portal.</span><span class="sxs-lookup"><span data-stu-id="f4b84-153">`ida:Audience` is the client ID of your application that you copied from the portal.</span></span>

## <a name="step-3-use-adal-to-help-secure-pages-in-the-single-page-app"></a><span data-ttu-id="f4b84-154">Step 3: Use ADAL to help secure pages in the single-page app</span><span class="sxs-lookup"><span data-stu-id="f4b84-154">Step 3: Use ADAL to help secure pages in the single-page app</span></span>
<span data-ttu-id="f4b84-155">Adal.js integrates with AngularJS route and HTTP providers, so you can help secure individual views in your single-page app.</span><span class="sxs-lookup"><span data-stu-id="f4b84-155">Adal.js integrates with AngularJS route and HTTP providers, so you can help secure individual views in your single-page app.</span></span>

1. <span data-ttu-id="f4b84-156">In `App/Scripts/app.js`, bring in the adal.js module:</span><span class="sxs-lookup"><span data-stu-id="f4b84-156">In `App/Scripts/app.js`, bring in the adal.js module:</span></span>

    ```js
    angular.module('todoApp', ['ngRoute','AdalAngular'])
    .config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
     function ($routeProvider, $httpProvider, adalProvider) {
    ...
    ```
2. <span data-ttu-id="f4b84-157">Initialize `adalProvider` by using the configuration values of your application registration, also in `App/Scripts/app.js`:</span><span class="sxs-lookup"><span data-stu-id="f4b84-157">Initialize `adalProvider` by using the configuration values of your application registration, also in `App/Scripts/app.js`:</span></span>

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
3. <span data-ttu-id="f4b84-158">Help secure the `TodoList` view in the app by using only one line of code: `requireADLogin`.</span><span class="sxs-lookup"><span data-stu-id="f4b84-158">Help secure the `TodoList` view in the app by using only one line of code: `requireADLogin`.</span></span>

    ```js
    ...
    }).when("/TodoList", {
            controller: "todoListCtrl",
            templateUrl: "/App/Views/TodoList.html",
            requireADLogin: true,
    ...
    ```

## <a name="summary"></a><span data-ttu-id="f4b84-159">Summary</span><span class="sxs-lookup"><span data-stu-id="f4b84-159">Summary</span></span>
<span data-ttu-id="f4b84-160">You now have a secure single-page app that can sign in users and issue bearer-token-protected requests to its back-end API.</span><span class="sxs-lookup"><span data-stu-id="f4b84-160">You now have a secure single-page app that can sign in users and issue bearer-token-protected requests to its back-end API.</span></span> <span data-ttu-id="f4b84-161">When a user clicks the **TodoList** link, adal.js will automatically redirect to Azure AD for sign-in if necessary.</span><span class="sxs-lookup"><span data-stu-id="f4b84-161">When a user clicks the **TodoList** link, adal.js will automatically redirect to Azure AD for sign-in if necessary.</span></span> <span data-ttu-id="f4b84-162">In addition, adal.js will automatically attach an access token to any Ajax requests that are sent to the app's back end.</span><span class="sxs-lookup"><span data-stu-id="f4b84-162">In addition, adal.js will automatically attach an access token to any Ajax requests that are sent to the app's back end.</span></span>  

<span data-ttu-id="f4b84-163">The preceding steps are the bare minimum necessary to build a single-page app by using adal.js.</span><span class="sxs-lookup"><span data-stu-id="f4b84-163">The preceding steps are the bare minimum necessary to build a single-page app by using adal.js.</span></span> <span data-ttu-id="f4b84-164">But a few other features are useful in single-page app:</span><span class="sxs-lookup"><span data-stu-id="f4b84-164">But a few other features are useful in single-page app:</span></span>

* <span data-ttu-id="f4b84-165">To explicitly issue sign-in and sign-out requests, you can define functions in your controllers that invoke adal.js.</span><span class="sxs-lookup"><span data-stu-id="f4b84-165">To explicitly issue sign-in and sign-out requests, you can define functions in your controllers that invoke adal.js.</span></span>  <span data-ttu-id="f4b84-166">In `App/Scripts/homeCtrl.js`:</span><span class="sxs-lookup"><span data-stu-id="f4b84-166">In `App/Scripts/homeCtrl.js`:</span></span>

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
* <span data-ttu-id="f4b84-167">You might want to present user information in the app's UI.</span><span class="sxs-lookup"><span data-stu-id="f4b84-167">You might want to present user information in the app's UI.</span></span> <span data-ttu-id="f4b84-168">The ADAL service has already been added to the `userDataCtrl` controller, so you can access the `userInfo` object in the associated view, `App/Views/UserData.html`:</span><span class="sxs-lookup"><span data-stu-id="f4b84-168">The ADAL service has already been added to the `userDataCtrl` controller, so you can access the `userInfo` object in the associated view, `App/Views/UserData.html`:</span></span>

    ```js
    <p>{{userInfo.userName}}</p>
    <p>aud:{{userInfo.profile.aud}}</p>
    <p>iss:{{userInfo.profile.iss}}</p>
    ...
    ```

* <span data-ttu-id="f4b84-169">There are many scenarios in which you'll want to know if the user is signed in or not.</span><span class="sxs-lookup"><span data-stu-id="f4b84-169">There are many scenarios in which you'll want to know if the user is signed in or not.</span></span> <span data-ttu-id="f4b84-170">You can also use the `userInfo` object to gather this information.</span><span class="sxs-lookup"><span data-stu-id="f4b84-170">You can also use the `userInfo` object to gather this information.</span></span>  <span data-ttu-id="f4b84-171">For instance, in `index.html`, you can show either the **Login** or **Logout** button based on authentication status:</span><span class="sxs-lookup"><span data-stu-id="f4b84-171">For instance, in `index.html`, you can show either the **Login** or **Logout** button based on authentication status:</span></span>

    ```js
    <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
    <li><a class="btn btn-link" ng-hide=" userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    ```

<span data-ttu-id="f4b84-172">Your Azure AD-integrated single-page app can authenticate users, securely call its back end by using OAuth 2.0, and get basic information about the user.</span><span class="sxs-lookup"><span data-stu-id="f4b84-172">Your Azure AD-integrated single-page app can authenticate users, securely call its back end by using OAuth 2.0, and get basic information about the user.</span></span> <span data-ttu-id="f4b84-173">If you haven't already, now is the time to populate your tenant with some users.</span><span class="sxs-lookup"><span data-stu-id="f4b84-173">If you haven't already, now is the time to populate your tenant with some users.</span></span> <span data-ttu-id="f4b84-174">Run your To Do List single-page app, and sign in with one of those users.</span><span class="sxs-lookup"><span data-stu-id="f4b84-174">Run your To Do List single-page app, and sign in with one of those users.</span></span> <span data-ttu-id="f4b84-175">Add tasks to the user's to-do list, sign out, and sign back in.</span><span class="sxs-lookup"><span data-stu-id="f4b84-175">Add tasks to the user's to-do list, sign out, and sign back in.</span></span>

<span data-ttu-id="f4b84-176">Adal.js makes it easy to incorporate common identity features into your application.</span><span class="sxs-lookup"><span data-stu-id="f4b84-176">Adal.js makes it easy to incorporate common identity features into your application.</span></span> <span data-ttu-id="f4b84-177">It takes care of all the dirty work for you: cache management, OAuth protocol support, presenting the user with a sign-in UI, refreshing expired tokens, and more.</span><span class="sxs-lookup"><span data-stu-id="f4b84-177">It takes care of all the dirty work for you: cache management, OAuth protocol support, presenting the user with a sign-in UI, refreshing expired tokens, and more.</span></span>

<span data-ttu-id="f4b84-178">For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="f4b84-178">For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4b84-179">Next steps</span><span class="sxs-lookup"><span data-stu-id="f4b84-179">Next steps</span></span>
<span data-ttu-id="f4b84-180">You can now move on to additional scenarios.</span><span class="sxs-lookup"><span data-stu-id="f4b84-180">You can now move on to additional scenarios.</span></span> <span data-ttu-id="f4b84-181">You might want to try: [Call a CORS web API from a single-page app](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span><span class="sxs-lookup"><span data-stu-id="f4b84-181">You might want to try: [Call a CORS web API from a single-page app](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
