---
title: Azure Mobile Engagement Android SDK Integration
description: Latest updates and procedures for Android SDK for Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: d72b5014-a22b-4a7f-a470-d2b8145b5b86
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 10/10/2016
ms.author: piyushjo
ms.openlocfilehash: 0282abbf44406cac89c13520bc2a4e375817ed1f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564269"
---
# <a name="how-to-integrate-gcm-with-mobile-engagement"></a><span data-ttu-id="89161-103">How to Integrate GCM with Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="89161-103">How to Integrate GCM with Mobile Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="89161-104">You must follow the integration procedure described in the How to Integrate Engagement on Android document before following this guide.</span><span class="sxs-lookup"><span data-stu-id="89161-104">You must follow the integration procedure described in the How to Integrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="89161-105">This document is useful only if you already integrated the Reach module and plan to push Google Play devices.</span><span class="sxs-lookup"><span data-stu-id="89161-105">This document is useful only if you already integrated the Reach module and plan to push Google Play devices.</span></span> <span data-ttu-id="89161-106">To integrate Reach campaigns in your application, please read first How to Integrate Engagement Reach on Android.</span><span class="sxs-lookup"><span data-stu-id="89161-106">To integrate Reach campaigns in your application, please read first How to Integrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="89161-107">Introduction</span><span class="sxs-lookup"><span data-stu-id="89161-107">Introduction</span></span>
<span data-ttu-id="89161-108">Integrating GCM allows your application to be pushed.</span><span class="sxs-lookup"><span data-stu-id="89161-108">Integrating GCM allows your application to be pushed.</span></span>

<span data-ttu-id="89161-109">GCM payloads pushed to the SDK always contain the `azme` key in the data object.</span><span class="sxs-lookup"><span data-stu-id="89161-109">GCM payloads pushed to the SDK always contain the `azme` key in the data object.</span></span> <span data-ttu-id="89161-110">Thus if you use GCM for another purpose in your application, you can filter pushes based on that key.</span><span class="sxs-lookup"><span data-stu-id="89161-110">Thus if you use GCM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="89161-111">Only devices running Android 2.2 or above, having Google Play installed and having Google background connection enabled can be pushed using GCM; however, you can integrate this code safely on unsupported devices (it just uses intents).</span><span class="sxs-lookup"><span data-stu-id="89161-111">Only devices running Android 2.2 or above, having Google Play installed and having Google background connection enabled can be pushed using GCM; however, you can integrate this code safely on unsupported devices (it just uses intents).</span></span>
> 
> 

## <a name="create-a-google-cloud-messaging-project-with-api-key"></a><span data-ttu-id="89161-112">Create a Google Cloud Messaging project with API key</span><span class="sxs-lookup"><span data-stu-id="89161-112">Create a Google Cloud Messaging project with API key</span></span>
[!INCLUDE [mobile-engagement-enable-Google-cloud-messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

## <a name="sdk-integration"></a><span data-ttu-id="89161-113">SDK integration</span><span class="sxs-lookup"><span data-stu-id="89161-113">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="89161-114">Managing device registrations</span><span class="sxs-lookup"><span data-stu-id="89161-114">Managing device registrations</span></span>
<span data-ttu-id="89161-115">Each device must send a registration command to the Google servers, otherwise they can't be reached.</span><span class="sxs-lookup"><span data-stu-id="89161-115">Each device must send a registration command to the Google servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="89161-116">A device can also unregister from GCM notifications (the device is automatically unregistered if the application is uninstalled).</span><span class="sxs-lookup"><span data-stu-id="89161-116">A device can also unregister from GCM notifications (the device is automatically unregistered if the application is uninstalled).</span></span>

<span data-ttu-id="89161-117">If you don't use [Google Play SDK] or you don't already send the registration intent yourself, you can make Engagement register the device automatically for you.</span><span class="sxs-lookup"><span data-stu-id="89161-117">If you don't use [Google Play SDK] or you don't already send the registration intent yourself, you can make Engagement register the device automatically for you.</span></span>

<span data-ttu-id="89161-118">To enable this, add the following to your `AndroidManifest.xml` file, inside the `<application/>` tag:</span><span class="sxs-lookup"><span data-stu-id="89161-118">To enable this, add the following to your `AndroidManifest.xml` file, inside the `<application/>` tag:</span></span>

            <!-- If only 1 sender, don't forget the \n, otherwise it will be parsed as a negative number... -->
            <meta-data android:name="engagement:gcm:sender" android:value="<Your Google Project Number>\n" />

### <a name="communicate-registration-id-to-the-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="89161-119">Communicate registration id to the Engagement Push service and receive notifications</span><span class="sxs-lookup"><span data-stu-id="89161-119">Communicate registration id to the Engagement Push service and receive notifications</span></span>
<span data-ttu-id="89161-120">In order to communicate the registration id of the device to the Engagement Push service and receive its notifications, add the following to your `AndroidManifest.xml` file, inside the `<application/>` tag (even if you manage device registrations yourself):</span><span class="sxs-lookup"><span data-stu-id="89161-120">In order to communicate the registration id of the device to the Engagement Push service and receive its notifications, add the following to your `AndroidManifest.xml` file, inside the `<application/>` tag (even if you manage device registrations yourself):</span></span>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver" android:permission="com.google.android.c2dm.permission.SEND">
              <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION" />
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your_package_name>" />
              </intent-filter>
            </receiver>

<span data-ttu-id="89161-121">Ensure you have the following permissions in your `AndroidManifest.xml` (after the `</application>` tag).</span><span class="sxs-lookup"><span data-stu-id="89161-121">Ensure you have the following permissions in your `AndroidManifest.xml` (after the `</application>` tag).</span></span>

            <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
            <uses-permission android:name="<your_package_name>.permission.C2D_MESSAGE" />
            <permission android:name="<your_package_name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

## <a name="grant-mobile-engagement-access-to-your-gcm-api-key"></a><span data-ttu-id="89161-122">Grant Mobile Engagement access to your GCM API Key</span><span class="sxs-lookup"><span data-stu-id="89161-122">Grant Mobile Engagement access to your GCM API Key</span></span>
<span data-ttu-id="89161-123">Follow [this guide](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) to grant Mobile Engagement access to your GCM API Key.</span><span class="sxs-lookup"><span data-stu-id="89161-123">Follow [this guide](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) to grant Mobile Engagement access to your GCM API Key.</span></span>

[Google Play SDK]:https://developers.google.com/cloud-messaging/android/start
