---
title: Azure AD v2.0 NodeJS AngularJS single page app getting started | Microsoft Docs
description: How to build an Angular JS Single Page app that signs in users with both personal Microsoft accounts and work or school accounts.
services: active-directory
documentationcenter: ''
author: dstrockis
manager: mbaldwin
editor: ''
ms.assetid: d286aa33-8a94-452f-beb7-ddc6c6daa5c8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.openlocfilehash: 3f2e856b71a42fe677d92c9c020236b8f0da9c1e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44672310"
---
# <a name="add-sign-in-to-an-angularjs-single-page-app---nodejs"></a><span data-ttu-id="f9825-103">Add sign-in to an AngularJS single page app - NodeJS</span><span class="sxs-lookup"><span data-stu-id="f9825-103">Add sign-in to an AngularJS single page app - NodeJS</span></span>
<span data-ttu-id="f9825-104">In this article we'll add sign in with Microsoft powered accounts to an AngularJS app using the Azure Active Directory v2.0 endpoint.</span><span class="sxs-lookup"><span data-stu-id="f9825-104">In this article we'll add sign in with Microsoft powered accounts to an AngularJS app using the Azure Active Directory v2.0 endpoint.</span></span> <span data-ttu-id="f9825-105">the v2.0 endpoint enable you to perform a single integration in your app and authenticate users with both personal and work/school accounts.</span><span class="sxs-lookup"><span data-stu-id="f9825-105">the v2.0 endpoint enable you to perform a single integration in your app and authenticate users with both personal and work/school accounts.</span></span>

<span data-ttu-id="f9825-106">This sample is a simple To-Do List single page app that stores tasks in a backend REST API, written in NodeJS and secured using OAuth bearer tokens from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f9825-106">This sample is a simple To-Do List single page app that stores tasks in a backend REST API, written in NodeJS and secured using OAuth bearer tokens from Azure AD.</span></span>  <span data-ttu-id="f9825-107">The AngularJS app will use our open source JavaScript authentication library [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) to handle the entire sign in process and acquire tokens for calling the REST API.</span><span class="sxs-lookup"><span data-stu-id="f9825-107">The AngularJS app will use our open source JavaScript authentication library [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) to handle the entire sign in process and acquire tokens for calling the REST API.</span></span>  <span data-ttu-id="f9825-108">The same pattern can be applied to authenticate to other REST APIs, like the [Microsoft Graph](https://graph.microsoft.com) or the Azure Resource Manager APIs.</span><span class="sxs-lookup"><span data-stu-id="f9825-108">The same pattern can be applied to authenticate to other REST APIs, like the [Microsoft Graph](https://graph.microsoft.com) or the Azure Resource Manager APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="f9825-109">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span><span class="sxs-lookup"><span data-stu-id="f9825-109">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="f9825-110">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="f9825-110">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download"></a><span data-ttu-id="f9825-111">Download</span><span class="sxs-lookup"><span data-stu-id="f9825-111">Download</span></span>
<span data-ttu-id="f9825-112">To get started, you'll need to download & install [node.js](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="f9825-112">To get started, you'll need to download & install [node.js](https://nodejs.org).</span></span>  <span data-ttu-id="f9825-113">Then you can clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) a skeleton app:</span><span class="sxs-lookup"><span data-stu-id="f9825-113">Then you can clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) a skeleton app:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS.git
```

<span data-ttu-id="f9825-114">The skeleton app includes all the boilerplate code for a simple AngularJS app, but is missing all of the identity-related pieces.</span><span class="sxs-lookup"><span data-stu-id="f9825-114">The skeleton app includes all the boilerplate code for a simple AngularJS app, but is missing all of the identity-related pieces.</span></span>  <span data-ttu-id="f9825-115">If you don't want to follow along, you can instead clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip) the completed sample.</span><span class="sxs-lookup"><span data-stu-id="f9825-115">If you don't want to follow along, you can instead clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip) the completed sample.</span></span>

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-NodeJS.git
```

## <a name="register-an-app"></a><span data-ttu-id="f9825-116">Register an app</span><span class="sxs-lookup"><span data-stu-id="f9825-116">Register an app</span></span>
<span data-ttu-id="f9825-117">First, create an app in the [App Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="f9825-117">First, create an app in the [App Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="f9825-118">Make sure to:</span><span class="sxs-lookup"><span data-stu-id="f9825-118">Make sure to:</span></span>

* <span data-ttu-id="f9825-119">Add the **Web** platform for your app.</span><span class="sxs-lookup"><span data-stu-id="f9825-119">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="f9825-120">Enter the correct **Redirect URI**.</span><span class="sxs-lookup"><span data-stu-id="f9825-120">Enter the correct **Redirect URI**.</span></span> <span data-ttu-id="f9825-121">The default for this sample is `http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="f9825-121">The default for this sample is `http://localhost:8080`.</span></span>
* <span data-ttu-id="f9825-122">Leave the **Allow Implicit Flow** checkbox enabled.</span><span class="sxs-lookup"><span data-stu-id="f9825-122">Leave the **Allow Implicit Flow** checkbox enabled.</span></span> 

<span data-ttu-id="f9825-123">Copy down the **Application ID** that is assigned to your app, you'll need it shortly.</span><span class="sxs-lookup"><span data-stu-id="f9825-123">Copy down the **Application ID** that is assigned to your app, you'll need it shortly.</span></span> 

## <a name="install-adaljs"></a><span data-ttu-id="f9825-124">Install adal.js</span><span class="sxs-lookup"><span data-stu-id="f9825-124">Install adal.js</span></span>
<span data-ttu-id="f9825-125">To start, navigate to project you downloaded and install adal.js.</span><span class="sxs-lookup"><span data-stu-id="f9825-125">To start, navigate to project you downloaded and install adal.js.</span></span>  <span data-ttu-id="f9825-126">If you have [bower](http://bower.io/) installed, you can just run this command.</span><span class="sxs-lookup"><span data-stu-id="f9825-126">If you have [bower](http://bower.io/) installed, you can just run this command.</span></span>  <span data-ttu-id="f9825-127">For any dependency version mismatches, just choose the higher version.</span><span class="sxs-lookup"><span data-stu-id="f9825-127">For any dependency version mismatches, just choose the higher version.</span></span>

```
bower install adal-angular#experimental
```

<span data-ttu-id="f9825-128">Alternatively, you can manually download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) and [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span><span class="sxs-lookup"><span data-stu-id="f9825-128">Alternatively, you can manually download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) and [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span></span>  <span data-ttu-id="f9825-129">Add both files to the `app/lib/adal-angular-experimental/dist` directory.</span><span class="sxs-lookup"><span data-stu-id="f9825-129">Add both files to the `app/lib/adal-angular-experimental/dist` directory.</span></span>

<span data-ttu-id="f9825-130">Now open the project in your favorite text editor, and load adal.js at the end of the page body:</span><span class="sxs-lookup"><span data-stu-id="f9825-130">Now open the project in your favorite text editor, and load adal.js at the end of the page body:</span></span>

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-the-rest-api"></a><span data-ttu-id="f9825-131">Set up the REST API</span><span class="sxs-lookup"><span data-stu-id="f9825-131">Set up the REST API</span></span>
<span data-ttu-id="f9825-132">While we're setting things up, lets get the backend REST API working.</span><span class="sxs-lookup"><span data-stu-id="f9825-132">While we're setting things up, lets get the backend REST API working.</span></span>  <span data-ttu-id="f9825-133">In a command prompt, install all the necessary packages by running (make sure you're in the top-level directory of the project):</span><span class="sxs-lookup"><span data-stu-id="f9825-133">In a command prompt, install all the necessary packages by running (make sure you're in the top-level directory of the project):</span></span>

```
npm install
```

<span data-ttu-id="f9825-134">Now open `config.js` and replace the `audience` value:</span><span class="sxs-lookup"><span data-stu-id="f9825-134">Now open `config.js` and replace the `audience` value:</span></span>

```js
exports.creds = {

     // TODO: Replace this value with the Application ID from the registration portal
     audience: '<Your-application-id>',

     ...
}
```

<span data-ttu-id="f9825-135">The REST API will use this value to validate tokens it receives from the Angular app on AJAX requests.</span><span class="sxs-lookup"><span data-stu-id="f9825-135">The REST API will use this value to validate tokens it receives from the Angular app on AJAX requests.</span></span>  <span data-ttu-id="f9825-136">Note that this simple REST API stores data in-memory - so each time to stop the server, you will lose all previously created tasks.</span><span class="sxs-lookup"><span data-stu-id="f9825-136">Note that this simple REST API stores data in-memory - so each time to stop the server, you will lose all previously created tasks.</span></span>

<span data-ttu-id="f9825-137">That's all the time we're going to spend discussing how the REST API works.</span><span class="sxs-lookup"><span data-stu-id="f9825-137">That's all the time we're going to spend discussing how the REST API works.</span></span>  <span data-ttu-id="f9825-138">Feel free to poke around in the code, but if you want to learn more about securing web APIs with Azure AD, check out [this article](active-directory-v2-devquickstarts-node-api.md).</span><span class="sxs-lookup"><span data-stu-id="f9825-138">Feel free to poke around in the code, but if you want to learn more about securing web APIs with Azure AD, check out [this article](active-directory-v2-devquickstarts-node-api.md).</span></span> 

## <a name="sign-users-in"></a><span data-ttu-id="f9825-139">Sign users in</span><span class="sxs-lookup"><span data-stu-id="f9825-139">Sign users in</span></span>
<span data-ttu-id="f9825-140">Time to write some identity code.</span><span class="sxs-lookup"><span data-stu-id="f9825-140">Time to write some identity code.</span></span>  <span data-ttu-id="f9825-141">You might have already noticed that adal.js contains an AngularJS provider, which plays nicely with Angular routing mechanisms.</span><span class="sxs-lookup"><span data-stu-id="f9825-141">You might have already noticed that adal.js contains an AngularJS provider, which plays nicely with Angular routing mechanisms.</span></span>  <span data-ttu-id="f9825-142">Start by adding the adal module to the app:</span><span class="sxs-lookup"><span data-stu-id="f9825-142">Start by adding the adal module to the app:</span></span>

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

<span data-ttu-id="f9825-143">You can now initialize the `adalProvider` with your Application ID:</span><span class="sxs-lookup"><span data-stu-id="f9825-143">You can now initialize the `adalProvider` with your Application ID:</span></span>

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

<span data-ttu-id="f9825-144">Great, now adal.js has all the information it needs to secure your app and sign users in.</span><span class="sxs-lookup"><span data-stu-id="f9825-144">Great, now adal.js has all the information it needs to secure your app and sign users in.</span></span>  <span data-ttu-id="f9825-145">To force sign in for a particular route in the app, all it takes is one line of code:</span><span class="sxs-lookup"><span data-stu-id="f9825-145">To force sign in for a particular route in the app, all it takes is one line of code:</span></span>

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

<span data-ttu-id="f9825-146">Now when a user clicks the `TodoList` link, adal.js will automatically redirect to Azure AD for sign-in if necessary.</span><span class="sxs-lookup"><span data-stu-id="f9825-146">Now when a user clicks the `TodoList` link, adal.js will automatically redirect to Azure AD for sign-in if necessary.</span></span>  <span data-ttu-id="f9825-147">You can also explicitly send sign-in and sign-out requests by invoking adal.js in your controllers:</span><span class="sxs-lookup"><span data-stu-id="f9825-147">You can also explicitly send sign-in and sign-out requests by invoking adal.js in your controllers:</span></span>

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

## <a name="display-user-info"></a><span data-ttu-id="f9825-148">Display user info</span><span class="sxs-lookup"><span data-stu-id="f9825-148">Display user info</span></span>
<span data-ttu-id="f9825-149">Now that the user is signed in, you'll probably need to access the signed-in user's authentication data in your application.</span><span class="sxs-lookup"><span data-stu-id="f9825-149">Now that the user is signed in, you'll probably need to access the signed-in user's authentication data in your application.</span></span>  <span data-ttu-id="f9825-150">Adal.js exposes this information for you in the `userInfo` object.</span><span class="sxs-lookup"><span data-stu-id="f9825-150">Adal.js exposes this information for you in the `userInfo` object.</span></span>  <span data-ttu-id="f9825-151">To access this object in a view, first add adal.js to the root scope of the corresponding controller:</span><span class="sxs-lookup"><span data-stu-id="f9825-151">To access this object in a view, first add adal.js to the root scope of the corresponding controller:</span></span>

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

<span data-ttu-id="f9825-152">Then you can directly address the `userInfo` object in your view:</span><span class="sxs-lookup"><span data-stu-id="f9825-152">Then you can directly address the `userInfo` object in your view:</span></span> 

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

<span data-ttu-id="f9825-153">You can also use the `userInfo` object to determine if the user is signed in or not.</span><span class="sxs-lookup"><span data-stu-id="f9825-153">You can also use the `userInfo` object to determine if the user is signed in or not.</span></span>

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

## <a name="call-the-rest-api"></a><span data-ttu-id="f9825-154">Call the REST API</span><span class="sxs-lookup"><span data-stu-id="f9825-154">Call the REST API</span></span>
<span data-ttu-id="f9825-155">Finally, it's time to get some tokens and call the REST API to create, read, update, and delete tasks.</span><span class="sxs-lookup"><span data-stu-id="f9825-155">Finally, it's time to get some tokens and call the REST API to create, read, update, and delete tasks.</span></span>  <span data-ttu-id="f9825-156">Well guess what?</span><span class="sxs-lookup"><span data-stu-id="f9825-156">Well guess what?</span></span>  <span data-ttu-id="f9825-157">You don't have to do *a thing*.</span><span class="sxs-lookup"><span data-stu-id="f9825-157">You don't have to do *a thing*.</span></span>  <span data-ttu-id="f9825-158">Adal.js will automatically take care of getting, caching, and refreshing tokens.</span><span class="sxs-lookup"><span data-stu-id="f9825-158">Adal.js will automatically take care of getting, caching, and refreshing tokens.</span></span>  <span data-ttu-id="f9825-159">It will also take care of attaching those tokens to outgoing AJAX requests that you send to the REST API.</span><span class="sxs-lookup"><span data-stu-id="f9825-159">It will also take care of attaching those tokens to outgoing AJAX requests that you send to the REST API.</span></span>  

<span data-ttu-id="f9825-160">How exactly does this work?</span><span class="sxs-lookup"><span data-stu-id="f9825-160">How exactly does this work?</span></span> <span data-ttu-id="f9825-161">It's all thanks to the magic of [AngularJS interceptors](https://docs.angularjs.org/api/ng/service/$http), which allows adal.js to transform outgoing and incoming http messages.</span><span class="sxs-lookup"><span data-stu-id="f9825-161">It's all thanks to the magic of [AngularJS interceptors](https://docs.angularjs.org/api/ng/service/$http), which allows adal.js to transform outgoing and incoming http messages.</span></span>  <span data-ttu-id="f9825-162">Furthermore, adal.js assumes that any requests send to the same domain as the window should use tokens intended for the same Application ID as the AngularJS app.</span><span class="sxs-lookup"><span data-stu-id="f9825-162">Furthermore, adal.js assumes that any requests send to the same domain as the window should use tokens intended for the same Application ID as the AngularJS app.</span></span>  <span data-ttu-id="f9825-163">This is why we used the same Application ID in both the Angular app and in the NodeJS REST API.</span><span class="sxs-lookup"><span data-stu-id="f9825-163">This is why we used the same Application ID in both the Angular app and in the NodeJS REST API.</span></span>  <span data-ttu-id="f9825-164">Of course, you can override this behavior and tell adal.js to get tokens for other REST APIs if necessary - but for this simple scenario the defaults will do.</span><span class="sxs-lookup"><span data-stu-id="f9825-164">Of course, you can override this behavior and tell adal.js to get tokens for other REST APIs if necessary - but for this simple scenario the defaults will do.</span></span>

<span data-ttu-id="f9825-165">Here's a snippet that shows how easy it is to send requests with bearer tokens from Azure AD:</span><span class="sxs-lookup"><span data-stu-id="f9825-165">Here's a snippet that shows how easy it is to send requests with bearer tokens from Azure AD:</span></span>

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

<span data-ttu-id="f9825-166">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="f9825-166">Congratulations!</span></span>  <span data-ttu-id="f9825-167">Your Azure AD integrated single page app is now complete.</span><span class="sxs-lookup"><span data-stu-id="f9825-167">Your Azure AD integrated single page app is now complete.</span></span>  <span data-ttu-id="f9825-168">Go ahead, take a bow.</span><span class="sxs-lookup"><span data-stu-id="f9825-168">Go ahead, take a bow.</span></span>  <span data-ttu-id="f9825-169">It can authenticate users, securely call its backend REST API using OpenID Connect, and get basic information about the user.</span><span class="sxs-lookup"><span data-stu-id="f9825-169">It can authenticate users, securely call its backend REST API using OpenID Connect, and get basic information about the user.</span></span>  <span data-ttu-id="f9825-170">Out of the box, it supports any user with a personal Microsoft Account or a work/school account from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f9825-170">Out of the box, it supports any user with a personal Microsoft Account or a work/school account from Azure AD.</span></span>  <span data-ttu-id="f9825-171">Give the app a try by running:</span><span class="sxs-lookup"><span data-stu-id="f9825-171">Give the app a try by running:</span></span>

```
node server.js
```

<span data-ttu-id="f9825-172">In a browser navigate to `http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="f9825-172">In a browser navigate to `http://localhost:8080`.</span></span>  <span data-ttu-id="f9825-173">Sign in using either a personal Microsoft account or a work/school account.</span><span class="sxs-lookup"><span data-stu-id="f9825-173">Sign in using either a personal Microsoft account or a work/school account.</span></span>  <span data-ttu-id="f9825-174">Add tasks to the user's to-do list, and sign out.  Try signing in with the other type of account.</span><span class="sxs-lookup"><span data-stu-id="f9825-174">Add tasks to the user's to-do list, and sign out.  Try signing in with the other type of account.</span></span> <span data-ttu-id="f9825-175">If you need an Azure AD tenant to create work/school users, [learn how to get one here](active-directory-howto-tenant.md) (it's free).</span><span class="sxs-lookup"><span data-stu-id="f9825-175">If you need an Azure AD tenant to create work/school users, [learn how to get one here](active-directory-howto-tenant.md) (it's free).</span></span>

<span data-ttu-id="f9825-176">To continue learning about the the v2.0 endpoint, head back to our [v2.0 developer guide](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f9825-176">To continue learning about the the v2.0 endpoint, head back to our [v2.0 developer guide](active-directory-appmodel-v2-overview.md).</span></span>  <span data-ttu-id="f9825-177">For additional resources, check out:</span><span class="sxs-lookup"><span data-stu-id="f9825-177">For additional resources, check out:</span></span>

* [<span data-ttu-id="f9825-178">Azure-Samples on GitHub >></span><span class="sxs-lookup"><span data-stu-id="f9825-178">Azure-Samples on GitHub >></span></span>](https://github.com/Azure-Samples)
* [<span data-ttu-id="f9825-179">Azure AD on Stack Overflow >></span><span class="sxs-lookup"><span data-stu-id="f9825-179">Azure AD on Stack Overflow >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* <span data-ttu-id="f9825-180">Azure AD documentation on [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span><span class="sxs-lookup"><span data-stu-id="f9825-180">Azure AD documentation on [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span></span>

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="f9825-181">Get security updates for our products</span><span class="sxs-lookup"><span data-stu-id="f9825-181">Get security updates for our products</span></span>
<span data-ttu-id="f9825-182">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span><span class="sxs-lookup"><span data-stu-id="f9825-182">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

