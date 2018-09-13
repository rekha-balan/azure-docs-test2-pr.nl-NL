---
title: Create a Cordova app on Azure App Service Mobile Apps | Microsoft Docs
description: Follow this tutorial to get started with using Azure mobile app backends for Apache Cordova development
services: app-service\mobile
documentationcenter: javascript
author: adrianhall
manager: adrianha
editor: ''
tags: ''
keywords: cordova,javascript,mobile,client
ms.assetid: 0b08fc12-0a80-42d3-9cc1-9b3f8d3e3a3f
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: hero-article
ms.date: 10/30/2016
ms.author: adrianha
ms.openlocfilehash: 7c0595aa0cee46a2af5d901f4652fcd862521aca
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550635"
---
# <a name="create-an-apache-cordova-app"></a><span data-ttu-id="a5858-104">Create an Apache Cordova app</span><span class="sxs-lookup"><span data-stu-id="a5858-104">Create an Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="a5858-105">Overview</span><span class="sxs-lookup"><span data-stu-id="a5858-105">Overview</span></span>
<span data-ttu-id="a5858-106">This tutorial shows you how to add a cloud-based backend service to an Apache Cordova mobile app by using an Azure mobile app backend.</span><span class="sxs-lookup"><span data-stu-id="a5858-106">This tutorial shows you how to add a cloud-based backend service to an Apache Cordova mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="a5858-107">You create both a new mobile app backend and a simple *Todo list* Apache Cordova app that stores app data in Azure.</span><span class="sxs-lookup"><span data-stu-id="a5858-107">You create both a new mobile app backend and a simple *Todo list* Apache Cordova app that stores app data in Azure.</span></span>

<span data-ttu-id="a5858-108">Completing this tutorial is a prerequisite for all other Apache Cordova tutorials about using the Mobile Apps feature in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="a5858-108">Completing this tutorial is a prerequisite for all other Apache Cordova tutorials about using the Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5858-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a5858-109">Prerequisites</span></span>
<span data-ttu-id="a5858-110">To complete this tutorial, you need the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="a5858-110">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="a5858-111">A PC with [Visual Studio Community 2015] or newer.</span><span class="sxs-lookup"><span data-stu-id="a5858-111">A PC with [Visual Studio Community 2015] or newer.</span></span>
* <span data-ttu-id="a5858-112">[Visual Studio Tools for Apache Cordova].</span><span class="sxs-lookup"><span data-stu-id="a5858-112">[Visual Studio Tools for Apache Cordova].</span></span>
* <span data-ttu-id="a5858-113">An [active Azure account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a5858-113">An [active Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="a5858-114">You may also bypass Visual Studio and use the Apache Cordova command line directly.</span><span class="sxs-lookup"><span data-stu-id="a5858-114">You may also bypass Visual Studio and use the Apache Cordova command line directly.</span></span>  <span data-ttu-id="a5858-115">Using the command line is useful when completing the tutorial on a Mac computer.</span><span class="sxs-lookup"><span data-stu-id="a5858-115">Using the command line is useful when completing the tutorial on a Mac computer.</span></span>  <span data-ttu-id="a5858-116">Compiling Apache Cordova client applications using the command line is not covered by this tutorial.</span><span class="sxs-lookup"><span data-stu-id="a5858-116">Compiling Apache Cordova client applications using the command line is not covered by this tutorial.</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="a5858-117">Create an Azure mobile app backend</span><span class="sxs-lookup"><span data-stu-id="a5858-117">Create an Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

[<span data-ttu-id="a5858-118">Watch a video showing similar steps</span><span class="sxs-lookup"><span data-stu-id="a5858-118">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-1-Create-an-Azure-Mobile-App)

## <a name="configure-the-server-project"></a><span data-ttu-id="a5858-119">Configure the server project</span><span class="sxs-lookup"><span data-stu-id="a5858-119">Configure the server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-apache-cordova-app"></a><span data-ttu-id="a5858-120">Download and run the Apache Cordova app</span><span class="sxs-lookup"><span data-stu-id="a5858-120">Download and run the Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-cordova-run-app](../../includes/app-service-mobile-cordova-run-app.md)]

## <a name="next-steps"></a><span data-ttu-id="a5858-121">Next Steps</span><span class="sxs-lookup"><span data-stu-id="a5858-121">Next Steps</span></span>
<span data-ttu-id="a5858-122">Now that you completed this quick start tutorial, move on to one of the following tutorials:</span><span class="sxs-lookup"><span data-stu-id="a5858-122">Now that you completed this quick start tutorial, move on to one of the following tutorials:</span></span>

* <span data-ttu-id="a5858-123">[Add Offline Data](app-service-mobile-cordova-get-started-offline-data.md) to your Apache Cordova app.</span><span class="sxs-lookup"><span data-stu-id="a5858-123">[Add Offline Data](app-service-mobile-cordova-get-started-offline-data.md) to your Apache Cordova app.</span></span>
* <span data-ttu-id="a5858-124">[Add Authentication](app-service-mobile-cordova-get-started-users.md) to your Apache Cordova app.</span><span class="sxs-lookup"><span data-stu-id="a5858-124">[Add Authentication](app-service-mobile-cordova-get-started-users.md) to your Apache Cordova app.</span></span>
* <span data-ttu-id="a5858-125">[Add Push Notifications](app-service-mobile-cordova-get-started-push.md) to your Apache Cordova app.</span><span class="sxs-lookup"><span data-stu-id="a5858-125">[Add Push Notifications](app-service-mobile-cordova-get-started-push.md) to your Apache Cordova app.</span></span>

<span data-ttu-id="a5858-126">Learn more about key concepts with Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="a5858-126">Learn more about key concepts with Azure App Service.</span></span>

* <span data-ttu-id="a5858-127">[Offline Data]</span><span class="sxs-lookup"><span data-stu-id="a5858-127">[Offline Data]</span></span>
* <span data-ttu-id="a5858-128">[Authentication]</span><span class="sxs-lookup"><span data-stu-id="a5858-128">[Authentication]</span></span>
* <span data-ttu-id="a5858-129">[Push Notifications]</span><span class="sxs-lookup"><span data-stu-id="a5858-129">[Push Notifications]</span></span>

<span data-ttu-id="a5858-130">Learn how to use the SDKs.</span><span class="sxs-lookup"><span data-stu-id="a5858-130">Learn how to use the SDKs.</span></span>

* <span data-ttu-id="a5858-131">[Apache Cordova SDK]</span><span class="sxs-lookup"><span data-stu-id="a5858-131">[Apache Cordova SDK]</span></span>
* <span data-ttu-id="a5858-132">[ASP.NET Server SDK]</span><span class="sxs-lookup"><span data-stu-id="a5858-132">[ASP.NET Server SDK]</span></span>
* <span data-ttu-id="a5858-133">[Node.js Server SDK]</span><span class="sxs-lookup"><span data-stu-id="a5858-133">[Node.js Server SDK]</span></span>

<!-- Images. -->

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2015]: http://www.visualstudio.com/
[Visual Studio Tools for Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[Offline Data]: app-service-mobile-offline-data-sync.md
[Authentication]: app-service-mobile-auth.md
[Push Notifications]: ../notification-hubs/notification-hubs-push-notification-overview.md
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
