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
# <a name="use-emoji-emoticon-within-push-notifications"></a><span data-ttu-id="c09a7-103">Use Emoji emoticon within Push Notifications</span><span class="sxs-lookup"><span data-stu-id="c09a7-103">Use Emoji emoticon within Push Notifications</span></span>
<span data-ttu-id="c09a7-104">You can include Emoji emoticons in you push notification in a few easy steps:</span><span class="sxs-lookup"><span data-stu-id="c09a7-104">You can include Emoji emoticons in you push notification in a few easy steps:</span></span> 

1. <span data-ttu-id="c09a7-105">First of all you need to find the Emoji you want to send in the message.</span><span class="sxs-lookup"><span data-stu-id="c09a7-105">First of all you need to find the Emoji you want to send in the message.</span></span> <span data-ttu-id="c09a7-106">Please ensure that the Emoji you are selecting will be supported by the target device as device manufactures take some time to add newly approved Emojis to the device platforms.</span><span class="sxs-lookup"><span data-stu-id="c09a7-106">Please ensure that the Emoji you are selecting will be supported by the target device as device manufactures take some time to add newly approved Emojis to the device platforms.</span></span> 
2. <span data-ttu-id="c09a7-107">On **Windows** - you can navigate to this [link](http://apps.timwhitlock.info/emoji/tables/unicode) and copy the 'Native' icon.</span><span class="sxs-lookup"><span data-stu-id="c09a7-107">On **Windows** - you can navigate to this [link](http://apps.timwhitlock.info/emoji/tables/unicode) and copy the 'Native' icon.</span></span>
   
    ![][7] 
3. <span data-ttu-id="c09a7-108">On **Mac** - you can find the Emojis in Dictionary application under Edit -> Emoji & Symbols.</span><span class="sxs-lookup"><span data-stu-id="c09a7-108">On **Mac** - you can find the Emojis in Dictionary application under Edit -> Emoji & Symbols.</span></span>
   
    ![][6] 
4. <span data-ttu-id="c09a7-109">Now, go to the **Reach** tab on the the Azure Mobile Engagement portal.</span><span class="sxs-lookup"><span data-stu-id="c09a7-109">Now, go to the **Reach** tab on the the Azure Mobile Engagement portal.</span></span> <span data-ttu-id="c09a7-110">Select the type of your push notification (Announcement, polls etc).</span><span class="sxs-lookup"><span data-stu-id="c09a7-110">Select the type of your push notification (Announcement, polls etc).</span></span> <span data-ttu-id="c09a7-111">For this example we choose an announcement push.</span><span class="sxs-lookup"><span data-stu-id="c09a7-111">For this example we choose an announcement push.</span></span>
5. <span data-ttu-id="c09a7-112">Specify the different fields of the notification until you reach the text of the notification.</span><span class="sxs-lookup"><span data-stu-id="c09a7-112">Specify the different fields of the notification until you reach the text of the notification.</span></span> <span data-ttu-id="c09a7-113">This is where you will add your Emoji Emoticon.</span><span class="sxs-lookup"><span data-stu-id="c09a7-113">This is where you will add your Emoji Emoticon.</span></span> <span data-ttu-id="c09a7-114">You can choose to put it in the title, the message, or both.</span><span class="sxs-lookup"><span data-stu-id="c09a7-114">You can choose to put it in the title, the message, or both.</span></span> <span data-ttu-id="c09a7-115">You will need to drag and drop or copy the Emoji that you find from the locations above.</span><span class="sxs-lookup"><span data-stu-id="c09a7-115">You will need to drag and drop or copy the Emoji that you find from the locations above.</span></span> 
   
    ![][1]
6. <span data-ttu-id="c09a7-116">Complete the other fields for the notification and save it.</span><span class="sxs-lookup"><span data-stu-id="c09a7-116">Complete the other fields for the notification and save it.</span></span> 
7. <span data-ttu-id="c09a7-117">When you run a test or activate the announcement you will see a notification with the emoticon as specified.</span><span class="sxs-lookup"><span data-stu-id="c09a7-117">When you run a test or activate the announcement you will see a notification with the emoticon as specified.</span></span>   
   
    <span data-ttu-id="c09a7-118">![][3] ![][4] ![][5]</span><span class="sxs-lookup"><span data-stu-id="c09a7-118">![][3] ![][4] ![][5]</span></span>

<!-- Images. -->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-use-emoji-with-push/notification_input.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-use-emoji-with-push/iOS_Emoji.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-use-emoji-with-push/Android_Emoji.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-use-emoji-with-push/WindowsPhone_Emoji.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-use-emoji-with-push/Mac_SelectEmoji.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-use-emoji-with-push/Windows_SelectEmoji.png







