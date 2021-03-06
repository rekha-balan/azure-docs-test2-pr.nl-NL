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
# <a name="help-secure-angularjs-single-page-apps-by-using-azure-ad"></a>Help secure AngularJS single-page apps by using Azure AD

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Azure Active Directory (Azure AD) makes it simple and straightforward for you to add sign-in, sign-out, and secure OAuth API calls to your single-page apps.  It enables your apps to authenticate users with their Windows Server Active Directory accounts and consume any web API that Azure AD helps protect, such as the Office 365 APIs or the Azure API.

For JavaScript applications running in a browser, Azure AD provides the Active Directory Authentication Library (ADAL), or adal.js. The sole purpose of adal.js is to make it easy for your app to get access tokens. To demonstrate just how easy it is, here we'll build an AngularJS To Do List application that:

* Signs the user in to the app by using Azure AD as the identity provider.
* Displays some information about the user.
* Securely calls the app's To Do List API by using bearer tokens from Azure AD.
* Signs the user out of the app.

To build the complete, working application, you need to:

1. Register your app with Azure AD.
2. Install ADAL and configure the single-page app.
3. Use ADAL to help secure pages in the single-page app.

To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip). You also need an Azure AD tenant in which you can create users and register an application. If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).

## <a name="step-1-register-the-directorysearcher-application"></a>Step 1: Register the DirectorySearcher application
To enable your app to authenticate users and get tokens, you first need to register it in your Azure AD tenant:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. On the top bar, click your account. Under the **Directory** list, choose the Azure AD tenant where you want to register your application.
3. Click **More Services** in the left pane, and then select **Azure Active Directory**.
4. Click **App registrations**, and then select **Add**.
5. Follow the prompts and create a new web application and/or web API:
  * **Name** describes your application to users.
  * **Redirect Uri** is the location to which Azure AD will return tokens. The default location for this sample is `https://localhost:44326/`.
6. After you finish registration, Azure AD assigns a unique application ID to your app.  You'll need this value in the next sections, so copy it from the application tab.
7. Adal.js uses the OAuth implicit flow to communicate with Azure AD. You must enable the implicit flow for your application:
  1. Click the application and select **Manifest** to open the inline manifest editor.
  2. Locate the `oauth2AllowImplicitFlow` property. Set its value to `true`.
  3. Click **Save** to save the manifest.
8. Grant permissions across your tenant for your application. Go to **Settings** > **Properties** > **Required Permissions**, and click the **Grant Permissions** button on the top bar. Click **Yes** to confirm.

## <a name="step-2-install-adal-and-configure-the-single-page-app"></a>Step 2: Install ADAL and configure the single-page app
Now that you have an application in Azure AD, you can install adal.js and write your identity-related code.

Begin by adding adal.js to the TodoSPA project by using the Package Manager Console:
  1. Download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) and add it to the `App/Scripts/` project directory.
  2. Download [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) and add it to the `App/Scripts/` project directory.
  3. Load each script before the end of the `</body>` in `index.html`:

    ```js
    ...
    <script src="App/Scripts/adal.js"></script>
    <script src="App/Scripts/adal-angular.js"></script>
    ...
    ```

For the single-page app's back-end To Do List API to accept tokens from the browser, the back end needs configuration information about the app registration. In the TodoSPA project, open `web.config`. Replace the values of the elements in the `<appSettings>` section to reflect the values that you used in the Azure portal. Your code will reference these values whenever it uses ADAL.
  * `ida:Tenant` is the domain of your Azure AD tenant--for example, contoso.onmicrosoft.com.
  * `ida:Audience` is the client ID of your application that you copied from the portal.

## <a name="step-3-use-adal-to-help-secure-pages-in-the-single-page-app"></a>Step 3: Use ADAL to help secure pages in the single-page app
Adal.js integrates with AngularJS route and HTTP providers, so you can help secure individual views in your single-page app.

1. In `App/Scripts/app.js`, bring in the adal.js module:

    ```js
    angular.module('todoApp', ['ngRoute','AdalAngular'])
    .config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
     function ($routeProvider, $httpProvider, adalProvider) {
    ...
    ```
2. Initialize `adalProvider` by using the configuration values of your application registration, also in `App/Scripts/app.js`:

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
3. Help secure the `TodoList` view in the app by using only one line of code: `requireADLogin`.

    ```js
    ...
    }).when("/TodoList", {
            controller: "todoListCtrl",
            templateUrl: "/App/Views/TodoList.html",
            requireADLogin: true,
    ...
    ```

## <a name="summary"></a>Summary
You now have a secure single-page app that can sign in users and issue bearer-token-protected requests to its back-end API. When a user clicks the **TodoList** link, adal.js will automatically redirect to Azure AD for sign-in if necessary. In addition, adal.js will automatically attach an access token to any Ajax requests that are sent to the app's back end.  

The preceding steps are the bare minimum necessary to build a single-page app by using adal.js. But a few other features are useful in single-page app:

* To explicitly issue sign-in and sign-out requests, you can define functions in your controllers that invoke adal.js.  In `App/Scripts/homeCtrl.js`:

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
* You might want to present user information in the app's UI. The ADAL service has already been added to the `userDataCtrl` controller, so you can access the `userInfo` object in the associated view, `App/Views/UserData.html`:

    ```js
    <p>{{userInfo.userName}}</p>
    <p>aud:{{userInfo.profile.aud}}</p>
    <p>iss:{{userInfo.profile.iss}}</p>
    ...
    ```

* There are many scenarios in which you'll want to know if the user is signed in or not. You can also use the `userInfo` object to gather this information.  For instance, in `index.html`, you can show either the **Login** or **Logout** button based on authentication status:

    ```js
    <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
    <li><a class="btn btn-link" ng-hide=" userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    ```

Your Azure AD-integrated single-page app can authenticate users, securely call its back end by using OAuth 2.0, and get basic information about the user. If you haven't already, now is the time to populate your tenant with some users. Run your To Do List single-page app, and sign in with one of those users. Add tasks to the user's to-do list, sign out, and sign back in.

Adal.js makes it easy to incorporate common identity features into your application. It takes care of all the dirty work for you: cache management, OAuth protocol support, presenting the user with a sign-in UI, refreshing expired tokens, and more.

For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).

## <a name="next-steps"></a>Next steps
You can now move on to additional scenarios. You might want to try: [Call a CORS web API from a single-page app](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
