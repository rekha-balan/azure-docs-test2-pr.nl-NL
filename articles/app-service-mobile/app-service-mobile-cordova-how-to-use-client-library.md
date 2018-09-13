---
title: How to Use Apache Cordova Plugin for Azure Mobile Apps
description: How to Use Apache Cordova Plugin for Azure Mobile Apps
services: app-service\mobile
documentationcenter: javascript
author: adrianhall
manager: adrianha
editor: ''
ms.assetid: a56a1ce4-de0c-4f3c-8763-66252c52aa59
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: adrianha
ms.openlocfilehash: 4b6acbf07385a0ad9042145c96af43e551f97e8d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551298"
---
# <a name="how-to-use-apache-cordova-client-library-for-azure-mobile-apps"></a><span data-ttu-id="51505-103">How to use Apache Cordova client library for Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="51505-103">How to use Apache Cordova client library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="51505-104">This guide teaches you to perform common scenarios using the latest [Apache Cordova Plugin for Azure Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="51505-104">This guide teaches you to perform common scenarios using the latest [Apache Cordova Plugin for Azure Mobile Apps].</span></span> <span data-ttu-id="51505-105">If you are new to Azure Mobile Apps, first complete [Azure Mobile Apps Quick Start] to create a backend, create a table, and download a pre-built Apache Cordova project.</span><span class="sxs-lookup"><span data-stu-id="51505-105">If you are new to Azure Mobile Apps, first complete [Azure Mobile Apps Quick Start] to create a backend, create a table, and download a pre-built Apache Cordova project.</span></span> <span data-ttu-id="51505-106">In this guide, we focus on the client-side Apache Cordova Plugin.</span><span class="sxs-lookup"><span data-stu-id="51505-106">In this guide, we focus on the client-side Apache Cordova Plugin.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="51505-107">Supported platforms</span><span class="sxs-lookup"><span data-stu-id="51505-107">Supported platforms</span></span>
<span data-ttu-id="51505-108">This SDK supports Apache Cordova v6.0.0 and later on iOS, Android, and Windows devices.</span><span class="sxs-lookup"><span data-stu-id="51505-108">This SDK supports Apache Cordova v6.0.0 and later on iOS, Android, and Windows devices.</span></span>  <span data-ttu-id="51505-109">The platform support is as follows:</span><span class="sxs-lookup"><span data-stu-id="51505-109">The platform support is as follows:</span></span>

* <span data-ttu-id="51505-110">Android API 19-24 (KitKat through Nougat).</span><span class="sxs-lookup"><span data-stu-id="51505-110">Android API 19-24 (KitKat through Nougat).</span></span>
* <span data-ttu-id="51505-111">iOS versions 8.0 and later.</span><span class="sxs-lookup"><span data-stu-id="51505-111">iOS versions 8.0 and later.</span></span>
* <span data-ttu-id="51505-112">Windows Phone 8.1.</span><span class="sxs-lookup"><span data-stu-id="51505-112">Windows Phone 8.1.</span></span>
* <span data-ttu-id="51505-113">Universal Windows Platform.</span><span class="sxs-lookup"><span data-stu-id="51505-113">Universal Windows Platform.</span></span>

## <a name="Setup"></a><span data-ttu-id="51505-114">Setup and prerequisites</span><span class="sxs-lookup"><span data-stu-id="51505-114">Setup and prerequisites</span></span>
<span data-ttu-id="51505-115">This guide assumes that you have created a backend with a table.</span><span class="sxs-lookup"><span data-stu-id="51505-115">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="51505-116">This guide assumes that the table has the same schema as the tables in those tutorials.</span><span class="sxs-lookup"><span data-stu-id="51505-116">This guide assumes that the table has the same schema as the tables in those tutorials.</span></span> <span data-ttu-id="51505-117">This guide also assumes that you have added the Apache Cordova Plugin to your code.</span><span class="sxs-lookup"><span data-stu-id="51505-117">This guide also assumes that you have added the Apache Cordova Plugin to your code.</span></span>  <span data-ttu-id="51505-118">If you have not done so, you may add the Apache Cordova plugin to your project on the command line:</span><span class="sxs-lookup"><span data-stu-id="51505-118">If you have not done so, you may add the Apache Cordova plugin to your project on the command line:</span></span>

```
cordova plugin add cordova-plugin-ms-azure-mobile-apps
```

<span data-ttu-id="51505-119">For more information on creating [your first Apache Cordova app], see their documentation.</span><span class="sxs-lookup"><span data-stu-id="51505-119">For more information on creating [your first Apache Cordova app], see their documentation.</span></span>

## <a name="ionic"></a><span data-ttu-id="51505-120">Setting up an Ionic v2 app</span><span class="sxs-lookup"><span data-stu-id="51505-120">Setting up an Ionic v2 app</span></span>

<span data-ttu-id="51505-121">To properly configure an Ionic v2 project, first create a basic app and add the Cordova plugin:</span><span class="sxs-lookup"><span data-stu-id="51505-121">To properly configure an Ionic v2 project, first create a basic app and add the Cordova plugin:</span></span>

```
ionic start projectName --v2
cd projectName
ionic plugin add cordova-plugin-ms-azure-mobile-apps
```

<span data-ttu-id="51505-122">Add the following lines to `app.component.ts` to create the client object:</span><span class="sxs-lookup"><span data-stu-id="51505-122">Add the following lines to `app.component.ts` to create the client object:</span></span>

```
declare var WindowsAzure: any;
var client = new WindowsAzure.MobileServiceClient("https://yoursite.azurewebsites.net");
```

<span data-ttu-id="51505-123">You can now build and run the project in the browser:</span><span class="sxs-lookup"><span data-stu-id="51505-123">You can now build and run the project in the browser:</span></span>

```
ionic platform add browser
ionic run browser
```

<span data-ttu-id="51505-124">The Azure Mobile Apps Cordova plugin supports both Ionic v1 and v2 apps.</span><span class="sxs-lookup"><span data-stu-id="51505-124">The Azure Mobile Apps Cordova plugin supports both Ionic v1 and v2 apps.</span></span>  <span data-ttu-id="51505-125">Only the Ionic v2 apps require the additional declaration for the `WindowsAzure` object.</span><span class="sxs-lookup"><span data-stu-id="51505-125">Only the Ionic v2 apps require the additional declaration for the `WindowsAzure` object.</span></span>

[!INCLUDE [app-service-mobile-html-js-library.md](../../includes/app-service-mobile-html-js-library.md)]

## <a name="auth"></a><span data-ttu-id="51505-126">How to: Authenticate users</span><span class="sxs-lookup"><span data-stu-id="51505-126">How to: Authenticate users</span></span>
<span data-ttu-id="51505-127">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span><span class="sxs-lookup"><span data-stu-id="51505-127">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span></span> <span data-ttu-id="51505-128">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span><span class="sxs-lookup"><span data-stu-id="51505-128">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="51505-129">You can also use the identity of authenticated users to implement authorization rules in server scripts.</span><span class="sxs-lookup"><span data-stu-id="51505-129">You can also use the identity of authenticated users to implement authorization rules in server scripts.</span></span> <span data-ttu-id="51505-130">For more information, see the [Get started with authentication] tutorial.</span><span class="sxs-lookup"><span data-stu-id="51505-130">For more information, see the [Get started with authentication] tutorial.</span></span>

<span data-ttu-id="51505-131">When using authentication in an Apache Cordova app, the following Cordova plugins must be available:</span><span class="sxs-lookup"><span data-stu-id="51505-131">When using authentication in an Apache Cordova app, the following Cordova plugins must be available:</span></span>

* <span data-ttu-id="51505-132">[cordova-plugin-device]</span><span class="sxs-lookup"><span data-stu-id="51505-132">[cordova-plugin-device]</span></span>
* <span data-ttu-id="51505-133">[cordova-plugin-inappbrowser]</span><span class="sxs-lookup"><span data-stu-id="51505-133">[cordova-plugin-inappbrowser]</span></span>

<span data-ttu-id="51505-134">Two authentication flows are supported: a server flow and a client flow.</span><span class="sxs-lookup"><span data-stu-id="51505-134">Two authentication flows are supported: a server flow and a client flow.</span></span>  <span data-ttu-id="51505-135">The server flow provides the simplest authentication experience, as it relies on the provider's web authentication interface.</span><span class="sxs-lookup"><span data-stu-id="51505-135">The server flow provides the simplest authentication experience, as it relies on the provider's web authentication interface.</span></span> <span data-ttu-id="51505-136">The client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific device-specific SDKs.</span><span class="sxs-lookup"><span data-stu-id="51505-136">The client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific device-specific SDKs.</span></span>

[!INCLUDE [app-service-mobile-html-js-auth-library.md](../../includes/app-service-mobile-html-js-auth-library.md)]

### <a name="configure-external-redirect-urls"></a><span data-ttu-id="51505-137">How to: Configure your Mobile App Service for external redirect URLs.</span><span class="sxs-lookup"><span data-stu-id="51505-137">How to: Configure your Mobile App Service for external redirect URLs.</span></span>
<span data-ttu-id="51505-138">Several types of Apache Cordova applications use a loopback capability to handle OAuth UI flows.</span><span class="sxs-lookup"><span data-stu-id="51505-138">Several types of Apache Cordova applications use a loopback capability to handle OAuth UI flows.</span></span>  <span data-ttu-id="51505-139">OAuth UI flows on localhost cause problems since the authentication service only knows how to utilize your service by default.</span><span class="sxs-lookup"><span data-stu-id="51505-139">OAuth UI flows on localhost cause problems since the authentication service only knows how to utilize your service by default.</span></span>  <span data-ttu-id="51505-140">Examples of problematic OAuth UI flows include:</span><span class="sxs-lookup"><span data-stu-id="51505-140">Examples of problematic OAuth UI flows include:</span></span>

* <span data-ttu-id="51505-141">The Ripple emulator.</span><span class="sxs-lookup"><span data-stu-id="51505-141">The Ripple emulator.</span></span>
* <span data-ttu-id="51505-142">Live Reload with Ionic.</span><span class="sxs-lookup"><span data-stu-id="51505-142">Live Reload with Ionic.</span></span>
* <span data-ttu-id="51505-143">Running the mobile backend locally</span><span class="sxs-lookup"><span data-stu-id="51505-143">Running the mobile backend locally</span></span>
* <span data-ttu-id="51505-144">Running the mobile backend in a different Azure App Service than the one providing authentication.</span><span class="sxs-lookup"><span data-stu-id="51505-144">Running the mobile backend in a different Azure App Service than the one providing authentication.</span></span>

<span data-ttu-id="51505-145">Follow these instructions to add your local settings to the configuration:</span><span class="sxs-lookup"><span data-stu-id="51505-145">Follow these instructions to add your local settings to the configuration:</span></span>

1. <span data-ttu-id="51505-146">Log in to the [Azure portal]</span><span class="sxs-lookup"><span data-stu-id="51505-146">Log in to the [Azure portal]</span></span>
2. <span data-ttu-id="51505-147">Select **All resources** or **App Services** then click the name of your Mobile App.</span><span class="sxs-lookup"><span data-stu-id="51505-147">Select **All resources** or **App Services** then click the name of your Mobile App.</span></span>
3. <span data-ttu-id="51505-148">Click **Tools**</span><span class="sxs-lookup"><span data-stu-id="51505-148">Click **Tools**</span></span>
4. <span data-ttu-id="51505-149">Click **Resource explorer** in the OBSERVE menu, then click **Go**.</span><span class="sxs-lookup"><span data-stu-id="51505-149">Click **Resource explorer** in the OBSERVE menu, then click **Go**.</span></span>  <span data-ttu-id="51505-150">A new window or tab opens.</span><span class="sxs-lookup"><span data-stu-id="51505-150">A new window or tab opens.</span></span>
5. <span data-ttu-id="51505-151">Expand the **config**, **authsettings** nodes for your site in the left-hand navigation.</span><span class="sxs-lookup"><span data-stu-id="51505-151">Expand the **config**, **authsettings** nodes for your site in the left-hand navigation.</span></span>
6. <span data-ttu-id="51505-152">Click **Edit**</span><span class="sxs-lookup"><span data-stu-id="51505-152">Click **Edit**</span></span>
7. <span data-ttu-id="51505-153">Look for the "allowedExternalRedirectUrls" element.</span><span class="sxs-lookup"><span data-stu-id="51505-153">Look for the "allowedExternalRedirectUrls" element.</span></span>  <span data-ttu-id="51505-154">It may be set to null or an array of values.</span><span class="sxs-lookup"><span data-stu-id="51505-154">It may be set to null or an array of values.</span></span>  <span data-ttu-id="51505-155">Change the value to the following value:</span><span class="sxs-lookup"><span data-stu-id="51505-155">Change the value to the following value:</span></span>

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    <span data-ttu-id="51505-156">Replace the URLs with the URLs of your service.</span><span class="sxs-lookup"><span data-stu-id="51505-156">Replace the URLs with the URLs of your service.</span></span>  <span data-ttu-id="51505-157">Examples include "http://localhost:3000" (for the Node.js sample service), or "http://localhost:4400" (for the Ripple service).</span><span class="sxs-lookup"><span data-stu-id="51505-157">Examples include "http://localhost:3000" (for the Node.js sample service), or "http://localhost:4400" (for the Ripple service).</span></span>  <span data-ttu-id="51505-158">However, these URLs are examples - your situation, including for the services mentioned in the examples, may be different.</span><span class="sxs-lookup"><span data-stu-id="51505-158">However, these URLs are examples - your situation, including for the services mentioned in the examples, may be different.</span></span>
8. <span data-ttu-id="51505-159">Click the **Read/Write** button in the top-right corner of the screen.</span><span class="sxs-lookup"><span data-stu-id="51505-159">Click the **Read/Write** button in the top-right corner of the screen.</span></span>
9. <span data-ttu-id="51505-160">Click the green **PUT** button.</span><span class="sxs-lookup"><span data-stu-id="51505-160">Click the green **PUT** button.</span></span>

<span data-ttu-id="51505-161">The settings are saved at this point.</span><span class="sxs-lookup"><span data-stu-id="51505-161">The settings are saved at this point.</span></span>  <span data-ttu-id="51505-162">Do not close the browser window until the settings have finished saving.</span><span class="sxs-lookup"><span data-stu-id="51505-162">Do not close the browser window until the settings have finished saving.</span></span>
<span data-ttu-id="51505-163">Also add these loopback URLs to the CORS settings for your App Service:</span><span class="sxs-lookup"><span data-stu-id="51505-163">Also add these loopback URLs to the CORS settings for your App Service:</span></span>

1. <span data-ttu-id="51505-164">Log in to the [Azure portal]</span><span class="sxs-lookup"><span data-stu-id="51505-164">Log in to the [Azure portal]</span></span>
2. <span data-ttu-id="51505-165">Select **All resources** or **App Services** then click the name of your Mobile App.</span><span class="sxs-lookup"><span data-stu-id="51505-165">Select **All resources** or **App Services** then click the name of your Mobile App.</span></span>
3. <span data-ttu-id="51505-166">The Settings blade opens automatically.</span><span class="sxs-lookup"><span data-stu-id="51505-166">The Settings blade opens automatically.</span></span>  <span data-ttu-id="51505-167">If it doesn't, click **All Settings**.</span><span class="sxs-lookup"><span data-stu-id="51505-167">If it doesn't, click **All Settings**.</span></span>
4. <span data-ttu-id="51505-168">Click **CORS** under the API menu.</span><span class="sxs-lookup"><span data-stu-id="51505-168">Click **CORS** under the API menu.</span></span>
5. <span data-ttu-id="51505-169">Enter the URL that you wish to add in the box provided and press Enter.</span><span class="sxs-lookup"><span data-stu-id="51505-169">Enter the URL that you wish to add in the box provided and press Enter.</span></span>
6. <span data-ttu-id="51505-170">Enter additional URLs as needed.</span><span class="sxs-lookup"><span data-stu-id="51505-170">Enter additional URLs as needed.</span></span>
7. <span data-ttu-id="51505-171">Click **Save** to save the settings.</span><span class="sxs-lookup"><span data-stu-id="51505-171">Click **Save** to save the settings.</span></span>

<span data-ttu-id="51505-172">It takes approximately 10-15 seconds for the new settings to take effect.</span><span class="sxs-lookup"><span data-stu-id="51505-172">It takes approximately 10-15 seconds for the new settings to take effect.</span></span>

## <a name="register-for-push"></a><span data-ttu-id="51505-173">How to: Register for push notifications</span><span class="sxs-lookup"><span data-stu-id="51505-173">How to: Register for push notifications</span></span>
<span data-ttu-id="51505-174">Install the [phonegap-plugin-push] to handle push notifications.</span><span class="sxs-lookup"><span data-stu-id="51505-174">Install the [phonegap-plugin-push] to handle push notifications.</span></span>  <span data-ttu-id="51505-175">This plugin can be easily added using the `cordova plugin add` command on the command line, or via the Git plugin installer within Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="51505-175">This plugin can be easily added using the `cordova plugin add` command on the command line, or via the Git plugin installer within Visual Studio.</span></span>  <span data-ttu-id="51505-176">The following code in your Apache Cordova app registers your device for push notifications:</span><span class="sxs-lookup"><span data-stu-id="51505-176">The following code in your Apache Cordova app registers your device for push notifications:</span></span>

```
var pushOptions = {
    android: {
        senderId: '<from-gcm-console>'
    },
    ios: {
        alert: true,
        badge: true,
        sound: true
    },
    windows: {
    }
};
pushHandler = PushNotification.init(pushOptions);

pushHandler.on('registration', function (data) {
    registrationId = data.registrationId;
    // For cross-platform, you can use the device plugin to determine the device
    // Best is to use device.platform
    var name = 'gcm'; // For android - default
    if (device.platform.toLowerCase() === 'ios')
        name = 'apns';
    if (device.platform.toLowerCase().substring(0, 3) === 'win')
        name = 'wns';
    client.push.register(name, registrationId);
});

pushHandler.on('notification', function (data) {
    // data is an object and is whatever is sent by the PNS - check the format
    // for your particular PNS
});

pushHandler.on('error', function (error) {
    // Handle errors
});
```

<span data-ttu-id="51505-177">Use the Notification Hubs SDK to send push notifications from the server.</span><span class="sxs-lookup"><span data-stu-id="51505-177">Use the Notification Hubs SDK to send push notifications from the server.</span></span>  <span data-ttu-id="51505-178">Never send push notifications directly from clients.</span><span class="sxs-lookup"><span data-stu-id="51505-178">Never send push notifications directly from clients.</span></span> <span data-ttu-id="51505-179">Doing so could be used to trigger a denial of service attack against Notification Hubs or the PNS.</span><span class="sxs-lookup"><span data-stu-id="51505-179">Doing so could be used to trigger a denial of service attack against Notification Hubs or the PNS.</span></span>  <span data-ttu-id="51505-180">The PNS could ban your traffic as a result of such attacks.</span><span class="sxs-lookup"><span data-stu-id="51505-180">The PNS could ban your traffic as a result of such attacks.</span></span>

## <a name="more-information"></a><span data-ttu-id="51505-181">More information</span><span class="sxs-lookup"><span data-stu-id="51505-181">More information</span></span>

<span data-ttu-id="51505-182">You can find detailed API details in our [API documentation](http://azure.github.io/azure-mobile-apps-js-client/).</span><span class="sxs-lookup"><span data-stu-id="51505-182">You can find detailed API details in our [API documentation](http://azure.github.io/azure-mobile-apps-js-client/).</span></span>

<!-- URLs. -->
[Azure portal]: https://portal.azure.com
[Azure Mobile Apps Quick Start]: app-service-mobile-cordova-get-started.md
[Get started with authentication]: app-service-mobile-cordova-get-started-users.md
[Add authentication to your app]: app-service-mobile-cordova-get-started-users.md

[Apache Cordova Plugin for Azure Mobile Apps]: https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-apps
[your first Apache Cordova app]: http://cordova.apache.org/#getstarted
[phonegap-facebook-plugin]: https://github.com/wizcorp/phonegap-facebook-plugin
[phonegap-plugin-push]: https://www.npmjs.com/package/phonegap-plugin-push
[cordova-plugin-device]: https://www.npmjs.com/package/cordova-plugin-device
[cordova-plugin-inappbrowser]: https://www.npmjs.com/package/cordova-plugin-inappbrowser
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
