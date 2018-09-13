---
title: Get Started with Azure Mobile Engagement for Unity iOS deployment
description: Learn how to use Azure Mobile Engagement with Analytics and Push Notifications for Unity apps deploying to iOS devices.
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 7ddfbac3-8d13-4ebe-b061-c865f357297f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f30290bfda7ed09c1289a4a49984e2a8a1ffa819
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549079"
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-ios-deployment"></a><span data-ttu-id="04fac-103">Get Started with Azure Mobile Engagement for Unity iOS deployment</span><span class="sxs-lookup"><span data-stu-id="04fac-103">Get Started with Azure Mobile Engagement for Unity iOS deployment</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="04fac-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of a Unity application when deploying to an iOS device.</span><span class="sxs-lookup"><span data-stu-id="04fac-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of a Unity application when deploying to an iOS device.</span></span>
<span data-ttu-id="04fac-105">This tutorial uses the classic Unity Roll a Ball tutorial as the starting point.</span><span class="sxs-lookup"><span data-stu-id="04fac-105">This tutorial uses the classic Unity Roll a Ball tutorial as the starting point.</span></span> <span data-ttu-id="04fac-106">You should follow the steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with the Mobile Engagement integration we showcase in the tutorial below.</span><span class="sxs-lookup"><span data-stu-id="04fac-106">You should follow the steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with the Mobile Engagement integration we showcase in the tutorial below.</span></span> 

<span data-ttu-id="04fac-107">This tutorial requires the following:</span><span class="sxs-lookup"><span data-stu-id="04fac-107">This tutorial requires the following:</span></span>

* [<span data-ttu-id="04fac-108">Unity Editor</span><span class="sxs-lookup"><span data-stu-id="04fac-108">Unity Editor</span></span>](http://unity3d.com/get-unity)
* [<span data-ttu-id="04fac-109">Mobile Engagement Unity SDK</span><span class="sxs-lookup"><span data-stu-id="04fac-109">Mobile Engagement Unity SDK</span></span>](https://aka.ms/azmeunitysdk)
* <span data-ttu-id="04fac-110">XCode Editor</span><span class="sxs-lookup"><span data-stu-id="04fac-110">XCode Editor</span></span>

> [!NOTE]
> <span data-ttu-id="04fac-111">To complete this tutorial, you must have an active Azure account.</span><span class="sxs-lookup"><span data-stu-id="04fac-111">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="04fac-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="04fac-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="04fac-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="04fac-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).</span></span>
> 
> 

## <a id="setup-azme"></a><span data-ttu-id="04fac-114">Setup Mobile Engagement for your iOS app</span><span class="sxs-lookup"><span data-stu-id="04fac-114">Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a><span data-ttu-id="04fac-115">Connect your app to the Mobile Engagement backend</span><span class="sxs-lookup"><span data-stu-id="04fac-115">Connect your app to the Mobile Engagement backend</span></span>
### <a name="import-the-unity-package"></a><span data-ttu-id="04fac-116">Import the Unity package</span><span class="sxs-lookup"><span data-stu-id="04fac-116">Import the Unity package</span></span>
1. <span data-ttu-id="04fac-117">Download the [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it to your local machine.</span><span class="sxs-lookup"><span data-stu-id="04fac-117">Download the [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it to your local machine.</span></span> 
2. <span data-ttu-id="04fac-118">Go to **Assets -> Import Package -> Custom Package** and select the package you downloaded in the above step.</span><span class="sxs-lookup"><span data-stu-id="04fac-118">Go to **Assets -> Import Package -> Custom Package** and select the package you downloaded in the above step.</span></span> 
   
    ![][70] 
3. <span data-ttu-id="04fac-119">Make sure all files are selected and click **Import** button.</span><span class="sxs-lookup"><span data-stu-id="04fac-119">Make sure all files are selected and click **Import** button.</span></span> 
   
    ![][71] 
4. <span data-ttu-id="04fac-120">Once Import is successful, you will see the imported SDK files in your project.</span><span class="sxs-lookup"><span data-stu-id="04fac-120">Once Import is successful, you will see the imported SDK files in your project.</span></span>  
   
    ![][72] 

### <a name="update-the-engagementconfiguration"></a><span data-ttu-id="04fac-121">Update the EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="04fac-121">Update the EngagementConfiguration</span></span>
1. <span data-ttu-id="04fac-122">Open up the **EngagementConfiguration** script file from the SDK folder and update the **IOS\_CONNECTION\_STRING** with the connection string you obtained earlier from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="04fac-122">Open up the **EngagementConfiguration** script file from the SDK folder and update the **IOS\_CONNECTION\_STRING** with the connection string you obtained earlier from the Azure portal.</span></span>  
   
    ![][73]
2. <span data-ttu-id="04fac-123">Save the file.</span><span class="sxs-lookup"><span data-stu-id="04fac-123">Save the file.</span></span> 

### <a name="configure-the-app-for-basic-tracking"></a><span data-ttu-id="04fac-124">Configure the app for basic tracking</span><span class="sxs-lookup"><span data-stu-id="04fac-124">Configure the app for basic tracking</span></span>
1. <span data-ttu-id="04fac-125">Open up the **PlayerController** script attached to the Player object for editing.</span><span class="sxs-lookup"><span data-stu-id="04fac-125">Open up the **PlayerController** script attached to the Player object for editing.</span></span> 
2. <span data-ttu-id="04fac-126">Add the following using statement:</span><span class="sxs-lookup"><span data-stu-id="04fac-126">Add the following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Unity;
3. <span data-ttu-id="04fac-127">Add the following to the `Start()` method</span><span class="sxs-lookup"><span data-stu-id="04fac-127">Add the following to the `Start()` method</span></span>
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-the-app"></a><span data-ttu-id="04fac-128">Deploy and run the app</span><span class="sxs-lookup"><span data-stu-id="04fac-128">Deploy and run the app</span></span>
1. <span data-ttu-id="04fac-129">Connect an iOS device to your machine.</span><span class="sxs-lookup"><span data-stu-id="04fac-129">Connect an iOS device to your machine.</span></span> 
2. <span data-ttu-id="04fac-130">Open up **File -> Build Settings**</span><span class="sxs-lookup"><span data-stu-id="04fac-130">Open up **File -> Build Settings**</span></span> 
   
    ![][40]
3. <span data-ttu-id="04fac-131">Select **iOS** and then click on **Switch Platform**</span><span class="sxs-lookup"><span data-stu-id="04fac-131">Select **iOS** and then click on **Switch Platform**</span></span>
   
    ![][41]
   
    ![][42]
4. <span data-ttu-id="04fac-132">Click on **Player settings** and provide a valid Bundle Identifier.</span><span class="sxs-lookup"><span data-stu-id="04fac-132">Click on **Player settings** and provide a valid Bundle Identifier.</span></span> 
   
    ![][53]
5. <span data-ttu-id="04fac-133">Finally click on **Build And Run**</span><span class="sxs-lookup"><span data-stu-id="04fac-133">Finally click on **Build And Run**</span></span>
   
    ![][54]
6. <span data-ttu-id="04fac-134">You may be asked to provide a folder name to store the iOS package.</span><span class="sxs-lookup"><span data-stu-id="04fac-134">You may be asked to provide a folder name to store the iOS package.</span></span> 
   
    ![][43]
7. <span data-ttu-id="04fac-135">If everything goes fine, then the project will be compiled and you should open it up on your XCode application.</span><span class="sxs-lookup"><span data-stu-id="04fac-135">If everything goes fine, then the project will be compiled and you should open it up on your XCode application.</span></span> 
8. <span data-ttu-id="04fac-136">Make sure that the **Bundle identifier** is correct in the project.</span><span class="sxs-lookup"><span data-stu-id="04fac-136">Make sure that the **Bundle identifier** is correct in the project.</span></span>  
   
    ![][75]
9. <span data-ttu-id="04fac-137">Now run the app in XCode so that the package is deployed to your connected device and you should see your Unity game on your phone!</span><span class="sxs-lookup"><span data-stu-id="04fac-137">Now run the app in XCode so that the package is deployed to your connected device and you should see your Unity game on your phone!</span></span> 

## <a id="monitor"></a><span data-ttu-id="04fac-138">Connect app with real-time monitoring</span><span class="sxs-lookup"><span data-stu-id="04fac-138">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a><span data-ttu-id="04fac-139">Enable push notifications and in-app messaging</span><span class="sxs-lookup"><span data-stu-id="04fac-139">Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="04fac-140">Mobile Engagement allows you to interact with your users and REACH with push notifications and in-app messaging in the context of campaigns.</span><span class="sxs-lookup"><span data-stu-id="04fac-140">Mobile Engagement allows you to interact with your users and REACH with push notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="04fac-141">This module is called REACH in the Mobile Engagement portal.</span><span class="sxs-lookup"><span data-stu-id="04fac-141">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="04fac-142">You don't have to do any additional configuration in your app to receive notifications and it is already setup for it.</span><span class="sxs-lookup"><span data-stu-id="04fac-142">You don't have to do any additional configuration in your app to receive notifications and it is already setup for it.</span></span>

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[40]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-ios-get-started/40.png
[41]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-ios-get-started/41.png
[42]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-ios-get-started/42.png
[43]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-ios-get-started/43.png
[53]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-ios-get-started/53.png
[54]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-ios-get-started/54.png
[70]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-ios-get-started/70.png
[71]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-ios-get-started/71.png
[72]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-ios-get-started/72.png
[73]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-ios-get-started/73.png
[74]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-ios-get-started/74.png
[75]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-ios-get-started/75.png












