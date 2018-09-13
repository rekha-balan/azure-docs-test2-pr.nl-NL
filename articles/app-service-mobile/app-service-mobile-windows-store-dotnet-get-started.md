---
title: Create a Universal Windows Platform (UWP) that uses on Mobile Apps | Microsoft Docs
description: Follow this tutorial to get started with using Azure mobile app backends for Universal Windows Platform (UWP) app development in C#, Visual Basic, or JavaScript.
services: app-service\mobile
documentationcenter: windows
author: adrianhall
manager: adrianha
editor: ''
ms.assetid: 47124296-2908-4d92-85e0-05c4aa6db916
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: adrianha
ms.openlocfilehash: 214fa66240944d60184a14ccf858ef383e08b9b7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549455"
---
# <a name="create-a-windows-app"></a><span data-ttu-id="5afe2-103">Create a Windows app</span><span class="sxs-lookup"><span data-stu-id="5afe2-103">Create a Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="5afe2-104">Overview</span><span class="sxs-lookup"><span data-stu-id="5afe2-104">Overview</span></span>
<span data-ttu-id="5afe2-105">This tutorial shows you how to add a cloud-based backend service to a Universal Windows Platform (UWP) app.</span><span class="sxs-lookup"><span data-stu-id="5afe2-105">This tutorial shows you how to add a cloud-based backend service to a Universal Windows Platform (UWP) app.</span></span> <span data-ttu-id="5afe2-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span><span class="sxs-lookup"><span data-stu-id="5afe2-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span></span> <span data-ttu-id="5afe2-107">The following are screen captures from the completed app:</span><span class="sxs-lookup"><span data-stu-id="5afe2-107">The following are screen captures from the completed app:</span></span>

![Completed desktop app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed-desktop.png)   
<span data-ttu-id="5afe2-109">Running on a desktop.</span><span class="sxs-lookup"><span data-stu-id="5afe2-109">Running on a desktop.</span></span> 

![Completed phone app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)  
<span data-ttu-id="5afe2-111">Running on a phone</span><span class="sxs-lookup"><span data-stu-id="5afe2-111">Running on a phone</span></span>

<span data-ttu-id="5afe2-112">Completing this tutorial is a prerequisite for all other Mobile App tutorials for UWP apps.</span><span class="sxs-lookup"><span data-stu-id="5afe2-112">Completing this tutorial is a prerequisite for all other Mobile App tutorials for UWP apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5afe2-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5afe2-113">Prerequisites</span></span>
<span data-ttu-id="5afe2-114">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="5afe2-114">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="5afe2-115">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="5afe2-115">An active Azure account.</span></span> <span data-ttu-id="5afe2-116">If you don't have an account, you can sign up for an Azure trial and get up to 10 free mobile apps that you can keep using even after your trial ends.</span><span class="sxs-lookup"><span data-stu-id="5afe2-116">If you don't have an account, you can sign up for an Azure trial and get up to 10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="5afe2-117">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5afe2-117">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="5afe2-118">[Visual Studio Community 2015] or a later version.</span><span class="sxs-lookup"><span data-stu-id="5afe2-118">[Visual Studio Community 2015] or a later version.</span></span>

> [!NOTE]
> <span data-ttu-id="5afe2-119">If you want to get started with Azure App Service before you sign up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/mobile/).</span><span class="sxs-lookup"><span data-stu-id="5afe2-119">If you want to get started with Azure App Service before you sign up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/mobile/).</span></span> <span data-ttu-id="5afe2-120">There, you can immediately create a short-lived starter mobile app in App Service—no credit card required, and no commitments.</span><span class="sxs-lookup"><span data-stu-id="5afe2-120">There, you can immediately create a short-lived starter mobile app in App Service—no credit card required, and no commitments.</span></span>
> 
> 

## <a name="create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="5afe2-121">Create a new Azure Mobile App backend</span><span class="sxs-lookup"><span data-stu-id="5afe2-121">Create a new Azure Mobile App backend</span></span>
<span data-ttu-id="5afe2-122">Follow these steps to create a new Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="5afe2-122">Follow these steps to create a new Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="5afe2-123">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span><span class="sxs-lookup"><span data-stu-id="5afe2-123">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="5afe2-124">Next, you will download a server project for a simple "todo list" backend and publish it to Azure.</span><span class="sxs-lookup"><span data-stu-id="5afe2-124">Next, you will download a server project for a simple "todo list" backend and publish it to Azure.</span></span>

## <a name="configure-the-server-project"></a><span data-ttu-id="5afe2-125">Configure the server project</span><span class="sxs-lookup"><span data-stu-id="5afe2-125">Configure the server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-client-project"></a><span data-ttu-id="5afe2-126">Download and run the client project</span><span class="sxs-lookup"><span data-stu-id="5afe2-126">Download and run the client project</span></span>
<span data-ttu-id="5afe2-127">Once you have configured your Mobile App backend, you can either create a new client app or modify an existing app to connect to Azure.</span><span class="sxs-lookup"><span data-stu-id="5afe2-127">Once you have configured your Mobile App backend, you can either create a new client app or modify an existing app to connect to Azure.</span></span> <span data-ttu-id="5afe2-128">In this section, you download a UWP app template project that is customized to connect to your Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="5afe2-128">In this section, you download a UWP app template project that is customized to connect to your Mobile App backend.</span></span>

1. <span data-ttu-id="5afe2-129">Back in the **Quick start** blade for your Mobile App backend, click **Create a new app** > **Download**, then extract the compressed project files to your local computer.</span><span class="sxs-lookup"><span data-stu-id="5afe2-129">Back in the **Quick start** blade for your Mobile App backend, click **Create a new app** > **Download**, then extract the compressed project files to your local computer.</span></span>
   
    ![Download Windows quickstart project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-windows-store-dotnet-get-started/mobile-app-windows-quickstart.png)
2. <span data-ttu-id="5afe2-131">(Optional) Add the UWP app project to the same solution as the server project.</span><span class="sxs-lookup"><span data-stu-id="5afe2-131">(Optional) Add the UWP app project to the same solution as the server project.</span></span> <span data-ttu-id="5afe2-132">This makes it easier to debug and test both the app and the backend in the same Visual Studio solution, if you choose to do so.</span><span class="sxs-lookup"><span data-stu-id="5afe2-132">This makes it easier to debug and test both the app and the backend in the same Visual Studio solution, if you choose to do so.</span></span> <span data-ttu-id="5afe2-133">To add a UWP app project to the solution, you must be using Visual Studio 2015 or a later version.</span><span class="sxs-lookup"><span data-stu-id="5afe2-133">To add a UWP app project to the solution, you must be using Visual Studio 2015 or a later version.</span></span>
3. <span data-ttu-id="5afe2-134">With the UWP app as the startup project, press the F5 key to deploy and run the app.</span><span class="sxs-lookup"><span data-stu-id="5afe2-134">With the UWP app as the startup project, press the F5 key to deploy and run the app.</span></span>
4. <span data-ttu-id="5afe2-135">In the app, type meaningful text, such as *Complete the tutorial*, in the **Insert a TodoItem** text box, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="5afe2-135">In the app, type meaningful text, such as *Complete the tutorial*, in the **Insert a TodoItem** text box, and then click **Save**.</span></span>
   
    ![Windows quickstart complete desktop](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-startup.png)
   
    <span data-ttu-id="5afe2-137">This sends a POST request to the new mobile app backend that's hosted in Azure.</span><span class="sxs-lookup"><span data-stu-id="5afe2-137">This sends a POST request to the new mobile app backend that's hosted in Azure.</span></span>
5. <span data-ttu-id="5afe2-138">(Optional) Stop the app and restart it on a different device or mobile emulator.</span><span class="sxs-lookup"><span data-stu-id="5afe2-138">(Optional) Stop the app and restart it on a different device or mobile emulator.</span></span>
   
    ![Windows quickstart complete phone](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)
   
    <span data-ttu-id="5afe2-140">Notice that data saved from the previous step is loaded from Azure after the UWP app starts.</span><span class="sxs-lookup"><span data-stu-id="5afe2-140">Notice that data saved from the previous step is loaded from Azure after the UWP app starts.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5afe2-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="5afe2-141">Next steps</span></span>
* [<span data-ttu-id="5afe2-142">Add authentication to your app</span><span class="sxs-lookup"><span data-stu-id="5afe2-142">Add authentication to your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  <span data-ttu-id="5afe2-143">Learn how to authenticate users of your app with an identity provider.</span><span class="sxs-lookup"><span data-stu-id="5afe2-143">Learn how to authenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="5afe2-144">Add push notifications to your app</span><span class="sxs-lookup"><span data-stu-id="5afe2-144">Add push notifications to your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="5afe2-145">Learn how to add push notifications support to your app and configure your Mobile App backend to use Azure Notification Hubs to send push notifications.</span><span class="sxs-lookup"><span data-stu-id="5afe2-145">Learn how to add push notifications support to your app and configure your Mobile App backend to use Azure Notification Hubs to send push notifications.</span></span>
* [<span data-ttu-id="5afe2-146">Enable offline sync for your app</span><span class="sxs-lookup"><span data-stu-id="5afe2-146">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="5afe2-147">Learn how to add offline support your app using an Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="5afe2-147">Learn how to add offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="5afe2-148">Offline sync allows end-users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span><span class="sxs-lookup"><span data-stu-id="5afe2-148">Offline sync allows end-users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->
<!-- Images. -->
<!-- URLs. -->
[Mobile App SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2015]: https://go.microsoft.com/fwLink/p/?LinkID=534203





