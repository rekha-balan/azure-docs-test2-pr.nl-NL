---
title: Azure Mobile Engagement User Interface - My Account
description: Learn how to manage your account profile and test devices using Azure Mobile Engagement
services: mobile-engagement
documentationcenter: ''
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 22832678-3959-4b8c-9fb2-f2ff5974e5d1
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: e8a044dab8868cbd31759999a72b703ac9a79fc4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564286"
---
# <a name="how-to-manage-your-account-profile-and-test-devices"></a><span data-ttu-id="c66de-103">How to manage your account profile and test devices</span><span class="sxs-lookup"><span data-stu-id="c66de-103">How to manage your account profile and test devices</span></span>
<span data-ttu-id="c66de-104">This article describes the **Home** page of the **Mobile Engagement** portal.</span><span class="sxs-lookup"><span data-stu-id="c66de-104">This article describes the **Home** page of the **Mobile Engagement** portal.</span></span> <span data-ttu-id="c66de-105">You use the **Mobile Engagement** portal to monitor and manage your mobile apps.</span><span class="sxs-lookup"><span data-stu-id="c66de-105">You use the **Mobile Engagement** portal to monitor and manage your mobile apps.</span></span> 

<span data-ttu-id="c66de-106">To get to the **my account** page, click on your account on the top of the page.</span><span class="sxs-lookup"><span data-stu-id="c66de-106">To get to the **my account** page, click on your account on the top of the page.</span></span>

<span data-ttu-id="c66de-107">The My Account section of the UI is where you can view and change the settings associated with your account, including your Profile settings and test Device IDs.</span><span class="sxs-lookup"><span data-stu-id="c66de-107">The My Account section of the UI is where you can view and change the settings associated with your account, including your Profile settings and test Device IDs.</span></span> <span data-ttu-id="c66de-108">These settings contain items that can also be accessed via the Device API.</span><span class="sxs-lookup"><span data-stu-id="c66de-108">These settings contain items that can also be accessed via the Device API.</span></span>

![MyAccount1][7]  

## <a name="profile"></a><span data-ttu-id="c66de-110">Profile:</span><span class="sxs-lookup"><span data-stu-id="c66de-110">Profile:</span></span>
<span data-ttu-id="c66de-111">You can view or change any of your account settings shown below.</span><span class="sxs-lookup"><span data-stu-id="c66de-111">You can view or change any of your account settings shown below.</span></span> <span data-ttu-id="c66de-112">You can also give another user permission to use your application based on their e-mail address from the [Home](mobile-engagement-user-interface-home.md).</span><span class="sxs-lookup"><span data-stu-id="c66de-112">You can also give another user permission to use your application based on their e-mail address from the [Home](mobile-engagement-user-interface-home.md).</span></span>

![MyAccount2][8]  

## <a name="devices"></a><span data-ttu-id="c66de-114">Devices:</span><span class="sxs-lookup"><span data-stu-id="c66de-114">Devices:</span></span>
<span data-ttu-id="c66de-115">You can view, add, or remove test Device ID's of the test devices that you can use to test your **reach** or **push** campaigns.</span><span class="sxs-lookup"><span data-stu-id="c66de-115">You can view, add, or remove test Device ID's of the test devices that you can use to test your **reach** or **push** campaigns.</span></span> <span data-ttu-id="c66de-116">Contextual instructions for how to find the Device ID of devices for each platform (iOS, Android, Windows Phone, etc.) are displayed when you click "New Device".</span><span class="sxs-lookup"><span data-stu-id="c66de-116">Contextual instructions for how to find the Device ID of devices for each platform (iOS, Android, Windows Phone, etc.) are displayed when you click "New Device".</span></span> 

![MyAccount3][9]  

<span data-ttu-id="c66de-118">To use Push API or Device API you need to know your users' unique device identifier (the deviceid parameter).</span><span class="sxs-lookup"><span data-stu-id="c66de-118">To use Push API or Device API you need to know your users' unique device identifier (the deviceid parameter).</span></span> <span data-ttu-id="c66de-119">There are several ways to retrieve it:</span><span class="sxs-lookup"><span data-stu-id="c66de-119">There are several ways to retrieve it:</span></span>

1. <span data-ttu-id="c66de-120">From your backend, you can use the "Get" feature of the Device API to get the full list of device identifiers.</span><span class="sxs-lookup"><span data-stu-id="c66de-120">From your backend, you can use the "Get" feature of the Device API to get the full list of device identifiers.</span></span>
2. <span data-ttu-id="c66de-121">From your app, you can use the SDK to get it.</span><span class="sxs-lookup"><span data-stu-id="c66de-121">From your app, you can use the SDK to get it.</span></span> <span data-ttu-id="c66de-122">(On Android, call the getDeviceID() function of the Agent class, and on iOS, read the deviceid property of the Agent class.)</span><span class="sxs-lookup"><span data-stu-id="c66de-122">(On Android, call the getDeviceID() function of the Agent class, and on iOS, read the deviceid property of the Agent class.)</span></span>
3. <span data-ttu-id="c66de-123">From a Reach announcement, if the action URL associated with the announcement contains the {deviceid} pattern, it will be automatically replaced by the identifier of the device triggering the action.</span><span class="sxs-lookup"><span data-stu-id="c66de-123">From a Reach announcement, if the action URL associated with the announcement contains the {deviceid} pattern, it will be automatically replaced by the identifier of the device triggering the action.</span></span>
   <span data-ttu-id="c66de-124">http://<example>.com/registeruser?deviceid={deviceid}&otherparam=myparamdata will be replaced by: http://<example>.com/registeruser?deviceid=XXXXXXXXXXXXXXXX&otherparam=myparamdata</span><span class="sxs-lookup"><span data-stu-id="c66de-124">http://<example>.com/registeruser?deviceid={deviceid}&otherparam=myparamdata will be replaced by: http://<example>.com/registeruser?deviceid=XXXXXXXXXXXXXXXX&otherparam=myparamdata</span></span> 
4. <span data-ttu-id="c66de-125">From a Reach web announcement, if the HTML code of the announcement contains the {deviceid} pattern, it will be automatically replaced by the identifier of the device displaying the web announcement.</span><span class="sxs-lookup"><span data-stu-id="c66de-125">From a Reach web announcement, if the HTML code of the announcement contains the {deviceid} pattern, it will be automatically replaced by the identifier of the device displaying the web announcement.</span></span>
   <span data-ttu-id="c66de-126">Here is my device identifier: {deviceid} will be replaced by: Here is my device identifier: XXXXXXXXXXXXXXXX</span><span class="sxs-lookup"><span data-stu-id="c66de-126">Here is my device identifier: {deviceid} will be replaced by: Here is my device identifier: XXXXXXXXXXXXXXXX</span></span>
5. <span data-ttu-id="c66de-127">Open your application on your device and perform an Event in your app which has been tagged.</span><span class="sxs-lookup"><span data-stu-id="c66de-127">Open your application on your device and perform an Event in your app which has been tagged.</span></span>
   <span data-ttu-id="c66de-128">From "UI - your app - Monitor - Events - Details", find the Event you performed in the list.</span><span class="sxs-lookup"><span data-stu-id="c66de-128">From "UI - your app - Monitor - Events - Details", find the Event you performed in the list.</span></span>
   <span data-ttu-id="c66de-129">Click to this event in the Monitor.</span><span class="sxs-lookup"><span data-stu-id="c66de-129">Click to this event in the Monitor.</span></span>
   <span data-ttu-id="c66de-130">You should find your Device ID in the list of the devices that have performed this event.</span><span class="sxs-lookup"><span data-stu-id="c66de-130">You should find your Device ID in the list of the devices that have performed this event.</span></span>
   <span data-ttu-id="c66de-131">Then, you can copy this Device ID and register it in the "UI - My Account - Devices - New Device - Select your device platform".</span><span class="sxs-lookup"><span data-stu-id="c66de-131">Then, you can copy this Device ID and register it in the "UI - My Account - Devices - New Device - Select your device platform".</span></span>
   ><span data-ttu-id="c66de-132">(Be aware that when IDFA is disabled for iOS, the Device ID may change over the time if you uninstall and reinstall your app.)</span><span class="sxs-lookup"><span data-stu-id="c66de-132">(Be aware that when IDFA is disabled for iOS, the Device ID may change over the time if you uninstall and reinstall your app.)</span></span>

## <a name="troubleshooting-guide"></a><span data-ttu-id="c66de-133">Troubleshooting Guide</span><span class="sxs-lookup"><span data-stu-id="c66de-133">Troubleshooting Guide</span></span>
* <span data-ttu-id="c66de-134">[Troubleshooting Guide - Service][Link 24]</span><span class="sxs-lookup"><span data-stu-id="c66de-134">[Troubleshooting Guide - Service][Link 24]</span></span>

## <a name="see-also"></a><span data-ttu-id="c66de-135">See also</span><span class="sxs-lookup"><span data-stu-id="c66de-135">See also</span></span>
* <span data-ttu-id="c66de-136">[UI Documentation - Home][Link 13]</span><span class="sxs-lookup"><span data-stu-id="c66de-136">[UI Documentation - Home][Link 13]</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-home/home1.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-home/home5.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-reach/reach1.png
[19]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-reach/reach2.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-segments/segments1.png
[36]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-segments/segments2.png
[37]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-segments/segments3.png
[38]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-segments/segments4.png
[39]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-segments/segments5.png
[40]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-segments/segments6.png
[41]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-segments/segments7.png
[42]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-segments/segments8.png
[43]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-segments/segments9.png
[44]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-segments/segments10.png
[45]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-segments/segments11.png
[46]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-settings/settings1.png
[47]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-settings/settings2.png
[48]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-settings/settings3.png
[49]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-settings/settings4.png
[50]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-settings/settings5.png
[51]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-settings/settings6.png
[52]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-settings/settings7.png
[53]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-settings/settings8.png
[54]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-settings/settings9.png
[55]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-settings/settings10.png
[56]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-settings/settings11.png
[57]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-settings/settings12.png
[58]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-settings/settings13.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md




























































