---
title: Azure Mobile Engagement - Key features
description: Describes the key features of Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: d98bafb6-4fd0-4cc3-8c2f-962af70c416c
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 6e17670eb5df5b68c6baf8c0e09cdf2fc8331585
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564545"
---
# <a name="azure-mobile-engagement---key-features"></a>Azure Mobile Engagement - Key features
This article gives a high level overview about the key features of the Mobile Engagement platform. 

## <a name="general"></a>**General**
* **Find SDKs for all major platforms** SDKs available for all major platforms - iOS, Android, Universal Windows, Windows Phone Silverlight, Kindle, Cordova. 
  We provide easy to integrate SDKs and helpful documentation to get you started on any platform of your choice. 
* **Separate SaaS portal** Allows easy access to the marketing team without the need to go through the Azure management portal. 
* **Availability of open REST APIs** To integrate and automate with CRM/CMS/IT systems using open-platform APIs, we provide open REST APIs and .NET SDK to consume these APIs that can allow you to easily integrate and automate with Mobile Engagement. See [this](mobile-engagement-api-authentication.md) for details. 
* **Power BI connector available** You can also pull out the key analytics charts into a Power BI dashboard. See this [guide](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-mobile/)
* **Assurance of Security & Privacy** Azure Mobile Engagement being part of the Azure family follows all the standard best practices around security & privacy expected for a cloud service.

## <a name="actionable-analytics"></a>**Actionable Analytics**
* **Monitor data in real time** You can track real time analytics using our Monitor module which shows details like sessions, events, errors & crashes all in real-time. Take a look at this [article](mobile-engagement-concepts.md) to get an understanding of the basic concepts. 
  
    ![][1]
  
    ![][2]        
* **View aggregated data** You also get a richer view of your aggregated analytics data using our Analytics module which allows you to easily filter your data based on your app version and time periods.
  
    ![][3]        
* **Get insights into your users and retention pattern**
  
    ![][4]        
* **Get insights into where your users are coming from and how much time are they spending in the screen**
  
    ![][5]        
  
    ![][6]        
* **Find out which screens are your app users visiting and how can you optimize the user path** This helps them to discover screens and features that you want them to.
  
    ![][7]        
  
    ![][8]        
* **Get insights into which are the most frequent events in your app and get an understanding of your business process based on these events** 
  
    ![][9]    
* **Track common errors and crashes and get insights for your developer team**
  
    ![][10]        
  
    ![][11]    
* **Understand which devices and networks are your app users accessing your app from, to optimize the app** 
  
    ![][12]    

## <a name="targeted--personalized-push-notifications"></a>**Targeted & Personalized Push Notifications**
* **Create a segment based on any of the collected data** You can use any of the Event/Session/Activity/Job/Crash/Error/Tags data for this.
  
    ![][13]
  
    ![][14]        
* **Track the history of your created segments day over day**
  
    ![][15]    
* **Send targeted notifications** targeting commonly used like old/new users etc. or to your custom created segment
  
    ![][16]    
* **Send both out-of-app/system & rich HTML based in-app push notifications as appropriate for your scenario**
  
    ![][17]    
  
    ![][18]    
* **Target in-app notifications to show up on a specific screen/activity in the app**
  
    ![][19]    
* **Specify an "action" when the user clicks on a notification** It could be as simple as opening up a webpage or navigating within the app to a specific screen at the click of the notification. 
  
    ![][20]
* **Send localized notifications** so that it appeals to the app users in the language they are most comfortable in. 
  
    ![][21]    
* **Specify a start and end time for your campaigns** 
  
    ![][22]    
* **Easily test your notifications** by registering a test device and sending the test notification to only this device.
  
    ![][23]    
* **Easily set up an in-app notification to show up as a quick poll/survey**  
  
    ![][24]
* **Get push campaign statistics** for your notifications to give you an idea about how successful were your notifications.
  
    ![][25]    
* **Easily personalize and give character to your notifications using app-info/tags and emojis** 
  
    ![][26]    
  
    ![][27]    
* **Set Push Limits to prevent spamming users** You don’t want to send a lot of pushes to your app users and come across as spamming them. This is where our Push limits feature is useful which allows you to configure push limits at the granularity of a segment. 
  
    ![][28]            

<!-- Images -->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-key-features/monitor1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-key-features/monitor2.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-key-features/analytics-filter.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-key-features/retention.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-key-features/analytics-geomap.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-key-features/analytics-session-length.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-key-features/analytics-activities.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-key-features/analytics-userpath.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-key-features/analytics-events.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-key-features/analyics-errors.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-key-features/analyics-errors-details.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-key-features/technicals.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-key-features/segment.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-key-features/segment-creation.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-key-features/segment-history.png
[16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-key-features/segment-push.png
[17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-key-features/out-of-app.png
[18]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-key-features/in-app-push.png
[19]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-key-features/push-in-activity.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-key-features/push-action.png
[21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-key-features/push-languages.png
[22]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-key-features/push-timeframe.png
[23]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-key-features/push-test.png
[24]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-key-features/push-poll.png
[25]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-key-features/push-stats.png
[26]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-key-features/push_personalized.png
[27]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-key-features/push_emoji.png
[28]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-key-features/push_limits.png





































