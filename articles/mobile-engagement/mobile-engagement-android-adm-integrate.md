---
title: Azure Mobile Engagement Android SDK Integration
description: Latest updates and procedures for Android SDK for Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: a7d719ec-67b3-4be3-9d7f-0b61a57fe978
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 43987962ea2b7b825b88643d18b4db65f1f1670e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671360"
---
# <a name="how-to-integrate-adm-with-engagement"></a><span data-ttu-id="c319a-103">How to Integrate ADM with Engagement</span><span class="sxs-lookup"><span data-stu-id="c319a-103">How to Integrate ADM with Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c319a-104">You must follow the integration procedure described in the How to Integrate Engagement on Android document before following this guide.</span><span class="sxs-lookup"><span data-stu-id="c319a-104">You must follow the integration procedure described in the How to Integrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="c319a-105">This document is useful only if you already integrated the Reach module and plan to push Amazon devices.</span><span class="sxs-lookup"><span data-stu-id="c319a-105">This document is useful only if you already integrated the Reach module and plan to push Amazon devices.</span></span> <span data-ttu-id="c319a-106">To integrate Reach campaigns in your application, please read first How to Integrate Engagement Reach on Android.</span><span class="sxs-lookup"><span data-stu-id="c319a-106">To integrate Reach campaigns in your application, please read first How to Integrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="c319a-107">Introduction</span><span class="sxs-lookup"><span data-stu-id="c319a-107">Introduction</span></span>
<span data-ttu-id="c319a-108">Integrating ADM allows your application to be pushed when targeting Amazon Android devices.</span><span class="sxs-lookup"><span data-stu-id="c319a-108">Integrating ADM allows your application to be pushed when targeting Amazon Android devices.</span></span>

<span data-ttu-id="c319a-109">ADM payloads pushed to the SDK always contain the `azme` key in the data object.</span><span class="sxs-lookup"><span data-stu-id="c319a-109">ADM payloads pushed to the SDK always contain the `azme` key in the data object.</span></span> <span data-ttu-id="c319a-110">Thus if you use ADM for another purpose in your application, you can filter pushes based on that key.</span><span class="sxs-lookup"><span data-stu-id="c319a-110">Thus if you use ADM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c319a-111">Only Amazon Kindle devices running Android 4.0.3 or above are supported by Amazon Device Messaging; however, you can integrate this code safely on other devices.</span><span class="sxs-lookup"><span data-stu-id="c319a-111">Only Amazon Kindle devices running Android 4.0.3 or above are supported by Amazon Device Messaging; however, you can integrate this code safely on other devices.</span></span>
> 
> 

## <a name="sign-up-to-adm"></a><span data-ttu-id="c319a-112">Sign up to ADM</span><span class="sxs-lookup"><span data-stu-id="c319a-112">Sign up to ADM</span></span>
<span data-ttu-id="c319a-113">If not already done, you must enable ADM on your Amazon account.</span><span class="sxs-lookup"><span data-stu-id="c319a-113">If not already done, you must enable ADM on your Amazon account.</span></span>

<span data-ttu-id="c319a-114">The procedure is detailed at: [<https://developer.amazon.com/sdk/adm/credentials.html>].</span><span class="sxs-lookup"><span data-stu-id="c319a-114">The procedure is detailed at: [<https://developer.amazon.com/sdk/adm/credentials.html>].</span></span>

<span data-ttu-id="c319a-115">Upon completing the procedure, you get:</span><span class="sxs-lookup"><span data-stu-id="c319a-115">Upon completing the procedure, you get:</span></span>

* <span data-ttu-id="c319a-116">OAuth credentials (a Client ID and a Client Secret) for Engagement to be able to push your devices.</span><span class="sxs-lookup"><span data-stu-id="c319a-116">OAuth credentials (a Client ID and a Client Secret) for Engagement to be able to push your devices.</span></span>
* <span data-ttu-id="c319a-117">An API Key that must be integrated into your application.</span><span class="sxs-lookup"><span data-stu-id="c319a-117">An API Key that must be integrated into your application.</span></span>

## <a name="sdk-integration"></a><span data-ttu-id="c319a-118">SDK integration</span><span class="sxs-lookup"><span data-stu-id="c319a-118">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="c319a-119">Managing device registrations</span><span class="sxs-lookup"><span data-stu-id="c319a-119">Managing device registrations</span></span>
<span data-ttu-id="c319a-120">Each device must send a registration command to the ADM servers, otherwise they can't be reached.</span><span class="sxs-lookup"><span data-stu-id="c319a-120">Each device must send a registration command to the ADM servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="c319a-121">If you already use the [ADM client library], and already have [integrated ADM] you can directly go to android-sdk-adm-receive.</span><span class="sxs-lookup"><span data-stu-id="c319a-121">If you already use the [ADM client library], and already have [integrated ADM] you can directly go to android-sdk-adm-receive.</span></span>

<span data-ttu-id="c319a-122">If you have not integrated ADM yet, Engagement has a simpler way to enable it in your application:</span><span class="sxs-lookup"><span data-stu-id="c319a-122">If you have not integrated ADM yet, Engagement has a simpler way to enable it in your application:</span></span>

<span data-ttu-id="c319a-123">Edit your `AndroidManifest.xml` file:</span><span class="sxs-lookup"><span data-stu-id="c319a-123">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="c319a-124">Add the Amazon namespace, the file should begin like this:</span><span class="sxs-lookup"><span data-stu-id="c319a-124">Add the Amazon namespace, the file should begin like this:</span></span>
  
      <?xml version="1.0" encoding="utf-8"?>
      <manifest xmlns:android="http://schemas.android.com/apk/res/android"
                xmlns:amazon="http://schemas.amazon.com/apk/res/android"
* <span data-ttu-id="c319a-125">Inside the `<application/>` tag, add this section:</span><span class="sxs-lookup"><span data-stu-id="c319a-125">Inside the `<application/>` tag, add this section:</span></span>
  
      <amazon:enable-feature
         android:name="com.amazon.device.messaging"
         android:required="false"/>
  
      <meta-data android:name="engagement:adm:register" android:value="true" />
* <span data-ttu-id="c319a-126">After adding the amazon tag, you may have a build error if your Project Build Target is below Android 2.1.</span><span class="sxs-lookup"><span data-stu-id="c319a-126">After adding the amazon tag, you may have a build error if your Project Build Target is below Android 2.1.</span></span> <span data-ttu-id="c319a-127">You have to use an **Android 2.1+** build target (don't worry, you can still have a `minSdkVersion` set to 4).</span><span class="sxs-lookup"><span data-stu-id="c319a-127">You have to use an **Android 2.1+** build target (don't worry, you can still have a `minSdkVersion` set to 4).</span></span>
* <span data-ttu-id="c319a-128">Integrate the ADM API Key as an asset by following [this procedure].</span><span class="sxs-lookup"><span data-stu-id="c319a-128">Integrate the ADM API Key as an asset by following [this procedure].</span></span>

<span data-ttu-id="c319a-129">Then follow the instructions of the next sections.</span><span class="sxs-lookup"><span data-stu-id="c319a-129">Then follow the instructions of the next sections.</span></span>

### <a name="communicate-registration-id-to-the-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="c319a-130">Communicate registration id to the Engagement Push service and receive notifications</span><span class="sxs-lookup"><span data-stu-id="c319a-130">Communicate registration id to the Engagement Push service and receive notifications</span></span>
<span data-ttu-id="c319a-131">In order to communicate the registration id of the device to the Engagement Push service and receive its notifications, add the following to your `AndroidManifest.xml` file, inside the `<application/>` tag (even if you use ADM without Engagement):</span><span class="sxs-lookup"><span data-stu-id="c319a-131">In order to communicate the registration id of the device to the Engagement Push service and receive its notifications, add the following to your `AndroidManifest.xml` file, inside the `<application/>` tag (even if you use ADM without Engagement):</span></span>

        <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMEnabler"
          android:exported="false">
          <intent-filter>
            <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT"/>
          </intent-filter>
        </receiver>

         <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMReceiver"
           android:permission="com.amazon.device.messaging.permission.SEND">
          <intent-filter>
            <action android:name="com.amazon.device.messaging.intent.REGISTRATION"/>
            <action android:name="com.amazon.device.messaging.intent.RECEIVE"/>
            <category android:name="<your_package_name>"/>
          </intent-filter>
        </receiver>   

<span data-ttu-id="c319a-132">Ensure you have the following permissions in your `AndroidManifest.xml` (before the `</application>` tag).</span><span class="sxs-lookup"><span data-stu-id="c319a-132">Ensure you have the following permissions in your `AndroidManifest.xml` (before the `</application>` tag).</span></span>

        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE"/>
        <uses-permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE"/>
        <permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE" android:protectionLevel="signature"/>

## <a name="grant-engagement-oauth-credentials"></a><span data-ttu-id="c319a-133">Grant Engagement OAuth credentials</span><span class="sxs-lookup"><span data-stu-id="c319a-133">Grant Engagement OAuth credentials</span></span>
<span data-ttu-id="c319a-134">Submit your OAuth Credentials (Client ID and Client Secret) in Engagement Portal.</span><span class="sxs-lookup"><span data-stu-id="c319a-134">Submit your OAuth Credentials (Client ID and Client Secret) in Engagement Portal.</span></span>

[<https://developer.amazon.com/sdk/adm/credentials.html>]:https://developer.amazon.com/sdk/adm/credentials.html
[ADM client library]:https://developer.amazon.com/sdk/adm/setup.html
[integrated ADM]:https://developer.amazon.com/sdk/adm/integrating-app.html
[this procedure]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset
