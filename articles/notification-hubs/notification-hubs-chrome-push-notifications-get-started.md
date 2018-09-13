---
title: Send push notifications to Chrome apps with Azure Notification Hubs | Microsoft Docs
description: Learn how to use Azure Notification Hubs to send push notifications to a Chrome App.
services: notification-hubs
keywords: mobile push notifications,push notifications,push notification,chrome push notifications
documentationcenter: ''
author: ysxu
manager: erikre
editor: ''
ms.assetid: 75d4ff59-d04a-455f-bd44-0130a68e641f
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-chrome
ms.devlang: JavaScript
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 9db60991f6935b3984a2f8f3ee10da12569c9b4e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549227"
---
# <a name="send-push-notifications-to-chrome-apps-with-azure-notification-hubs"></a><span data-ttu-id="e026c-104">Send push notifications to Chrome apps with Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="e026c-104">Send push notifications to Chrome apps with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

<span data-ttu-id="e026c-105">This topic shows you how to use Azure Notification Hubs to send push notifications to a Chrome App, which will be displayed within the context of the Google Chrome browser.</span><span class="sxs-lookup"><span data-stu-id="e026c-105">This topic shows you how to use Azure Notification Hubs to send push notifications to a Chrome App, which will be displayed within the context of the Google Chrome browser.</span></span> <span data-ttu-id="e026c-106">In this tutorial, we will create a Chrome app that receives push notifications by using [Google Cloud Messaging (GCM)](https://developers.google.com/cloud-messaging/).</span><span class="sxs-lookup"><span data-stu-id="e026c-106">In this tutorial, we will create a Chrome app that receives push notifications by using [Google Cloud Messaging (GCM)](https://developers.google.com/cloud-messaging/).</span></span> 

> [!NOTE]
> <span data-ttu-id="e026c-107">To complete this tutorial, you must have an active Azure account.</span><span class="sxs-lookup"><span data-stu-id="e026c-107">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="e026c-108">If you don't have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="e026c-108">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="e026c-109">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="e026c-109">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F).</span></span>
> 
> 

<span data-ttu-id="e026c-110">The tutorial walks you through these basic steps to enable push notifications:</span><span class="sxs-lookup"><span data-stu-id="e026c-110">The tutorial walks you through these basic steps to enable push notifications:</span></span>

* [<span data-ttu-id="e026c-111">Enable Google Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="e026c-111">Enable Google Cloud Messaging</span></span>](#register)
* [<span data-ttu-id="e026c-112">Configure your notification hub</span><span class="sxs-lookup"><span data-stu-id="e026c-112">Configure your notification hub</span></span>](#configure-hub)
* [<span data-ttu-id="e026c-113">Connect your Chrome App to the notification hub</span><span class="sxs-lookup"><span data-stu-id="e026c-113">Connect your Chrome App to the notification hub</span></span>](#connect-app)
* [<span data-ttu-id="e026c-114">Send a push notification to your Chrome App</span><span class="sxs-lookup"><span data-stu-id="e026c-114">Send a push notification to your Chrome App</span></span>](#send)
* [<span data-ttu-id="e026c-115">Additional functionality & capabilities</span><span class="sxs-lookup"><span data-stu-id="e026c-115">Additional functionality & capabilities</span></span>](#next-steps)

> [!NOTE]
> <span data-ttu-id="e026c-116">Chrome app push notifications are not generic in-browser notifications - they are specific to the browser extensibility model (see [Chrome Apps Overview] for details).</span><span class="sxs-lookup"><span data-stu-id="e026c-116">Chrome app push notifications are not generic in-browser notifications - they are specific to the browser extensibility model (see [Chrome Apps Overview] for details).</span></span> <span data-ttu-id="e026c-117">In addition to the desktop browser, Chrome apps run on mobile (Android and iOS) through Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="e026c-117">In addition to the desktop browser, Chrome apps run on mobile (Android and iOS) through Apache Cordova.</span></span> <span data-ttu-id="e026c-118">See [Chrome Apps on Mobile] to learn more.</span><span class="sxs-lookup"><span data-stu-id="e026c-118">See [Chrome Apps on Mobile] to learn more.</span></span>
> 
> 

<span data-ttu-id="e026c-119">Configuring GCM and Azure Notification Hubs is identical to configuring for Android, since [Google Cloud Messaging for Chrome] has been deprecated and the same GCM now supports both Android devices and Chrome instances.</span><span class="sxs-lookup"><span data-stu-id="e026c-119">Configuring GCM and Azure Notification Hubs is identical to configuring for Android, since [Google Cloud Messaging for Chrome] has been deprecated and the same GCM now supports both Android devices and Chrome instances.</span></span>

## <a id="register"></a><span data-ttu-id="e026c-120">Enable Google Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="e026c-120">Enable Google Cloud Messaging</span></span>
1. <span data-ttu-id="e026c-121">Navigate to the [Google Cloud Console] website, sign in with your Google account credentials, and then click the **Create Project** button.</span><span class="sxs-lookup"><span data-stu-id="e026c-121">Navigate to the [Google Cloud Console] website, sign in with your Google account credentials, and then click the **Create Project** button.</span></span> <span data-ttu-id="e026c-122">Provide an appropriate **Project Name**, and then click the **Create** button.</span><span class="sxs-lookup"><span data-stu-id="e026c-122">Provide an appropriate **Project Name**, and then click the **Create** button.</span></span>
   
       ![Google Cloud Console - Create Project][1]
2. <span data-ttu-id="e026c-123">Make a note of the **Project Number** on the **Projects** page for the project that you just created.</span><span class="sxs-lookup"><span data-stu-id="e026c-123">Make a note of the **Project Number** on the **Projects** page for the project that you just created.</span></span> <span data-ttu-id="e026c-124">You will use this as the **GCM Sender ID** in the Chrome App to register with GCM.</span><span class="sxs-lookup"><span data-stu-id="e026c-124">You will use this as the **GCM Sender ID** in the Chrome App to register with GCM.</span></span>
   
       ![Google Cloud Console - Project Number][2]
3. <span data-ttu-id="e026c-125">In the left pane, click **APIs & auth**, and then scroll down and click the toggle to enable **Google Cloud Messaging for Android**.</span><span class="sxs-lookup"><span data-stu-id="e026c-125">In the left pane, click **APIs & auth**, and then scroll down and click the toggle to enable **Google Cloud Messaging for Android**.</span></span> <span data-ttu-id="e026c-126">You don't have to enable **Google Cloud Messaging for Chrome**.</span><span class="sxs-lookup"><span data-stu-id="e026c-126">You don't have to enable **Google Cloud Messaging for Chrome**.</span></span>
   
       ![Google Cloud Console - Server Key][3]
4. <span data-ttu-id="e026c-127">In the left pane, click **Credentials** > **Create New Key** > **Server Key** > **Create**.</span><span class="sxs-lookup"><span data-stu-id="e026c-127">In the left pane, click **Credentials** > **Create New Key** > **Server Key** > **Create**.</span></span>
   
       ![Google Cloud Console - Credentials][4]
5. <span data-ttu-id="e026c-128">Make a note of the server **API Key**.</span><span class="sxs-lookup"><span data-stu-id="e026c-128">Make a note of the server **API Key**.</span></span> <span data-ttu-id="e026c-129">You will configure this in your notification hub next, to enable it to send push notifications to GCM.</span><span class="sxs-lookup"><span data-stu-id="e026c-129">You will configure this in your notification hub next, to enable it to send push notifications to GCM.</span></span>
   
       ![Google Cloud Console - API Key][5]

## <a id="configure-hub"></a><span data-ttu-id="e026c-130">Configure your notification hub</span><span class="sxs-lookup"><span data-stu-id="e026c-130">Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="e026c-131">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="e026c-131">&emsp;&emsp;6.</span></span>   <span data-ttu-id="e026c-132">In the **Settings** blade, select **Notification Services** and then **Google (GCM)**.</span><span class="sxs-lookup"><span data-stu-id="e026c-132">In the **Settings** blade, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="e026c-133">Enter the API key and save.</span><span class="sxs-lookup"><span data-stu-id="e026c-133">Enter the API key and save.</span></span>

&emsp;&emsp;![Azure Notification Hubs - Google (GCM)](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

## <a id="connect-app"></a><span data-ttu-id="e026c-135">Connect your Chrome App to the notification hub</span><span class="sxs-lookup"><span data-stu-id="e026c-135">Connect your Chrome App to the notification hub</span></span>
<span data-ttu-id="e026c-136">Your notification hub is now configured to work with GCM, and you have the connection strings to register your app to both receive and send push notifications.</span><span class="sxs-lookup"><span data-stu-id="e026c-136">Your notification hub is now configured to work with GCM, and you have the connection strings to register your app to both receive and send push notifications.</span></span> <span data-ttu-id="e026c-137">LK</span><span class="sxs-lookup"><span data-stu-id="e026c-137">LK</span></span>

### <a name="create-a-new-chrome-app"></a><span data-ttu-id="e026c-138">Create a new Chrome App</span><span class="sxs-lookup"><span data-stu-id="e026c-138">Create a new Chrome App</span></span>
<span data-ttu-id="e026c-139">The sample below is based on the [Chrome App GCM Sample] and uses the recommended way to create a Chrome App.</span><span class="sxs-lookup"><span data-stu-id="e026c-139">The sample below is based on the [Chrome App GCM Sample] and uses the recommended way to create a Chrome App.</span></span> <span data-ttu-id="e026c-140">We will highlight the steps specifically related to Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="e026c-140">We will highlight the steps specifically related to Azure Notification Hubs.</span></span> 

> [!NOTE]
> <span data-ttu-id="e026c-141">We recommend that you download the source for this Chrome App from [Chrome App Notification Hub Sample].</span><span class="sxs-lookup"><span data-stu-id="e026c-141">We recommend that you download the source for this Chrome App from [Chrome App Notification Hub Sample].</span></span>
> 
> 

<span data-ttu-id="e026c-142">The Chrome App is created via JavaScript, and you can use any of your preferred word editors for creating it.</span><span class="sxs-lookup"><span data-stu-id="e026c-142">The Chrome App is created via JavaScript, and you can use any of your preferred word editors for creating it.</span></span> <span data-ttu-id="e026c-143">Below is what this Chrome App will look like.</span><span class="sxs-lookup"><span data-stu-id="e026c-143">Below is what this Chrome App will look like.</span></span>

![Google Chrome App][15]

1. <span data-ttu-id="e026c-145">Create a folder and name it `ChromePushApp`.</span><span class="sxs-lookup"><span data-stu-id="e026c-145">Create a folder and name it `ChromePushApp`.</span></span> <span data-ttu-id="e026c-146">Of course, the name is arbitrary - if you name it something different, make sure you substitute the path in the required code segments.</span><span class="sxs-lookup"><span data-stu-id="e026c-146">Of course, the name is arbitrary - if you name it something different, make sure you substitute the path in the required code segments.</span></span>
2. <span data-ttu-id="e026c-147">Download the [crypto-js library] in the folder you created in the second step.</span><span class="sxs-lookup"><span data-stu-id="e026c-147">Download the [crypto-js library] in the folder you created in the second step.</span></span> <span data-ttu-id="e026c-148">This library folder will contain two subfolders: `components` and `rollups`.</span><span class="sxs-lookup"><span data-stu-id="e026c-148">This library folder will contain two subfolders: `components` and `rollups`.</span></span>
3. <span data-ttu-id="e026c-149">Create a `manifest.json` file.</span><span class="sxs-lookup"><span data-stu-id="e026c-149">Create a `manifest.json` file.</span></span> <span data-ttu-id="e026c-150">All Chrome Apps are backed by a manifest file that contains the app metadata and, most importantly, all permissions that are granted to the app when the user installs it.</span><span class="sxs-lookup"><span data-stu-id="e026c-150">All Chrome Apps are backed by a manifest file that contains the app metadata and, most importantly, all permissions that are granted to the app when the user installs it.</span></span>
   
        {
          "name": "NH-GCM Notifications",
          "description": "Chrome platform app.",
          "manifest_version": 2,
          "version": "0.1",
          "app": {
            "background": {
              "scripts": ["background.js"]
            }
          },
          "permissions": ["gcm", "storage", "notifications", "https://*.servicebus.windows.net/*"],
          "icons": { "128": "gcm_128.png" }
        }
   
    <span data-ttu-id="e026c-151">Notice the `permissions` element, which specifies that this Chrome App will be able to receive push notifications from GCM.</span><span class="sxs-lookup"><span data-stu-id="e026c-151">Notice the `permissions` element, which specifies that this Chrome App will be able to receive push notifications from GCM.</span></span> <span data-ttu-id="e026c-152">It must also specify the Azure Notification Hubs URI where the Chrome App will make a REST call to register.</span><span class="sxs-lookup"><span data-stu-id="e026c-152">It must also specify the Azure Notification Hubs URI where the Chrome App will make a REST call to register.</span></span>
    <span data-ttu-id="e026c-153">Our sample app also uses an icon file, `gcm_128.png`, that you will find at the source that's reused from the original GCM sample.</span><span class="sxs-lookup"><span data-stu-id="e026c-153">Our sample app also uses an icon file, `gcm_128.png`, that you will find at the source that's reused from the original GCM sample.</span></span> <span data-ttu-id="e026c-154">You can substitute it for any image that fits the [icon criteria](https://developer.chrome.com/apps/manifest/icons).</span><span class="sxs-lookup"><span data-stu-id="e026c-154">You can substitute it for any image that fits the [icon criteria](https://developer.chrome.com/apps/manifest/icons).</span></span>
4. <span data-ttu-id="e026c-155">Create a file called `background.js` with the following code:</span><span class="sxs-lookup"><span data-stu-id="e026c-155">Create a file called `background.js` with the following code:</span></span>
   
        // Returns a new notification ID used in the notification.
        function getNotificationId() {
          var id = Math.floor(Math.random() * 9007199254740992) + 1;
          return id.toString();
        }
   
        function messageReceived(message) {
          // A message is an object with a data property that
          // consists of key-value pairs.
   
          // Concatenate all key-value pairs to form a display string.
          var messageString = "";
          for (var key in message.data) {
            if (messageString != "")
              messageString += ", "
            messageString += key + ":" + message.data[key];
          }
          console.log("Message received: " + messageString);
   
          // Pop up a notification to show the GCM message.
          chrome.notifications.create(getNotificationId(), {
            title: 'GCM Message',
            iconUrl: 'gcm_128.png',
            type: 'basic',
            message: messageString
          }, function() {});
        }
   
        var registerWindowCreated = false;
   
        function firstTimeRegistration() {
          chrome.storage.local.get("registered", function(result) {
   
            registerWindowCreated = true;
            chrome.app.window.create(
              "register.html",
              {  width: 520,
                 height: 500,
                 frame: 'chrome'
              },
              function(appWin) {}
            );
          });
        }
   
        // Set up a listener for GCM message event.
        chrome.gcm.onMessage.addListener(messageReceived);
   
        // Set up listeners to trigger the first-time registration.
        chrome.runtime.onInstalled.addListener(firstTimeRegistration);
        chrome.runtime.onStartup.addListener(firstTimeRegistration);
   
    <span data-ttu-id="e026c-156">This is the file that pops up the Chrome App window HTML (**register.html**) and also defines the handler **messageReceived** to handle the incoming push notification.</span><span class="sxs-lookup"><span data-stu-id="e026c-156">This is the file that pops up the Chrome App window HTML (**register.html**) and also defines the handler **messageReceived** to handle the incoming push notification.</span></span>
5. <span data-ttu-id="e026c-157">Create a file called `register.html` - this defines the UI of the Chrome App.</span><span class="sxs-lookup"><span data-stu-id="e026c-157">Create a file called `register.html` - this defines the UI of the Chrome App.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="e026c-158">This sample uses **CryptoJS v3.1.2**.</span><span class="sxs-lookup"><span data-stu-id="e026c-158">This sample uses **CryptoJS v3.1.2**.</span></span> <span data-ttu-id="e026c-159">If you downloaded another version of the library, make sure you properly substitute the version in the `src` path.</span><span class="sxs-lookup"><span data-stu-id="e026c-159">If you downloaded another version of the library, make sure you properly substitute the version in the `src` path.</span></span>
   > 
   > 
   
        <html>
   
        <head>
        <title>GCM Registration</title>
        <script src="register.js"></script>
        <script src="CryptoJS v3.1.2/rollups/hmac-sha256.js"></script>
        <script src="CryptoJS v3.1.2/components/enc-base64-min.js"></script>
        </head>
   
        <body>
   
        Sender ID:<br/><input id="senderId" type="TEXT" size="20"><br/>
        <button id="registerWithGCM">Register with GCM</button>
        <br/>
        <br/>
        <br/>
   
        Notification Hub Name:<br/><input id="hubName" type="TEXT" style="width:400px"><br/><br/>
        Connection String:<br/><textarea id="connectionString" type="TEXT" style="width:400px;height:60px"></textarea>
   
        <br/>
   
        <button id="registerWithNH" disabled="true">Register with Azure Notification Hubs</button>
   
        <br/>
        <br/>
   
        <textarea id="console" type="TEXT" readonly style="width:500px;height:200px;background-color:#e5e5e5;padding:5px"></textarea>
   
        </body>
   
        </html>
6. <span data-ttu-id="e026c-160">Create a file called `register.js` with the code below.</span><span class="sxs-lookup"><span data-stu-id="e026c-160">Create a file called `register.js` with the code below.</span></span> <span data-ttu-id="e026c-161">This file specifies the script behind `register.html`.</span><span class="sxs-lookup"><span data-stu-id="e026c-161">This file specifies the script behind `register.html`.</span></span> <span data-ttu-id="e026c-162">Chrome Apps do not allow inline execution, so you have to create a separate backing script for your UI.</span><span class="sxs-lookup"><span data-stu-id="e026c-162">Chrome Apps do not allow inline execution, so you have to create a separate backing script for your UI.</span></span>
   
        var registrationId = "";
        var hubName        = "", connectionString = "";
        var originalUri    = "", targetUri = "", endpoint = "", sasKeyName = "", sasKeyValue = "", sasToken = "";
   
        window.onload = function() {
           document.getElementById("registerWithGCM").onclick = registerWithGCM;  
           document.getElementById("registerWithNH").onclick = registerWithNH;
           updateLog("You have not registered yet. Please provider sender ID and register with GCM and then with  Notification Hubs.");
        }
   
        function updateLog(status) {
          currentStatus = document.getElementById("console").innerHTML;
          if (currentStatus != "") {
            currentStatus = currentStatus + "\n\n";
          }
   
          document.getElementById("console").innerHTML = currentStatus  + status;
        }
   
        function registerWithGCM() {
          var senderId = document.getElementById("senderId").value.trim();
          chrome.gcm.register([senderId], registerCallback);
   
          // Prevent register button from being clicked again before the registration finishes.
          document.getElementById("registerWithGCM").disabled = true;
        }
   
        function registerCallback(regId) {
          registrationId = regId;
          document.getElementById("registerWithGCM").disabled = false;
   
          if (chrome.runtime.lastError) {
            // When the registration fails, handle the error and retry the
            // registration later.
            updateLog("Registration failed: " + chrome.runtime.lastError.message);
            return;
          }
   
          updateLog("Registration with GCM succeeded.");
          document.getElementById("registerWithNH").disabled = false;
   
          // Mark that the first-time registration is done.
          chrome.storage.local.set({registered: true});
        }
   
        function registerWithNH() {
          hubName = document.getElementById("hubName").value.trim();
          connectionString = document.getElementById("connectionString").value.trim();
          splitConnectionString();
          generateSaSToken();
          sendNHRegistrationRequest();
        }
   
        // From http://msdn.microsoft.com/library/dn495627.aspx
        function splitConnectionString()
        {
          var parts = connectionString.split(';');
          if (parts.length != 3)
          throw "Error parsing connection string";
   
          parts.forEach(function(part) {
            if (part.indexOf('Endpoint') == 0) {
            endpoint = 'https' + part.substring(11);
            } else if (part.indexOf('SharedAccessKeyName') == 0) {
            sasKeyName = part.substring(20);
            } else if (part.indexOf('SharedAccessKey') == 0) {
            sasKeyValue = part.substring(16);
            }
          });
   
          originalUri = endpoint + hubName;
        }
   
        function generateSaSToken()
        {
          targetUri = encodeURIComponent(originalUri.toLowerCase()).toLowerCase();
          var expiresInMins = 10; // 10 minute expiration
   
          // Set expiration in seconds.
          var expireOnDate = new Date();
          expireOnDate.setMinutes(expireOnDate.getMinutes() + expiresInMins);
          var expires = Date.UTC(expireOnDate.getUTCFullYear(), expireOnDate
            .getUTCMonth(), expireOnDate.getUTCDate(), expireOnDate
            .getUTCHours(), expireOnDate.getUTCMinutes(), expireOnDate
            .getUTCSeconds()) / 1000;
          var tosign = targetUri + '\n' + expires;
   
          // Using CryptoJS.
          var signature = CryptoJS.HmacSHA256(tosign, sasKeyValue);
          var base64signature = signature.toString(CryptoJS.enc.Base64);
          var base64UriEncoded = encodeURIComponent(base64signature);
   
          // Construct authorization string.
          sasToken = "SharedAccessSignature sr=" + targetUri + "&sig="
                          + base64UriEncoded + "&se=" + expires + "&skn=" + sasKeyName;
        }
   
        function sendNHRegistrationRequest()
        {
          var registrationPayload =
          "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
          "<entry xmlns=\"http://www.w3.org/2005/Atom\">" +
              "<content type=\"application/xml\">" +
                  "<GcmRegistrationDescription xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/netservices/2010/10/servicebus/connect\">" +
                      "<GcmRegistrationId>{GCMRegistrationId}</GcmRegistrationId>" +
                  "</GcmRegistrationDescription>" +
              "</content>" +
          "</entry>";
   
          // Update the payload with the registration ID obtained earlier.
          registrationPayload = registrationPayload.replace("{GCMRegistrationId}", registrationId);
   
          var url = originalUri + "/registrations/?api-version=2014-09";
          var client = new XMLHttpRequest();
   
          client.onload = function () {
            if (client.readyState == 4) {
              if (client.status == 200) {
                updateLog("Notification Hub Registration succesful!");
                updateLog(client.responseText);
              } else {
                updateLog("Notification Hub Registration did not succeed!");
                updateLog("HTTP Status: " + client.status + " : " + client.statusText);
                updateLog("HTTP Response: " + "\n" + client.responseText);
              }
            }
          };
   
          client.onerror = function () {
                updateLog("ERROR - Notification Hub Registration did not succeed!");
          }
   
          client.open("POST", url, true);
          client.setRequestHeader("Content-Type", "application/atom+xml;type=entry;charset=utf-8");
          client.setRequestHeader("Authorization", sasToken);
          client.setRequestHeader("x-ms-version", "2014-09");
   
          try {
              client.send(registrationPayload);
          }
          catch(err) {
              updateLog(err.message);
          }
        }
   
    <span data-ttu-id="e026c-163">The above script has the following key parameters:</span><span class="sxs-lookup"><span data-stu-id="e026c-163">The above script has the following key parameters:</span></span>
   
   * <span data-ttu-id="e026c-164">**window.onload** defines the button-click events of the two buttons on the UI.</span><span class="sxs-lookup"><span data-stu-id="e026c-164">**window.onload** defines the button-click events of the two buttons on the UI.</span></span> <span data-ttu-id="e026c-165">One registers with GCM, and the other uses the registration ID that's returned after registration with GCM to register with Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="e026c-165">One registers with GCM, and the other uses the registration ID that's returned after registration with GCM to register with Azure Notification Hubs.</span></span>
   * <span data-ttu-id="e026c-166">**updateLog** is the function that allows us to handle simple logging capabilities.</span><span class="sxs-lookup"><span data-stu-id="e026c-166">**updateLog** is the function that allows us to handle simple logging capabilities.</span></span>
   * <span data-ttu-id="e026c-167">**registerWithGCM** is the first button-click handler, which makes the `chrome.gcm.register` call to GCM to register the current Chrome App instance.</span><span class="sxs-lookup"><span data-stu-id="e026c-167">**registerWithGCM** is the first button-click handler, which makes the `chrome.gcm.register` call to GCM to register the current Chrome App instance.</span></span>
   * <span data-ttu-id="e026c-168">**registerCallback** is the callback function that gets called when the GCM registration call returns.</span><span class="sxs-lookup"><span data-stu-id="e026c-168">**registerCallback** is the callback function that gets called when the GCM registration call returns.</span></span>
   * <span data-ttu-id="e026c-169">**registerWithNH** is the second button-click handler, which registers with Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="e026c-169">**registerWithNH** is the second button-click handler, which registers with Notification Hubs.</span></span> <span data-ttu-id="e026c-170">It gets `hubName` and `connectionString` (which the user has specified) and crafts the Notification Hubs Registration REST API call.</span><span class="sxs-lookup"><span data-stu-id="e026c-170">It gets `hubName` and `connectionString` (which the user has specified) and crafts the Notification Hubs Registration REST API call.</span></span>
   * <span data-ttu-id="e026c-171">**splitConnectionString** and **generateSaSToken** are helpers that represent the JavaScript implementation of a SaS token creation process, that must be used in all REST API calls.</span><span class="sxs-lookup"><span data-stu-id="e026c-171">**splitConnectionString** and **generateSaSToken** are helpers that represent the JavaScript implementation of a SaS token creation process, that must be used in all REST API calls.</span></span> <span data-ttu-id="e026c-172">For more information, see [Common Concepts](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="e026c-172">For more information, see [Common Concepts](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
   * <span data-ttu-id="e026c-173">**sendNHRegistrationRequest** is the function that makes a HTTP REST call to Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="e026c-173">**sendNHRegistrationRequest** is the function that makes a HTTP REST call to Azure Notification Hubs.</span></span>
   * <span data-ttu-id="e026c-174">**registrationPayload** defines the registration XML payload.</span><span class="sxs-lookup"><span data-stu-id="e026c-174">**registrationPayload** defines the registration XML payload.</span></span> <span data-ttu-id="e026c-175">For more information, see [Create Registration NH REST API].</span><span class="sxs-lookup"><span data-stu-id="e026c-175">For more information, see [Create Registration NH REST API].</span></span> <span data-ttu-id="e026c-176">We update the registration ID in it with what we received from GCM.</span><span class="sxs-lookup"><span data-stu-id="e026c-176">We update the registration ID in it with what we received from GCM.</span></span>
   * <span data-ttu-id="e026c-177">**client** is an instance of **XMLHttpRequest** that we use to make the HTTP POST request.</span><span class="sxs-lookup"><span data-stu-id="e026c-177">**client** is an instance of **XMLHttpRequest** that we use to make the HTTP POST request.</span></span> <span data-ttu-id="e026c-178">Note that we update the `Authorization` header with `sasToken`.</span><span class="sxs-lookup"><span data-stu-id="e026c-178">Note that we update the `Authorization` header with `sasToken`.</span></span> <span data-ttu-id="e026c-179">Successful completion of this call will register this Chrome App instance with Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="e026c-179">Successful completion of this call will register this Chrome App instance with Azure Notification Hubs.</span></span>

<span data-ttu-id="e026c-180">The overall folder structure for this project should resemble this: ![Google Chrome App - Folder Structure][21]</span><span class="sxs-lookup"><span data-stu-id="e026c-180">The overall folder structure for this project should resemble this: ![Google Chrome App - Folder Structure][21]</span></span>

### <a name="set-up-and-test-your-chrome-app"></a><span data-ttu-id="e026c-181">Set up and test your Chrome App</span><span class="sxs-lookup"><span data-stu-id="e026c-181">Set up and test your Chrome App</span></span>
1. <span data-ttu-id="e026c-182">Open your Chrome browser.</span><span class="sxs-lookup"><span data-stu-id="e026c-182">Open your Chrome browser.</span></span> <span data-ttu-id="e026c-183">Open **Chrome extensions** and enable **Developer mode**.</span><span class="sxs-lookup"><span data-stu-id="e026c-183">Open **Chrome extensions** and enable **Developer mode**.</span></span>
   
       ![Google Chrome - Enable Developer Mode][16]
2. <span data-ttu-id="e026c-184">Click **Load unpacked extension** and navigate to the folder where you created the files.</span><span class="sxs-lookup"><span data-stu-id="e026c-184">Click **Load unpacked extension** and navigate to the folder where you created the files.</span></span> <span data-ttu-id="e026c-185">You can also optionally use the **Chrome Apps & Extensions Developer Tool**.</span><span class="sxs-lookup"><span data-stu-id="e026c-185">You can also optionally use the **Chrome Apps & Extensions Developer Tool**.</span></span> <span data-ttu-id="e026c-186">This tool is a Chrome App in itself (installed from the Chrome Web Store) and provides advanced debugging capabilities for your Chrome App development.</span><span class="sxs-lookup"><span data-stu-id="e026c-186">This tool is a Chrome App in itself (installed from the Chrome Web Store) and provides advanced debugging capabilities for your Chrome App development.</span></span>
   
       ![Google Chrome - Load Unpacked Extension][17]
3. <span data-ttu-id="e026c-187">If the Chrome App is created without any errors, then you will see your Chrome App show up.</span><span class="sxs-lookup"><span data-stu-id="e026c-187">If the Chrome App is created without any errors, then you will see your Chrome App show up.</span></span>
   
       ![Google Chrome - Chrome App Display][18]
4. <span data-ttu-id="e026c-188">Enter the **Project Number** that you got earlier from the **Google Cloud Console** as the sender ID, and click **Register with GCM**.</span><span class="sxs-lookup"><span data-stu-id="e026c-188">Enter the **Project Number** that you got earlier from the **Google Cloud Console** as the sender ID, and click **Register with GCM**.</span></span> <span data-ttu-id="e026c-189">You must see the message **Registration with GCM succeeded.**</span><span class="sxs-lookup"><span data-stu-id="e026c-189">You must see the message **Registration with GCM succeeded.**</span></span>
   
       ![Google Chrome - Chrome App Customization][19]
5. <span data-ttu-id="e026c-190">Enter your **Notification Hub Name** and the **DefaultListenSharedAccessSignature** that you obtained from the portal earlier, and click **Register with Azure Notification Hub**.</span><span class="sxs-lookup"><span data-stu-id="e026c-190">Enter your **Notification Hub Name** and the **DefaultListenSharedAccessSignature** that you obtained from the portal earlier, and click **Register with Azure Notification Hub**.</span></span> <span data-ttu-id="e026c-191">You must see the message **Notification Hub Registration successful!**</span><span class="sxs-lookup"><span data-stu-id="e026c-191">You must see the message **Notification Hub Registration successful!**</span></span> <span data-ttu-id="e026c-192">and the details of the registration response, which contains the Azure Notification Hubs registration ID.</span><span class="sxs-lookup"><span data-stu-id="e026c-192">and the details of the registration response, which contains the Azure Notification Hubs registration ID.</span></span>
   
       ![Google Chrome - Specify Notification Hub Details][20]  

## <a name="send"></a><span data-ttu-id="e026c-193">Send a notification to your Chrome App</span><span class="sxs-lookup"><span data-stu-id="e026c-193">Send a notification to your Chrome App</span></span>
<span data-ttu-id="e026c-194">For testing purposes, we will send Chrome push notifications by using a .NET console application.</span><span class="sxs-lookup"><span data-stu-id="e026c-194">For testing purposes, we will send Chrome push notifications by using a .NET console application.</span></span> 

> [!NOTE]
> <span data-ttu-id="e026c-195">You can send push notifications with Notification Hubs from any backend via our public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST interface</a>.</span><span class="sxs-lookup"><span data-stu-id="e026c-195">You can send push notifications with Notification Hubs from any backend via our public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST interface</a>.</span></span> <span data-ttu-id="e026c-196">Check out our [documentation portal](https://azure.microsoft.com/documentation/services/notification-hubs/) for more cross-platform examples.</span><span class="sxs-lookup"><span data-stu-id="e026c-196">Check out our [documentation portal](https://azure.microsoft.com/documentation/services/notification-hubs/) for more cross-platform examples.</span></span>
> 
> 

1. <span data-ttu-id="e026c-197">In Visual Studio, from the **File** menu, select **New** and then **Project**.</span><span class="sxs-lookup"><span data-stu-id="e026c-197">In Visual Studio, from the **File** menu, select **New** and then **Project**.</span></span> <span data-ttu-id="e026c-198">Under **Visual C#**, click **Windows** and **Console Application**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="e026c-198">Under **Visual C#**, click **Windows** and **Console Application**, and then click **OK**.</span></span>  <span data-ttu-id="e026c-199">This creates a new console application project.</span><span class="sxs-lookup"><span data-stu-id="e026c-199">This creates a new console application project.</span></span>
2. <span data-ttu-id="e026c-200">From the **Tools** menu, click **Library Package Manager** and then **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="e026c-200">From the **Tools** menu, click **Library Package Manager** and then **Package Manager Console**.</span></span> <span data-ttu-id="e026c-201">This displays the Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="e026c-201">This displays the Package Manager Console.</span></span>
3. <span data-ttu-id="e026c-202">In the console window, execute the following command:</span><span class="sxs-lookup"><span data-stu-id="e026c-202">In the console window, execute the following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
       This adds a reference to the Azure Service Bus SDK with the <a href="http://nuget.org/packages/  WindowsAzure.ServiceBus/">WindowsAzure.ServiceBus NuGet package</a>.
4. <span data-ttu-id="e026c-203">Open `Program.cs` and add the following `using` statement:</span><span class="sxs-lookup"><span data-stu-id="e026c-203">Open `Program.cs` and add the following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="e026c-204">In the `Program` class, add the following method:</span><span class="sxs-lookup"><span data-stu-id="e026c-204">In the `Program` class, add the following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            String message = "{\"data\":{\"message\":\"Hello Chrome from Azure Notification Hubs\"}}";
            await hub.SendGcmNativeNotificationAsync(message);
        }
   
       Make sure to replace the `<hub name>` placeholder with the name of the notification hub that appears in the [portal](https://portal.azure.com) in your Notification Hub blade. Also, replace the connection string placeholder with the connection string called `DefaultFullSharedAccessSignature` that you obtained in the notification hub configuration section.
   
   > [!NOTE]
   > <span data-ttu-id="e026c-205">Make sure that you use the connection string with **Full** access, not **Listen** access.</span><span class="sxs-lookup"><span data-stu-id="e026c-205">Make sure that you use the connection string with **Full** access, not **Listen** access.</span></span> <span data-ttu-id="e026c-206">The **Listen** access connection string does not grant permissions to send push notifications.</span><span class="sxs-lookup"><span data-stu-id="e026c-206">The **Listen** access connection string does not grant permissions to send push notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="e026c-207">Add the following calls in the `Main` method:</span><span class="sxs-lookup"><span data-stu-id="e026c-207">Add the following calls in the `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="e026c-208">Make sure that Chrome is running, and run the console application.</span><span class="sxs-lookup"><span data-stu-id="e026c-208">Make sure that Chrome is running, and run the console application.</span></span>
8. <span data-ttu-id="e026c-209">You should see the following notification pop up on your desktop.</span><span class="sxs-lookup"><span data-stu-id="e026c-209">You should see the following notification pop up on your desktop.</span></span>
   
       ![Google Chrome - Notification][13]
9. <span data-ttu-id="e026c-210">You can also see all your notifications by using the Chrome Notifications window in the taskbar (in Windows) when Chrome is running.</span><span class="sxs-lookup"><span data-stu-id="e026c-210">You can also see all your notifications by using the Chrome Notifications window in the taskbar (in Windows) when Chrome is running.</span></span>
   
       ![Google Chrome - Notifications List][14]

> [!NOTE]
> <span data-ttu-id="e026c-211">You don't need to have the Chrome App running or open in the browser (though the Chrome browser itself must be running).</span><span class="sxs-lookup"><span data-stu-id="e026c-211">You don't need to have the Chrome App running or open in the browser (though the Chrome browser itself must be running).</span></span> <span data-ttu-id="e026c-212">You also get a consolidated view of all your notifications in the Chrome Notifications window.</span><span class="sxs-lookup"><span data-stu-id="e026c-212">You also get a consolidated view of all your notifications in the Chrome Notifications window.</span></span>
> 
> 

## <span data-ttu-id="e026c-213"><a name="next-steps"> </a>Next steps</span><span class="sxs-lookup"><span data-stu-id="e026c-213"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="e026c-214">Learn more about Notification Hubs in [Notification Hubs Overview].</span><span class="sxs-lookup"><span data-stu-id="e026c-214">Learn more about Notification Hubs in [Notification Hubs Overview].</span></span>

<span data-ttu-id="e026c-215">To target specific users, refer to the [Azure Notification Hubs Notify Users] tutorial.</span><span class="sxs-lookup"><span data-stu-id="e026c-215">To target specific users, refer to the [Azure Notification Hubs Notify Users] tutorial.</span></span> 

<span data-ttu-id="e026c-216">If you want to segment your users by interest groups, you can follow the [Azure Notification Hubs breaking news] tutorial.</span><span class="sxs-lookup"><span data-stu-id="e026c-216">If you want to segment your users by interest groups, you can follow the [Azure Notification Hubs breaking news] tutorial.</span></span>

<!-- Images. -->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-chrome-get-started/GoogleConsoleCreateProject.PNG
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-chrome-get-started/GoogleProjectNumber.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-chrome-get-started/EnableGCM.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-chrome-get-started/CreateServerKey.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-chrome-get-started/ServerKey.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-chrome-get-started/CreateNH.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-chrome-get-started/NHNamespace.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-chrome-get-started/NamespaceConfigure.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-chrome-get-started/NHConfigure.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-chrome-get-started/NHConfigureGCM.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-chrome-get-started/NHDashboard.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-chrome-get-started/NHConnString.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-chrome-get-started/ChromeNotification.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-chrome-get-started/ChromeNotificationWindow.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-chrome-get-started/ChromeApp.png
[16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-chrome-get-started/ChromeExtensions.png
[17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-chrome-get-started/ChromeLoadExtension.png
[18]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-chrome-get-started/ChromeAppLoaded.png
[19]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-chrome-get-started/ChromeAppGCM.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-chrome-get-started/ChromeAppNH.png
[21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-chrome-get-started/FinalFolderView.png

<!-- URLs. -->
[Chrome App Notification Hub Sample]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToChromeApps
[Google Cloud Console]: http://cloud.google.com/console
[Azure Classic Portal]: https://manage.windowsazure.com/
[Notification Hubs Overview]: notification-hubs-push-notification-overview.md
[Chrome Apps Overview]: https://developer.chrome.com/apps/about_apps
[Chrome App GCM Sample]: https://github.com/GoogleChrome/chrome-app-samples/tree/master/samples/gcm-notifications
[Installable Web Apps]: https://developers.google.com/chrome/apps/docs/
[Chrome Apps on Mobile]: https://developer.chrome.com/apps/chrome_apps_on_mobile
[Create Registration NH REST API]: http://msdn.microsoft.com/library/azure/dn223265.aspx
[crypto-js library]: http://code.google.com/p/crypto-js/
[GCM with Chrome Apps]: https://developer.chrome.com/apps/cloudMessaging
[Google Cloud Messaging for Chrome]: https://developer.chrome.com/apps/cloudMessagingV1
[Azure Notification Hubs Notify Users]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[Azure Notification Hubs breaking news]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md






















