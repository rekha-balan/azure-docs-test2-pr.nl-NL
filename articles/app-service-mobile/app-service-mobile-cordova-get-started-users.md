---
title: Add authentication on Apache Cordova with Mobile Apps | Microsoft Docs
description: Learn how to use Mobile Apps in Azure App Service to authenticate users of your Apache Cordova app through a variety of identity providers, including Google, Facebook, Twitter, and Microsoft.
services: app-service\mobile
documentationcenter: javascript
author: adrianhall
manager: adrianha
editor: ''
ms.assetid: 10dd6dc9-ddf5-423d-8205-00ad74929f0d
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: adrianha
ms.openlocfilehash: 00470453d1a228346160b90ae0b30cc558fe6f5f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553100"
---
# <a name="add-authentication-to-your-apache-cordova-app"></a><span data-ttu-id="9f791-103">Add authentication to your Apache Cordova app</span><span class="sxs-lookup"><span data-stu-id="9f791-103">Add authentication to your Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a><span data-ttu-id="9f791-104">Summary</span><span class="sxs-lookup"><span data-stu-id="9f791-104">Summary</span></span>
<span data-ttu-id="9f791-105">In this tutorial, you add authentication to the todolist quickstart project on Apache Cordova using a supported identity provider.</span><span class="sxs-lookup"><span data-stu-id="9f791-105">In this tutorial, you add authentication to the todolist quickstart project on Apache Cordova using a supported identity provider.</span></span> <span data-ttu-id="9f791-106">This tutorial is based on the [Get started with Mobile Apps] tutorial, which you must complete first.</span><span class="sxs-lookup"><span data-stu-id="9f791-106">This tutorial is based on the [Get started with Mobile Apps] tutorial, which you must complete first.</span></span>

## <a name="register"></a><span data-ttu-id="9f791-107">Register your app for authentication and configure the App Service</span><span class="sxs-lookup"><span data-stu-id="9f791-107">Register your app for authentication and configure the App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

[<span data-ttu-id="9f791-108">Watch a video showing similar steps</span><span class="sxs-lookup"><span data-stu-id="9f791-108">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-8-Azure-authentication)

## <a name="permissions"></a><span data-ttu-id="9f791-109">Restrict permissions to authenticated users</span><span class="sxs-lookup"><span data-stu-id="9f791-109">Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="9f791-110">Now, you can verify that anonymous access to your backend has been disabled.</span><span class="sxs-lookup"><span data-stu-id="9f791-110">Now, you can verify that anonymous access to your backend has been disabled.</span></span> <span data-ttu-id="9f791-111">In Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="9f791-111">In Visual Studio:</span></span>

* <span data-ttu-id="9f791-112">Open the project that you created when you completed the tutorial [Get started with Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="9f791-112">Open the project that you created when you completed the tutorial [Get started with Mobile Apps].</span></span>
* <span data-ttu-id="9f791-113">Run your application in the **Google Android Emulator**.</span><span class="sxs-lookup"><span data-stu-id="9f791-113">Run your application in the **Google Android Emulator**.</span></span>
* <span data-ttu-id="9f791-114">Verify that an Unexpected Connection Failure is shown after the app starts.</span><span class="sxs-lookup"><span data-stu-id="9f791-114">Verify that an Unexpected Connection Failure is shown after the app starts.</span></span>

<span data-ttu-id="9f791-115">Next, update the app to authenticate users before requesting resources from the Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="9f791-115">Next, update the app to authenticate users before requesting resources from the Mobile App backend.</span></span>

## <a name="add-authentication"></a><span data-ttu-id="9f791-116">Add authentication to the app</span><span class="sxs-lookup"><span data-stu-id="9f791-116">Add authentication to the app</span></span>
1. <span data-ttu-id="9f791-117">Open your project in **Visual Studio**, then open the `www/index.html` file for editing.</span><span class="sxs-lookup"><span data-stu-id="9f791-117">Open your project in **Visual Studio**, then open the `www/index.html` file for editing.</span></span>
2. <span data-ttu-id="9f791-118">Locate the `Content-Security-Policy` meta tag in the head section.</span><span class="sxs-lookup"><span data-stu-id="9f791-118">Locate the `Content-Security-Policy` meta tag in the head section.</span></span>  <span data-ttu-id="9f791-119">Add the OAuth host to the list of allowed sources.</span><span class="sxs-lookup"><span data-stu-id="9f791-119">Add the OAuth host to the list of allowed sources.</span></span>

   | <span data-ttu-id="9f791-120">Provider</span><span class="sxs-lookup"><span data-stu-id="9f791-120">Provider</span></span> | <span data-ttu-id="9f791-121">SDK Provider Name</span><span class="sxs-lookup"><span data-stu-id="9f791-121">SDK Provider Name</span></span> | <span data-ttu-id="9f791-122">OAuth Host</span><span class="sxs-lookup"><span data-stu-id="9f791-122">OAuth Host</span></span> |
   |:--- |:--- |:--- |
   | <span data-ttu-id="9f791-123">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9f791-123">Azure Active Directory</span></span> | <span data-ttu-id="9f791-124">aad</span><span class="sxs-lookup"><span data-stu-id="9f791-124">aad</span></span> | https://login.windows.net |
   | <span data-ttu-id="9f791-125">Facebook</span><span class="sxs-lookup"><span data-stu-id="9f791-125">Facebook</span></span> | <span data-ttu-id="9f791-126">facebook</span><span class="sxs-lookup"><span data-stu-id="9f791-126">facebook</span></span> | https://www.facebook.com |
   | <span data-ttu-id="9f791-127">Google</span><span class="sxs-lookup"><span data-stu-id="9f791-127">Google</span></span> | <span data-ttu-id="9f791-128">google</span><span class="sxs-lookup"><span data-stu-id="9f791-128">google</span></span> | https://accounts.google.com |
   | <span data-ttu-id="9f791-129">Microsoft</span><span class="sxs-lookup"><span data-stu-id="9f791-129">Microsoft</span></span> | <span data-ttu-id="9f791-130">microsoftaccount</span><span class="sxs-lookup"><span data-stu-id="9f791-130">microsoftaccount</span></span> | https://login.live.com |
   | <span data-ttu-id="9f791-131">Twitter</span><span class="sxs-lookup"><span data-stu-id="9f791-131">Twitter</span></span> | <span data-ttu-id="9f791-132">twitter</span><span class="sxs-lookup"><span data-stu-id="9f791-132">twitter</span></span> | https://api.twitter.com |

    <span data-ttu-id="9f791-133">An example Content-Security-Policy (implemented for Azure Active Directory) is as follows:</span><span class="sxs-lookup"><span data-stu-id="9f791-133">An example Content-Security-Policy (implemented for Azure Active Directory) is as follows:</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self'
            data: gap: https://login.windows.net https://yourapp.azurewebsites.net; style-src 'self'">

    <span data-ttu-id="9f791-134">Replace `https://login.windows.net` with the OAuth host from the preceding table.</span><span class="sxs-lookup"><span data-stu-id="9f791-134">Replace `https://login.windows.net` with the OAuth host from the preceding table.</span></span>  <span data-ttu-id="9f791-135">For more information about the content-security-policy meta tag, see the [Content-Security-Policy documentation].</span><span class="sxs-lookup"><span data-stu-id="9f791-135">For more information about the content-security-policy meta tag, see the [Content-Security-Policy documentation].</span></span>

    <span data-ttu-id="9f791-136">Some authentication providers do not require Content-Security-Policy changes when used on appropriate mobile devices.</span><span class="sxs-lookup"><span data-stu-id="9f791-136">Some authentication providers do not require Content-Security-Policy changes when used on appropriate mobile devices.</span></span>  <span data-ttu-id="9f791-137">For example, no Content-Security-Policy changes are required when using Google authentication on an Android device.</span><span class="sxs-lookup"><span data-stu-id="9f791-137">For example, no Content-Security-Policy changes are required when using Google authentication on an Android device.</span></span>

3. <span data-ttu-id="9f791-138">Open the `www/js/index.js` file for editing, locate the `onDeviceReady()` method, and under the client  creation code add the following code:</span><span class="sxs-lookup"><span data-stu-id="9f791-138">Open the `www/js/index.js` file for editing, locate the `onDeviceReady()` method, and under the client  creation code add the following code:</span></span>

        // Login to the service
        client.login('SDK_Provider_Name')
            .then(function () {

                // BEGINNING OF ORIGINAL CODE

                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh the todoItems
                refreshDisplay();

                // Wire up the UI Event Handler for the Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                // END OF ORIGINAL CODE

            }, handleError);

    <span data-ttu-id="9f791-139">This code replaces the existing code that creates the table reference and refreshes the UI.</span><span class="sxs-lookup"><span data-stu-id="9f791-139">This code replaces the existing code that creates the table reference and refreshes the UI.</span></span>

    <span data-ttu-id="9f791-140">The login() method starts authentication with the provider.</span><span class="sxs-lookup"><span data-stu-id="9f791-140">The login() method starts authentication with the provider.</span></span> <span data-ttu-id="9f791-141">The login() method is an async function that returns a JavaScript Promise.</span><span class="sxs-lookup"><span data-stu-id="9f791-141">The login() method is an async function that returns a JavaScript Promise.</span></span>  <span data-ttu-id="9f791-142">The rest of the initialization is placed inside the promise response so that it is not executed until the login() method completes.</span><span class="sxs-lookup"><span data-stu-id="9f791-142">The rest of the initialization is placed inside the promise response so that it is not executed until the login() method completes.</span></span>

4. <span data-ttu-id="9f791-143">In the code that you just added, replace `SDK_Provider_Name` with the name of your login provider.</span><span class="sxs-lookup"><span data-stu-id="9f791-143">In the code that you just added, replace `SDK_Provider_Name` with the name of your login provider.</span></span> <span data-ttu-id="9f791-144">For example, for Azure Active Directory, use `client.login('aad')`.</span><span class="sxs-lookup"><span data-stu-id="9f791-144">For example, for Azure Active Directory, use `client.login('aad')`.</span></span>
5. <span data-ttu-id="9f791-145">Run your project.</span><span class="sxs-lookup"><span data-stu-id="9f791-145">Run your project.</span></span>  <span data-ttu-id="9f791-146">When the project has finished initializing, your application shows the OAuth login page for the chosen authentication provider.</span><span class="sxs-lookup"><span data-stu-id="9f791-146">When the project has finished initializing, your application shows the OAuth login page for the chosen authentication provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f791-147">Next Steps</span><span class="sxs-lookup"><span data-stu-id="9f791-147">Next Steps</span></span>
* <span data-ttu-id="9f791-148">Learn more [About Authentication] with Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="9f791-148">Learn more [About Authentication] with Azure App Service.</span></span>
* <span data-ttu-id="9f791-149">Continue the tutorial by adding [Push Notifications] to your Apache Cordova app.</span><span class="sxs-lookup"><span data-stu-id="9f791-149">Continue the tutorial by adding [Push Notifications] to your Apache Cordova app.</span></span>

<span data-ttu-id="9f791-150">Learn how to use the SDKs.</span><span class="sxs-lookup"><span data-stu-id="9f791-150">Learn how to use the SDKs.</span></span>

* <span data-ttu-id="9f791-151">[Apache Cordova SDK]</span><span class="sxs-lookup"><span data-stu-id="9f791-151">[Apache Cordova SDK]</span></span>
* <span data-ttu-id="9f791-152">[ASP.NET Server SDK]</span><span class="sxs-lookup"><span data-stu-id="9f791-152">[ASP.NET Server SDK]</span></span>
* <span data-ttu-id="9f791-153">[Node.js Server SDK]</span><span class="sxs-lookup"><span data-stu-id="9f791-153">[Node.js Server SDK]</span></span>

<!-- URLs. -->
[Get started with Mobile Apps]: app-service-mobile-cordova-get-started.md
[Content-Security-Policy documentation]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html
[Push Notifications]: app-service-mobile-cordova-get-started-push.md
[About Authentication]: app-service-mobile-auth.md
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
