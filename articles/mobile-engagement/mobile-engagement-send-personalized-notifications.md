---
title: Send personalized notification with Azure Mobile Engagement
description: How to send personalized notifications by including user profile information in the notifications like their names
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 51007089-156a-4bac-bb1b-a590633bf2a2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: all
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1a7860985140c3f3efd5bdf76bed3f1c940c9786
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552747"
---
# <a name="personalize-notifications-by-including-user-name"></a><span data-ttu-id="a73e7-103">Personalize notifications by including user name</span><span class="sxs-lookup"><span data-stu-id="a73e7-103">Personalize notifications by including user name</span></span>
<span data-ttu-id="a73e7-104">In your quest to make notifications more appealing to your app users, you should consider personalizing them.</span><span class="sxs-lookup"><span data-stu-id="a73e7-104">In your quest to make notifications more appealing to your app users, you should consider personalizing them.</span></span> <span data-ttu-id="a73e7-105">One powerful approach comprises of selectively using the app users names to address the notifications to make them more personal.</span><span class="sxs-lookup"><span data-stu-id="a73e7-105">One powerful approach comprises of selectively using the app users names to address the notifications to make them more personal.</span></span> <span data-ttu-id="a73e7-106">A word of caution here - you should approach adding user names to the notifications carefully because if you overuse this strategy then it could come across as creepy for some app users.</span><span class="sxs-lookup"><span data-stu-id="a73e7-106">A word of caution here - you should approach adding user names to the notifications carefully because if you overuse this strategy then it could come across as creepy for some app users.</span></span> <span data-ttu-id="a73e7-107">You should also ensure that you are letting the user opt in to provide these personal details to you with full consent in the mobile app before starting to use this.</span><span class="sxs-lookup"><span data-stu-id="a73e7-107">You should also ensure that you are letting the user opt in to provide these personal details to you with full consent in the mobile app before starting to use this.</span></span> 

<span data-ttu-id="a73e7-108">Technically, with Azure Mobile Engagement, you can accomplish personalizing the notifications by following the steps below in which we will use the scenario of including user name in the notifications.</span><span class="sxs-lookup"><span data-stu-id="a73e7-108">Technically, with Azure Mobile Engagement, you can accomplish personalizing the notifications by following the steps below in which we will use the scenario of including user name in the notifications.</span></span> <span data-ttu-id="a73e7-109">You will use the concept of App-Info or Tags whose values could either be passed by the SDKs integrated in the Mobile App or via APIs.</span><span class="sxs-lookup"><span data-stu-id="a73e7-109">You will use the concept of App-Info or Tags whose values could either be passed by the SDKs integrated in the Mobile App or via APIs.</span></span> <span data-ttu-id="a73e7-110">These App-Infos or Tags could then be used:</span><span class="sxs-lookup"><span data-stu-id="a73e7-110">These App-Infos or Tags could then be used:</span></span>

1. <span data-ttu-id="a73e7-111">for targeting notifications to specific users based on the values of the App-Info or</span><span class="sxs-lookup"><span data-stu-id="a73e7-111">for targeting notifications to specific users based on the values of the App-Info or</span></span> 
2. <span data-ttu-id="a73e7-112">as placeholders in the notifications which will be replaced with values specific to the device/user while sending notifications to that device.</span><span class="sxs-lookup"><span data-stu-id="a73e7-112">as placeholders in the notifications which will be replaced with values specific to the device/user while sending notifications to that device.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="a73e7-113">Note that the speed of sending notifications will see a reduction because of this additional processing of replacing app-info values with each notifications.</span><span class="sxs-lookup"><span data-stu-id="a73e7-113">Note that the speed of sending notifications will see a reduction because of this additional processing of replacing app-info values with each notifications.</span></span> 
> 
> 

## <a name="register-app-info-in-the-mobile-engagement-portal"></a><span data-ttu-id="a73e7-114">Register App-Info in the Mobile Engagement Portal</span><span class="sxs-lookup"><span data-stu-id="a73e7-114">Register App-Info in the Mobile Engagement Portal</span></span>
1) <span data-ttu-id="a73e7-115">You start with registering App Info or Tags in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a73e7-115">You start with registering App Info or Tags in the Azure portal.</span></span> <span data-ttu-id="a73e7-116">Go to **Settings** -> **Tag (App-Info)** for this.</span><span class="sxs-lookup"><span data-stu-id="a73e7-116">Go to **Settings** -> **Tag (App-Info)** for this.</span></span>  

![][1]    

2) <span data-ttu-id="a73e7-117">Click on **New tag (app-info)** and provide the name as *user_name* and the type as *string* and click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="a73e7-117">Click on **New tag (app-info)** and provide the name as *user_name* and the type as *string* and click **Submit**.</span></span> 

![][2]

3) <span data-ttu-id="a73e7-118">You will finally see this app-info registered like the following:</span><span class="sxs-lookup"><span data-stu-id="a73e7-118">You will finally see this app-info registered like the following:</span></span>

![][3]

## <a name="send-app-info-from-the-client-sdk"></a><span data-ttu-id="a73e7-119">Send App-Info from the client SDK</span><span class="sxs-lookup"><span data-stu-id="a73e7-119">Send App-Info from the client SDK</span></span>
<span data-ttu-id="a73e7-120">Here we are using the Windows Universal app example but equivalent methods exist for our other SDKs also.</span><span class="sxs-lookup"><span data-stu-id="a73e7-120">Here we are using the Windows Universal app example but equivalent methods exist for our other SDKs also.</span></span> 

<span data-ttu-id="a73e7-121">Assuming you have a method in the mobile app where you get the profile information from the user like their names probably after authenticating them, you will call `SendAppInfo` method here and populate the value of the `user_name` app info that you registered earlier into the Mobile Engagement service backend.</span><span class="sxs-lookup"><span data-stu-id="a73e7-121">Assuming you have a method in the mobile app where you get the profile information from the user like their names probably after authenticating them, you will call `SendAppInfo` method here and populate the value of the `user_name` app info that you registered earlier into the Mobile Engagement service backend.</span></span> 

    Dictionary<object, object> appInfo = new Dictionary<object, object>();
    appInfo.Add("user_name", str);
    EngagementAgent.Instance.SendAppInfo(appInfo); 

## <a name="send-personalized-notifications"></a><span data-ttu-id="a73e7-122">Send personalized notifications</span><span class="sxs-lookup"><span data-stu-id="a73e7-122">Send personalized notifications</span></span>
<span data-ttu-id="a73e7-123">Now you are all set to send notifications using this **user_name**.</span><span class="sxs-lookup"><span data-stu-id="a73e7-123">Now you are all set to send notifications using this **user_name**.</span></span> 

1) <span data-ttu-id="a73e7-124">Go to Mobile Engagement Portal on the **Reach** tab to create a notification and you can use this placeholder in the following format anywhere in the notification title or the body.</span><span class="sxs-lookup"><span data-stu-id="a73e7-124">Go to Mobile Engagement Portal on the **Reach** tab to create a notification and you can use this placeholder in the following format anywhere in the notification title or the body.</span></span> 

![][4]    

> [!NOTE]
> <span data-ttu-id="a73e7-125">Any users for which the user_name app info is not set, will not get any notification.</span><span class="sxs-lookup"><span data-stu-id="a73e7-125">Any users for which the user_name app info is not set, will not get any notification.</span></span> <span data-ttu-id="a73e7-126">If you run the notification campaign in test mode and if you do not have app-info set then we will send '?' character to replace the placeholder.</span><span class="sxs-lookup"><span data-stu-id="a73e7-126">If you run the notification campaign in test mode and if you do not have app-info set then we will send '?' character to replace the placeholder.</span></span> 
> 
> 

2) <span data-ttu-id="a73e7-127">When Mobile Engagement will select a device to send this notification then it will look at this app-info and replace the value in the placeholder.</span><span class="sxs-lookup"><span data-stu-id="a73e7-127">When Mobile Engagement will select a device to send this notification then it will look at this app-info and replace the value in the placeholder.</span></span>  
<span data-ttu-id="a73e7-128">For example, if we have set `str = "Scott"` for a user than the device registration will get associated with the app info of **user_name = SCOTT** for this user and this user will see an out of app push notification in the following format.</span><span class="sxs-lookup"><span data-stu-id="a73e7-128">For example, if we have set `str = "Scott"` for a user than the device registration will get associated with the app info of **user_name = SCOTT** for this user and this user will see an out of app push notification in the following format.</span></span> 

![][5]    

<!-- Images. -->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-send-personalized-notifications/app-info.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-send-personalized-notifications/create-app-info.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-send-personalized-notifications/app-info-user-name.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-send-personalized-notifications/personal-notification.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-send-personalized-notifications/notification.png






