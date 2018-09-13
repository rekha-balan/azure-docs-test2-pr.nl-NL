---
title: Use Emoji emoticons within Azure Mobile Engagement
description: How to use Emoji emoticons within your push notifications
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 663317d7-3c93-4e8f-b13d-c6fb342124ee
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b50127ef561f2821c3a6ee4c3de024dc9a916e32
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553332"
---
# <a name="use-emoji-emoticon-within-push-notifications"></a>Use Emoji emoticon within Push Notifications
You can include Emoji emoticons in you push notification in a few easy steps: 

1. First of all you need to find the Emoji you want to send in the message. Please ensure that the Emoji you are selecting will be supported by the target device as device manufactures take some time to add newly approved Emojis to the device platforms. 
2. On **Windows** - you can navigate to this [link](http://apps.timwhitlock.info/emoji/tables/unicode) and copy the 'Native' icon.
   
    ![][7] 
3. On **Mac** - you can find the Emojis in Dictionary application under Edit -> Emoji & Symbols.
   
    ![][6] 
4. Now, go to the **Reach** tab on the the Azure Mobile Engagement portal. Select the type of your push notification (Announcement, polls etc). For this example we choose an announcement push.
5. Specify the different fields of the notification until you reach the text of the notification. This is where you will add your Emoji Emoticon. You can choose to put it in the title, the message, or both. You will need to drag and drop or copy the Emoji that you find from the locations above. 
   
    ![][1]
6. Complete the other fields for the notification and save it. 
7. When you run a test or activate the announcement you will see a notification with the emoticon as specified.   
   
    ![][3] ![][4] ![][5]

<!-- Images. -->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-use-emoji-with-push/notification_input.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-use-emoji-with-push/iOS_Emoji.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-use-emoji-with-push/Android_Emoji.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-use-emoji-with-push/WindowsPhone_Emoji.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-use-emoji-with-push/Mac_SelectEmoji.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-use-emoji-with-push/Windows_SelectEmoji.png







