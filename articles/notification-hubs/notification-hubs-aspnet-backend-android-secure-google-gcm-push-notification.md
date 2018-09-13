---
title: Sending Secure Push Notifications with Azure Notification Hubs
description: Learn how to send secure push notifications to an Android app from Azure. Code samples written in Java and C#.
documentationcenter: android
keywords: push notification,push notifications,push messages,android push notifications
author: ysxu
manager: erikre
editor: ''
services: notification-hubs
ms.assetid: daf3de1c-f6a9-43c4-8165-a76bfaa70893
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: android
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 29f8c516e611c13fb73c7edc15e7c52708c75bb0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555277"
---
# <a name="sending-secure-push-notifications-with-azure-notification-hubs"></a><span data-ttu-id="58ae3-105">Sending Secure Push Notifications with Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="58ae3-105">Sending Secure Push Notifications with Azure Notification Hubs</span></span>
> [!div class="op_single_selector"]
> * [Windows Universal](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [iOS](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [Android](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="58ae3-109">Overview</span><span class="sxs-lookup"><span data-stu-id="58ae3-109">Overview</span></span>
> [!IMPORTANT]
> To complete this tutorial, you must have an active Azure account. If you don't have an account, you can create a free trial account in just a couple of minutes. For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).
> 
> 

<span data-ttu-id="58ae3-113">Push notification support in Microsoft Azure enables you to access an easy-to-use, multiplatform, scaled-out push message infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span><span class="sxs-lookup"><span data-stu-id="58ae3-113">Push notification support in Microsoft Azure enables you to access an easy-to-use, multiplatform, scaled-out push message infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="58ae3-114">Due to regulatory or security constraints, sometimes an application might want to include something in the notification that cannot be transmitted through the standard push notification infrastructure.</span><span class="sxs-lookup"><span data-stu-id="58ae3-114">Due to regulatory or security constraints, sometimes an application might want to include something in the notification that cannot be transmitted through the standard push notification infrastructure.</span></span> <span data-ttu-id="58ae3-115">This tutorial describes how to achieve the same experience by sending sensitive information through a secure, authenticated connection between the client Android device and the app backend.</span><span class="sxs-lookup"><span data-stu-id="58ae3-115">This tutorial describes how to achieve the same experience by sending sensitive information through a secure, authenticated connection between the client Android device and the app backend.</span></span>

<span data-ttu-id="58ae3-116">At a high level, the flow is as follows:</span><span class="sxs-lookup"><span data-stu-id="58ae3-116">At a high level, the flow is as follows:</span></span>

1. <span data-ttu-id="58ae3-117">The app back-end:</span><span class="sxs-lookup"><span data-stu-id="58ae3-117">The app back-end:</span></span>
   * <span data-ttu-id="58ae3-118">Stores secure payload in back-end database.</span><span class="sxs-lookup"><span data-stu-id="58ae3-118">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="58ae3-119">Sends the ID of this notification to the Android device (no secure information is sent).</span><span class="sxs-lookup"><span data-stu-id="58ae3-119">Sends the ID of this notification to the Android device (no secure information is sent).</span></span>
2. <span data-ttu-id="58ae3-120">The app on the device, when receiving the notification:</span><span class="sxs-lookup"><span data-stu-id="58ae3-120">The app on the device, when receiving the notification:</span></span>
   * <span data-ttu-id="58ae3-121">The Android device contacts the back-end requesting the secure payload.</span><span class="sxs-lookup"><span data-stu-id="58ae3-121">The Android device contacts the back-end requesting the secure payload.</span></span>
   * <span data-ttu-id="58ae3-122">The app can show the payload as a notification on the device.</span><span class="sxs-lookup"><span data-stu-id="58ae3-122">The app can show the payload as a notification on the device.</span></span>

<span data-ttu-id="58ae3-123">It is important to note that in the preceding flow (and in this tutorial), we assume that the device stores an authentication token in local storage, after the user logs in.</span><span class="sxs-lookup"><span data-stu-id="58ae3-123">It is important to note that in the preceding flow (and in this tutorial), we assume that the device stores an authentication token in local storage, after the user logs in.</span></span> <span data-ttu-id="58ae3-124">This guarantees a completely seamless experience, as the device can retrieve the notification’s secure payload using this token.</span><span class="sxs-lookup"><span data-stu-id="58ae3-124">This guarantees a completely seamless experience, as the device can retrieve the notification’s secure payload using this token.</span></span> <span data-ttu-id="58ae3-125">If your application does not store authentication tokens on the device, or if these tokens can be expired, the device app, upon receiving the push notification should display a generic notification prompting the user to launch the app.</span><span class="sxs-lookup"><span data-stu-id="58ae3-125">If your application does not store authentication tokens on the device, or if these tokens can be expired, the device app, upon receiving the push notification should display a generic notification prompting the user to launch the app.</span></span> <span data-ttu-id="58ae3-126">The app then authenticates the user and shows the notification payload.</span><span class="sxs-lookup"><span data-stu-id="58ae3-126">The app then authenticates the user and shows the notification payload.</span></span>

<span data-ttu-id="58ae3-127">This tutorial shows how to send secure push notifications.</span><span class="sxs-lookup"><span data-stu-id="58ae3-127">This tutorial shows how to send secure push notifications.</span></span> <span data-ttu-id="58ae3-128">It builds on the [Notify Users](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) tutorial, so you should complete the steps in that tutorial first if you haven't already.</span><span class="sxs-lookup"><span data-stu-id="58ae3-128">It builds on the [Notify Users](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) tutorial, so you should complete the steps in that tutorial first if you haven't already.</span></span>

> [!NOTE]
> This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-the-android-project"></a><span data-ttu-id="58ae3-130">Modify the Android project</span><span class="sxs-lookup"><span data-stu-id="58ae3-130">Modify the Android project</span></span>
<span data-ttu-id="58ae3-131">Now that you modified your app back-end to send just the *id* of a push notification, you have to change your Android app to handle that notification and call back your back-end to retrieve the secure message to be displayed.</span><span class="sxs-lookup"><span data-stu-id="58ae3-131">Now that you modified your app back-end to send just the *id* of a push notification, you have to change your Android app to handle that notification and call back your back-end to retrieve the secure message to be displayed.</span></span>
<span data-ttu-id="58ae3-132">To achieve this goal, you have to make sure that your Android app knows how to authenticate itself with your back-end when it receives the push notifications.</span><span class="sxs-lookup"><span data-stu-id="58ae3-132">To achieve this goal, you have to make sure that your Android app knows how to authenticate itself with your back-end when it receives the push notifications.</span></span>

<span data-ttu-id="58ae3-133">We will now modify the *login* flow in order to save the authentication header value in the shared preferences of your app.</span><span class="sxs-lookup"><span data-stu-id="58ae3-133">We will now modify the *login* flow in order to save the authentication header value in the shared preferences of your app.</span></span> <span data-ttu-id="58ae3-134">Analogous mechanisms can be used to store any authentication token (e.g. OAuth tokens) that the app will have to use without requiring user credentials.</span><span class="sxs-lookup"><span data-stu-id="58ae3-134">Analogous mechanisms can be used to store any authentication token (e.g. OAuth tokens) that the app will have to use without requiring user credentials.</span></span>

1. <span data-ttu-id="58ae3-135">In your Android app project, add the following constants at the top of the **MainActivity** class:</span><span class="sxs-lookup"><span data-stu-id="58ae3-135">In your Android app project, add the following constants at the top of the **MainActivity** class:</span></span>
   
        public static final String NOTIFY_USERS_PROPERTIES = "NotifyUsersProperties";
        public static final String AUTHORIZATION_HEADER_PROPERTY = "AuthorizationHeader";
2. <span data-ttu-id="58ae3-136">Still in the **MainActivity** class, update the `getAuthorizationHeader()` method to contain the following code:</span><span class="sxs-lookup"><span data-stu-id="58ae3-136">Still in the **MainActivity** class, update the `getAuthorizationHeader()` method to contain the following code:</span></span>
   
        private String getAuthorizationHeader() throws UnsupportedEncodingException {
            EditText username = (EditText) findViewById(R.id.usernameText);
            EditText password = (EditText) findViewById(R.id.passwordText);
            String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
            basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
   
            SharedPreferences sp = getSharedPreferences(NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            sp.edit().putString(AUTHORIZATION_HEADER_PROPERTY, basicAuthHeader).commit();
   
            return basicAuthHeader;
        }
3. <span data-ttu-id="58ae3-137">Add the following `import` statements at the top of the **MainActivity** file:</span><span class="sxs-lookup"><span data-stu-id="58ae3-137">Add the following `import` statements at the top of the **MainActivity** file:</span></span>
   
        import android.content.SharedPreferences;

<span data-ttu-id="58ae3-138">Now we will change the handler that is called when the notification is received.</span><span class="sxs-lookup"><span data-stu-id="58ae3-138">Now we will change the handler that is called when the notification is received.</span></span>

1. <span data-ttu-id="58ae3-139">In the **MyHandler** class change the `OnReceive()` method to contain:</span><span class="sxs-lookup"><span data-stu-id="58ae3-139">In the **MyHandler** class change the `OnReceive()` method to contain:</span></span>
   
        public void onReceive(Context context, Bundle bundle) {
            ctx = context;
            String secureMessageId = bundle.getString("secureId");
            retrieveNotification(secureMessageId);
        }
2. <span data-ttu-id="58ae3-140">Then add the `retrieveNotification()` method, replacing the placeholder `{back-end endpoint}` with the back-end endpoint obtained while deploying your back-end:</span><span class="sxs-lookup"><span data-stu-id="58ae3-140">Then add the `retrieveNotification()` method, replacing the placeholder `{back-end endpoint}` with the back-end endpoint obtained while deploying your back-end:</span></span>
   
        private void retrieveNotification(final String secureMessageId) {
            SharedPreferences sp = ctx.getSharedPreferences(MainActivity.NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            final String authorizationHeader = sp.getString(MainActivity.AUTHORIZATION_HEADER_PROPERTY, null);
   
            new AsyncTask<Object, Object, Object>() {
                @Override
                protected Object doInBackground(Object... params) {
                    try {
                        HttpUriRequest request = new HttpGet("{back-end endpoint}/api/notifications/"+secureMessageId);
                        request.addHeader("Authorization", "Basic "+authorizationHeader);
                        HttpResponse response = new DefaultHttpClient().execute(request);
                        if (response.getStatusLine().getStatusCode() != HttpStatus.SC_OK) {
                            Log.e("MainActivity", "Error retrieving secure notification" + response.getStatusLine().getStatusCode());
                            throw new RuntimeException("Error retrieving secure notification");
                        }
                        String secureNotificationJSON = EntityUtils.toString(response.getEntity());
                        JSONObject secureNotification = new JSONObject(secureNotificationJSON);
                        sendNotification(secureNotification.getString("Payload"));
                    } catch (Exception e) {
                        Log.e("MainActivity", "Failed to retrieve secure notification - " + e.getMessage());
                        return e;
                    }
                    return null;
                }
            }.execute(null, null, null);
        }

<span data-ttu-id="58ae3-141">This method calls your app back-end to retrieve the notification content using the credentials stored in the shared preferences and displays it as a normal notification.</span><span class="sxs-lookup"><span data-stu-id="58ae3-141">This method calls your app back-end to retrieve the notification content using the credentials stored in the shared preferences and displays it as a normal notification.</span></span> <span data-ttu-id="58ae3-142">The notification looks to the app user exactly like any other push notification.</span><span class="sxs-lookup"><span data-stu-id="58ae3-142">The notification looks to the app user exactly like any other push notification.</span></span>

<span data-ttu-id="58ae3-143">Note that it is preferable to handle the cases of missing authentication header property or rejection by the back-end.</span><span class="sxs-lookup"><span data-stu-id="58ae3-143">Note that it is preferable to handle the cases of missing authentication header property or rejection by the back-end.</span></span> <span data-ttu-id="58ae3-144">The specific handling of these cases depend mostly on your target user experience.</span><span class="sxs-lookup"><span data-stu-id="58ae3-144">The specific handling of these cases depend mostly on your target user experience.</span></span> <span data-ttu-id="58ae3-145">One option is to display a notification with a generic prompt for the user to authenticate to retrieve the actual notification.</span><span class="sxs-lookup"><span data-stu-id="58ae3-145">One option is to display a notification with a generic prompt for the user to authenticate to retrieve the actual notification.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="58ae3-146">Run the Application</span><span class="sxs-lookup"><span data-stu-id="58ae3-146">Run the Application</span></span>
<span data-ttu-id="58ae3-147">To run the application, do the following:</span><span class="sxs-lookup"><span data-stu-id="58ae3-147">To run the application, do the following:</span></span>

1. <span data-ttu-id="58ae3-148">Make sure **AppBackend** is deployed in Azure.</span><span class="sxs-lookup"><span data-stu-id="58ae3-148">Make sure **AppBackend** is deployed in Azure.</span></span> <span data-ttu-id="58ae3-149">If using Visual Studio, run the **AppBackend** Web API application.</span><span class="sxs-lookup"><span data-stu-id="58ae3-149">If using Visual Studio, run the **AppBackend** Web API application.</span></span> <span data-ttu-id="58ae3-150">An ASP.NET web page is displayed.</span><span class="sxs-lookup"><span data-stu-id="58ae3-150">An ASP.NET web page is displayed.</span></span>
2. <span data-ttu-id="58ae3-151">In Eclipse, run the app on a physical Android device or the emulator.</span><span class="sxs-lookup"><span data-stu-id="58ae3-151">In Eclipse, run the app on a physical Android device or the emulator.</span></span>
3. <span data-ttu-id="58ae3-152">In the Android app UI, enter a username and password.</span><span class="sxs-lookup"><span data-stu-id="58ae3-152">In the Android app UI, enter a username and password.</span></span> <span data-ttu-id="58ae3-153">These can be any string, but they must be the same value.</span><span class="sxs-lookup"><span data-stu-id="58ae3-153">These can be any string, but they must be the same value.</span></span>
4. <span data-ttu-id="58ae3-154">In the Android app UI, click **Log in**.</span><span class="sxs-lookup"><span data-stu-id="58ae3-154">In the Android app UI, click **Log in**.</span></span> <span data-ttu-id="58ae3-155">Then click **Send push**.</span><span class="sxs-lookup"><span data-stu-id="58ae3-155">Then click **Send push**.</span></span>

