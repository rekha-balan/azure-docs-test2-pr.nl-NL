---
title: Get Started with Azure Mobile Apps for Xamarin.Android apps
description: Follow this tutorial to get started using Azure Mobile Apps for Xamarin Android development
services: app-service\mobile
documentationcenter: xamarin
author: adrianhall
manager: adrianha
editor: ''
ms.assetid: 81649dd3-544f-40ff-b9b7-60c66d683e60
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: adrianha
ms.openlocfilehash: 3af6dbca1d05ce4cc8d0db18e70756b0643f7936
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670918"
---
# <a name="create-a-xamarinandroid-app"></a><span data-ttu-id="331b9-103">Create a Xamarin.Android App</span><span class="sxs-lookup"><span data-stu-id="331b9-103">Create a Xamarin.Android App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="331b9-104">Overview</span><span class="sxs-lookup"><span data-stu-id="331b9-104">Overview</span></span>
<span data-ttu-id="331b9-105">This tutorial shows you how to add a cloud-based backend service to a Xamarin.Android app.</span><span class="sxs-lookup"><span data-stu-id="331b9-105">This tutorial shows you how to add a cloud-based backend service to a Xamarin.Android app.</span></span> <span data-ttu-id="331b9-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span><span class="sxs-lookup"><span data-stu-id="331b9-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span></span>

<span data-ttu-id="331b9-107">A screenshot from the completed app is below:</span><span class="sxs-lookup"><span data-stu-id="331b9-107">A screenshot from the completed app is below:</span></span>

![][0]

<span data-ttu-id="331b9-108">Completing this tutorial is a prerequisite for all other Mobile Apps tutorials for Xamarin.Android apps.</span><span class="sxs-lookup"><span data-stu-id="331b9-108">Completing this tutorial is a prerequisite for all other Mobile Apps tutorials for Xamarin.Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="331b9-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="331b9-109">Prerequisites</span></span>
<span data-ttu-id="331b9-110">To complete this tutorial, you need the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="331b9-110">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="331b9-111">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="331b9-111">An active Azure account.</span></span> <span data-ttu-id="331b9-112">If you don't have an account, sign up for an Azure trial and get up to 10 free Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="331b9-112">If you don't have an account, sign up for an Azure trial and get up to 10 free Mobile Apps.</span></span> <span data-ttu-id="331b9-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="331b9-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="331b9-114">Visual Studio with Xamarin.</span><span class="sxs-lookup"><span data-stu-id="331b9-114">Visual Studio with Xamarin.</span></span> <span data-ttu-id="331b9-115">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span><span class="sxs-lookup"><span data-stu-id="331b9-115">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span></span>

> [!NOTE]
> <span data-ttu-id="331b9-116">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/mobile/).</span><span class="sxs-lookup"><span data-stu-id="331b9-116">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/mobile/).</span></span>  <span data-ttu-id="331b9-117">You can immediately create a short-lived starter Mobile App in App Service.</span><span class="sxs-lookup"><span data-stu-id="331b9-117">You can immediately create a short-lived starter Mobile App in App Service.</span></span> <span data-ttu-id="331b9-118">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="331b9-118">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="331b9-119">Create an Azure Mobile App backend</span><span class="sxs-lookup"><span data-stu-id="331b9-119">Create an Azure Mobile App backend</span></span>
<span data-ttu-id="331b9-120">Follow these steps to create a Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="331b9-120">Follow these steps to create a Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="331b9-121">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span><span class="sxs-lookup"><span data-stu-id="331b9-121">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="331b9-122">Next, download a server project for a simple "todo list" backend and publish it to Azure.</span><span class="sxs-lookup"><span data-stu-id="331b9-122">Next, download a server project for a simple "todo list" backend and publish it to Azure.</span></span>

## <a name="configure-the-server-project"></a><span data-ttu-id="331b9-123">Configure the server project</span><span class="sxs-lookup"><span data-stu-id="331b9-123">Configure the server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-xamarinandroid-app"></a><span data-ttu-id="331b9-124">Download and run the Xamarin.Android app</span><span class="sxs-lookup"><span data-stu-id="331b9-124">Download and run the Xamarin.Android app</span></span>
1. <span data-ttu-id="331b9-125">Under **Download and run your Xamarin.Android project**, click the **Download** button.</span><span class="sxs-lookup"><span data-stu-id="331b9-125">Under **Download and run your Xamarin.Android project**, click the **Download** button.</span></span>
   
      <span data-ttu-id="331b9-126">Save the compressed project file to your local computer, and make a note of where you save it.</span><span class="sxs-lookup"><span data-stu-id="331b9-126">Save the compressed project file to your local computer, and make a note of where you save it.</span></span>
2. <span data-ttu-id="331b9-127">Press the **F5** key to build the project and start the app.</span><span class="sxs-lookup"><span data-stu-id="331b9-127">Press the **F5** key to build the project and start the app.</span></span>
3. <span data-ttu-id="331b9-128">In the app, type meaningful text, such as *Complete the tutorial* and then click the **Add** button.</span><span class="sxs-lookup"><span data-stu-id="331b9-128">In the app, type meaningful text, such as *Complete the tutorial* and then click the **Add** button.</span></span>
   
    ![][10]
   
    <span data-ttu-id="331b9-129">Data from the request is inserted into the TodoItem table.</span><span class="sxs-lookup"><span data-stu-id="331b9-129">Data from the request is inserted into the TodoItem table.</span></span> <span data-ttu-id="331b9-130">Items stored in the table are returned by the mobile app backend, and the data appears in the list.</span><span class="sxs-lookup"><span data-stu-id="331b9-130">Items stored in the table are returned by the mobile app backend, and the data appears in the list.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="331b9-131">You can review the code that accesses your mobile app backend to query and insert data, which is found in the ToDoActivity.cs C# file.</span><span class="sxs-lookup"><span data-stu-id="331b9-131">You can review the code that accesses your mobile app backend to query and insert data, which is found in the ToDoActivity.cs C# file.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="331b9-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="331b9-132">Next steps</span></span>
* [<span data-ttu-id="331b9-133">Add Offline Sync to your app</span><span class="sxs-lookup"><span data-stu-id="331b9-133">Add Offline Sync to your app</span></span>](app-service-mobile-xamarin-android-get-started-offline-data.md)
* [<span data-ttu-id="331b9-134">Add authentication to your app </span><span class="sxs-lookup"><span data-stu-id="331b9-134">Add authentication to your app </span></span>](app-service-mobile-xamarin-android-get-started-users.md)
* [<span data-ttu-id="331b9-135">Add push notifications to your Xamarin.Android app</span><span class="sxs-lookup"><span data-stu-id="331b9-135">Add push notifications to your Xamarin.Android app</span></span>](app-service-mobile-xamarin-android-get-started-push.md)
* [<span data-ttu-id="331b9-136">How to use the managed client for Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="331b9-136">How to use the managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Images. -->
[0]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-completed-android.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-xamarin-android-get-started/mobile-portal-quickstart-xamarin.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-vs.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-xs.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-startup-android.png

<!-- URLs. -->
[Azure Portal]: https://azure.portal.com/
[Visual Studio]: https://go.microsoft.com/fwLink/p/?LinkID=534203





