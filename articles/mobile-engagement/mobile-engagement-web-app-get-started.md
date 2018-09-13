---
title: Get started with Azure Mobile Engagement for Web Apps | Microsoft Docs
description: Learn how to use Azure Mobile Engagement with analytics and push notifications for Web Apps.
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 04afe53a-4caf-4c80-bd75-20cc630cd75c
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: js
ms.topic: hero-article
ms.date: 06/01/2016
ms.author: piyushjo
ms.openlocfilehash: 54585d88da2893cabc8bfd3172410ed89465a36d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552432"
---
# <a name="get-started-with-azure-mobile-engagement-for-web-apps"></a><span data-ttu-id="6340e-103">Get started with Azure Mobile Engagement for Web Apps</span><span class="sxs-lookup"><span data-stu-id="6340e-103">Get started with Azure Mobile Engagement for Web Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="6340e-104">This topic shows you how to use Azure Mobile Engagement to understand your Web App usage.</span><span class="sxs-lookup"><span data-stu-id="6340e-104">This topic shows you how to use Azure Mobile Engagement to understand your Web App usage.</span></span>

<span data-ttu-id="6340e-105">This tutorial requires the following:</span><span class="sxs-lookup"><span data-stu-id="6340e-105">This tutorial requires the following:</span></span>

* <span data-ttu-id="6340e-106">Visual Studio 2015 or any other editor of your choice</span><span class="sxs-lookup"><span data-stu-id="6340e-106">Visual Studio 2015 or any other editor of your choice</span></span>
* [<span data-ttu-id="6340e-107">Web SDK</span><span class="sxs-lookup"><span data-stu-id="6340e-107">Web SDK</span></span>](http://aka.ms/P7b453) 

<span data-ttu-id="6340e-108">This Web SDK is in Preview and only supports Analytics at the moment and doesn't support sending browser or in-app push notifications yet.</span><span class="sxs-lookup"><span data-stu-id="6340e-108">This Web SDK is in Preview and only supports Analytics at the moment and doesn't support sending browser or in-app push notifications yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="6340e-109">To complete this tutorial, you must have an active Azure account.</span><span class="sxs-lookup"><span data-stu-id="6340e-109">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="6340e-110">If you don't have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="6340e-110">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="6340e-111">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started).</span><span class="sxs-lookup"><span data-stu-id="6340e-111">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started).</span></span>
> 
> 

## <a name="setup-mobile-engagement-for-your-web-app"></a><span data-ttu-id="6340e-112">Setup Mobile Engagement for your Web app</span><span class="sxs-lookup"><span data-stu-id="6340e-112">Setup Mobile Engagement for your Web app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a><span data-ttu-id="6340e-113">Connect your app to the Mobile Engagement backend</span><span class="sxs-lookup"><span data-stu-id="6340e-113">Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="6340e-114">This tutorial presents a "basic integration," which is the minimal set required to collect data.</span><span class="sxs-lookup"><span data-stu-id="6340e-114">This tutorial presents a "basic integration," which is the minimal set required to collect data.</span></span>

<span data-ttu-id="6340e-115">We will create a basic web app with Visual Studio to demonstrate the integration though you can follow the steps with any web application created outside of Visual Studio also.</span><span class="sxs-lookup"><span data-stu-id="6340e-115">We will create a basic web app with Visual Studio to demonstrate the integration though you can follow the steps with any web application created outside of Visual Studio also.</span></span> 

### <a name="create-a-new-web-app"></a><span data-ttu-id="6340e-116">Create a new Web App</span><span class="sxs-lookup"><span data-stu-id="6340e-116">Create a new Web App</span></span>
<span data-ttu-id="6340e-117">The following steps assume the use of Visual Studio 2015 though the steps are similar in earlier versions of Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6340e-117">The following steps assume the use of Visual Studio 2015 though the steps are similar in earlier versions of Visual Studio.</span></span> 

1. <span data-ttu-id="6340e-118">Start Visual Studio, and in the **Home** screen, select **New Project**.</span><span class="sxs-lookup"><span data-stu-id="6340e-118">Start Visual Studio, and in the **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="6340e-119">In the pop-up, select **Web** -> **ASP.Net Web Application**.</span><span class="sxs-lookup"><span data-stu-id="6340e-119">In the pop-up, select **Web** -> **ASP.Net Web Application**.</span></span> <span data-ttu-id="6340e-120">Fill in the app **Name**, **Location** and  **Solution name**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="6340e-120">Fill in the app **Name**, **Location** and  **Solution name**, and then click **OK**.</span></span>
3. <span data-ttu-id="6340e-121">In the **Select a template** popup, select **Empty** under **ASP.Net 4.5 Templates** and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="6340e-121">In the **Select a template** popup, select **Empty** under **ASP.Net 4.5 Templates** and click **OK**.</span></span> 

<span data-ttu-id="6340e-122">You have now created a new blank Web App project into which we will integrate the Azure Mobile Engagement Web SDK.</span><span class="sxs-lookup"><span data-stu-id="6340e-122">You have now created a new blank Web App project into which we will integrate the Azure Mobile Engagement Web SDK.</span></span>

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="6340e-123">Connect your app to Mobile Engagement backend</span><span class="sxs-lookup"><span data-stu-id="6340e-123">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="6340e-124">Create a new folder called **javascript** in your solution and add the Web SDK JS file **azure-engagement.js** into it.</span><span class="sxs-lookup"><span data-stu-id="6340e-124">Create a new folder called **javascript** in your solution and add the Web SDK JS file **azure-engagement.js** into it.</span></span> 
2. <span data-ttu-id="6340e-125">Add a new file called **main.js** in this javascript folder with the following code.</span><span class="sxs-lookup"><span data-stu-id="6340e-125">Add a new file called **main.js** in this javascript folder with the following code.</span></span> <span data-ttu-id="6340e-126">Make sure to update the connection string.</span><span class="sxs-lookup"><span data-stu-id="6340e-126">Make sure to update the connection string.</span></span> <span data-ttu-id="6340e-127">This `azureEngagement` object will be used to access Web SDK methods.</span><span class="sxs-lookup"><span data-stu-id="6340e-127">This `azureEngagement` object will be used to access Web SDK methods.</span></span> 
   
        var azureEngagement = {
            debug: true,
            connectionString: 'xxxxx'
        };
   
    ![Visual Studio with js files][1]

## <a name="enable-real-time-monitoring"></a><span data-ttu-id="6340e-129">Enable real-time monitoring</span><span class="sxs-lookup"><span data-stu-id="6340e-129">Enable real-time monitoring</span></span>
<span data-ttu-id="6340e-130">In order to start sending data and ensuring that the users are active, you must send at least one Activity to the Mobile Engagement backend.</span><span class="sxs-lookup"><span data-stu-id="6340e-130">In order to start sending data and ensuring that the users are active, you must send at least one Activity to the Mobile Engagement backend.</span></span> <span data-ttu-id="6340e-131">An activity in the context of a web app is a web page.</span><span class="sxs-lookup"><span data-stu-id="6340e-131">An activity in the context of a web app is a web page.</span></span> 

1. <span data-ttu-id="6340e-132">Create a new page called **home.html** in your solution and set it as the starting page for your web app.</span><span class="sxs-lookup"><span data-stu-id="6340e-132">Create a new page called **home.html** in your solution and set it as the starting page for your web app.</span></span> 
2. <span data-ttu-id="6340e-133">Include the two javascripts we added earlier in this page by adding the following within the body tag.</span><span class="sxs-lookup"><span data-stu-id="6340e-133">Include the two javascripts we added earlier in this page by adding the following within the body tag.</span></span> 
   
        <script type="text/javascript" src="javascript/main.js"></script>
        <script type="text/javascript" src="javascript/azure-engagement.js"></script>
3. <span data-ttu-id="6340e-134">Update the body tag to call EngagementAgent's `startActivity` method</span><span class="sxs-lookup"><span data-stu-id="6340e-134">Update the body tag to call EngagementAgent's `startActivity` method</span></span>
   
        <body onload="engagement.agent.startActivity('Home')">
4. <span data-ttu-id="6340e-135">Here is what your **home.html** will look like</span><span class="sxs-lookup"><span data-stu-id="6340e-135">Here is what your **home.html** will look like</span></span>
   
        <html>
        <head>
            ...
        </head>
        <body onload="engagement.agent.startActivity('Home')">
            <script type="text/javascript" src="javascript/main.js"></script>
            <script type="text/javascript" src="javascript/azure-engagement.js"></script>
        </body>
        </html>

## <a name="connect-app-with-real-time-monitoring"></a><span data-ttu-id="6340e-136">Connect app with real-time monitoring</span><span class="sxs-lookup"><span data-stu-id="6340e-136">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

  ![][2]

## <a name="extend-analytics"></a><span data-ttu-id="6340e-137">Extend analytics</span><span class="sxs-lookup"><span data-stu-id="6340e-137">Extend analytics</span></span>
<span data-ttu-id="6340e-138">Here are all the methods currently available with Web SDK that you can use for analytics:</span><span class="sxs-lookup"><span data-stu-id="6340e-138">Here are all the methods currently available with Web SDK that you can use for analytics:</span></span>

1. <span data-ttu-id="6340e-139">Activities/Web pages:</span><span class="sxs-lookup"><span data-stu-id="6340e-139">Activities/Web pages:</span></span>
   
        engagement.agent.startActivity(name);
        engagement.agent.endActivity();
2. <span data-ttu-id="6340e-140">Events</span><span class="sxs-lookup"><span data-stu-id="6340e-140">Events</span></span>
   
        engagement.agent.sendEvent(name, extras);
3. <span data-ttu-id="6340e-141">Errors</span><span class="sxs-lookup"><span data-stu-id="6340e-141">Errors</span></span>
   
        engagement.agent.sendError(name, extras);
4. <span data-ttu-id="6340e-142">Jobs</span><span class="sxs-lookup"><span data-stu-id="6340e-142">Jobs</span></span>
   
        engagement.agent.startJob(name);
        engagement.agent.endJob(name);

<!-- Images. -->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-web-app-get-started/visual-studio-solution-js.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-web-app-get-started/session.png



