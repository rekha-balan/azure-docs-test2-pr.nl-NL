---
title: How to Use the JavaScript SDK for Azure Mobile Apps
description: How to Use v for Azure Mobile Apps
services: app-service\mobile
documentationcenter: javascript
author: adrianhall
manager: adrianha
editor: ''
ms.assetid: 53b78965-caa3-4b22-bb67-5bd5c19d03c4
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: adrianha
ms.openlocfilehash: 29b9ce7cad1e007619dab4d2086cb79d39d65667
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564585"
---
# <a name="how-to-use-the-javascript-client-library-for-azure-mobile-apps"></a><span data-ttu-id="41823-103">How to Use the JavaScript client library for Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="41823-103">How to Use the JavaScript client library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="41823-104">This guide teaches you to perform common scenarios using the latest [JavaScript SDK for Azure Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="41823-104">This guide teaches you to perform common scenarios using the latest [JavaScript SDK for Azure Mobile Apps].</span></span> <span data-ttu-id="41823-105">If you are new to Azure Mobile Apps, first complete [Azure Mobile Apps Quick Start] to create a backend and create a table.</span><span class="sxs-lookup"><span data-stu-id="41823-105">If you are new to Azure Mobile Apps, first complete [Azure Mobile Apps Quick Start] to create a backend and create a table.</span></span> <span data-ttu-id="41823-106">In this guide, we focus on using the mobile backend in HTML/JavaScript Web applications.</span><span class="sxs-lookup"><span data-stu-id="41823-106">In this guide, we focus on using the mobile backend in HTML/JavaScript Web applications.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="41823-107">Supported platforms</span><span class="sxs-lookup"><span data-stu-id="41823-107">Supported platforms</span></span>
<span data-ttu-id="41823-108">We limit browser support to the current and last versions of the major browsers:  Google Chrome, Microsoft Edge, Microsoft Internet Explorer, and Mozilla Firefox.</span><span class="sxs-lookup"><span data-stu-id="41823-108">We limit browser support to the current and last versions of the major browsers:  Google Chrome, Microsoft Edge, Microsoft Internet Explorer, and Mozilla Firefox.</span></span>  <span data-ttu-id="41823-109">We expect the SDK to function with any relatively modern browser.</span><span class="sxs-lookup"><span data-stu-id="41823-109">We expect the SDK to function with any relatively modern browser.</span></span>

<span data-ttu-id="41823-110">The package is distributed as a Universal JavaScript Module, so it supports globals, AMD, and CommonJS formats.</span><span class="sxs-lookup"><span data-stu-id="41823-110">The package is distributed as a Universal JavaScript Module, so it supports globals, AMD, and CommonJS formats.</span></span>

## <a name="Setup"></a><span data-ttu-id="41823-111">Setup and prerequisites</span><span class="sxs-lookup"><span data-stu-id="41823-111">Setup and prerequisites</span></span>
<span data-ttu-id="41823-112">This guide assumes that you have created a backend with a table.</span><span class="sxs-lookup"><span data-stu-id="41823-112">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="41823-113">This guide assumes that the table has the same schema as the tables in those tutorials.</span><span class="sxs-lookup"><span data-stu-id="41823-113">This guide assumes that the table has the same schema as the tables in those tutorials.</span></span>

<span data-ttu-id="41823-114">Installing the Azure Mobile Apps JavaScript SDK can be done via the `npm` command:</span><span class="sxs-lookup"><span data-stu-id="41823-114">Installing the Azure Mobile Apps JavaScript SDK can be done via the `npm` command:</span></span>

```
npm install azure-mobile-apps-client --save
```

<span data-ttu-id="41823-115">The library can also be used as an ES2015 module, within CommonJS environments such as Browserify and Webpack and as an AMD library.</span><span class="sxs-lookup"><span data-stu-id="41823-115">The library can also be used as an ES2015 module, within CommonJS environments such as Browserify and Webpack and as an AMD library.</span></span>  <span data-ttu-id="41823-116">For example:</span><span class="sxs-lookup"><span data-stu-id="41823-116">For example:</span></span>

```
# For ECMAScript 5.1 CommonJS
var WindowsAzure = require('azure-mobile-apps-client');
# For ES2015 modules
import * as WindowsAzure from 'azure-mobile-apps-client';
```

<span data-ttu-id="41823-117">You can also use a pre-built version of the SDK by downloading directly from our CDN:</span><span class="sxs-lookup"><span data-stu-id="41823-117">You can also use a pre-built version of the SDK by downloading directly from our CDN:</span></span>

```html
<script src="https://zumo.blob.core.windows.net/sdk/azure-mobile-apps-client.min.js"></script>
```

[!INCLUDE [app-service-mobile-html-js-library](../../includes/app-service-mobile-html-js-library.md)]

## <a name="auth"></a><span data-ttu-id="41823-118">How to: Authenticate users</span><span class="sxs-lookup"><span data-stu-id="41823-118">How to: Authenticate users</span></span>
<span data-ttu-id="41823-119">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span><span class="sxs-lookup"><span data-stu-id="41823-119">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span></span> <span data-ttu-id="41823-120">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span><span class="sxs-lookup"><span data-stu-id="41823-120">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="41823-121">You can also use the identity of authenticated users to implement authorization rules in server scripts.</span><span class="sxs-lookup"><span data-stu-id="41823-121">You can also use the identity of authenticated users to implement authorization rules in server scripts.</span></span> <span data-ttu-id="41823-122">For more information, see the [Get started with authentication] tutorial.</span><span class="sxs-lookup"><span data-stu-id="41823-122">For more information, see the [Get started with authentication] tutorial.</span></span>

<span data-ttu-id="41823-123">Two authentication flows are supported: a server flow and a client flow.</span><span class="sxs-lookup"><span data-stu-id="41823-123">Two authentication flows are supported: a server flow and a client flow.</span></span>  <span data-ttu-id="41823-124">The server flow provides the simplest authentication experience, as it relies on the provider's web authentication interface.</span><span class="sxs-lookup"><span data-stu-id="41823-124">The server flow provides the simplest authentication experience, as it relies on the provider's web authentication interface.</span></span> <span data-ttu-id="41823-125">The client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific SDKs.</span><span class="sxs-lookup"><span data-stu-id="41823-125">The client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific SDKs.</span></span>

[!INCLUDE [app-service-mobile-html-js-auth-library](../../includes/app-service-mobile-html-js-auth-library.md)]

### <a name="configure-external-redirect-urls"></a><span data-ttu-id="41823-126">How to: Configure your Mobile App Service for external redirect URLs.</span><span class="sxs-lookup"><span data-stu-id="41823-126">How to: Configure your Mobile App Service for external redirect URLs.</span></span>
<span data-ttu-id="41823-127">Several types of JavaScript applications use a loopback capability to handle OAuth UI flows.</span><span class="sxs-lookup"><span data-stu-id="41823-127">Several types of JavaScript applications use a loopback capability to handle OAuth UI flows.</span></span>  <span data-ttu-id="41823-128">These capabilities include:</span><span class="sxs-lookup"><span data-stu-id="41823-128">These capabilities include:</span></span>

* <span data-ttu-id="41823-129">Running your service locally</span><span class="sxs-lookup"><span data-stu-id="41823-129">Running your service locally</span></span>
* <span data-ttu-id="41823-130">Using Live Reload with the Ionic Framework</span><span class="sxs-lookup"><span data-stu-id="41823-130">Using Live Reload with the Ionic Framework</span></span>
* <span data-ttu-id="41823-131">Redirecting to App Service for authentication.</span><span class="sxs-lookup"><span data-stu-id="41823-131">Redirecting to App Service for authentication.</span></span>

<span data-ttu-id="41823-132">Running locally can cause problems because, by default, App Service authentication is only configured to allow access from your Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="41823-132">Running locally can cause problems because, by default, App Service authentication is only configured to allow access from your Mobile App backend.</span></span> <span data-ttu-id="41823-133">Use the following steps to change the App Service settings to enable authentication when running the server locally:</span><span class="sxs-lookup"><span data-stu-id="41823-133">Use the following steps to change the App Service settings to enable authentication when running the server locally:</span></span>

1. <span data-ttu-id="41823-134">Log in to the [Azure portal]</span><span class="sxs-lookup"><span data-stu-id="41823-134">Log in to the [Azure portal]</span></span>
2. <span data-ttu-id="41823-135">Navigate to your Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="41823-135">Navigate to your Mobile App backend.</span></span>
3. <span data-ttu-id="41823-136">Select **Resource explorer** in the **DEVELOPMENT TOOLS** menu.</span><span class="sxs-lookup"><span data-stu-id="41823-136">Select **Resource explorer** in the **DEVELOPMENT TOOLS** menu.</span></span>
4. <span data-ttu-id="41823-137">Click **Go** to open the resource explorer for your Mobile App backend in a new tab or window.</span><span class="sxs-lookup"><span data-stu-id="41823-137">Click **Go** to open the resource explorer for your Mobile App backend in a new tab or window.</span></span>
5. <span data-ttu-id="41823-138">Expand the **config** > **authsettings** node for your app.</span><span class="sxs-lookup"><span data-stu-id="41823-138">Expand the **config** > **authsettings** node for your app.</span></span>
6. <span data-ttu-id="41823-139">Click the **Edit** button to enable editing of the resource.</span><span class="sxs-lookup"><span data-stu-id="41823-139">Click the **Edit** button to enable editing of the resource.</span></span>
7. <span data-ttu-id="41823-140">Find the **allowedExternalRedirectUrls** element, which should be null.</span><span class="sxs-lookup"><span data-stu-id="41823-140">Find the **allowedExternalRedirectUrls** element, which should be null.</span></span> <span data-ttu-id="41823-141">Add your URLs in an array:</span><span class="sxs-lookup"><span data-stu-id="41823-141">Add your URLs in an array:</span></span>

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    <span data-ttu-id="41823-142">Replace the URLs in the array with the URLs of your service, which in this example is `http://localhost:3000` for the local Node.js sample service.</span><span class="sxs-lookup"><span data-stu-id="41823-142">Replace the URLs in the array with the URLs of your service, which in this example is `http://localhost:3000` for the local Node.js sample service.</span></span> <span data-ttu-id="41823-143">You could also use `http://localhost:4400` for the Ripple service or some other URL, depending on how your app is configured.</span><span class="sxs-lookup"><span data-stu-id="41823-143">You could also use `http://localhost:4400` for the Ripple service or some other URL, depending on how your app is configured.</span></span>
8. <span data-ttu-id="41823-144">At the top of the page, click **Read/Write**, then click **PUT** to save your updates.</span><span class="sxs-lookup"><span data-stu-id="41823-144">At the top of the page, click **Read/Write**, then click **PUT** to save your updates.</span></span>

<span data-ttu-id="41823-145">You also need to add the same loopback URLs to the CORS whitelist settings:</span><span class="sxs-lookup"><span data-stu-id="41823-145">You also need to add the same loopback URLs to the CORS whitelist settings:</span></span>

1. <span data-ttu-id="41823-146">Navigate back to the [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="41823-146">Navigate back to the [Azure portal].</span></span>
2. <span data-ttu-id="41823-147">Navigate to your Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="41823-147">Navigate to your Mobile App backend.</span></span>
3. <span data-ttu-id="41823-148">Click **CORS** in the **API** menu.</span><span class="sxs-lookup"><span data-stu-id="41823-148">Click **CORS** in the **API** menu.</span></span>
4. <span data-ttu-id="41823-149">Enter each URL in the empty **Allowed Origins** text box.</span><span class="sxs-lookup"><span data-stu-id="41823-149">Enter each URL in the empty **Allowed Origins** text box.</span></span>  <span data-ttu-id="41823-150">A new text box is created.</span><span class="sxs-lookup"><span data-stu-id="41823-150">A new text box is created.</span></span>
5. <span data-ttu-id="41823-151">Click **SAVE**</span><span class="sxs-lookup"><span data-stu-id="41823-151">Click **SAVE**</span></span>

<span data-ttu-id="41823-152">After the backend updates, you will be able to use the new loopback URLs in your app.</span><span class="sxs-lookup"><span data-stu-id="41823-152">After the backend updates, you will be able to use the new loopback URLs in your app.</span></span>

<!-- URLs. -->
[Azure Mobile Apps Quick Start]: app-service-mobile-cordova-get-started.md
[Get started with authentication]: app-service-mobile-cordova-get-started-users.md
[Add authentication to your app]: app-service-mobile-cordova-get-started-users.md

[Azure portal]: https://portal.azure.com/
[JavaScript SDK for Azure Mobile Apps]: https://www.npmjs.com/package/azure-mobile-apps-client
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx

