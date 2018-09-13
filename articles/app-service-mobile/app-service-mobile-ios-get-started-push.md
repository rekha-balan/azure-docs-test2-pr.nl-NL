---
title: Add Push Notifications to iOS App with Azure Mobile Apps
description: Learn how to use Azure Mobile Apps to send push notifications to your iOS app.
services: app-service\mobile
documentationcenter: ios
manager: yochayk
editor: ''
author: ysxu
ms.assetid: fa503833-d23e-4925-8d93-341bb3fbab7d
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/10/2016
ms.author: yuaxu
ms.openlocfilehash: a21ae4b13479f66ada053153834a2b3cc5687e5a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550624"
---
# <a name="add-push-notifications-to-your-ios-app"></a><span data-ttu-id="4044a-103">Add Push Notifications to your iOS App</span><span class="sxs-lookup"><span data-stu-id="4044a-103">Add Push Notifications to your iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="4044a-104">Overview</span><span class="sxs-lookup"><span data-stu-id="4044a-104">Overview</span></span>
<span data-ttu-id="4044a-105">In this tutorial, you add push notifications to the [iOS quick start] project so that a push notification is sent to the device every time a record is inserted.</span><span class="sxs-lookup"><span data-stu-id="4044a-105">In this tutorial, you add push notifications to the [iOS quick start] project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="4044a-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span><span class="sxs-lookup"><span data-stu-id="4044a-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="4044a-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="4044a-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

<span data-ttu-id="4044a-108">The [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span><span class="sxs-lookup"><span data-stu-id="4044a-108">The [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span></span> <span data-ttu-id="4044a-109">You need a physical iOS device and an [Apple Developer Program membership](https://developer.apple.com/programs/ios/).</span><span class="sxs-lookup"><span data-stu-id="4044a-109">You need a physical iOS device and an [Apple Developer Program membership](https://developer.apple.com/programs/ios/).</span></span>

## <a name="configure-hub"></a><span data-ttu-id="4044a-110">Configure Notification Hub</span><span class="sxs-lookup"><span data-stu-id="4044a-110">Configure Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a id="register"></a><span data-ttu-id="4044a-111">Register app for push notifications</span><span class="sxs-lookup"><span data-stu-id="4044a-111">Register app for push notifications</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-azure-to-send-push-notifications"></a><span data-ttu-id="4044a-112">Configure Azure to send push notifications</span><span class="sxs-lookup"><span data-stu-id="4044a-112">Configure Azure to send push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a id="update-server"></a><span data-ttu-id="4044a-113">Update backend to send push notifications</span><span class="sxs-lookup"><span data-stu-id="4044a-113">Update backend to send push notifications</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-apns](../../includes/app-service-mobile-dotnet-backend-configure-push-apns.md)]

## <a id="add-push"></a><span data-ttu-id="4044a-114">Add push notifications to app</span><span class="sxs-lookup"><span data-stu-id="4044a-114">Add push notifications to app</span></span>
[!INCLUDE [app-service-mobile-add-push-notifications-to-ios-app.md](../../includes/app-service-mobile-add-push-notifications-to-ios-app.md)]

## <a id="test"></a><span data-ttu-id="4044a-115">Test push notifications</span><span class="sxs-lookup"><span data-stu-id="4044a-115">Test push notifications</span></span>
[!INCLUDE [Test Push Notifications in App](../../includes/test-push-notifications-in-app.md)]

## <a id="more"></a><span data-ttu-id="4044a-116">More</span><span class="sxs-lookup"><span data-stu-id="4044a-116">More</span></span>
* <span data-ttu-id="4044a-117">Templates give you flexibility to send cross-platform pushes and localized pushes.</span><span class="sxs-lookup"><span data-stu-id="4044a-117">Templates give you flexibility to send cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="4044a-118">[How to Use iOS Client Library for Azure Mobile Apps](app-service-mobile-ios-how-to-use-client-library.md#templates) shows you how to register templates.</span><span class="sxs-lookup"><span data-stu-id="4044a-118">[How to Use iOS Client Library for Azure Mobile Apps](app-service-mobile-ios-how-to-use-client-library.md#templates) shows you how to register templates.</span></span>

<!-- Anchors.  -->

<!-- Images. -->

<!-- URLs. -->
[iOS quick start]: app-service-mobile-ios-get-started.md
