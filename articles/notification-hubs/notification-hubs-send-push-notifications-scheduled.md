---
title: How to send scheduled notifications | Microsoft Docs
description: This topic describes using Scheduled Notifications with Azure Notification Hubs.
services: notification-hubs
documentationcenter: .net
keywords: push notifications,push notification,scheduling push notifications
author: ysxu
manager: erikre
editor: ''
ms.assetid: 6b718c75-75dd-4c99-aee3-db1288235c1a
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: efac6e1ecc00359f1622d380333140bc055c83e0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550178"
---
# <a name="how-to-send-scheduled-notifications"></a><span data-ttu-id="a459a-104">How To: Send scheduled notifications</span><span class="sxs-lookup"><span data-stu-id="a459a-104">How To: Send scheduled notifications</span></span>
## <a name="overview"></a><span data-ttu-id="a459a-105">Overview</span><span class="sxs-lookup"><span data-stu-id="a459a-105">Overview</span></span>
<span data-ttu-id="a459a-106">If you have a scenario in which you want to send a notification at some point in the future, but do not have an easy way to wake up your back-end code to send the notification.</span><span class="sxs-lookup"><span data-stu-id="a459a-106">If you have a scenario in which you want to send a notification at some point in the future, but do not have an easy way to wake up your back-end code to send the notification.</span></span> <span data-ttu-id="a459a-107">Standard tier Notification Hubs supports a feature that enables you to schedule notifications up to 7 days in the future.</span><span class="sxs-lookup"><span data-stu-id="a459a-107">Standard tier Notification Hubs supports a feature that enables you to schedule notifications up to 7 days in the future.</span></span>

<span data-ttu-id="a459a-108">When sending a notification, simply use the [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) class in the Notification Hubs SDK as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a459a-108">When sending a notification, simply use the [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) class in the Notification Hubs SDK as shown in the following example:</span></span>

    Notification notification = new AppleNotification("{\"aps\":{\"alert\":\"Happy birthday!\"}}");
    var scheduled = await hub.ScheduleNotificationAsync(notification, new DateTime(2014, 7, 19, 0, 0, 0));

<span data-ttu-id="a459a-109">Also, you can cancel a previously scheduled notification using its notificationId:</span><span class="sxs-lookup"><span data-stu-id="a459a-109">Also, you can cancel a previously scheduled notification using its notificationId:</span></span>

    await hub.CancelNotificationAsync(scheduled.ScheduledNotificationId);

<span data-ttu-id="a459a-110">There are no limits on the number of scheduled notifications you can send.</span><span class="sxs-lookup"><span data-stu-id="a459a-110">There are no limits on the number of scheduled notifications you can send.</span></span>

