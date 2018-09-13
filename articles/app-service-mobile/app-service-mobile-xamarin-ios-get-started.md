---
title: Get started with Azure App Service Mobile Apps for Xamarin.iOS apps | Microsoft Docs
description: Follow this tutorial to get started with using Mobile Apps for Xamarin.iOS development.
services: app-service\mobile
documentationcenter: xamarin
author: conceptdev
manager: crdun
editor: ''
ms.assetid: 14428794-52ad-4b51-956c-deb296cafa34
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: crdun
ms.openlocfilehash: 8b890630d352619da86c3017426e24f55ef016d9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44821098"
---
# <a name="create-a-xamarinios-app"></a><span data-ttu-id="bb99e-103">Create a Xamarin.iOS app</span><span class="sxs-lookup"><span data-stu-id="bb99e-103">Create a Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="bb99e-104">Overview</span><span class="sxs-lookup"><span data-stu-id="bb99e-104">Overview</span></span>
<span data-ttu-id="bb99e-105">This tutorial shows you how to add a cloud-based backend service to a Xamarin.iOS mobile app by using an Azure mobile app backend.</span><span class="sxs-lookup"><span data-stu-id="bb99e-105">This tutorial shows you how to add a cloud-based backend service to a Xamarin.iOS mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="bb99e-106">You create both a new mobile app backend and a simple *Todo list* Xamarin.iOS app that stores app data in Azure.</span><span class="sxs-lookup"><span data-stu-id="bb99e-106">You create both a new mobile app backend and a simple *Todo list* Xamarin.iOS app that stores app data in Azure.</span></span>

<span data-ttu-id="bb99e-107">Completing this tutorial is a prerequisite for all other Xamarin.iOS tutorials about using the Mobile Apps feature in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="bb99e-107">Completing this tutorial is a prerequisite for all other Xamarin.iOS tutorials about using the Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb99e-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bb99e-108">Prerequisites</span></span>
<span data-ttu-id="bb99e-109">To complete this tutorial, you need the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="bb99e-109">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="bb99e-110">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="bb99e-110">An active Azure account.</span></span> <span data-ttu-id="bb99e-111">If you don't have an account, sign up for an Azure trial and get up to 10 free mobile apps that you can keep using even after your trial ends.</span><span class="sxs-lookup"><span data-stu-id="bb99e-111">If you don't have an account, sign up for an Azure trial and get up to 10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="bb99e-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bb99e-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="bb99e-113">Visual Studio with Xamarin.</span><span class="sxs-lookup"><span data-stu-id="bb99e-113">Visual Studio with Xamarin.</span></span> <span data-ttu-id="bb99e-114">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span><span class="sxs-lookup"><span data-stu-id="bb99e-114">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span></span>
* <span data-ttu-id="bb99e-115">A Mac with Xcode v7.0 or later and Xamarin Studio Community installed.</span><span class="sxs-lookup"><span data-stu-id="bb99e-115">A Mac with Xcode v7.0 or later and Xamarin Studio Community installed.</span></span> <span data-ttu-id="bb99e-116">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) and [Setup, install, and verifications for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span><span class="sxs-lookup"><span data-stu-id="bb99e-116">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) and [Setup, install, and verifications for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="bb99e-117">Create an Azure Mobile App backend</span><span class="sxs-lookup"><span data-stu-id="bb99e-117">Create an Azure Mobile App backend</span></span>
<span data-ttu-id="bb99e-118">Follow these steps to create a Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="bb99e-118">Follow these steps to create a Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-the-server-project"></a><span data-ttu-id="bb99e-119">Configure the server project</span><span class="sxs-lookup"><span data-stu-id="bb99e-119">Configure the server project</span></span>
<span data-ttu-id="bb99e-120">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span><span class="sxs-lookup"><span data-stu-id="bb99e-120">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="bb99e-121">Next, download a server project for a simple "todo list" backend and publish it to Azure.</span><span class="sxs-lookup"><span data-stu-id="bb99e-121">Next, download a server project for a simple "todo list" backend and publish it to Azure.</span></span>

<span data-ttu-id="bb99e-122">Follow the following steps to configure the server project to use either the Node.js or .NET backend.</span><span class="sxs-lookup"><span data-stu-id="bb99e-122">Follow the following steps to configure the server project to use either the Node.js or .NET backend.</span></span>

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-xamarinios-app"></a><span data-ttu-id="bb99e-123">Download and run the Xamarin.iOS app</span><span class="sxs-lookup"><span data-stu-id="bb99e-123">Download and run the Xamarin.iOS app</span></span>
1. <span data-ttu-id="bb99e-124">Open the [Azure portal] in a browser window.</span><span class="sxs-lookup"><span data-stu-id="bb99e-124">Open the [Azure portal] in a browser window.</span></span>
2. <span data-ttu-id="bb99e-125">On the settings blade for your Mobile App, click **Get Started** > **Xamarin.iOS**.</span><span class="sxs-lookup"><span data-stu-id="bb99e-125">On the settings blade for your Mobile App, click **Get Started** > **Xamarin.iOS**.</span></span> <span data-ttu-id="bb99e-126">Under step 3, click **Create a new app** if it's not already selected.</span><span class="sxs-lookup"><span data-stu-id="bb99e-126">Under step 3, click **Create a new app** if it's not already selected.</span></span>  <span data-ttu-id="bb99e-127">Next click the **Download** button.</span><span class="sxs-lookup"><span data-stu-id="bb99e-127">Next click the **Download** button.</span></span>

      <span data-ttu-id="bb99e-128">A client application that connects to your mobile backend is downloaded.</span><span class="sxs-lookup"><span data-stu-id="bb99e-128">A client application that connects to your mobile backend is downloaded.</span></span> <span data-ttu-id="bb99e-129">Save the compressed project file to your local computer, and make a note of where you save it.</span><span class="sxs-lookup"><span data-stu-id="bb99e-129">Save the compressed project file to your local computer, and make a note of where you save it.</span></span>
3. <span data-ttu-id="bb99e-130">Extract the project that you downloaded, and then open it in Xamarin Studio (or Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="bb99e-130">Extract the project that you downloaded, and then open it in Xamarin Studio (or Visual Studio).</span></span>

    ![][9]

    ![][8]
4. <span data-ttu-id="bb99e-131">Press the F5 key to build the project and start the app in the iPhone emulator.</span><span class="sxs-lookup"><span data-stu-id="bb99e-131">Press the F5 key to build the project and start the app in the iPhone emulator.</span></span>
5. <span data-ttu-id="bb99e-132">In the app, type meaningful text, such as *Learn Xamarin*, and then click the **+** button.</span><span class="sxs-lookup"><span data-stu-id="bb99e-132">In the app, type meaningful text, such as *Learn Xamarin*, and then click the **+** button.</span></span>

    ![][10]

    <span data-ttu-id="bb99e-133">Data from the request is inserted into the TodoItem table.</span><span class="sxs-lookup"><span data-stu-id="bb99e-133">Data from the request is inserted into the TodoItem table.</span></span> <span data-ttu-id="bb99e-134">Items stored in the table are returned by the mobile app backend, and the data is displayed in the list.</span><span class="sxs-lookup"><span data-stu-id="bb99e-134">Items stored in the table are returned by the mobile app backend, and the data is displayed in the list.</span></span>

> [!NOTE]
> <span data-ttu-id="bb99e-135">You can review the code that accesses your mobile app backend to query and insert data in the QSTodoService.cs C# file.</span><span class="sxs-lookup"><span data-stu-id="bb99e-135">You can review the code that accesses your mobile app backend to query and insert data in the QSTodoService.cs C# file.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="bb99e-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="bb99e-136">Next steps</span></span>
* [<span data-ttu-id="bb99e-137">Add Offline Sync to your app</span><span class="sxs-lookup"><span data-stu-id="bb99e-137">Add Offline Sync to your app</span></span>](app-service-mobile-xamarin-ios-get-started-offline-data.md)
* [<span data-ttu-id="bb99e-138">Add authentication to your app </span><span class="sxs-lookup"><span data-stu-id="bb99e-138">Add authentication to your app </span></span>](app-service-mobile-xamarin-ios-get-started-users.md)
* [<span data-ttu-id="bb99e-139">Add push notifications to your Xamarin.Android app</span><span class="sxs-lookup"><span data-stu-id="bb99e-139">Add push notifications to your Xamarin.Android app</span></span>](app-service-mobile-xamarin-ios-get-started-push.md)
* [<span data-ttu-id="bb99e-140">How to use the managed client for Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="bb99e-140">How to use the managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Anchors. -->
[Getting started with mobile app backends]:#getting-started
[Create a new mobile app backend]:#create-new-service
[Next Steps]:#next-steps

<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-ios-get-started/xamarin-ios-quickstart.png
[8]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-vs.png
[9]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-xs.png
[10]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-quickstart-startup-ios.png

<!-- URLs. -->
[Azure portal]: https://portal.azure.com/
