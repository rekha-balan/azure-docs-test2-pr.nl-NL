---
title: Deploy an ASP.NET MVC 5 mobile web app in Azure App Service
description: A tutorial that teaches you how to deploy a web app to Azure App Service using mobile features in ASP.NET MVC 5 web application.
services: app-service
documentationcenter: .net
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 0752c802-8609-4956-a755-686116913645
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin;riande
ms.openlocfilehash: 0846d4157d266fe9202497b59aeca8989442bc3b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550803"
---
# <a name="deploy-an-aspnet-mvc-5-mobile-web-app-in-azure-app-service"></a><span data-ttu-id="49891-103">Deploy an ASP.NET MVC 5 mobile web app in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="49891-103">Deploy an ASP.NET MVC 5 mobile web app in Azure App Service</span></span>
<span data-ttu-id="49891-104">This tutorial will teach you the basics of how to build an ASP.NET MVC 5 web app that is mobile-friendly and deploy it to Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="49891-104">This tutorial will teach you the basics of how to build an ASP.NET MVC 5 web app that is mobile-friendly and deploy it to Azure App Service.</span></span> <span data-ttu-id="49891-105">For this tutorial, you need [Visual Studio Express 2013 for Web][Visual Studio Express 2013] or the professional edition of Visual Studio if you already have that.</span><span class="sxs-lookup"><span data-stu-id="49891-105">For this tutorial, you need [Visual Studio Express 2013 for Web][Visual Studio Express 2013] or the professional edition of Visual Studio if you already have that.</span></span> <span data-ttu-id="49891-106">You can use [Visual Studio 2015] but the screen shots will be different and you must use the ASP.NET 4.x templates.</span><span class="sxs-lookup"><span data-stu-id="49891-106">You can use [Visual Studio 2015] but the screen shots will be different and you must use the ASP.NET 4.x templates.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-youll-build"></a><span data-ttu-id="49891-107">What You'll Build</span><span class="sxs-lookup"><span data-stu-id="49891-107">What You'll Build</span></span>
<span data-ttu-id="49891-108">For this tutorial, you'll add mobile features to the simple conference-listing application that's provided in the [starter project][StarterProject].</span><span class="sxs-lookup"><span data-stu-id="49891-108">For this tutorial, you'll add mobile features to the simple conference-listing application that's provided in the [starter project][StarterProject].</span></span> <span data-ttu-id="49891-109">The following screenshot shows the ASP.NET sessions in the completed application, as seen in the browser emulator in Internet Explorer 11 F12 developer tools.</span><span class="sxs-lookup"><span data-stu-id="49891-109">The following screenshot shows the ASP.NET sessions in the completed application, as seen in the browser emulator in Internet Explorer 11 F12 developer tools.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="49891-110">You can use the Internet Explorer 11 F12 developer tools and the [Fiddler tool][Fiddler] to help debug your application.</span><span class="sxs-lookup"><span data-stu-id="49891-110">You can use the Internet Explorer 11 F12 developer tools and the [Fiddler tool][Fiddler] to help debug your application.</span></span> 

## <a name="skills-youll-learn"></a><span data-ttu-id="49891-111">Skills You'll Learn</span><span class="sxs-lookup"><span data-stu-id="49891-111">Skills You'll Learn</span></span>
<span data-ttu-id="49891-112">Here's what you'll learn:</span><span class="sxs-lookup"><span data-stu-id="49891-112">Here's what you'll learn:</span></span>

* <span data-ttu-id="49891-113">How to use Visual Studio 2013 to publish your web application directly to a web app in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="49891-113">How to use Visual Studio 2013 to publish your web application directly to a web app in Azure App Service.</span></span>
* <span data-ttu-id="49891-114">How the ASP.NET MVC 5 templates use the CSS Bootstrap framework to improve display on mobile devices</span><span class="sxs-lookup"><span data-stu-id="49891-114">How the ASP.NET MVC 5 templates use the CSS Bootstrap framework to improve display on mobile devices</span></span>
* <span data-ttu-id="49891-115">How to create mobile-specific views to target specific mobile browsers, such as the iPhone and Android</span><span class="sxs-lookup"><span data-stu-id="49891-115">How to create mobile-specific views to target specific mobile browsers, such as the iPhone and Android</span></span>
* <span data-ttu-id="49891-116">How to create responsive views (views that respond to different browsers across devices)</span><span class="sxs-lookup"><span data-stu-id="49891-116">How to create responsive views (views that respond to different browsers across devices)</span></span>

## <a name="set-up-the-development-environment"></a><span data-ttu-id="49891-117">Set up the development environment</span><span class="sxs-lookup"><span data-stu-id="49891-117">Set up the development environment</span></span>
<span data-ttu-id="49891-118">Set up your development environment by installing the Azure SDK for .NET 2.5.1 or later.</span><span class="sxs-lookup"><span data-stu-id="49891-118">Set up your development environment by installing the Azure SDK for .NET 2.5.1 or later.</span></span> 

1. <span data-ttu-id="49891-119">To install the Azure SDK for .NET, click the link below.</span><span class="sxs-lookup"><span data-stu-id="49891-119">To install the Azure SDK for .NET, click the link below.</span></span> <span data-ttu-id="49891-120">If you don't have Visual Studio 2013 installed yet, it will be installed by the link.</span><span class="sxs-lookup"><span data-stu-id="49891-120">If you don't have Visual Studio 2013 installed yet, it will be installed by the link.</span></span> <span data-ttu-id="49891-121">This tutorial requires Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="49891-121">This tutorial requires Visual Studio 2013.</span></span> <span data-ttu-id="49891-122">[Azure SDK for Visual Studio 2013][AzureSDKVs2013]</span><span class="sxs-lookup"><span data-stu-id="49891-122">[Azure SDK for Visual Studio 2013][AzureSDKVs2013]</span></span>
2. <span data-ttu-id="49891-123">In the Web Platform Installer window, click **Install** and proceed with the installation.</span><span class="sxs-lookup"><span data-stu-id="49891-123">In the Web Platform Installer window, click **Install** and proceed with the installation.</span></span>

<span data-ttu-id="49891-124">You will also need a mobile browser emulator.</span><span class="sxs-lookup"><span data-stu-id="49891-124">You will also need a mobile browser emulator.</span></span> <span data-ttu-id="49891-125">Any of the following will work:</span><span class="sxs-lookup"><span data-stu-id="49891-125">Any of the following will work:</span></span>

* <span data-ttu-id="49891-126">Browser Emulator in [Internet Explorer 11 F12 developer tools][EmulatorIE11] (used in all mobile browser screenshots).</span><span class="sxs-lookup"><span data-stu-id="49891-126">Browser Emulator in [Internet Explorer 11 F12 developer tools][EmulatorIE11] (used in all mobile browser screenshots).</span></span> <span data-ttu-id="49891-127">It has user agent string presets for Windows Phone 8, Windows Phone 7, and Apple iPad.</span><span class="sxs-lookup"><span data-stu-id="49891-127">It has user agent string presets for Windows Phone 8, Windows Phone 7, and Apple iPad.</span></span>
* <span data-ttu-id="49891-128">Browser Emulator in [Google Chrome DevTools][EmulatorChrome].</span><span class="sxs-lookup"><span data-stu-id="49891-128">Browser Emulator in [Google Chrome DevTools][EmulatorChrome].</span></span> <span data-ttu-id="49891-129">It contains presets for numerous Android devices, as well as Apple iPhone, Apple iPad, and Amazon Kindle Fire.</span><span class="sxs-lookup"><span data-stu-id="49891-129">It contains presets for numerous Android devices, as well as Apple iPhone, Apple iPad, and Amazon Kindle Fire.</span></span> <span data-ttu-id="49891-130">It also emulates touch events.</span><span class="sxs-lookup"><span data-stu-id="49891-130">It also emulates touch events.</span></span>
* <span data-ttu-id="49891-131">[Opera Mobile Emulator][EmulatorOpera]</span><span class="sxs-lookup"><span data-stu-id="49891-131">[Opera Mobile Emulator][EmulatorOpera]</span></span>

<span data-ttu-id="49891-132">Visual Studio projects with C\# source code are available to accompany this topic:</span><span class="sxs-lookup"><span data-stu-id="49891-132">Visual Studio projects with C\# source code are available to accompany this topic:</span></span>

* <span data-ttu-id="49891-133">[Starter project download][StarterProject]</span><span class="sxs-lookup"><span data-stu-id="49891-133">[Starter project download][StarterProject]</span></span>
* <span data-ttu-id="49891-134">[Completed project download][CompletedProject]</span><span class="sxs-lookup"><span data-stu-id="49891-134">[Completed project download][CompletedProject]</span></span>

## <a name="bkmk_DeployStarterProject"></a><span data-ttu-id="49891-135">Deploy the starter project to an Azure web app</span><span class="sxs-lookup"><span data-stu-id="49891-135">Deploy the starter project to an Azure web app</span></span>
1. <span data-ttu-id="49891-136">Download the conference-listing application [starter project][StarterProject].</span><span class="sxs-lookup"><span data-stu-id="49891-136">Download the conference-listing application [starter project][StarterProject].</span></span>
2. <span data-ttu-id="49891-137">Then in Windows Explorer, right-click the downloaded ZIP file and choose *Properties*.</span><span class="sxs-lookup"><span data-stu-id="49891-137">Then in Windows Explorer, right-click the downloaded ZIP file and choose *Properties*.</span></span>
3. <span data-ttu-id="49891-138">In the **Properties** dialog box, choose the **Unblock** button.</span><span class="sxs-lookup"><span data-stu-id="49891-138">In the **Properties** dialog box, choose the **Unblock** button.</span></span> <span data-ttu-id="49891-139">(Unblocking prevents a security warning that occurs when you try to use a *.zip* file that you've downloaded from the web.)</span><span class="sxs-lookup"><span data-stu-id="49891-139">(Unblocking prevents a security warning that occurs when you try to use a *.zip* file that you've downloaded from the web.)</span></span>
4. <span data-ttu-id="49891-140">Right-click the ZIP file and select **Extract All** to unzip the file.</span><span class="sxs-lookup"><span data-stu-id="49891-140">Right-click the ZIP file and select **Extract All** to unzip the file.</span></span> 
5. <span data-ttu-id="49891-141">In Visual Studio, open the *C#\Mvc5Mobile.sln* file.</span><span class="sxs-lookup"><span data-stu-id="49891-141">In Visual Studio, open the *C#\Mvc5Mobile.sln* file.</span></span>
6. <span data-ttu-id="49891-142">In Solution Explorer, right-click the project and click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="49891-142">In Solution Explorer, right-click the project and click **Publish**.</span></span>
   
   ![][DeployClickPublish]
7. <span data-ttu-id="49891-143">In Publish Web, click **Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="49891-143">In Publish Web, click **Microsoft Azure App Service**.</span></span>
   
   ![][DeployClickWebSites]
8. <span data-ttu-id="49891-144">If you haven't already logged into Azure, click **Add an account**.</span><span class="sxs-lookup"><span data-stu-id="49891-144">If you haven't already logged into Azure, click **Add an account**.</span></span>
   
   ![][DeploySignIn]
9. <span data-ttu-id="49891-145">Follow the prompts to log into your Azure account.</span><span class="sxs-lookup"><span data-stu-id="49891-145">Follow the prompts to log into your Azure account.</span></span>
10. <span data-ttu-id="49891-146">The App Service dialog should now show you as signed in.</span><span class="sxs-lookup"><span data-stu-id="49891-146">The App Service dialog should now show you as signed in.</span></span> <span data-ttu-id="49891-147">Click **New**.</span><span class="sxs-lookup"><span data-stu-id="49891-147">Click **New**.</span></span>
    
    ![][DeployNewWebsite]  
11. <span data-ttu-id="49891-148">In the **Web App Name** field, specify a unique app name prefix.</span><span class="sxs-lookup"><span data-stu-id="49891-148">In the **Web App Name** field, specify a unique app name prefix.</span></span> <span data-ttu-id="49891-149">Your fully-qualified web app name will be *&lt;prefix>*.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="49891-149">Your fully-qualified web app name will be *&lt;prefix>*.azurewebsites.net.</span></span> <span data-ttu-id="49891-150">Also, select or specify a new resource group name in **Resource group**.</span><span class="sxs-lookup"><span data-stu-id="49891-150">Also, select or specify a new resource group name in **Resource group**.</span></span> <span data-ttu-id="49891-151">Then, click **New** to create a new App Service plan.</span><span class="sxs-lookup"><span data-stu-id="49891-151">Then, click **New** to create a new App Service plan.</span></span>
    
    ![][DeploySiteSettings]
12. <span data-ttu-id="49891-152">Configure the new App Service plan and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="49891-152">Configure the new App Service plan and click **OK**.</span></span> 
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7a.png)
13. <span data-ttu-id="49891-153">Back in the Create App Service dialog, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="49891-153">Back in the Create App Service dialog, click **Create**.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7b.png) 
14. <span data-ttu-id="49891-154">After the Azure resources are created, the Publish Web dialog will be filled with the settings for your new app.</span><span class="sxs-lookup"><span data-stu-id="49891-154">After the Azure resources are created, the Publish Web dialog will be filled with the settings for your new app.</span></span> <span data-ttu-id="49891-155">Click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="49891-155">Click **Publish**.</span></span>
    
    ![][DeployPublishSite]
    
    <span data-ttu-id="49891-156">Once Visual Studio finishes publishing the starter project to the Azure web app, the desktop browser opens to display the live web app.</span><span class="sxs-lookup"><span data-stu-id="49891-156">Once Visual Studio finishes publishing the starter project to the Azure web app, the desktop browser opens to display the live web app.</span></span>
15. <span data-ttu-id="49891-157">Start your mobile browser emulator, copy the URL for the conference application (*<prefix>*.azurewebsites.net) into the emulator, and then click the top-right button and select **Browse by tag**.</span><span class="sxs-lookup"><span data-stu-id="49891-157">Start your mobile browser emulator, copy the URL for the conference application (*<prefix>*.azurewebsites.net) into the emulator, and then click the top-right button and select **Browse by tag**.</span></span> <span data-ttu-id="49891-158">If you are using Internet Explorer 11 as the default browser, you just need to type `F12`, then `Ctrl+8`, and then change the browser profile to **Windows Phone**.</span><span class="sxs-lookup"><span data-stu-id="49891-158">If you are using Internet Explorer 11 as the default browser, you just need to type `F12`, then `Ctrl+8`, and then change the browser profile to **Windows Phone**.</span></span> <span data-ttu-id="49891-159">The image below shows the *AllTags* view in portrait mode (from choosing **Browse by tag**).</span><span class="sxs-lookup"><span data-stu-id="49891-159">The image below shows the *AllTags* view in portrait mode (from choosing **Browse by tag**).</span></span>
    
    ![][AllTags]

> [!TIP]
> <span data-ttu-id="49891-160">While you can debug your MVC 5 application from within Visual Studio, you can publish your web app to Azure again to verify the live web app directly from your mobile browser or a browser emulator.</span><span class="sxs-lookup"><span data-stu-id="49891-160">While you can debug your MVC 5 application from within Visual Studio, you can publish your web app to Azure again to verify the live web app directly from your mobile browser or a browser emulator.</span></span>
> 
> 

<span data-ttu-id="49891-161">The display is very readable on a mobile device.</span><span class="sxs-lookup"><span data-stu-id="49891-161">The display is very readable on a mobile device.</span></span> <span data-ttu-id="49891-162">You can also already see some of the visual effects applied by the Bootstrap CSS framework.</span><span class="sxs-lookup"><span data-stu-id="49891-162">You can also already see some of the visual effects applied by the Bootstrap CSS framework.</span></span>
<span data-ttu-id="49891-163">Click the **ASP.NET** link.</span><span class="sxs-lookup"><span data-stu-id="49891-163">Click the **ASP.NET** link.</span></span>

![][SessionsByTagASP.NET]

<span data-ttu-id="49891-164">The ASP.NET tag view is zoom-fitted to the screen, which Bootstrap does for you automatically.</span><span class="sxs-lookup"><span data-stu-id="49891-164">The ASP.NET tag view is zoom-fitted to the screen, which Bootstrap does for you automatically.</span></span> <span data-ttu-id="49891-165">However, you can improve this view to better suit the mobile browser.</span><span class="sxs-lookup"><span data-stu-id="49891-165">However, you can improve this view to better suit the mobile browser.</span></span> <span data-ttu-id="49891-166">For example, the **Date** column is difficult to read.</span><span class="sxs-lookup"><span data-stu-id="49891-166">For example, the **Date** column is difficult to read.</span></span> <span data-ttu-id="49891-167">Later in the tutorial you'll change the *AllTags* view to make it mobile-friendly.</span><span class="sxs-lookup"><span data-stu-id="49891-167">Later in the tutorial you'll change the *AllTags* view to make it mobile-friendly.</span></span>

## <a name="bkmk_bootstrap"></a> <span data-ttu-id="49891-168">Bootstrap CSS Framework</span><span class="sxs-lookup"><span data-stu-id="49891-168">Bootstrap CSS Framework</span></span>
<span data-ttu-id="49891-169">New in the MVC 5 template is built-in Bootstrap support.</span><span class="sxs-lookup"><span data-stu-id="49891-169">New in the MVC 5 template is built-in Bootstrap support.</span></span> <span data-ttu-id="49891-170">You have already seen how it immediately improves the different views in your application.</span><span class="sxs-lookup"><span data-stu-id="49891-170">You have already seen how it immediately improves the different views in your application.</span></span> <span data-ttu-id="49891-171">For example, the navigation bar at the top is automatically collapsible when the browser width is smaller.</span><span class="sxs-lookup"><span data-stu-id="49891-171">For example, the navigation bar at the top is automatically collapsible when the browser width is smaller.</span></span> <span data-ttu-id="49891-172">On the desktop browser, try resizing the browser window and see how the navigation bar changes its look and feel.</span><span class="sxs-lookup"><span data-stu-id="49891-172">On the desktop browser, try resizing the browser window and see how the navigation bar changes its look and feel.</span></span> <span data-ttu-id="49891-173">This is the responsive web design that is built into Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="49891-173">This is the responsive web design that is built into Bootstrap.</span></span>

<span data-ttu-id="49891-174">To see how the Web app would look without Bootstrap, open *App\_Start\\BundleConfig.cs* and comment out the lines that contain *bootstrap.js* and *bootstrap.css*.</span><span class="sxs-lookup"><span data-stu-id="49891-174">To see how the Web app would look without Bootstrap, open *App\_Start\\BundleConfig.cs* and comment out the lines that contain *bootstrap.js* and *bootstrap.css*.</span></span> <span data-ttu-id="49891-175">The following code shows the last two statements of the `RegisterBundles` method after the change:</span><span class="sxs-lookup"><span data-stu-id="49891-175">The following code shows the last two statements of the `RegisterBundles` method after the change:</span></span>

     bundles.Add(new ScriptBundle("~/bundles/bootstrap").Include(
              //"~/Scripts/bootstrap.js",
              "~/Scripts/respond.js"));

    bundles.Add(new StyleBundle("~/Content/css").Include(
              //"~/Content/bootstrap.css",
              "~/Content/site.css"));

<span data-ttu-id="49891-176">Press `Ctrl+F5` to run the application.</span><span class="sxs-lookup"><span data-stu-id="49891-176">Press `Ctrl+F5` to run the application.</span></span>

<span data-ttu-id="49891-177">Observe that the collapsible navigation bar is now just an ordinary unordered list.</span><span class="sxs-lookup"><span data-stu-id="49891-177">Observe that the collapsible navigation bar is now just an ordinary unordered list.</span></span> <span data-ttu-id="49891-178">Click **Browse by tag** again, then click **ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="49891-178">Click **Browse by tag** again, then click **ASP.NET**.</span></span>
<span data-ttu-id="49891-179">In the mobile emulator view, you can see now that it is no longer zoom-fitted to the screen, and you must scroll sideways in order to see the right side of the table.</span><span class="sxs-lookup"><span data-stu-id="49891-179">In the mobile emulator view, you can see now that it is no longer zoom-fitted to the screen, and you must scroll sideways in order to see the right side of the table.</span></span>

![][SessionsByTagASP.NETNoBootstrap]

<span data-ttu-id="49891-180">Undo your changes and refresh the mobile browser to verify that the mobile-friendly display has been restored.</span><span class="sxs-lookup"><span data-stu-id="49891-180">Undo your changes and refresh the mobile browser to verify that the mobile-friendly display has been restored.</span></span>

<span data-ttu-id="49891-181">Bootstrap is not specific to ASP.NET MVC 5, and you can take advantage of these features in any web application.</span><span class="sxs-lookup"><span data-stu-id="49891-181">Bootstrap is not specific to ASP.NET MVC 5, and you can take advantage of these features in any web application.</span></span> <span data-ttu-id="49891-182">But it is now built into the ASP.NET MVC 5 project template, so that your MVC 5 Web application can take advantage of Bootstrap by default.</span><span class="sxs-lookup"><span data-stu-id="49891-182">But it is now built into the ASP.NET MVC 5 project template, so that your MVC 5 Web application can take advantage of Bootstrap by default.</span></span>

<span data-ttu-id="49891-183">For more information about Bootstrap, go to the [Bootstrap][BootstrapSite] site.</span><span class="sxs-lookup"><span data-stu-id="49891-183">For more information about Bootstrap, go to the [Bootstrap][BootstrapSite] site.</span></span>

<span data-ttu-id="49891-184">In the next section you'll see how to provide mobile-browser specific views.</span><span class="sxs-lookup"><span data-stu-id="49891-184">In the next section you'll see how to provide mobile-browser specific views.</span></span>

## <a name="bkmk_overrideviews"></a> <span data-ttu-id="49891-185">Override the Views, Layouts, and Partial Views</span><span class="sxs-lookup"><span data-stu-id="49891-185">Override the Views, Layouts, and Partial Views</span></span>
<span data-ttu-id="49891-186">You can override any view (including layouts and partial views) for mobile browsers in general, for an individual mobile browser, or for any specific browser.</span><span class="sxs-lookup"><span data-stu-id="49891-186">You can override any view (including layouts and partial views) for mobile browsers in general, for an individual mobile browser, or for any specific browser.</span></span> <span data-ttu-id="49891-187">To provide a mobile-specific view, you can copy a view file and add *.Mobile* to the file name.</span><span class="sxs-lookup"><span data-stu-id="49891-187">To provide a mobile-specific view, you can copy a view file and add *.Mobile* to the file name.</span></span> <span data-ttu-id="49891-188">For example, to create a mobile *Index* view, you can copy *Views\\Home\\Index.cshtml* to *Views\\Home\\Index.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="49891-188">For example, to create a mobile *Index* view, you can copy *Views\\Home\\Index.cshtml* to *Views\\Home\\Index.Mobile.cshtml*.</span></span>

<span data-ttu-id="49891-189">In this section, you'll create a mobile-specific layout file.</span><span class="sxs-lookup"><span data-stu-id="49891-189">In this section, you'll create a mobile-specific layout file.</span></span>

<span data-ttu-id="49891-190">To start, copy *Views\\Shared\\\_Layout.cshtml* to *Views\\Shared\\\_Layout.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="49891-190">To start, copy *Views\\Shared\\\_Layout.cshtml* to *Views\\Shared\\\_Layout.Mobile.cshtml*.</span></span> <span data-ttu-id="49891-191">Open *\_Layout.Mobile.cshtml* and change the title from **MVC5 Application** to **MVC5 Application (Mobile)**.</span><span class="sxs-lookup"><span data-stu-id="49891-191">Open *\_Layout.Mobile.cshtml* and change the title from **MVC5 Application** to **MVC5 Application (Mobile)**.</span></span>

<span data-ttu-id="49891-192">In each `Html.ActionLink` call for the navigation bar, remove "Browse by" in each link *ActionLink*.</span><span class="sxs-lookup"><span data-stu-id="49891-192">In each `Html.ActionLink` call for the navigation bar, remove "Browse by" in each link *ActionLink*.</span></span> <span data-ttu-id="49891-193">The following code shows the completed `<ul class="nav navbar-nav">` tag of the mobile layout file.</span><span class="sxs-lookup"><span data-stu-id="49891-193">The following code shows the completed `<ul class="nav navbar-nav">` tag of the mobile layout file.</span></span>

    <ul class="nav navbar-nav">
        <li>@Html.ActionLink("Home", "Index", "Home")</li>
        <li>@Html.ActionLink("Date", "AllDates", "Home")</li>
        <li>@Html.ActionLink("Speaker", "AllSpeakers", "Home")</li>
        <li>@Html.ActionLink("Tag", "AllTags", "Home")</li>
    </ul>

<span data-ttu-id="49891-194">Copy the *Views\\Home\\AllTags.cshtml* file to *Views\\Home\\AllTags.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="49891-194">Copy the *Views\\Home\\AllTags.cshtml* file to *Views\\Home\\AllTags.Mobile.cshtml*.</span></span> <span data-ttu-id="49891-195">Open the new file and change the `<h2>` element from "Tags" to "Tags (M)":</span><span class="sxs-lookup"><span data-stu-id="49891-195">Open the new file and change the `<h2>` element from "Tags" to "Tags (M)":</span></span>

    <h2>Tags (M)</h2>

<span data-ttu-id="49891-196">Browse to the tags page using a desktop browser and using mobile browser emulator.</span><span class="sxs-lookup"><span data-stu-id="49891-196">Browse to the tags page using a desktop browser and using mobile browser emulator.</span></span> <span data-ttu-id="49891-197">The mobile browser emulator shows the two changes you made (the title from *\_Layout.Mobile.cshtml* and the title from *AllTags.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="49891-197">The mobile browser emulator shows the two changes you made (the title from *\_Layout.Mobile.cshtml* and the title from *AllTags.Mobile.cshtml*).</span></span>

![][AllTagsMobile_LayoutMobile]

<span data-ttu-id="49891-198">In contrast, the desktop display has not changed (with titles from *\_Layout.cshtml* and *AllTags.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="49891-198">In contrast, the desktop display has not changed (with titles from *\_Layout.cshtml* and *AllTags.cshtml*).</span></span>

![][AllTagsMobile_LayoutMobileDesktop]

## <a name="bkmk_browserviews"></a> <span data-ttu-id="49891-199">Create Browser-Specific Views</span><span class="sxs-lookup"><span data-stu-id="49891-199">Create Browser-Specific Views</span></span>
<span data-ttu-id="49891-200">In addition to mobile-specific and desktop-specific views, you can create views for an individual browser.</span><span class="sxs-lookup"><span data-stu-id="49891-200">In addition to mobile-specific and desktop-specific views, you can create views for an individual browser.</span></span> <span data-ttu-id="49891-201">For example, you can create views that are specifically for the iPhone or the Android browser.</span><span class="sxs-lookup"><span data-stu-id="49891-201">For example, you can create views that are specifically for the iPhone or the Android browser.</span></span> <span data-ttu-id="49891-202">In this section, you'll create a layout for the iPhone browser and an iPhone version of the *AllTags* view.</span><span class="sxs-lookup"><span data-stu-id="49891-202">In this section, you'll create a layout for the iPhone browser and an iPhone version of the *AllTags* view.</span></span>

<span data-ttu-id="49891-203">Open the *Global.asax* file and add the following code to the bottom of the `Application_Start` method.</span><span class="sxs-lookup"><span data-stu-id="49891-203">Open the *Global.asax* file and add the following code to the bottom of the `Application_Start` method.</span></span>

    DisplayModeProvider.Instance.Modes.Insert(0, new DefaultDisplayMode("iPhone")
    {
        ContextCondition = (context => context.GetOverriddenUserAgent().IndexOf
            ("iPhone", StringComparison.OrdinalIgnoreCase) >= 0)
    });

<span data-ttu-id="49891-204">This code defines a new display mode named "iPhone" that will be matched against each incoming request.</span><span class="sxs-lookup"><span data-stu-id="49891-204">This code defines a new display mode named "iPhone" that will be matched against each incoming request.</span></span> <span data-ttu-id="49891-205">If the incoming request matches the condition you defined (that is, if the user agent contains the string "iPhone"), ASP.NET MVC will look for views whose name contains the "iPhone" suffix.</span><span class="sxs-lookup"><span data-stu-id="49891-205">If the incoming request matches the condition you defined (that is, if the user agent contains the string "iPhone"), ASP.NET MVC will look for views whose name contains the "iPhone" suffix.</span></span>

> [!NOTE]
> <span data-ttu-id="49891-206">When adding mobile browser-specific display modes, such as for iPhone and Android, be sure to set the first argument to `0` (insert at the top of the list) to make sure that the browser-specific mode takes precedence over the mobile template (\*.Mobile.cshtml).</span><span class="sxs-lookup"><span data-stu-id="49891-206">When adding mobile browser-specific display modes, such as for iPhone and Android, be sure to set the first argument to `0` (insert at the top of the list) to make sure that the browser-specific mode takes precedence over the mobile template (\*.Mobile.cshtml).</span></span> <span data-ttu-id="49891-207">If the mobile template is at the top of the list instead, it will be selected over your intended display mode (the first match wins, and the mobile template matches all mobile browsers).</span><span class="sxs-lookup"><span data-stu-id="49891-207">If the mobile template is at the top of the list instead, it will be selected over your intended display mode (the first match wins, and the mobile template matches all mobile browsers).</span></span> 
> 
> 

<span data-ttu-id="49891-208">In the code, right-click `DefaultDisplayMode`, choose **Resolve**, and then choose `using System.Web.WebPages;`.</span><span class="sxs-lookup"><span data-stu-id="49891-208">In the code, right-click `DefaultDisplayMode`, choose **Resolve**, and then choose `using System.Web.WebPages;`.</span></span> <span data-ttu-id="49891-209">This adds a reference to the `System.Web.WebPages` namespace, which is where the `DisplayModeProvider` and `DefaultDisplayMode` types are defined.</span><span class="sxs-lookup"><span data-stu-id="49891-209">This adds a reference to the `System.Web.WebPages` namespace, which is where the `DisplayModeProvider` and `DefaultDisplayMode` types are defined.</span></span>

![][ResolveDefaultDisplayMode]

<span data-ttu-id="49891-210">Alternatively, you can just manually add the following line to the `using` section of the file.</span><span class="sxs-lookup"><span data-stu-id="49891-210">Alternatively, you can just manually add the following line to the `using` section of the file.</span></span>

    using System.Web.WebPages;

<span data-ttu-id="49891-211">Save the changes.</span><span class="sxs-lookup"><span data-stu-id="49891-211">Save the changes.</span></span> <span data-ttu-id="49891-212">Copy the *Views\\Shared\\\_Layout.Mobile.cshtml* file to *Views\\Shared\\\_Layout.iPhone.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="49891-212">Copy the *Views\\Shared\\\_Layout.Mobile.cshtml* file to *Views\\Shared\\\_Layout.iPhone.cshtml*.</span></span> <span data-ttu-id="49891-213">Open the new file and then change the title from `MVC5 Application (Mobile)` to `MVC5 Application (iPhone)`.</span><span class="sxs-lookup"><span data-stu-id="49891-213">Open the new file and then change the title from `MVC5 Application (Mobile)` to `MVC5 Application (iPhone)`.</span></span>

<span data-ttu-id="49891-214">Copy the *Views\\Home\\AllTags.Mobile.cshtml* file to *Views\\Home\\AllTags.iPhone.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="49891-214">Copy the *Views\\Home\\AllTags.Mobile.cshtml* file to *Views\\Home\\AllTags.iPhone.cshtml*.</span></span> <span data-ttu-id="49891-215">In the new file, change the `<h2>` element from "Tags (M)" to "Tags (iPhone)".</span><span class="sxs-lookup"><span data-stu-id="49891-215">In the new file, change the `<h2>` element from "Tags (M)" to "Tags (iPhone)".</span></span>

<span data-ttu-id="49891-216">Run the application.</span><span class="sxs-lookup"><span data-stu-id="49891-216">Run the application.</span></span> <span data-ttu-id="49891-217">Run a mobile browser emulator, make sure its user agent is set to "iPhone", and browse to the *AllTags* view.</span><span class="sxs-lookup"><span data-stu-id="49891-217">Run a mobile browser emulator, make sure its user agent is set to "iPhone", and browse to the *AllTags* view.</span></span> <span data-ttu-id="49891-218">If you are using the emulator in Internet Explorer 11 F12 developer tools, configure emulation to the following:</span><span class="sxs-lookup"><span data-stu-id="49891-218">If you are using the emulator in Internet Explorer 11 F12 developer tools, configure emulation to the following:</span></span>

* <span data-ttu-id="49891-219">Browser profile = **Windows Phone**</span><span class="sxs-lookup"><span data-stu-id="49891-219">Browser profile = **Windows Phone**</span></span>
* <span data-ttu-id="49891-220">User agent string =  **Custom**</span><span class="sxs-lookup"><span data-stu-id="49891-220">User agent string =  **Custom**</span></span>
* <span data-ttu-id="49891-221">Custom string = **Apple-iPhone5C1/1001.525**</span><span class="sxs-lookup"><span data-stu-id="49891-221">Custom string = **Apple-iPhone5C1/1001.525**</span></span>

<span data-ttu-id="49891-222">The following screenshot shows the *AllTags* view rendered in the emulator in Internet Explorer 11 F12 developer tools with the custom user agent string (this is an iPhone 5C user agent string).</span><span class="sxs-lookup"><span data-stu-id="49891-222">The following screenshot shows the *AllTags* view rendered in the emulator in Internet Explorer 11 F12 developer tools with the custom user agent string (this is an iPhone 5C user agent string).</span></span>

![][AllTagsIPhone_LayoutIPhone]

<span data-ttu-id="49891-223">In the mobile browser, select the **Speakers** link.</span><span class="sxs-lookup"><span data-stu-id="49891-223">In the mobile browser, select the **Speakers** link.</span></span> <span data-ttu-id="49891-224">Because there's not a mobile view (*AllSpeakers.Mobile.cshtml*), the default speakers view (*AllSpeakers.cshtml*) is rendered using the mobile layout view (*\_Layout.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="49891-224">Because there's not a mobile view (*AllSpeakers.Mobile.cshtml*), the default speakers view (*AllSpeakers.cshtml*) is rendered using the mobile layout view (*\_Layout.Mobile.cshtml*).</span></span> <span data-ttu-id="49891-225">As shown below, the title **MVC5 Application (Mobile)** is defined in *\_Layout.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="49891-225">As shown below, the title **MVC5 Application (Mobile)** is defined in *\_Layout.Mobile.cshtml*.</span></span>

![][AllSpeakers_LayoutMobile]

<span data-ttu-id="49891-226">You can globally disable a default (non-mobile) view from rendering inside a mobile layout by setting `RequireConsistentDisplayMode` to `true` in the *Views\\\_ViewStart.cshtml* file, like this:</span><span class="sxs-lookup"><span data-stu-id="49891-226">You can globally disable a default (non-mobile) view from rendering inside a mobile layout by setting `RequireConsistentDisplayMode` to `true` in the *Views\\\_ViewStart.cshtml* file, like this:</span></span>

    @{
        Layout = "~/Views/Shared/_Layout.cshtml";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = true;
    }

<span data-ttu-id="49891-227">When `RequireConsistentDisplayMode` is set to `true`, the mobile layout (*\_Layout.Mobile.cshtml*) is used only for mobile views (i.e. when the view file is of the form \***ViewName**.Mobile.cshtml\*).</span><span class="sxs-lookup"><span data-stu-id="49891-227">When `RequireConsistentDisplayMode` is set to `true`, the mobile layout (*\_Layout.Mobile.cshtml*) is used only for mobile views (i.e. when the view file is of the form \***ViewName**.Mobile.cshtml\*).</span></span> <span data-ttu-id="49891-228">You might want to set `RequireConsistentDisplayMode` to `true` if your mobile layout doesn't work well with your non-mobile views.</span><span class="sxs-lookup"><span data-stu-id="49891-228">You might want to set `RequireConsistentDisplayMode` to `true` if your mobile layout doesn't work well with your non-mobile views.</span></span> <span data-ttu-id="49891-229">The screenshot below shows how the *Speakers* page renders when `RequireConsistentDisplayMode` is set to `true` (without the string "(Mobile)" in the navigational bar at the top).</span><span class="sxs-lookup"><span data-stu-id="49891-229">The screenshot below shows how the *Speakers* page renders when `RequireConsistentDisplayMode` is set to `true` (without the string "(Mobile)" in the navigational bar at the top).</span></span>

![][AllSpeakers_LayoutMobileOverridden]

<span data-ttu-id="49891-230">You can disable consistent display mode in a specific view by setting `RequireConsistentDisplayMode` to `false` in the view file.</span><span class="sxs-lookup"><span data-stu-id="49891-230">You can disable consistent display mode in a specific view by setting `RequireConsistentDisplayMode` to `false` in the view file.</span></span> <span data-ttu-id="49891-231">The following markup in the *Views\\Home\\AllSpeakers.cshtml* file sets `RequireConsistentDisplayMode` to `false`:</span><span class="sxs-lookup"><span data-stu-id="49891-231">The following markup in the *Views\\Home\\AllSpeakers.cshtml* file sets `RequireConsistentDisplayMode` to `false`:</span></span>

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All speakers";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = false;
    }

<span data-ttu-id="49891-232">In this section we've seen how to create mobile layouts and views and how to create layouts and views for specific devices such as the iPhone.</span><span class="sxs-lookup"><span data-stu-id="49891-232">In this section we've seen how to create mobile layouts and views and how to create layouts and views for specific devices such as the iPhone.</span></span>
<span data-ttu-id="49891-233">However, the main advantage of the Bootstrap CSS framework is the responsive layout, which means that a single stylesheet can be applied across desktop, phone, and tablet browsers to create a consistent look and feel.</span><span class="sxs-lookup"><span data-stu-id="49891-233">However, the main advantage of the Bootstrap CSS framework is the responsive layout, which means that a single stylesheet can be applied across desktop, phone, and tablet browsers to create a consistent look and feel.</span></span> <span data-ttu-id="49891-234">In the next section you'll see how to leverage Bootstrap to create mobile-friendly views.</span><span class="sxs-lookup"><span data-stu-id="49891-234">In the next section you'll see how to leverage Bootstrap to create mobile-friendly views.</span></span>

## <a name="bkmk_Improvespeakerslist"></a> <span data-ttu-id="49891-235">Improve the Speakers List</span><span class="sxs-lookup"><span data-stu-id="49891-235">Improve the Speakers List</span></span>
<span data-ttu-id="49891-236">As you just saw, the *Speakers* view is readable, but the links are small and are difficult to tap on a mobile device.</span><span class="sxs-lookup"><span data-stu-id="49891-236">As you just saw, the *Speakers* view is readable, but the links are small and are difficult to tap on a mobile device.</span></span> <span data-ttu-id="49891-237">In this section, you'll make the *AllSpeakers* view mobile-friendly, which displays large, easy-to-tap links and contains a search box to quickly find speakers.</span><span class="sxs-lookup"><span data-stu-id="49891-237">In this section, you'll make the *AllSpeakers* view mobile-friendly, which displays large, easy-to-tap links and contains a search box to quickly find speakers.</span></span>

<span data-ttu-id="49891-238">You can use the Bootstrap [linked list group][linked list group] styling to improve the *Speakers* view.</span><span class="sxs-lookup"><span data-stu-id="49891-238">You can use the Bootstrap [linked list group][linked list group] styling to improve the *Speakers* view.</span></span> <span data-ttu-id="49891-239">In *Views\\Home\\AllSpeakers.cshtml*, replace the contents of the Razor file with the code below.</span><span class="sxs-lookup"><span data-stu-id="49891-239">In *Views\\Home\\AllSpeakers.cshtml*, replace the contents of the Razor file with the code below.</span></span>

     @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, "SessionsBySpeaker", new { speaker }, new { @class = "list-group-item" })
        }
    </div>

<span data-ttu-id="49891-240">The `class="list-group"` attribute in the `<div>` tag applies the Bootstrap list styling, and the `class="input-group-item"` attribute applies Bootstrap list item styling to each link.</span><span class="sxs-lookup"><span data-stu-id="49891-240">The `class="list-group"` attribute in the `<div>` tag applies the Bootstrap list styling, and the `class="input-group-item"` attribute applies Bootstrap list item styling to each link.</span></span>

<span data-ttu-id="49891-241">Refresh the mobile browser.</span><span class="sxs-lookup"><span data-stu-id="49891-241">Refresh the mobile browser.</span></span> <span data-ttu-id="49891-242">The updated view looks like this:</span><span class="sxs-lookup"><span data-stu-id="49891-242">The updated view looks like this:</span></span>

![][AllSpeakersFixed]

<span data-ttu-id="49891-243">The Bootstrap [linked list group][linked list group] styling makes the entire box for each link clickable, which is a much better user experience.</span><span class="sxs-lookup"><span data-stu-id="49891-243">The Bootstrap [linked list group][linked list group] styling makes the entire box for each link clickable, which is a much better user experience.</span></span> <span data-ttu-id="49891-244">Switch to the desktop view and observe the consistent look and feel.</span><span class="sxs-lookup"><span data-stu-id="49891-244">Switch to the desktop view and observe the consistent look and feel.</span></span>

![][AllSpeakersFixedDesktop]

<span data-ttu-id="49891-245">Although the mobile browser view has improved, it's difficult to navigate the long list of speakers.</span><span class="sxs-lookup"><span data-stu-id="49891-245">Although the mobile browser view has improved, it's difficult to navigate the long list of speakers.</span></span> <span data-ttu-id="49891-246">Bootstrap doesn't provide a search filter functionality out-of-the-box, but you can add it with a few lines of code.</span><span class="sxs-lookup"><span data-stu-id="49891-246">Bootstrap doesn't provide a search filter functionality out-of-the-box, but you can add it with a few lines of code.</span></span> <span data-ttu-id="49891-247">You will first add a search box to the view, then hook up with the JavaScript code for the filter function.</span><span class="sxs-lookup"><span data-stu-id="49891-247">You will first add a search box to the view, then hook up with the JavaScript code for the filter function.</span></span> <span data-ttu-id="49891-248">In *Views\\Home\\AllSpeakers.cshtml*, add a \<form\> tag just after the \<h2\> tag, as shown below:</span><span class="sxs-lookup"><span data-stu-id="49891-248">In *Views\\Home\\AllSpeakers.cshtml*, add a \<form\> tag just after the \<h2\> tag, as shown below:</span></span>

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <form class="input-group">
        <span class="input-group-addon"><span class="glyphicon glyphicon-search"></span></span>
        <input type="text" class="form-control" placeholder="Search speaker">
    </form>
    <br />
    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class = "list-group-item" })
        }
    </div>

<span data-ttu-id="49891-249">Notice that the `<form>` and `<input>` tags both have the Bootstrap styles applied to them.</span><span class="sxs-lookup"><span data-stu-id="49891-249">Notice that the `<form>` and `<input>` tags both have the Bootstrap styles applied to them.</span></span> <span data-ttu-id="49891-250">The `<span>` element adds a Bootstrap [glyphicon][glyphicon] to the search box.</span><span class="sxs-lookup"><span data-stu-id="49891-250">The `<span>` element adds a Bootstrap [glyphicon][glyphicon] to the search box.</span></span>

<span data-ttu-id="49891-251">In the *Scripts* folder, add a JavaScript file called *filter.js*.</span><span class="sxs-lookup"><span data-stu-id="49891-251">In the *Scripts* folder, add a JavaScript file called *filter.js*.</span></span> <span data-ttu-id="49891-252">Open the file and paste the following code into it:</span><span class="sxs-lookup"><span data-stu-id="49891-252">Open the file and paste the following code into it:</span></span>

    $(function () {

        // reset the search form when the page loads
        $("form").each(function () {
            this.reset();
        });

        // wire up the events to the <input> element for search/filter
        $("input").bind("keyup change", function () {
            var searchtxt = this.value.toLowerCase();
            var items = $(".list-group-item");

            // show all speakers that begin with the typed text and hide others
            for (var i = 0; i < items.length; i++) {
                var val = items[i].text.toLowerCase();
                val = val.substring(0, searchtxt.length);
                if (val == searchtxt) {
                    $(items[i]).show();
                }
                else {
                    $(items[i]).hide();
                }
            }
        });
    });

<span data-ttu-id="49891-253">You also need to include filter.js in your registered bundles.</span><span class="sxs-lookup"><span data-stu-id="49891-253">You also need to include filter.js in your registered bundles.</span></span> <span data-ttu-id="49891-254">Open *App\_Start\\BundleConfig.cs* and change the first bundles.</span><span class="sxs-lookup"><span data-stu-id="49891-254">Open *App\_Start\\BundleConfig.cs* and change the first bundles.</span></span> <span data-ttu-id="49891-255">Change the first `bundles.Add` statement (for the **jquery** bundle) to include *Scripts\\filter.js*, as follows:</span><span class="sxs-lookup"><span data-stu-id="49891-255">Change the first `bundles.Add` statement (for the **jquery** bundle) to include *Scripts\\filter.js*, as follows:</span></span>

     bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                "~/Scripts/jquery-{version}.js",
                "~/Scripts/filter.js"));

<span data-ttu-id="49891-256">The **jquery** bundle is already rendered by the default *\_Layout* view.</span><span class="sxs-lookup"><span data-stu-id="49891-256">The **jquery** bundle is already rendered by the default *\_Layout* view.</span></span> <span data-ttu-id="49891-257">Later, you can utilize the same JavaScript code to apply the filter functionality to other list views.</span><span class="sxs-lookup"><span data-stu-id="49891-257">Later, you can utilize the same JavaScript code to apply the filter functionality to other list views.</span></span>

<span data-ttu-id="49891-258">Refresh the mobile browser and go to the *AllSpeakers* view.</span><span class="sxs-lookup"><span data-stu-id="49891-258">Refresh the mobile browser and go to the *AllSpeakers* view.</span></span> <span data-ttu-id="49891-259">In the search box, type "sc".</span><span class="sxs-lookup"><span data-stu-id="49891-259">In the search box, type "sc".</span></span> <span data-ttu-id="49891-260">The speakers list should now be filtered according to your search string.</span><span class="sxs-lookup"><span data-stu-id="49891-260">The speakers list should now be filtered according to your search string.</span></span>

![][AllSpeakersFixedSearchBySC]

## <a name="bkmk_improvetags"></a> <span data-ttu-id="49891-261">Improve the Tags List</span><span class="sxs-lookup"><span data-stu-id="49891-261">Improve the Tags List</span></span>
<span data-ttu-id="49891-262">Like the *Speakers* view, the *Tags* view is readable, but the links are small and difficult to tap on a mobile device.</span><span class="sxs-lookup"><span data-stu-id="49891-262">Like the *Speakers* view, the *Tags* view is readable, but the links are small and difficult to tap on a mobile device.</span></span> <span data-ttu-id="49891-263">You can fix the *Tags* view the same way you fix the *Speakers* view, if you use the code changes described earlier, but with the following `Html.ActionLink` method syntax in *Views\\Home\\AllTags.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="49891-263">You can fix the *Tags* view the same way you fix the *Speakers* view, if you use the code changes described earlier, but with the following `Html.ActionLink` method syntax in *Views\\Home\\AllTags.cshtml*:</span></span>

    @Html.ActionLink(tag, 
                     "SessionsByTag", 
                     new { tag }, 
                     new { @class = "list-group-item" })

<span data-ttu-id="49891-264">The refreshed desktop browser looks as follows:</span><span class="sxs-lookup"><span data-stu-id="49891-264">The refreshed desktop browser looks as follows:</span></span>

![][AllTagsFixedDesktop]

<span data-ttu-id="49891-265">And the refreshed mobile browser looks as follows:</span><span class="sxs-lookup"><span data-stu-id="49891-265">And the refreshed mobile browser looks as follows:</span></span> 

![][AllTagsFixed]

> [!NOTE]
> <span data-ttu-id="49891-266">If you notice that the original list formatting is still there in the mobile browser and wonder what happened to your nice Bootstrap styling, this is an artifact of your earlier action to create mobile specific views.</span><span class="sxs-lookup"><span data-stu-id="49891-266">If you notice that the original list formatting is still there in the mobile browser and wonder what happened to your nice Bootstrap styling, this is an artifact of your earlier action to create mobile specific views.</span></span> <span data-ttu-id="49891-267">However, now that you are using the Bootstrap CSS framework to create a responsive web design, go head and remove these mobile-specific views and the mobile-specific layout views.</span><span class="sxs-lookup"><span data-stu-id="49891-267">However, now that you are using the Bootstrap CSS framework to create a responsive web design, go head and remove these mobile-specific views and the mobile-specific layout views.</span></span> <span data-ttu-id="49891-268">Once you have done so, the refreshed mobile browser will show the Bootstrap styling.</span><span class="sxs-lookup"><span data-stu-id="49891-268">Once you have done so, the refreshed mobile browser will show the Bootstrap styling.</span></span>
> 
> 

## <a name="bkmk_improvedates"></a> <span data-ttu-id="49891-269">Improve the Dates List</span><span class="sxs-lookup"><span data-stu-id="49891-269">Improve the Dates List</span></span>
<span data-ttu-id="49891-270">You can improve the *Dates* view like you improved the *Speakers* and *Tags* views if you use the code changes described earlier, but with the following `Html.ActionLink` method syntax in *Views\\Home\\AllDates.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="49891-270">You can improve the *Dates* view like you improved the *Speakers* and *Tags* views if you use the code changes described earlier, but with the following `Html.ActionLink` method syntax in *Views\\Home\\AllDates.cshtml*:</span></span>

    @Html.ActionLink(date.ToString("ddd, MMM dd, h:mm tt"), 
                     "SessionsByDate", 
                     new { date }, 
                     new { @class = "list-group-item" })

<span data-ttu-id="49891-271">You will get a refreshed mobile browser view like this:</span><span class="sxs-lookup"><span data-stu-id="49891-271">You will get a refreshed mobile browser view like this:</span></span>

![][AllDatesFixed]

<span data-ttu-id="49891-272">You can further improve the *Dates* view by organizing the date-time values by date.</span><span class="sxs-lookup"><span data-stu-id="49891-272">You can further improve the *Dates* view by organizing the date-time values by date.</span></span> <span data-ttu-id="49891-273">This can be done with the Bootstrap [panels][panels] styling.</span><span class="sxs-lookup"><span data-stu-id="49891-273">This can be done with the Bootstrap [panels][panels] styling.</span></span> <span data-ttu-id="49891-274">Replace the contents of the *Views\\Home\\AllDates.cshtml* file with the following code:</span><span class="sxs-lookup"><span data-stu-id="49891-274">Replace the contents of the *Views\\Home\\AllDates.cshtml* file with the following code:</span></span>

    @model IEnumerable<DateTime>

    @{
        ViewBag.Title = "All Dates";
    }

    <h2>Dates</h2>

    @foreach (var dategroup in Model.GroupBy(x=>x.Date))
    {
        <div class="panel panel-primary">
            <div class="panel-heading">
                @dategroup.Key.ToString("ddd, MMM dd")
            </div>
            <div class="panel-body list-group">
                @foreach (var date in dategroup)
                {
                    @Html.ActionLink(date.ToString("h:mm tt"), 
                                     "SessionsByDate", 
                                     new { date }, 
                                     new { @class = "list-group-item" })
                }
            </div>
        </div>
    }

<span data-ttu-id="49891-275">This code creates a separate `<div class="panel panel-primary">` tag for each distinct date in the list, and uses the [linked list group][linked list group] for the respective links as before.</span><span class="sxs-lookup"><span data-stu-id="49891-275">This code creates a separate `<div class="panel panel-primary">` tag for each distinct date in the list, and uses the [linked list group][linked list group] for the respective links as before.</span></span> <span data-ttu-id="49891-276">Here's what the mobile browser looks like when this code runs:</span><span class="sxs-lookup"><span data-stu-id="49891-276">Here's what the mobile browser looks like when this code runs:</span></span>

![][AllDatesFixed2]

<span data-ttu-id="49891-277">Switch to the desktop browser.</span><span class="sxs-lookup"><span data-stu-id="49891-277">Switch to the desktop browser.</span></span> <span data-ttu-id="49891-278">Again, note the consistent look.</span><span class="sxs-lookup"><span data-stu-id="49891-278">Again, note the consistent look.</span></span>

![][AllDatesFixed2Desktop]

## <a name="bkmk_improvesessionstable"></a> <span data-ttu-id="49891-279">Improve the SessionsTable View</span><span class="sxs-lookup"><span data-stu-id="49891-279">Improve the SessionsTable View</span></span>
<span data-ttu-id="49891-280">In this section, you'll make the *SessionsTable* view more mobile-friendly.</span><span class="sxs-lookup"><span data-stu-id="49891-280">In this section, you'll make the *SessionsTable* view more mobile-friendly.</span></span> <span data-ttu-id="49891-281">This change is more extensive the previous changes.</span><span class="sxs-lookup"><span data-stu-id="49891-281">This change is more extensive the previous changes.</span></span>

<span data-ttu-id="49891-282">In the mobile browser, tap the **Tag** button, then enter `asp` in the search box.</span><span class="sxs-lookup"><span data-stu-id="49891-282">In the mobile browser, tap the **Tag** button, then enter `asp` in the search box.</span></span>

![][AllTagsFixedSearchByASP]

<span data-ttu-id="49891-283">Tap the **ASP.NET** link.</span><span class="sxs-lookup"><span data-stu-id="49891-283">Tap the **ASP.NET** link.</span></span>

![][SessionsTableTagASP.NET]

<span data-ttu-id="49891-284">As you can see, the display is formatted as a table, which is currently designed to be viewed in the desktop browser.</span><span class="sxs-lookup"><span data-stu-id="49891-284">As you can see, the display is formatted as a table, which is currently designed to be viewed in the desktop browser.</span></span> <span data-ttu-id="49891-285">However, it's a little bit difficult to read on a mobile browser.</span><span class="sxs-lookup"><span data-stu-id="49891-285">However, it's a little bit difficult to read on a mobile browser.</span></span> <span data-ttu-id="49891-286">To fix this, open *Views\\Home\\SessionsTable.cshtml* and then replace the contents of the file with the following code:</span><span class="sxs-lookup"><span data-stu-id="49891-286">To fix this, open *Views\\Home\\SessionsTable.cshtml* and then replace the contents of the file with the following code:</span></span>

    @model IEnumerable<Mvc5Mobile.Models.Session>

    <h2>@ViewBag.Title</h2>

    <div class="container">
        <div class="row">
            @foreach (var session in Model)
            {
                <div class="col-md-4">
                    <div class="list-group">
                        @Html.ActionLink(session.Title, 
                                         "SessionByCode", 
                                         new { session.Code }, 
                                         new { @class="list-group-item active" })
                        <div class="list-group-item">
                            <div class="list-group-item-text">
                                @Html.Partial("_SpeakersLinks", session)
                            </div>
                            <div class="list-group-item-info">
                                @session.DateText
                            </div>
                            <div class="list-group-item-info small hidden-xs">
                                @Html.Partial("_TagsLinks", session)
                            </div>
                        </div>
                    </div>
                </div>
            }
        </div>
    </div>

<span data-ttu-id="49891-287">The code does 3 things:</span><span class="sxs-lookup"><span data-stu-id="49891-287">The code does 3 things:</span></span>

* <span data-ttu-id="49891-288">uses the Bootstrap [custom linked list group][custom linked list group] to format the session information vertically, so that all this information is readable on a mobile browser (using classes such as list-group-item-text)</span><span class="sxs-lookup"><span data-stu-id="49891-288">uses the Bootstrap [custom linked list group][custom linked list group] to format the session information vertically, so that all this information is readable on a mobile browser (using classes such as list-group-item-text)</span></span>
* <span data-ttu-id="49891-289">applies the [grid system][grid system] to the layout, so that the session items flow horizontally in the desktop browser and vertically in the mobile browser (using the col-md-4 class)</span><span class="sxs-lookup"><span data-stu-id="49891-289">applies the [grid system][grid system] to the layout, so that the session items flow horizontally in the desktop browser and vertically in the mobile browser (using the col-md-4 class)</span></span>
* <span data-ttu-id="49891-290">uses the [responsive utilities][responsive utilities] to hide the session tags when viewed in the mobile browser (using the hidden-xs class)</span><span class="sxs-lookup"><span data-stu-id="49891-290">uses the [responsive utilities][responsive utilities] to hide the session tags when viewed in the mobile browser (using the hidden-xs class)</span></span>

<span data-ttu-id="49891-291">You can also tap a title link to go to the respective session.</span><span class="sxs-lookup"><span data-stu-id="49891-291">You can also tap a title link to go to the respective session.</span></span> <span data-ttu-id="49891-292">The image below reflects the code changes.</span><span class="sxs-lookup"><span data-stu-id="49891-292">The image below reflects the code changes.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="49891-293">The Bootstrap grid system that you applied automatically arranges the sessions vertically in the mobile browser.</span><span class="sxs-lookup"><span data-stu-id="49891-293">The Bootstrap grid system that you applied automatically arranges the sessions vertically in the mobile browser.</span></span> <span data-ttu-id="49891-294">Also, notice that the tags are not shown.</span><span class="sxs-lookup"><span data-stu-id="49891-294">Also, notice that the tags are not shown.</span></span> <span data-ttu-id="49891-295">Switch to the desktop browser.</span><span class="sxs-lookup"><span data-stu-id="49891-295">Switch to the desktop browser.</span></span>

![][SessionsTableFixedTagASP.NETDesktop]

<span data-ttu-id="49891-296">In the desktop browser, notice that the tags are now displayed.</span><span class="sxs-lookup"><span data-stu-id="49891-296">In the desktop browser, notice that the tags are now displayed.</span></span> <span data-ttu-id="49891-297">Also, you can see that the Bootstrap grid system you applied arranges the session items in two columns.</span><span class="sxs-lookup"><span data-stu-id="49891-297">Also, you can see that the Bootstrap grid system you applied arranges the session items in two columns.</span></span> <span data-ttu-id="49891-298">If you enlarge the browser, you will see that the arrangement changes to three columns.</span><span class="sxs-lookup"><span data-stu-id="49891-298">If you enlarge the browser, you will see that the arrangement changes to three columns.</span></span>

## <a name="bkmk_improvesessionbycode"></a> <span data-ttu-id="49891-299">Improve the SessionByCode View</span><span class="sxs-lookup"><span data-stu-id="49891-299">Improve the SessionByCode View</span></span>
<span data-ttu-id="49891-300">Finally, you'll fix the *SessionByCode* view to make it mobile-friendly.</span><span class="sxs-lookup"><span data-stu-id="49891-300">Finally, you'll fix the *SessionByCode* view to make it mobile-friendly.</span></span>

<span data-ttu-id="49891-301">In the mobile browser, tap the **Tag** button, then enter `asp` in the search box.</span><span class="sxs-lookup"><span data-stu-id="49891-301">In the mobile browser, tap the **Tag** button, then enter `asp` in the search box.</span></span>

![][AllTagsFixedSearchByASP]

<span data-ttu-id="49891-302">Tap the **ASP.NET** link.</span><span class="sxs-lookup"><span data-stu-id="49891-302">Tap the **ASP.NET** link.</span></span> <span data-ttu-id="49891-303">Sessions for the ASP.NET tag are displayed.</span><span class="sxs-lookup"><span data-stu-id="49891-303">Sessions for the ASP.NET tag are displayed.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="49891-304">Choose the **Building a Single Page Application with ASP.NET and AngularJS** link.</span><span class="sxs-lookup"><span data-stu-id="49891-304">Choose the **Building a Single Page Application with ASP.NET and AngularJS** link.</span></span>

![][SessionByCode3-644]

<span data-ttu-id="49891-305">The default desktop view is fine, but you can improve the look easily by using some Bootstrap GUI components.</span><span class="sxs-lookup"><span data-stu-id="49891-305">The default desktop view is fine, but you can improve the look easily by using some Bootstrap GUI components.</span></span>

<span data-ttu-id="49891-306">Open *Views\\Home\\SessionByCode.cshtml* and replace the contents with the following markup:</span><span class="sxs-lookup"><span data-stu-id="49891-306">Open *Views\\Home\\SessionByCode.cshtml* and replace the contents with the following markup:</span></span>

    @model Mvc5Mobile.Models.Session

    @{
        ViewBag.Title = "Session details";
    }
    <h3>@Model.Title (@Model.Code)</h3>
    <p>
        <strong>@Model.DateText</strong> in <strong>@Model.Room</strong>
    </p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Speakers
        </div>
        @foreach (var speaker in Model.Speakers)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class="panel-body" })
        }
    </div>

    <p>@Model.Abstract</p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Tags
        </div>
        @foreach (var tag in Model.Tags)
        {
            @Html.ActionLink(tag, 
                             "SessionsByTag", 
                             new { tag }, 
                             new { @class = "panel-body" })
        }
    </div>

<span data-ttu-id="49891-307">The new markup uses Bootstrap panels styling to improve the mobile view.</span><span class="sxs-lookup"><span data-stu-id="49891-307">The new markup uses Bootstrap panels styling to improve the mobile view.</span></span> 

<span data-ttu-id="49891-308">Refresh the mobile browser.</span><span class="sxs-lookup"><span data-stu-id="49891-308">Refresh the mobile browser.</span></span> <span data-ttu-id="49891-309">The following image reflects the code changes that you just made:</span><span class="sxs-lookup"><span data-stu-id="49891-309">The following image reflects the code changes that you just made:</span></span>

![][SessionByCodeFixed3-644]

## <a name="wrap-up-and-review"></a><span data-ttu-id="49891-310">Wrap Up and Review</span><span class="sxs-lookup"><span data-stu-id="49891-310">Wrap Up and Review</span></span>
<span data-ttu-id="49891-311">This tutorial has shown you how to use ASP.NET MVC 5 to develop mobile-friendly Web applications.</span><span class="sxs-lookup"><span data-stu-id="49891-311">This tutorial has shown you how to use ASP.NET MVC 5 to develop mobile-friendly Web applications.</span></span> <span data-ttu-id="49891-312">These include:</span><span class="sxs-lookup"><span data-stu-id="49891-312">These include:</span></span>

* <span data-ttu-id="49891-313">Deploy an ASP.NET MVC 5 application to an App Service web app</span><span class="sxs-lookup"><span data-stu-id="49891-313">Deploy an ASP.NET MVC 5 application to an App Service web app</span></span>
* <span data-ttu-id="49891-314">Use Bootstrap to create responsive web layout in your MVC 5 application</span><span class="sxs-lookup"><span data-stu-id="49891-314">Use Bootstrap to create responsive web layout in your MVC 5 application</span></span>
* <span data-ttu-id="49891-315">Override layout, views, and partial views, both globally and for an individual view</span><span class="sxs-lookup"><span data-stu-id="49891-315">Override layout, views, and partial views, both globally and for an individual view</span></span>
* <span data-ttu-id="49891-316">Control layout and partial override enforcement using the `RequireConsistentDisplayMode` property</span><span class="sxs-lookup"><span data-stu-id="49891-316">Control layout and partial override enforcement using the `RequireConsistentDisplayMode` property</span></span>
* <span data-ttu-id="49891-317">Create views that target specific browsers, such as the iPhone browser</span><span class="sxs-lookup"><span data-stu-id="49891-317">Create views that target specific browsers, such as the iPhone browser</span></span>
* <span data-ttu-id="49891-318">Apply Bootstrap styling in Razor code</span><span class="sxs-lookup"><span data-stu-id="49891-318">Apply Bootstrap styling in Razor code</span></span>

## <a name="see-also"></a><span data-ttu-id="49891-319">See Also</span><span class="sxs-lookup"><span data-stu-id="49891-319">See Also</span></span>
* [<span data-ttu-id="49891-320">9 basic principles of responsive web design</span><span class="sxs-lookup"><span data-stu-id="49891-320">9 basic principles of responsive web design</span></span>](http://blog.froont.com/9-basic-principles-of-responsive-web-design/)
* <span data-ttu-id="49891-321">[Bootstrap][BootstrapSite]</span><span class="sxs-lookup"><span data-stu-id="49891-321">[Bootstrap][BootstrapSite]</span></span>
* <span data-ttu-id="49891-322">[Official Bootstrap Blog][Official Bootstrap Blog]</span><span class="sxs-lookup"><span data-stu-id="49891-322">[Official Bootstrap Blog][Official Bootstrap Blog]</span></span>
* <span data-ttu-id="49891-323">[Twitter Bootstrap Tutorial from Tutorial Republic][Twitter Bootstrap Tutorial from Tutorial Republic]</span><span class="sxs-lookup"><span data-stu-id="49891-323">[Twitter Bootstrap Tutorial from Tutorial Republic][Twitter Bootstrap Tutorial from Tutorial Republic]</span></span>
* <span data-ttu-id="49891-324">[The Bootstrap Playground][The Bootstrap Playground]</span><span class="sxs-lookup"><span data-stu-id="49891-324">[The Bootstrap Playground][The Bootstrap Playground]</span></span>
* <span data-ttu-id="49891-325">[W3C Recommendation Mobile Web Application Best Practices][W3C Recommendation Mobile Web Application Best Practices]</span><span class="sxs-lookup"><span data-stu-id="49891-325">[W3C Recommendation Mobile Web Application Best Practices][W3C Recommendation Mobile Web Application Best Practices]</span></span>
* <span data-ttu-id="49891-326">[W3C Candidate Recommendation for media queries][W3C Candidate Recommendation for media queries]</span><span class="sxs-lookup"><span data-stu-id="49891-326">[W3C Candidate Recommendation for media queries][W3C Candidate Recommendation for media queries]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="49891-327">What's changed</span><span class="sxs-lookup"><span data-stu-id="49891-327">What's changed</span></span>
* <span data-ttu-id="49891-328">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="49891-328">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- Internal Links -->
[Deploy the starter project to an Azure web app]: #bkmk_DeployStarterProject
[Bootstrap CSS Framework]: #bkmk_bootstrap
[Override the Views, Layouts, and Partial Views]: #bkmk_overrideviews
[Create Browser-Specific Views]:#bkmk_browserviews
[Improve the Speakers List]: #bkmk_Improvespeakerslist
[Improve the Tags List]: #bkmk_improvetags
[Improve the Dates List]: #bkmk_improvedates
[Improve the SessionsTable View]: #bkmk_improvesessionstable
[Improve the SessionByCode View]: #bkmk_improvesessionbycode

<!-- External Links -->
[Visual Studio Express 2013]: http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-web
[Visual Studio 2015]: https://www.visualstudio.com/downloads/download-visual-studio-vs
[AzureSDKVs2013]: http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409
[Fiddler]: http://www.fiddler2.com/fiddler2/
[EmulatorIE11]: http://msdn.microsoft.com/library/ie/dn255001.aspx
[EmulatorChrome]: https://developers.google.com/chrome-developer-tools/docs/mobile-emulation
[EmulatorOpera]: http://www.opera.com/developer/tools/mobile/
[StarterProject]: http://go.microsoft.com/fwlink/?LinkID=398780&clcid=0x409
[CompletedProject]: http://go.microsoft.com/fwlink/?LinkID=398781&clcid=0x409
[BootstrapSite]: http://getbootstrap.com/
[WebPIAzureSdk23NetVS13]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/WebPIAzureSdk23NetVS13.png
[linked list group]: http://getbootstrap.com/components/#list-group-linked
[glyphicon]: http://getbootstrap.com/components/#glyphicons
[panels]: http://getbootstrap.com/components/#panels
[custom linked list group]: http://getbootstrap.com/components/#list-group-custom-content
[grid system]: http://getbootstrap.com/css/#grid
[responsive utilities]: http://getbootstrap.com/css/#responsive-utilities
[Official Bootstrap Blog]: http://blog.getbootstrap.com/
[Twitter Bootstrap Tutorial from Tutorial Republic]: http://www.tutorialrepublic.com/twitter-bootstrap-tutorial/
[The Bootstrap Playground]: http://www.bootply.com/
[W3C Recommendation Mobile Web Application Best Practices]: http://www.w3.org/TR/mwabp/
[W3C Candidate Recommendation for media queries]: http://www.w3.org/TR/css3-mediaqueries/

<!-- Images -->
[DeployClickPublish]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-1.png
[DeployClickWebSites]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-2.png
[DeploySignIn]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-3.png
[DeployUsername]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-4.png
[DeployPassword]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-5.png
[DeployNewWebsite]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-6.png
[DeploySiteSettings]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7.png
[DeployPublishSite]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-8.png
[MobileHomePage]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/mobile-home-page.png
[FixedSessionsByTag]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-Fixed.png
[AllTags]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags.png
[SessionsByTagASP.NET]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET.png
[SessionsByTagASP.NETNoBootstrap]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-NoBootstrap.png
[AllTagsMobile_LayoutMobile]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile.png
[AllTagsMobile_LayoutMobileDesktop]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile-Desktop.png
[ResolveDefaultDisplayMode]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/Resolve-DefaultDisplayMode.png
[AllTagsIPhone_LayoutIPhone]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsIPhone-_LayoutIPhone.png
[AllSpeakers_LayoutMobile]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile.png
[AllSpeakers_LayoutMobileOverridden]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile-Overridden.png
[AllSpeakersFixed]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed.png
[AllSpeakersFixedDesktop]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-Desktop.png
[AllSpeakersFixedSearchBySC]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-SearchBySC.png
[AllTagsFixedDesktop]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-Desktop.png 
[AllTagsFixed]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed.png
[AllDatesFixed]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed.png
[AllDatesFixed2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2.png
[AllDatesFixed2Desktop]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2-Desktop.png
[AllTagsFixedSearchByASP]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-SearchByASP.png
[SessionsTableTagASP.NET]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Tag-ASP.NET.png
[SessionsTableFixedTagASP.NETDesktop]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Fixed-Tag-ASP.NET-Desktop.png
[SessionByCode3-644]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-3-644.png
[SessionByCodeFixed3-644]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-Fixed-3-644.png
































