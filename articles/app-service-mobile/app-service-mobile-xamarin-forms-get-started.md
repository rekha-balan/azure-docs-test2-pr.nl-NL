---
title: Get Started with Mobile Apps by using Xamarin.Forms
description: Follow this tutorial to get started using Azure Mobile Apps for Xamarin.Forms development
services: app-service\mobile
documentationcenter: xamarin
author: adrianhall
manager: adrianha
editor: ''
ms.assetid: 5e692220-cc89-4548-96c8-35259722acf5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: adrianha
ms.openlocfilehash: 733b51aad95843135afb02dfd27a836eba04bbf3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540804"
---
# <a name="create-a-xamarinforms-app"></a><span data-ttu-id="637c0-103">Create a Xamarin.Forms app</span><span class="sxs-lookup"><span data-stu-id="637c0-103">Create a Xamarin.Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="637c0-104">Overview</span><span class="sxs-lookup"><span data-stu-id="637c0-104">Overview</span></span>
<span data-ttu-id="637c0-105">This tutorial shows you how to add a cloud-based backend service to a Xamarin.Forms mobile app using an Azure Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="637c0-105">This tutorial shows you how to add a cloud-based backend service to a Xamarin.Forms mobile app using an Azure Mobile App backend.</span></span> <span data-ttu-id="637c0-106">You will create both a new Mobile App backend and a simple *Todo list* Xamarin.Forms app that stores app data in Azure.</span><span class="sxs-lookup"><span data-stu-id="637c0-106">You will create both a new Mobile App backend and a simple *Todo list* Xamarin.Forms app that stores app data in Azure.</span></span>

<span data-ttu-id="637c0-107">Completing this tutorial is a prerequisite for all other Mobile Apps tutorials for Xamarin.Forms.</span><span class="sxs-lookup"><span data-stu-id="637c0-107">Completing this tutorial is a prerequisite for all other Mobile Apps tutorials for Xamarin.Forms.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="637c0-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="637c0-108">Prerequisites</span></span>
<span data-ttu-id="637c0-109">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="637c0-109">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="637c0-110">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="637c0-110">An active Azure account.</span></span> <span data-ttu-id="637c0-111">If you don't have an account, you can sign up for an Azure trial and get up to 10 free Mobile Apps that you can keep using even after your trial ends.</span><span class="sxs-lookup"><span data-stu-id="637c0-111">If you don't have an account, you can sign up for an Azure trial and get up to 10 free Mobile Apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="637c0-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="637c0-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="637c0-113">Visual Studio with Xamarin.</span><span class="sxs-lookup"><span data-stu-id="637c0-113">Visual Studio with Xamarin.</span></span> <span data-ttu-id="637c0-114">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span><span class="sxs-lookup"><span data-stu-id="637c0-114">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span></span> 
* <span data-ttu-id="637c0-115">A Mac with Xcode v7.0 or later and Xamarin Studio Community installed.</span><span class="sxs-lookup"><span data-stu-id="637c0-115">A Mac with Xcode v7.0 or later and Xamarin Studio Community installed.</span></span> <span data-ttu-id="637c0-116">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) and [Setup, install, and verifications for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span><span class="sxs-lookup"><span data-stu-id="637c0-116">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) and [Setup, install, and verifications for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span></span>

> [!NOTE]
> <span data-ttu-id="637c0-117">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/mobile/), where you can immediately create a short-lived starter Mobile App in App Service.</span><span class="sxs-lookup"><span data-stu-id="637c0-117">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/mobile/), where you can immediately create a short-lived starter Mobile App in App Service.</span></span> <span data-ttu-id="637c0-118">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="637c0-118">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="637c0-119">Create a new Azure Mobile App backend</span><span class="sxs-lookup"><span data-stu-id="637c0-119">Create a new Azure Mobile App backend</span></span>
<span data-ttu-id="637c0-120">Follow these steps to create a new Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="637c0-120">Follow these steps to create a new Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="637c0-121">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span><span class="sxs-lookup"><span data-stu-id="637c0-121">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="637c0-122">Next, you will download a server project for a simple "todo list" backend and publish it to Azure.</span><span class="sxs-lookup"><span data-stu-id="637c0-122">Next, you will download a server project for a simple "todo list" backend and publish it to Azure.</span></span>

## <a name="configure-the-server-project"></a><span data-ttu-id="637c0-123">Configure the server project</span><span class="sxs-lookup"><span data-stu-id="637c0-123">Configure the server project</span></span>
<span data-ttu-id="637c0-124">Follow the steps below to configure the server project to use either the Node.js or .NET backend.</span><span class="sxs-lookup"><span data-stu-id="637c0-124">Follow the steps below to configure the server project to use either the Node.js or .NET backend.</span></span>

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-xamarinforms-solution"></a><span data-ttu-id="637c0-125">Download and run the Xamarin.Forms solution</span><span class="sxs-lookup"><span data-stu-id="637c0-125">Download and run the Xamarin.Forms solution</span></span>
<span data-ttu-id="637c0-126">Here you have a couple of choices.</span><span class="sxs-lookup"><span data-stu-id="637c0-126">Here you have a couple of choices.</span></span> <span data-ttu-id="637c0-127">You can download the solution to a Mac and open it in Xamarin Studio, or you can download the solution to a Windows computer and open it in Visual Studio using a networked Mac for building the iOS app.</span><span class="sxs-lookup"><span data-stu-id="637c0-127">You can download the solution to a Mac and open it in Xamarin Studio, or you can download the solution to a Windows computer and open it in Visual Studio using a networked Mac for building the iOS app.</span></span> <span data-ttu-id="637c0-128">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) if you need more detailed instructions on the Xamarin setup scenarios.</span><span class="sxs-lookup"><span data-stu-id="637c0-128">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) if you need more detailed instructions on the Xamarin setup scenarios.</span></span>

<span data-ttu-id="637c0-129">Let's proceed:</span><span class="sxs-lookup"><span data-stu-id="637c0-129">Let's proceed:</span></span>

1. <span data-ttu-id="637c0-130">On your Mac or on your Windows computer, open the [Azure Portal] in a browser window.</span><span class="sxs-lookup"><span data-stu-id="637c0-130">On your Mac or on your Windows computer, open the [Azure Portal] in a browser window.</span></span>
2. <span data-ttu-id="637c0-131">On the settings blade for your Mobile App, click **Get Started** (under Mobile) > **Xamarin.Forms**.</span><span class="sxs-lookup"><span data-stu-id="637c0-131">On the settings blade for your Mobile App, click **Get Started** (under Mobile) > **Xamarin.Forms**.</span></span> <span data-ttu-id="637c0-132">Under step 3, click  **Create a new app** if it's not already selected.</span><span class="sxs-lookup"><span data-stu-id="637c0-132">Under step 3, click  **Create a new app** if it's not already selected.</span></span>  <span data-ttu-id="637c0-133">Next click the **Download** button.</span><span class="sxs-lookup"><span data-stu-id="637c0-133">Next click the **Download** button.</span></span>
   
   <span data-ttu-id="637c0-134">This downloads a project that contains a client application that is connected to your mobile app.</span><span class="sxs-lookup"><span data-stu-id="637c0-134">This downloads a project that contains a client application that is connected to your mobile app.</span></span> <span data-ttu-id="637c0-135">Save the compressed project file to your local computer, and make a note of where you save it.</span><span class="sxs-lookup"><span data-stu-id="637c0-135">Save the compressed project file to your local computer, and make a note of where you save it.</span></span>
3. <span data-ttu-id="637c0-136">Extract the project that you downloaded, and then open it in Xamarin Studio or Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="637c0-136">Extract the project that you downloaded, and then open it in Xamarin Studio or Visual Studio.</span></span>
   
   ![][9]
   
   ![][8]

## <a name="optional-run-the-ios-project"></a><span data-ttu-id="637c0-137">(Optional) Run the iOS project</span><span class="sxs-lookup"><span data-stu-id="637c0-137">(Optional) Run the iOS project</span></span>
<span data-ttu-id="637c0-138">This section is for running the Xamarin iOS project for iOS devices.</span><span class="sxs-lookup"><span data-stu-id="637c0-138">This section is for running the Xamarin iOS project for iOS devices.</span></span> <span data-ttu-id="637c0-139">You can skip this section if you are not working with iOS devices.</span><span class="sxs-lookup"><span data-stu-id="637c0-139">You can skip this section if you are not working with iOS devices.</span></span>

#### <a name="in-xamarin-studio"></a><span data-ttu-id="637c0-140">In Xamarin Studio</span><span class="sxs-lookup"><span data-stu-id="637c0-140">In Xamarin Studio</span></span>
1. <span data-ttu-id="637c0-141">Right-click the iOS project, and then click **Set As Startup Project**.</span><span class="sxs-lookup"><span data-stu-id="637c0-141">Right-click the iOS project, and then click **Set As Startup Project**.</span></span>
2. <span data-ttu-id="637c0-142">On the **Run** menu, click **Start Debugging** to build the project and start the app in the iPhone emulator.</span><span class="sxs-lookup"><span data-stu-id="637c0-142">On the **Run** menu, click **Start Debugging** to build the project and start the app in the iPhone emulator.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="637c0-143">In Visual Studio</span><span class="sxs-lookup"><span data-stu-id="637c0-143">In Visual Studio</span></span>
1. <span data-ttu-id="637c0-144">Right-click the iOS project, and then click **Set as StartUp Project**.</span><span class="sxs-lookup"><span data-stu-id="637c0-144">Right-click the iOS project, and then click **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="637c0-145">On the **Build** menu, click **Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="637c0-145">On the **Build** menu, click **Configuration Manager**.</span></span>
3. <span data-ttu-id="637c0-146">In the **Configuration Manager** dialog box, select the **Build** and **Deploy** checkboxes of the iOS project.</span><span class="sxs-lookup"><span data-stu-id="637c0-146">In the **Configuration Manager** dialog box, select the **Build** and **Deploy** checkboxes of the iOS project.</span></span>
4. <span data-ttu-id="637c0-147">Press the **F5** key to build the project and start the app in the iPhone emulator.</span><span class="sxs-lookup"><span data-stu-id="637c0-147">Press the **F5** key to build the project and start the app in the iPhone emulator.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="637c0-148">If you have problems building, run NuGet package manager and update to the latest version of the Xamarin support packages.</span><span class="sxs-lookup"><span data-stu-id="637c0-148">If you have problems building, run NuGet package manager and update to the latest version of the Xamarin support packages.</span></span> <span data-ttu-id="637c0-149">Sometimes the Quickstart projects may lag behind in being updated to the latest.</span><span class="sxs-lookup"><span data-stu-id="637c0-149">Sometimes the Quickstart projects may lag behind in being updated to the latest.</span></span>    
   > 
   > 

<span data-ttu-id="637c0-150">In the app, type meaningful text, such as *Learn Xamarin* and then click the **+** button.</span><span class="sxs-lookup"><span data-stu-id="637c0-150">In the app, type meaningful text, such as *Learn Xamarin* and then click the **+** button.</span></span>

![][10]

<span data-ttu-id="637c0-151">This sends a POST request to the new mobile app backend hosted in Azure.</span><span class="sxs-lookup"><span data-stu-id="637c0-151">This sends a POST request to the new mobile app backend hosted in Azure.</span></span> <span data-ttu-id="637c0-152">Data from the request is inserted into the TodoItem table.</span><span class="sxs-lookup"><span data-stu-id="637c0-152">Data from the request is inserted into the TodoItem table.</span></span> <span data-ttu-id="637c0-153">Items stored in the table are returned by the mobile app backend, and the data is displayed in the list.</span><span class="sxs-lookup"><span data-stu-id="637c0-153">Items stored in the table are returned by the mobile app backend, and the data is displayed in the list.</span></span>

> [!NOTE]
> <span data-ttu-id="637c0-154">You'll find the code that accesses your mobile app backend in the TodoItemManager.cs C# file of the portable class library project of your solution.</span><span class="sxs-lookup"><span data-stu-id="637c0-154">You'll find the code that accesses your mobile app backend in the TodoItemManager.cs C# file of the portable class library project of your solution.</span></span>
> 
> 

## <a name="optional-run-the-android-project"></a><span data-ttu-id="637c0-155">(Optional) Run the Android project</span><span class="sxs-lookup"><span data-stu-id="637c0-155">(Optional) Run the Android project</span></span>
<span data-ttu-id="637c0-156">This section is for running the Xamarin droid project for Android.</span><span class="sxs-lookup"><span data-stu-id="637c0-156">This section is for running the Xamarin droid project for Android.</span></span> <span data-ttu-id="637c0-157">You can skip this section if you are not working with Android devices.</span><span class="sxs-lookup"><span data-stu-id="637c0-157">You can skip this section if you are not working with Android devices.</span></span>

#### <a name="in-xamarin-studio"></a><span data-ttu-id="637c0-158">In Xamarin Studio</span><span class="sxs-lookup"><span data-stu-id="637c0-158">In Xamarin Studio</span></span>
1. <span data-ttu-id="637c0-159">Right-click the Android project, and then click **Set As Startup Project**.</span><span class="sxs-lookup"><span data-stu-id="637c0-159">Right-click the Android project, and then click **Set As Startup Project**.</span></span>
2. <span data-ttu-id="637c0-160">On the **Run** menu, click **Start Debugging** to build the project and start the app in an Android emulator.</span><span class="sxs-lookup"><span data-stu-id="637c0-160">On the **Run** menu, click **Start Debugging** to build the project and start the app in an Android emulator.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="637c0-161">In Visual Studio</span><span class="sxs-lookup"><span data-stu-id="637c0-161">In Visual Studio</span></span>
1. <span data-ttu-id="637c0-162">Right-click the Android (Droid) project, and then click **Set as StartUp Project**.</span><span class="sxs-lookup"><span data-stu-id="637c0-162">Right-click the Android (Droid) project, and then click **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="637c0-163">On the **Build** menu, click **Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="637c0-163">On the **Build** menu, click **Configuration Manager**.</span></span>
3. <span data-ttu-id="637c0-164">In the **Configuration Manager** dialog box, select the **Build** and **Deploy** checkboxes of the Android project.</span><span class="sxs-lookup"><span data-stu-id="637c0-164">In the **Configuration Manager** dialog box, select the **Build** and **Deploy** checkboxes of the Android project.</span></span>
4. <span data-ttu-id="637c0-165">Press the **F5** key to build the project and start the app in an Android emulator.</span><span class="sxs-lookup"><span data-stu-id="637c0-165">Press the **F5** key to build the project and start the app in an Android emulator.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="637c0-166">If you have problems building, run NuGet package manager and update to the latest version of the Xamarin support packages.</span><span class="sxs-lookup"><span data-stu-id="637c0-166">If you have problems building, run NuGet package manager and update to the latest version of the Xamarin support packages.</span></span> <span data-ttu-id="637c0-167">Sometimes the Quickstart projects may lag behind in being updated to the latest.</span><span class="sxs-lookup"><span data-stu-id="637c0-167">Sometimes the Quickstart projects may lag behind in being updated to the latest.</span></span>    
   > 
   > 

<span data-ttu-id="637c0-168">In the app, type meaningful text, such as *Learn Xamarin* and then click the **+** button.</span><span class="sxs-lookup"><span data-stu-id="637c0-168">In the app, type meaningful text, such as *Learn Xamarin* and then click the **+** button.</span></span>

![][11]

<span data-ttu-id="637c0-169">This sends a POST request to the new mobile app backend hosted in Azure.</span><span class="sxs-lookup"><span data-stu-id="637c0-169">This sends a POST request to the new mobile app backend hosted in Azure.</span></span> <span data-ttu-id="637c0-170">Data from the request is inserted into the TodoItem table.</span><span class="sxs-lookup"><span data-stu-id="637c0-170">Data from the request is inserted into the TodoItem table.</span></span> <span data-ttu-id="637c0-171">Items stored in the table are returned by the mobile app backend, and the data is displayed in the list.</span><span class="sxs-lookup"><span data-stu-id="637c0-171">Items stored in the table are returned by the mobile app backend, and the data is displayed in the list.</span></span>

> [!NOTE]
> <span data-ttu-id="637c0-172">You'll find the code that accesses your mobile app backend in the TodoItemManager.cs C# file of the portable class library project of your solution.</span><span class="sxs-lookup"><span data-stu-id="637c0-172">You'll find the code that accesses your mobile app backend in the TodoItemManager.cs C# file of the portable class library project of your solution.</span></span>
> 
> 

## <a name="optional-run-the-windows-project"></a><span data-ttu-id="637c0-173">(Optional) Run the Windows project</span><span class="sxs-lookup"><span data-stu-id="637c0-173">(Optional) Run the Windows project</span></span>
<span data-ttu-id="637c0-174">This section is for running the Xamarin WinApp project for Windows devices.</span><span class="sxs-lookup"><span data-stu-id="637c0-174">This section is for running the Xamarin WinApp project for Windows devices.</span></span> <span data-ttu-id="637c0-175">You can skip this section if you are not working with Windows devices.</span><span class="sxs-lookup"><span data-stu-id="637c0-175">You can skip this section if you are not working with Windows devices.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="637c0-176">In Visual Studio</span><span class="sxs-lookup"><span data-stu-id="637c0-176">In Visual Studio</span></span>
1. <span data-ttu-id="637c0-177">Right-click any of the Windows projects, and then click **Set as StartUp Project**.</span><span class="sxs-lookup"><span data-stu-id="637c0-177">Right-click any of the Windows projects, and then click **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="637c0-178">On the **Build** menu, click **Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="637c0-178">On the **Build** menu, click **Configuration Manager**.</span></span>
3. <span data-ttu-id="637c0-179">In the **Configuration Manager** dialog box, select the **Build** and **Deploy** checkboxes of the Windows project that you chose.</span><span class="sxs-lookup"><span data-stu-id="637c0-179">In the **Configuration Manager** dialog box, select the **Build** and **Deploy** checkboxes of the Windows project that you chose.</span></span>
4. <span data-ttu-id="637c0-180">Press the **F5** key to build the project and start the app in a Windows emulator.</span><span class="sxs-lookup"><span data-stu-id="637c0-180">Press the **F5** key to build the project and start the app in a Windows emulator.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="637c0-181">If you have problems building, run NuGet package manager and update to the latest version of the Xamarin support packages.</span><span class="sxs-lookup"><span data-stu-id="637c0-181">If you have problems building, run NuGet package manager and update to the latest version of the Xamarin support packages.</span></span> <span data-ttu-id="637c0-182">Sometimes the Quickstart projects may lag behind in being updated to the latest.</span><span class="sxs-lookup"><span data-stu-id="637c0-182">Sometimes the Quickstart projects may lag behind in being updated to the latest.</span></span>    
   > 
   > 

<span data-ttu-id="637c0-183">In the app, type meaningful text, such as *Learn Xamarin* and then click the **+** button.</span><span class="sxs-lookup"><span data-stu-id="637c0-183">In the app, type meaningful text, such as *Learn Xamarin* and then click the **+** button.</span></span>

<span data-ttu-id="637c0-184">This sends a POST request to the new mobile app backend hosted in Azure.</span><span class="sxs-lookup"><span data-stu-id="637c0-184">This sends a POST request to the new mobile app backend hosted in Azure.</span></span> <span data-ttu-id="637c0-185">Data from the request is inserted into the TodoItem table.</span><span class="sxs-lookup"><span data-stu-id="637c0-185">Data from the request is inserted into the TodoItem table.</span></span> <span data-ttu-id="637c0-186">Items stored in the table are returned by the mobile app backend, and the data is displayed in the list.</span><span class="sxs-lookup"><span data-stu-id="637c0-186">Items stored in the table are returned by the mobile app backend, and the data is displayed in the list.</span></span>

![][12]

> [!NOTE]
> <span data-ttu-id="637c0-187">You'll find the code that accesses your mobile app backend in the TodoItemManager.cs C# file of the portable class library project of your solution.</span><span class="sxs-lookup"><span data-stu-id="637c0-187">You'll find the code that accesses your mobile app backend in the TodoItemManager.cs C# file of the portable class library project of your solution.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="637c0-188">Next steps</span><span class="sxs-lookup"><span data-stu-id="637c0-188">Next steps</span></span>
* [<span data-ttu-id="637c0-189">Add authentication to your app</span><span class="sxs-lookup"><span data-stu-id="637c0-189">Add authentication to your app</span></span>](app-service-mobile-xamarin-forms-get-started-users.md)  
  <span data-ttu-id="637c0-190">Learn how to authenticate users of your app with an identity provider.</span><span class="sxs-lookup"><span data-stu-id="637c0-190">Learn how to authenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="637c0-191">Add push notifications to your app</span><span class="sxs-lookup"><span data-stu-id="637c0-191">Add push notifications to your app</span></span>](app-service-mobile-xamarin-forms-get-started-push.md)  
  <span data-ttu-id="637c0-192">Learn how to add push notifications support to your app and configure your Mobile App backend to use Azure Notification Hubs to send push notifications.</span><span class="sxs-lookup"><span data-stu-id="637c0-192">Learn how to add push notifications support to your app and configure your Mobile App backend to use Azure Notification Hubs to send push notifications.</span></span>
* [<span data-ttu-id="637c0-193">Enable offline sync for your app</span><span class="sxs-lookup"><span data-stu-id="637c0-193">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  <span data-ttu-id="637c0-194">Learn how to add offline support your app using an Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="637c0-194">Learn how to add offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="637c0-195">Offline sync allows end-users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span><span class="sxs-lookup"><span data-stu-id="637c0-195">Offline sync allows end-users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>
* [<span data-ttu-id="637c0-196">How to use the managed client for Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="637c0-196">How to use the managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)  
  <span data-ttu-id="637c0-197">Learn how to work with the managed client SDK in your Xamarin app.</span><span class="sxs-lookup"><span data-stu-id="637c0-197">Learn how to work with the managed client SDK in your Xamarin app.</span></span> 

<!-- Anchors. -->
[Getting started with mobile app backends]:#getting-started
[Create a new mobile app backend]:#create-new-service
[Next Steps]:#next-steps


<!-- Images. -->
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-vs.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-xs.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-ios.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-android.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-mobile/media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-windows.png


<!-- URLs. -->
[Visual Studio Professional 2013]: https://go.microsoft.com/fwLink/p/?LinkID=257546
[Mobile app SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure Portal]: https://portal.azure.com/







