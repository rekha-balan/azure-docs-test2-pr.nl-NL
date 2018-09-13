---
title: Azure AD v2.0 .NET AngularJS single page app getting started | Microsoft Docs
description: How to build an Angular JS Single Page app that signs in users with both personal Microsoft accounts and work or school accounts.
services: active-directory
documentationcenter: ''
author: dstrockis
manager: mbaldwin
editor: ''
ms.assetid: 6a341781-278f-461b-92ca-7572a06e6852
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.openlocfilehash: 0ab6506e14997c0c6d58afa22db63f928d7cceb9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552606"
---
# <a name="add-sign-in-to-an-angularjs-single-page-app---net"></a><span data-ttu-id="36f52-103">Add sign-in to an AngularJS single page app - .NET</span><span class="sxs-lookup"><span data-stu-id="36f52-103">Add sign-in to an AngularJS single page app - .NET</span></span>
<span data-ttu-id="36f52-104">In this article we'll add sign in with Microsoft powered accounts to an AngularJS app using the Azure Active Directory v2.0 endpoint.</span><span class="sxs-lookup"><span data-stu-id="36f52-104">In this article we'll add sign in with Microsoft powered accounts to an AngularJS app using the Azure Active Directory v2.0 endpoint.</span></span>  <span data-ttu-id="36f52-105">The v2.0 endpoint enables you to perform a single integration in your app and authenticate users with both personal and work/school accounts.</span><span class="sxs-lookup"><span data-stu-id="36f52-105">The v2.0 endpoint enables you to perform a single integration in your app and authenticate users with both personal and work/school accounts.</span></span>

<span data-ttu-id="36f52-106">This sample is a simple To-Do List single page app that stores tasks in a backend REST API, written using the .NET 4.5 MVC framework and secured using OAuth bearer tokens from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="36f52-106">This sample is a simple To-Do List single page app that stores tasks in a backend REST API, written using the .NET 4.5 MVC framework and secured using OAuth bearer tokens from Azure AD.</span></span>  <span data-ttu-id="36f52-107">The AngularJS app will use our open source JavaScript authentication library [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) to handle the entire sign in process and acquire tokens for calling the REST API.</span><span class="sxs-lookup"><span data-stu-id="36f52-107">The AngularJS app will use our open source JavaScript authentication library [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) to handle the entire sign in process and acquire tokens for calling the REST API.</span></span>  <span data-ttu-id="36f52-108">The same pattern can be applied to authenticate to other REST APIs, like the [Microsoft Graph](https://graph.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="36f52-108">The same pattern can be applied to authenticate to other REST APIs, like the [Microsoft Graph](https://graph.microsoft.com).</span></span>

> [!NOTE]
> <span data-ttu-id="36f52-109">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span><span class="sxs-lookup"><span data-stu-id="36f52-109">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="36f52-110">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="36f52-110">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download"></a><span data-ttu-id="36f52-111">Download</span><span class="sxs-lookup"><span data-stu-id="36f52-111">Download</span></span>
<span data-ttu-id="36f52-112">To get started, you'll need to download & install Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="36f52-112">To get started, you'll need to download & install Visual Studio.</span></span>  <span data-ttu-id="36f52-113">Then you can clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) a skeleton app:</span><span class="sxs-lookup"><span data-stu-id="36f52-113">Then you can clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) a skeleton app:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet.git
```

<span data-ttu-id="36f52-114">The skeleton app includes all the boilerplate code for a simple AngularJS app, but is missing all of the identity-related pieces.</span><span class="sxs-lookup"><span data-stu-id="36f52-114">The skeleton app includes all the boilerplate code for a simple AngularJS app, but is missing all of the identity-related pieces.</span></span>  <span data-ttu-id="36f52-115">If you don't want to follow along, you can instead clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/complete.zip) the completed sample.</span><span class="sxs-lookup"><span data-stu-id="36f52-115">If you don't want to follow along, you can instead clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/complete.zip) the completed sample.</span></span>

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-DotNet.git
```

## <a name="register-an-app"></a><span data-ttu-id="36f52-116">Register an app</span><span class="sxs-lookup"><span data-stu-id="36f52-116">Register an app</span></span>
<span data-ttu-id="36f52-117">First, create an app in the [App Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="36f52-117">First, create an app in the [App Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="36f52-118">Make sure to:</span><span class="sxs-lookup"><span data-stu-id="36f52-118">Make sure to:</span></span>

* <span data-ttu-id="36f52-119">Add the **Web** platform for your app.</span><span class="sxs-lookup"><span data-stu-id="36f52-119">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="36f52-120">Enter the correct **Redirect URI**.</span><span class="sxs-lookup"><span data-stu-id="36f52-120">Enter the correct **Redirect URI**.</span></span> <span data-ttu-id="36f52-121">The default for this sample is `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="36f52-121">The default for this sample is `https://localhost:44326/`.</span></span>
* <span data-ttu-id="36f52-122">Leave the **Allow Implicit Flow** checkbox enabled.</span><span class="sxs-lookup"><span data-stu-id="36f52-122">Leave the **Allow Implicit Flow** checkbox enabled.</span></span> 

<span data-ttu-id="36f52-123">Copy down the **Application ID** that is assigned to your app, you'll need it shortly.</span><span class="sxs-lookup"><span data-stu-id="36f52-123">Copy down the **Application ID** that is assigned to your app, you'll need it shortly.</span></span> 

## <a name="install-adaljs"></a><span data-ttu-id="36f52-124">Install adal.js</span><span class="sxs-lookup"><span data-stu-id="36f52-124">Install adal.js</span></span>
<span data-ttu-id="36f52-125">To start, navigate to project you downloaded and install adal.js.</span><span class="sxs-lookup"><span data-stu-id="36f52-125">To start, navigate to project you downloaded and install adal.js.</span></span>  <span data-ttu-id="36f52-126">If you have [bower](http://bower.io/) installed, you can just run this command.</span><span class="sxs-lookup"><span data-stu-id="36f52-126">If you have [bower](http://bower.io/) installed, you can just run this command.</span></span>  <span data-ttu-id="36f52-127">For any dependency version mismatches, just choose the higher version.</span><span class="sxs-lookup"><span data-stu-id="36f52-127">For any dependency version mismatches, just choose the higher version.</span></span>

```
bower install adal-angular#experimental
```

<span data-ttu-id="36f52-128">Alternatively, you can manually download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) and [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span><span class="sxs-lookup"><span data-stu-id="36f52-128">Alternatively, you can manually download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) and [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span></span>  <span data-ttu-id="36f52-129">Add both files to the `app/lib/adal-angular-experimental/dist` directory of the `TodoSPA` project.</span><span class="sxs-lookup"><span data-stu-id="36f52-129">Add both files to the `app/lib/adal-angular-experimental/dist` directory of the `TodoSPA` project.</span></span>

<span data-ttu-id="36f52-130">Now open the project in Visual Studio, and load adal.js at the end of the main page's body:</span><span class="sxs-lookup"><span data-stu-id="36f52-130">Now open the project in Visual Studio, and load adal.js at the end of the main page's body:</span></span>

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-the-rest-api"></a><span data-ttu-id="36f52-131">Set up the REST API</span><span class="sxs-lookup"><span data-stu-id="36f52-131">Set up the REST API</span></span>
<span data-ttu-id="36f52-132">While we're setting things up, let's get the backend REST API working.</span><span class="sxs-lookup"><span data-stu-id="36f52-132">While we're setting things up, let's get the backend REST API working.</span></span>  <span data-ttu-id="36f52-133">In the root of the project, open `web.config` and replace the `audience` value.</span><span class="sxs-lookup"><span data-stu-id="36f52-133">In the root of the project, open `web.config` and replace the `audience` value.</span></span>  <span data-ttu-id="36f52-134">The REST API will use this value to validate tokens it receives from the Angular app on AJAX requests.</span><span class="sxs-lookup"><span data-stu-id="36f52-134">The REST API will use this value to validate tokens it receives from the Angular app on AJAX requests.</span></span>

```xml
<!--web.config-->

...

    <appSettings>
        <add key="ida:Audience" value="[Your-application-id]" />
    </appSettings>

...
```

<span data-ttu-id="36f52-135">That's all the time we're going to spend discussing how the REST API works.</span><span class="sxs-lookup"><span data-stu-id="36f52-135">That's all the time we're going to spend discussing how the REST API works.</span></span>  <span data-ttu-id="36f52-136">Feel free to poke around in the code, but if you want to learn more about securing web APIs with Azure AD, check out [this article](active-directory-v2-devquickstarts-dotnet-api.md).</span><span class="sxs-lookup"><span data-stu-id="36f52-136">Feel free to poke around in the code, but if you want to learn more about securing web APIs with Azure AD, check out [this article](active-directory-v2-devquickstarts-dotnet-api.md).</span></span> 

## <a name="sign-users-in"></a><span data-ttu-id="36f52-137">Sign users in</span><span class="sxs-lookup"><span data-stu-id="36f52-137">Sign users in</span></span>
<span data-ttu-id="36f52-138">Time to write some identity code.</span><span class="sxs-lookup"><span data-stu-id="36f52-138">Time to write some identity code.</span></span>  <span data-ttu-id="36f52-139">You might have already noticed that adal.js contains an AngularJS provider, which plays nicely with Angular routing mechanisms.</span><span class="sxs-lookup"><span data-stu-id="36f52-139">You might have already noticed that adal.js contains an AngularJS provider, which plays nicely with Angular routing mechanisms.</span></span>  <span data-ttu-id="36f52-140">Start by adding the adal module to the app:</span><span class="sxs-lookup"><span data-stu-id="36f52-140">Start by adding the adal module to the app:</span></span>

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

<span data-ttu-id="36f52-141">You can now initialize the `adalProvider` with your Application ID:</span><span class="sxs-lookup"><span data-stu-id="36f52-141">You can now initialize the `adalProvider` with your Application ID:</span></span>

```js
// app/scripts/app.js

...

adalProvider.init({

        // Use this value for the public instance of Azure AD
        instance: 'https://login.microsoftonline.com/', 

        // The 'common' endpoint is used for multi-tenant applications like this one
        tenant: 'common',

        // Your application id from the registration portal
        clientId: '<Your-application-id>',

        // If you're using IE, uncommment this line - the default HTML5 sessionStorage does not work for localhost.
        //cacheLocation: 'localStorage',

    }, $httpProvider);
```

<span data-ttu-id="36f52-142">Great, now adal.js has all the information it needs to secure your app and sign users in.</span><span class="sxs-lookup"><span data-stu-id="36f52-142">Great, now adal.js has all the information it needs to secure your app and sign users in.</span></span>  <span data-ttu-id="36f52-143">To force sign in for a particular route in the app, all it takes is one line of code:</span><span class="sxs-lookup"><span data-stu-id="36f52-143">To force sign in for a particular route in the app, all it takes is one line of code:</span></span>

```js
// app/scripts/app.js

...

}).when("/TodoList", {
    controller: "todoListCtrl",
    templateUrl: "/static/views/TodoList.html",
    requireADLogin: true, // Ensures that the user must be logged in to access the route
})

...
```

<span data-ttu-id="36f52-144">Now when a user clicks the `TodoList` link, adal.js will automatically redirect to Azure AD for sign-in if necessary.</span><span class="sxs-lookup"><span data-stu-id="36f52-144">Now when a user clicks the `TodoList` link, adal.js will automatically redirect to Azure AD for sign-in if necessary.</span></span>  <span data-ttu-id="36f52-145">You can also explicitly send sign-in and sign-out requests by invoking adal.js in your controllers:</span><span class="sxs-lookup"><span data-stu-id="36f52-145">You can also explicitly send sign-in and sign-out requests by invoking adal.js in your controllers:</span></span>

```js
// app/scripts/homeCtrl.js

angular.module('todoApp')
// Load adal.js the same way for use in controllers and views   
.controller('homeCtrl', ['$scope', 'adalAuthenticationService','$location', function ($scope, adalService, $location) {
    $scope.login = function () {

        // Redirect the user to sign in
        adalService.login();

    };
    $scope.logout = function () {

        // Redirect the user to log out    
        adalService.logOut();

    };
...
```

## <a name="display-user-info"></a><span data-ttu-id="36f52-146">Display user info</span><span class="sxs-lookup"><span data-stu-id="36f52-146">Display user info</span></span>
<span data-ttu-id="36f52-147">Now that the user is signed in, you'll probably need to access the signed-in user's authentication data in your application.</span><span class="sxs-lookup"><span data-stu-id="36f52-147">Now that the user is signed in, you'll probably need to access the signed-in user's authentication data in your application.</span></span>  <span data-ttu-id="36f52-148">Adal.js exposes this information for you in the `userInfo` object.</span><span class="sxs-lookup"><span data-stu-id="36f52-148">Adal.js exposes this information for you in the `userInfo` object.</span></span>  <span data-ttu-id="36f52-149">To access this object in a view, first add adal.js to the root scope of the corresponding controller:</span><span class="sxs-lookup"><span data-stu-id="36f52-149">To access this object in a view, first add adal.js to the root scope of the corresponding controller:</span></span>

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

<span data-ttu-id="36f52-150">Then you can directly address the `userInfo` object in your view:</span><span class="sxs-lookup"><span data-stu-id="36f52-150">Then you can directly address the `userInfo` object in your view:</span></span> 

```html
<!--app/views/UserData.html-->

...

    <!--Get the user's profile information from the ADAL userInfo object-->
    <tr ng-repeat="(key, value) in userInfo.profile">
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
...
```

<span data-ttu-id="36f52-151">You can also use the `userInfo` object to determine if the user is signed in or not.</span><span class="sxs-lookup"><span data-stu-id="36f52-151">You can also use the `userInfo` object to determine if the user is signed in or not.</span></span>

```html
<!--index.html-->

...

    <!--Use the ADAL userInfo object to show the right login/logout button-->
    <ul class="nav navbar-nav navbar-right">
        <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
        <li><a class="btn btn-link" ng-hide="userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    </ul>
...
```

## <a name="call-the-rest-api"></a><span data-ttu-id="36f52-152">Call the REST API</span><span class="sxs-lookup"><span data-stu-id="36f52-152">Call the REST API</span></span>
<span data-ttu-id="36f52-153">Finally, it's time to get some tokens and call the REST API to create, read, update, and delete tasks.</span><span class="sxs-lookup"><span data-stu-id="36f52-153">Finally, it's time to get some tokens and call the REST API to create, read, update, and delete tasks.</span></span>  <span data-ttu-id="36f52-154">Well guess what?</span><span class="sxs-lookup"><span data-stu-id="36f52-154">Well guess what?</span></span>  <span data-ttu-id="36f52-155">You don't have to do *a thing*.</span><span class="sxs-lookup"><span data-stu-id="36f52-155">You don't have to do *a thing*.</span></span>  <span data-ttu-id="36f52-156">Adal.js will automatically take care of getting, caching, and refreshing tokens.</span><span class="sxs-lookup"><span data-stu-id="36f52-156">Adal.js will automatically take care of getting, caching, and refreshing tokens.</span></span>  <span data-ttu-id="36f52-157">It will also take care of attaching those tokens to outgoing AJAX requests that you send to the REST API.</span><span class="sxs-lookup"><span data-stu-id="36f52-157">It will also take care of attaching those tokens to outgoing AJAX requests that you send to the REST API.</span></span>  

<span data-ttu-id="36f52-158">How exactly does this work?</span><span class="sxs-lookup"><span data-stu-id="36f52-158">How exactly does this work?</span></span> <span data-ttu-id="36f52-159">It's all thanks to the magic of [AngularJS interceptors](https://docs.angularjs.org/api/ng/service/$http), which allows adal.js to transform outgoing and incoming http messages.</span><span class="sxs-lookup"><span data-stu-id="36f52-159">It's all thanks to the magic of [AngularJS interceptors](https://docs.angularjs.org/api/ng/service/$http), which allows adal.js to transform outgoing and incoming http messages.</span></span>  <span data-ttu-id="36f52-160">Furthermore, adal.js assumes that any requests send to the same domain as the window should use tokens intended for the same Application ID as the AngularJS app.</span><span class="sxs-lookup"><span data-stu-id="36f52-160">Furthermore, adal.js assumes that any requests send to the same domain as the window should use tokens intended for the same Application ID as the AngularJS app.</span></span>  <span data-ttu-id="36f52-161">This is why we used the same Application ID in both the Angular app and in the NodeJS REST API.</span><span class="sxs-lookup"><span data-stu-id="36f52-161">This is why we used the same Application ID in both the Angular app and in the NodeJS REST API.</span></span>  <span data-ttu-id="36f52-162">Of course, you can override this behavior and tell adal.js to get tokens for other REST APIs if necessary - but for this simple scenario the defaults will do.</span><span class="sxs-lookup"><span data-stu-id="36f52-162">Of course, you can override this behavior and tell adal.js to get tokens for other REST APIs if necessary - but for this simple scenario the defaults will do.</span></span>

<span data-ttu-id="36f52-163">Here's a snippet that shows how easy it is to send requests with bearer tokens from Azure AD:</span><span class="sxs-lookup"><span data-stu-id="36f52-163">Here's a snippet that shows how easy it is to send requests with bearer tokens from Azure AD:</span></span>

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

<span data-ttu-id="36f52-164">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="36f52-164">Congratulations!</span></span>  <span data-ttu-id="36f52-165">Your Azure AD integrated single page app is now complete.</span><span class="sxs-lookup"><span data-stu-id="36f52-165">Your Azure AD integrated single page app is now complete.</span></span>  <span data-ttu-id="36f52-166">Go ahead, take a bow.</span><span class="sxs-lookup"><span data-stu-id="36f52-166">Go ahead, take a bow.</span></span>  <span data-ttu-id="36f52-167">It can authenticate users, securely call its backend REST API using OpenID Connect, and get basic information about the user.</span><span class="sxs-lookup"><span data-stu-id="36f52-167">It can authenticate users, securely call its backend REST API using OpenID Connect, and get basic information about the user.</span></span>  <span data-ttu-id="36f52-168">Out of the box, it supports any user with a personal Microsoft Account or a work/school account from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="36f52-168">Out of the box, it supports any user with a personal Microsoft Account or a work/school account from Azure AD.</span></span>  <span data-ttu-id="36f52-169">Run the app, and in a browser navigate to `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="36f52-169">Run the app, and in a browser navigate to `https://localhost:44326/`.</span></span>  <span data-ttu-id="36f52-170">Sign in using either a personal Microsoft account or a work/school account.</span><span class="sxs-lookup"><span data-stu-id="36f52-170">Sign in using either a personal Microsoft account or a work/school account.</span></span>  <span data-ttu-id="36f52-171">Add tasks to the user's to-do list, and sign out.  Try signing in with the other type of account.</span><span class="sxs-lookup"><span data-stu-id="36f52-171">Add tasks to the user's to-do list, and sign out.  Try signing in with the other type of account.</span></span> <span data-ttu-id="36f52-172">If you need an Azure AD tenant to create work/school users, [learn how to get one here](active-directory-howto-tenant.md) (it's free).</span><span class="sxs-lookup"><span data-stu-id="36f52-172">If you need an Azure AD tenant to create work/school users, [learn how to get one here](active-directory-howto-tenant.md) (it's free).</span></span>

<span data-ttu-id="36f52-173">To continue learning about the v2.0 endpoint, head back to our [v2.0 developer guide](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="36f52-173">To continue learning about the v2.0 endpoint, head back to our [v2.0 developer guide](active-directory-appmodel-v2-overview.md).</span></span>  <span data-ttu-id="36f52-174">For additional resources, check out:</span><span class="sxs-lookup"><span data-stu-id="36f52-174">For additional resources, check out:</span></span>

* [<span data-ttu-id="36f52-175">Azure-Samples on GitHub >></span><span class="sxs-lookup"><span data-stu-id="36f52-175">Azure-Samples on GitHub >></span></span>](https://github.com/Azure-Samples)
* [<span data-ttu-id="36f52-176">Azure AD on Stack Overflow >></span><span class="sxs-lookup"><span data-stu-id="36f52-176">Azure AD on Stack Overflow >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* <span data-ttu-id="36f52-177">Azure AD documentation on [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span><span class="sxs-lookup"><span data-stu-id="36f52-177">Azure AD documentation on [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span></span>

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="36f52-178">Get security updates for our products</span><span class="sxs-lookup"><span data-stu-id="36f52-178">Get security updates for our products</span></span>
<span data-ttu-id="36f52-179">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span><span class="sxs-lookup"><span data-stu-id="36f52-179">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

