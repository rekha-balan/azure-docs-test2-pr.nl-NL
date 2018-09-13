---
title: Get Started with Azure Mobile Engagement for Unity Android deployment
description: Learn how to use Azure Mobile Engagement with Analytics and Push Notifications for Unity apps deploying to iOS devices.
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: ''
ms.assetid: d5f0ef79-be00-4cec-97a5-a0b2fdaa380e
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 2f19ee05e96d87deed492dbe525f1b84361ee2d6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555256"
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-android-deployment"></a><span data-ttu-id="86398-103">Get Started with Azure Mobile Engagement for Unity Android deployment</span><span class="sxs-lookup"><span data-stu-id="86398-103">Get Started with Azure Mobile Engagement for Unity Android deployment</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="86398-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of a Unity application when deploying to an Android device.</span><span class="sxs-lookup"><span data-stu-id="86398-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of a Unity application when deploying to an Android device.</span></span>
<span data-ttu-id="86398-105">This tutorial uses the classic Unity Roll a Ball tutorial as the starting point.</span><span class="sxs-lookup"><span data-stu-id="86398-105">This tutorial uses the classic Unity Roll a Ball tutorial as the starting point.</span></span> <span data-ttu-id="86398-106">You should follow the steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with the Mobile Engagement integration we showcase in the tutorial below.</span><span class="sxs-lookup"><span data-stu-id="86398-106">You should follow the steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with the Mobile Engagement integration we showcase in the tutorial below.</span></span> 

<span data-ttu-id="86398-107">This tutorial requires the following:</span><span class="sxs-lookup"><span data-stu-id="86398-107">This tutorial requires the following:</span></span>

* [<span data-ttu-id="86398-108">Unity Editor</span><span class="sxs-lookup"><span data-stu-id="86398-108">Unity Editor</span></span>](http://unity3d.com/get-unity)
* [<span data-ttu-id="86398-109">Mobile Engagement Unity SDK</span><span class="sxs-lookup"><span data-stu-id="86398-109">Mobile Engagement Unity SDK</span></span>](https://aka.ms/azmeunitysdk)
* <span data-ttu-id="86398-110">Google Android SDK</span><span class="sxs-lookup"><span data-stu-id="86398-110">Google Android SDK</span></span>

> [!NOTE]
> <span data-ttu-id="86398-111">To complete this tutorial, you must have an active Azure account.</span><span class="sxs-lookup"><span data-stu-id="86398-111">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="86398-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="86398-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="86398-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="86398-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).</span></span>
> 
> 

## <a id="setup-azme"></a><span data-ttu-id="86398-114">Setup Mobile Engagement for your Android app</span><span class="sxs-lookup"><span data-stu-id="86398-114">Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a><span data-ttu-id="86398-115">Connect your app to the Mobile Engagement backend</span><span class="sxs-lookup"><span data-stu-id="86398-115">Connect your app to the Mobile Engagement backend</span></span>
### <a name="import-the-unity-package"></a><span data-ttu-id="86398-116">Import the Unity package</span><span class="sxs-lookup"><span data-stu-id="86398-116">Import the Unity package</span></span>
1. <span data-ttu-id="86398-117">Download the [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it to your local machine.</span><span class="sxs-lookup"><span data-stu-id="86398-117">Download the [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it to your local machine.</span></span> 
2. <span data-ttu-id="86398-118">Go to **Assets -> Import Package -> Custom Package** and select the package you downloaded in the above step.</span><span class="sxs-lookup"><span data-stu-id="86398-118">Go to **Assets -> Import Package -> Custom Package** and select the package you downloaded in the above step.</span></span> 
   
    ![][70] 
3. <span data-ttu-id="86398-119">Make sure all files are selected and click **Import** button.</span><span class="sxs-lookup"><span data-stu-id="86398-119">Make sure all files are selected and click **Import** button.</span></span> 
   
    ![][71] 
4. <span data-ttu-id="86398-120">Once Import is successful, you will see the imported SDK files in your project.</span><span class="sxs-lookup"><span data-stu-id="86398-120">Once Import is successful, you will see the imported SDK files in your project.</span></span>  
   
    ![][72] 

### <a name="update-the-engagementconfiguration"></a><span data-ttu-id="86398-121">Update the EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="86398-121">Update the EngagementConfiguration</span></span>
1. <span data-ttu-id="86398-122">Open up the **EngagementConfiguration** script file from the SDK folder and update the **ANDROID\_CONNECTION\_STRING** with the connection string you obtained earlier from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="86398-122">Open up the **EngagementConfiguration** script file from the SDK folder and update the **ANDROID\_CONNECTION\_STRING** with the connection string you obtained earlier from the Azure portal.</span></span>  
   
    ![][73]
2. <span data-ttu-id="86398-123">Save the file</span><span class="sxs-lookup"><span data-stu-id="86398-123">Save the file</span></span> 
3. <span data-ttu-id="86398-124">Execute **File -> Engagement -> Generate Android Manifest**.</span><span class="sxs-lookup"><span data-stu-id="86398-124">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="86398-125">This is the plugin added by the Mobile Engagement SDK and clicking on it will automatically update your project settings.</span><span class="sxs-lookup"><span data-stu-id="86398-125">This is the plugin added by the Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

> [!IMPORTANT]
> <span data-ttu-id="86398-126">Make sure to execute this every time you update the **EngagementConfiguration** file otherwise your changes will not be reflected in the app.</span><span class="sxs-lookup"><span data-stu-id="86398-126">Make sure to execute this every time you update the **EngagementConfiguration** file otherwise your changes will not be reflected in the app.</span></span> 
> 
> 

### <a name="configure-the-app-for-basic-tracking"></a><span data-ttu-id="86398-127">Configure the app for basic tracking</span><span class="sxs-lookup"><span data-stu-id="86398-127">Configure the app for basic tracking</span></span>
1. <span data-ttu-id="86398-128">Open up the **PlayerController** script attached to the Player object for editing.</span><span class="sxs-lookup"><span data-stu-id="86398-128">Open up the **PlayerController** script attached to the Player object for editing.</span></span> 
2. <span data-ttu-id="86398-129">Add the following using statement:</span><span class="sxs-lookup"><span data-stu-id="86398-129">Add the following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Unity;
3. <span data-ttu-id="86398-130">Add the following to the `Start()` method</span><span class="sxs-lookup"><span data-stu-id="86398-130">Add the following to the `Start()` method</span></span>
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-the-app"></a><span data-ttu-id="86398-131">Deploy and run the app</span><span class="sxs-lookup"><span data-stu-id="86398-131">Deploy and run the app</span></span>
<span data-ttu-id="86398-132">Make sure that you have Android SDK installed on your machine before attempting to deploy this Unity app to your device.</span><span class="sxs-lookup"><span data-stu-id="86398-132">Make sure that you have Android SDK installed on your machine before attempting to deploy this Unity app to your device.</span></span> 

1. <span data-ttu-id="86398-133">Connect an Android device to your machine.</span><span class="sxs-lookup"><span data-stu-id="86398-133">Connect an Android device to your machine.</span></span> 
2. <span data-ttu-id="86398-134">Open up **File -> Build Settings**</span><span class="sxs-lookup"><span data-stu-id="86398-134">Open up **File -> Build Settings**</span></span> 
   
    ![][40]
3. <span data-ttu-id="86398-135">Select **Android** and then click on **Switch Platform**</span><span class="sxs-lookup"><span data-stu-id="86398-135">Select **Android** and then click on **Switch Platform**</span></span>
   
    ![][51]
   
    ![][52]
4. <span data-ttu-id="86398-136">Click on **Player settings** and provide a valid Bundle Identifier.</span><span class="sxs-lookup"><span data-stu-id="86398-136">Click on **Player settings** and provide a valid Bundle Identifier.</span></span> 
   
    ![][53]
5. <span data-ttu-id="86398-137">Finally click on **Build And Run**</span><span class="sxs-lookup"><span data-stu-id="86398-137">Finally click on **Build And Run**</span></span>
   
    ![][54]
6. <span data-ttu-id="86398-138">You may be asked to provide a folder name to store the Android package.</span><span class="sxs-lookup"><span data-stu-id="86398-138">You may be asked to provide a folder name to store the Android package.</span></span> 
7. <span data-ttu-id="86398-139">If everything goes fine, then the package will be deployed to your connected device and you should see your Unity game on your phone!</span><span class="sxs-lookup"><span data-stu-id="86398-139">If everything goes fine, then the package will be deployed to your connected device and you should see your Unity game on your phone!</span></span> 

## <a id="monitor"></a><span data-ttu-id="86398-140">Connect app with real-time monitoring</span><span class="sxs-lookup"><span data-stu-id="86398-140">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a><span data-ttu-id="86398-141">Enable push notifications and in-app messaging</span><span class="sxs-lookup"><span data-stu-id="86398-141">Enable push notifications and in-app messaging</span></span>
[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

### <a name="update-the-engagementconfiguration"></a><span data-ttu-id="86398-142">Update the EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="86398-142">Update the EngagementConfiguration</span></span>
1. <span data-ttu-id="86398-143">Open up the **EngagementConfiguration** script file from the SDK folder and update the **ANDROID\_GOOGLE\_NUMBER** with the **Google Project Number** you obtained earlier from the Google Cloud Developer portal.</span><span class="sxs-lookup"><span data-stu-id="86398-143">Open up the **EngagementConfiguration** script file from the SDK folder and update the **ANDROID\_GOOGLE\_NUMBER** with the **Google Project Number** you obtained earlier from the Google Cloud Developer portal.</span></span> <span data-ttu-id="86398-144">This is a string value so make sure to enclose it in double quotes.</span><span class="sxs-lookup"><span data-stu-id="86398-144">This is a string value so make sure to enclose it in double quotes.</span></span> 
   
    ![][75]
2. <span data-ttu-id="86398-145">Save the file.</span><span class="sxs-lookup"><span data-stu-id="86398-145">Save the file.</span></span> 
3. <span data-ttu-id="86398-146">Execute **File -> Engagement -> Generate Android Manifest**.</span><span class="sxs-lookup"><span data-stu-id="86398-146">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="86398-147">This is the plugin added by the Mobile Engagement SDK and clicking on it will automatically update your project settings.</span><span class="sxs-lookup"><span data-stu-id="86398-147">This is the plugin added by the Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

### <a name="configure-the-app-to-receive-notifications"></a><span data-ttu-id="86398-148">Configure the app to receive notifications</span><span class="sxs-lookup"><span data-stu-id="86398-148">Configure the app to receive notifications</span></span>
1. <span data-ttu-id="86398-149">Open up the **PlayerController** script attached to the Player object for editing.</span><span class="sxs-lookup"><span data-stu-id="86398-149">Open up the **PlayerController** script attached to the Player object for editing.</span></span> 
2. <span data-ttu-id="86398-150">Add the following to the `Start()` method</span><span class="sxs-lookup"><span data-stu-id="86398-150">Add the following to the `Start()` method</span></span>
   
        EngagementReachAgent.Initialize();
3. <span data-ttu-id="86398-151">Now that the app is updated, deploy and run the app on a device per the instructions provided below.</span><span class="sxs-lookup"><span data-stu-id="86398-151">Now that the app is updated, deploy and run the app on a device per the instructions provided below.</span></span> 

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[40]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-android-get-started/40.png
[70]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-android-get-started/70.png
[71]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-android-get-started/71.png
[72]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-android-get-started/72.png
[73]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-android-get-started/73.png
[74]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-android-get-started/74.png
[75]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-android-get-started/75.png
[51]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-android-get-started/51.png
[52]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-android-get-started/52.png
[53]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-android-get-started/53.png
[54]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-android-get-started/54.png











