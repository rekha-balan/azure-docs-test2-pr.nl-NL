---
title: Troubleshoot a web app in Azure App Service using Visual Studio
description: Learn how to troubleshoot an Azure web app by using remote debugging, tracing, and logging tools that are built in to Visual Studio 2013.
services: app-service
documentationcenter: .net
author: tdykstra
manager: erikre
editor: ''
ms.assetid: def8e481-7803-4371-aa55-64025d116c97
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/29/2016
ms.author: rachelap
ms.openlocfilehash: 15fef4f707979cba69bb2242f9450a76b0f8a42d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669639"
---
# <a name="troubleshoot-a-web-app-in-azure-app-service-using-visual-studio"></a><span data-ttu-id="b04a7-103">Troubleshoot a web app in Azure App Service using Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b04a7-103">Troubleshoot a web app in Azure App Service using Visual Studio</span></span>
## <a name="overview"></a><span data-ttu-id="b04a7-104">Overview</span><span class="sxs-lookup"><span data-stu-id="b04a7-104">Overview</span></span>
<span data-ttu-id="b04a7-105">This tutorial shows how to use Visual Studio tools that help debug a web app in [App Service](http://go.microsoft.com/fwlink/?LinkId=529714), by running in [debug mode](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) remotely or by viewing application logs and web server logs.</span><span class="sxs-lookup"><span data-stu-id="b04a7-105">This tutorial shows how to use Visual Studio tools that help debug a web app in [App Service](http://go.microsoft.com/fwlink/?LinkId=529714), by running in [debug mode](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) remotely or by viewing application logs and web server logs.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="b04a7-106">You'll learn:</span><span class="sxs-lookup"><span data-stu-id="b04a7-106">You'll learn:</span></span>

* <span data-ttu-id="b04a7-107">Which Azure web app management functions are available in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b04a7-107">Which Azure web app management functions are available in Visual Studio.</span></span>
* <span data-ttu-id="b04a7-108">How to use Visual Studio remote view to make quick changes in a remote web app.</span><span class="sxs-lookup"><span data-stu-id="b04a7-108">How to use Visual Studio remote view to make quick changes in a remote web app.</span></span>
* <span data-ttu-id="b04a7-109">How to run debug mode remotely while a project is running in Azure, both for a web app and for a WebJob.</span><span class="sxs-lookup"><span data-stu-id="b04a7-109">How to run debug mode remotely while a project is running in Azure, both for a web app and for a WebJob.</span></span>
* <span data-ttu-id="b04a7-110">How to create application trace logs and view them while the application is creating them.</span><span class="sxs-lookup"><span data-stu-id="b04a7-110">How to create application trace logs and view them while the application is creating them.</span></span>
* <span data-ttu-id="b04a7-111">How to view web server logs, including detailed error messages and failed request tracing.</span><span class="sxs-lookup"><span data-stu-id="b04a7-111">How to view web server logs, including detailed error messages and failed request tracing.</span></span>
* <span data-ttu-id="b04a7-112">How to send diagnostic logs to an Azure Storage account and view them there.</span><span class="sxs-lookup"><span data-stu-id="b04a7-112">How to send diagnostic logs to an Azure Storage account and view them there.</span></span>

<span data-ttu-id="b04a7-113">If you have Visual Studio Ultimate, you can also use [IntelliTrace](http://msdn.microsoft.com/library/vstudio/dd264915.aspx) for debugging.</span><span class="sxs-lookup"><span data-stu-id="b04a7-113">If you have Visual Studio Ultimate, you can also use [IntelliTrace](http://msdn.microsoft.com/library/vstudio/dd264915.aspx) for debugging.</span></span> <span data-ttu-id="b04a7-114">IntelliTrace is not covered in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="b04a7-114">IntelliTrace is not covered in this tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b04a7-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b04a7-115">Prerequisites</span></span>
<span data-ttu-id="b04a7-116">This tutorial works with the development environment, web project, and Azure web app that you set up in [Get started with Azure and ASP.NET][GetStarted].</span><span class="sxs-lookup"><span data-stu-id="b04a7-116">This tutorial works with the development environment, web project, and Azure web app that you set up in [Get started with Azure and ASP.NET][GetStarted].</span></span> <span data-ttu-id="b04a7-117">For the WebJobs sections, you'll need the application that you create in [Get Started with the Azure WebJobs SDK][GetStartedWJ].</span><span class="sxs-lookup"><span data-stu-id="b04a7-117">For the WebJobs sections, you'll need the application that you create in [Get Started with the Azure WebJobs SDK][GetStartedWJ].</span></span>

<span data-ttu-id="b04a7-118">The code samples shown in this tutorial are for a C# MVC web application, but the troubleshooting procedures are the same for Visual Basic and Web Forms applications.</span><span class="sxs-lookup"><span data-stu-id="b04a7-118">The code samples shown in this tutorial are for a C# MVC web application, but the troubleshooting procedures are the same for Visual Basic and Web Forms applications.</span></span>

<span data-ttu-id="b04a7-119">The tutorial assumes you're using Visual Studio 2015 or 2013.</span><span class="sxs-lookup"><span data-stu-id="b04a7-119">The tutorial assumes you're using Visual Studio 2015 or 2013.</span></span> <span data-ttu-id="b04a7-120">If you're using Visual Studio 2013, the WebJobs features require [Update 4](http://go.microsoft.com/fwlink/?LinkID=510314) or later.</span><span class="sxs-lookup"><span data-stu-id="b04a7-120">If you're using Visual Studio 2013, the WebJobs features require [Update 4](http://go.microsoft.com/fwlink/?LinkID=510314) or later.</span></span>

<span data-ttu-id="b04a7-121">The streaming logs feature only works for applications that target .NET Framework 4 or later.</span><span class="sxs-lookup"><span data-stu-id="b04a7-121">The streaming logs feature only works for applications that target .NET Framework 4 or later.</span></span>

## <a name="sitemanagement"></a><span data-ttu-id="b04a7-122">Web app configuration and management</span><span class="sxs-lookup"><span data-stu-id="b04a7-122">Web app configuration and management</span></span>
<span data-ttu-id="b04a7-123">Visual Studio provides access to a subset of the web app management functions and configuration settings available in the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span><span class="sxs-lookup"><span data-stu-id="b04a7-123">Visual Studio provides access to a subset of the web app management functions and configuration settings available in the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="b04a7-124">In this section you'll see what's available by using **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-124">In this section you'll see what's available by using **Server Explorer**.</span></span> <span data-ttu-id="b04a7-125">To see the latest Azure integration features, try out **Cloud Explorer** also.</span><span class="sxs-lookup"><span data-stu-id="b04a7-125">To see the latest Azure integration features, try out **Cloud Explorer** also.</span></span> <span data-ttu-id="b04a7-126">You can open both windows from the **View** menu.</span><span class="sxs-lookup"><span data-stu-id="b04a7-126">You can open both windows from the **View** menu.</span></span>

1. <span data-ttu-id="b04a7-127">If you aren't already signed in to Azure in Visual Studio, click the **Connect to Azure** button in **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-127">If you aren't already signed in to Azure in Visual Studio, click the **Connect to Azure** button in **Server Explorer**.</span></span>

    <span data-ttu-id="b04a7-128">An alternative is to install a management certificate that enables access to your account.</span><span class="sxs-lookup"><span data-stu-id="b04a7-128">An alternative is to install a management certificate that enables access to your account.</span></span> <span data-ttu-id="b04a7-129">If you choose to install a certificate, right-click the **Azure** node in **Server Explorer**, and then click **Manage and Filter Subscriptions** in the context menu.</span><span class="sxs-lookup"><span data-stu-id="b04a7-129">If you choose to install a certificate, right-click the **Azure** node in **Server Explorer**, and then click **Manage and Filter Subscriptions** in the context menu.</span></span> <span data-ttu-id="b04a7-130">In the **Manage Azure Subscriptions** dialog box, click the **Certificates** tab, and then click **Import**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-130">In the **Manage Azure Subscriptions** dialog box, click the **Certificates** tab, and then click **Import**.</span></span> <span data-ttu-id="b04a7-131">Follow the directions to download and then import a subscription file (also called a *.publishsettings* file) for your Azure account.</span><span class="sxs-lookup"><span data-stu-id="b04a7-131">Follow the directions to download and then import a subscription file (also called a *.publishsettings* file) for your Azure account.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b04a7-132">If you download a subscription file, save it to a folder outside your source code directories (for example, in the Downloads folder), and then delete it once the import has completed.</span><span class="sxs-lookup"><span data-stu-id="b04a7-132">If you download a subscription file, save it to a folder outside your source code directories (for example, in the Downloads folder), and then delete it once the import has completed.</span></span> <span data-ttu-id="b04a7-133">A malicious user who gains access to the subscription file can edit, create, and delete your Azure services.</span><span class="sxs-lookup"><span data-stu-id="b04a7-133">A malicious user who gains access to the subscription file can edit, create, and delete your Azure services.</span></span>
   >
   >

    <span data-ttu-id="b04a7-134">For more information about connecting to Azure resources from Visual Studio, see [Manage Accounts, Subscriptions, and Administrative Roles](http://go.microsoft.com/fwlink/?LinkId=324796#BKMK_AccountVCert).</span><span class="sxs-lookup"><span data-stu-id="b04a7-134">For more information about connecting to Azure resources from Visual Studio, see [Manage Accounts, Subscriptions, and Administrative Roles](http://go.microsoft.com/fwlink/?LinkId=324796#BKMK_AccountVCert).</span></span>
2. <span data-ttu-id="b04a7-135">In **Server Explorer**, expand **Azure** and expand **App Service**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-135">In **Server Explorer**, expand **Azure** and expand **App Service**.</span></span>
3. <span data-ttu-id="b04a7-136">Expand the resource group that includes the web app that you created in [Getting started with Azure and ASP.NET][GetStarted], and then right-click the web app node and click **View Settings**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-136">Expand the resource group that includes the web app that you created in [Getting started with Azure and ASP.NET][GetStarted], and then right-click the web app node and click **View Settings**.</span></span>

    ![View Settings in Server Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-viewsettings.png)

    <span data-ttu-id="b04a7-138">The **Azure Web App** tab appears, and you can see there the web app management and configuration tasks that are available in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b04a7-138">The **Azure Web App** tab appears, and you can see there the web app management and configuration tasks that are available in Visual Studio.</span></span>

    ![Azure Web App window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-configtab.png)

    <span data-ttu-id="b04a7-140">In this tutorial you'll be using the logging and tracing drop-downs.</span><span class="sxs-lookup"><span data-stu-id="b04a7-140">In this tutorial you'll be using the logging and tracing drop-downs.</span></span> <span data-ttu-id="b04a7-141">You'll also use remote debugging but you'll use a different method to enable it.</span><span class="sxs-lookup"><span data-stu-id="b04a7-141">You'll also use remote debugging but you'll use a different method to enable it.</span></span>

    <span data-ttu-id="b04a7-142">For information about the App Settings and Connection Strings boxes in this window, see [Azure Web Apps: How Application Strings and Connection Strings Work](http://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx).</span><span class="sxs-lookup"><span data-stu-id="b04a7-142">For information about the App Settings and Connection Strings boxes in this window, see [Azure Web Apps: How Application Strings and Connection Strings Work](http://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx).</span></span>

    <span data-ttu-id="b04a7-143">If you want to perform a web app management task that can't be done in this window, click **Open in Management Portal** to open a browser window to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b04a7-143">If you want to perform a web app management task that can't be done in this window, click **Open in Management Portal** to open a browser window to the Azure portal.</span></span>

## <a name="remoteview"></a><span data-ttu-id="b04a7-144">Access web app files in Server Explorer</span><span class="sxs-lookup"><span data-stu-id="b04a7-144">Access web app files in Server Explorer</span></span>
<span data-ttu-id="b04a7-145">You typically deploy a web project with the `customErrors` flag in the Web.config file set to `On` or `RemoteOnly`, which means you don't get a helpful error message when something goes wrong.</span><span class="sxs-lookup"><span data-stu-id="b04a7-145">You typically deploy a web project with the `customErrors` flag in the Web.config file set to `On` or `RemoteOnly`, which means you don't get a helpful error message when something goes wrong.</span></span> <span data-ttu-id="b04a7-146">For many errors all you get is a page like one of the following ones.</span><span class="sxs-lookup"><span data-stu-id="b04a7-146">For many errors all you get is a page like one of the following ones.</span></span>

<span data-ttu-id="b04a7-147">**Server Error in '/' Application:**</span><span class="sxs-lookup"><span data-stu-id="b04a7-147">**Server Error in '/' Application:**</span></span>

![Unhelpful error page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/genericerror.png)

<span data-ttu-id="b04a7-149">**An error occurred:**</span><span class="sxs-lookup"><span data-stu-id="b04a7-149">**An error occurred:**</span></span>

![Unhelpful error page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/genericerror1.png)

<span data-ttu-id="b04a7-151">**The website cannot display the page**</span><span class="sxs-lookup"><span data-stu-id="b04a7-151">**The website cannot display the page**</span></span>

![Unhelpful error page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/genericerror2.png)

<span data-ttu-id="b04a7-153">Frequently the easiest way to find the cause of the error is to enable detailed error messages, which the first of the preceding screenshots explains how to do.</span><span class="sxs-lookup"><span data-stu-id="b04a7-153">Frequently the easiest way to find the cause of the error is to enable detailed error messages, which the first of the preceding screenshots explains how to do.</span></span> <span data-ttu-id="b04a7-154">That requires a change in the deployed Web.config file.</span><span class="sxs-lookup"><span data-stu-id="b04a7-154">That requires a change in the deployed Web.config file.</span></span> <span data-ttu-id="b04a7-155">You could edit the *Web.config* file in the project and redeploy the project, or create a [Web.config transform](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) and deploy a debug build, but there's a quicker way: in **Solution Explorer** you can directly view and edit files in the remote web app by using the *remote view* feature.</span><span class="sxs-lookup"><span data-stu-id="b04a7-155">You could edit the *Web.config* file in the project and redeploy the project, or create a [Web.config transform](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) and deploy a debug build, but there's a quicker way: in **Solution Explorer** you can directly view and edit files in the remote web app by using the *remote view* feature.</span></span>

1. <span data-ttu-id="b04a7-156">In **Server Explorer**, expand **Azure**, expand **App Service**, expand the resource group that your web app is located in, and then expand the node for your web app.</span><span class="sxs-lookup"><span data-stu-id="b04a7-156">In **Server Explorer**, expand **Azure**, expand **App Service**, expand the resource group that your web app is located in, and then expand the node for your web app.</span></span>

    <span data-ttu-id="b04a7-157">You see nodes that give you access to the web app's content files and log files.</span><span class="sxs-lookup"><span data-stu-id="b04a7-157">You see nodes that give you access to the web app's content files and log files.</span></span>
2. <span data-ttu-id="b04a7-158">Expand the **Files** node, and double-click the *Web.config* file.</span><span class="sxs-lookup"><span data-stu-id="b04a7-158">Expand the **Files** node, and double-click the *Web.config* file.</span></span>

    ![Open Web.config](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/webconfig.png)

    <span data-ttu-id="b04a7-160">Visual Studio opens the Web.config file from the remote web app and shows [Remote] next to the file name in the title bar.</span><span class="sxs-lookup"><span data-stu-id="b04a7-160">Visual Studio opens the Web.config file from the remote web app and shows [Remote] next to the file name in the title bar.</span></span>
3. <span data-ttu-id="b04a7-161">Add the following line to the `system.web` element:</span><span class="sxs-lookup"><span data-stu-id="b04a7-161">Add the following line to the `system.web` element:</span></span>

    `<customErrors mode="Off"></customErrors>`

    ![Edit Web.config](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/webconfigedit.png)
4. <span data-ttu-id="b04a7-163">Refresh the browser that is showing the unhelpful error message, and now you get a detailed error message, such as the following example:</span><span class="sxs-lookup"><span data-stu-id="b04a7-163">Refresh the browser that is showing the unhelpful error message, and now you get a detailed error message, such as the following example:</span></span>

    ![Detailed error message](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/detailederror.png)

    <span data-ttu-id="b04a7-165">(The error shown was created by adding the line shown in red to *Views\Home\Index.cshtml*.)</span><span class="sxs-lookup"><span data-stu-id="b04a7-165">(The error shown was created by adding the line shown in red to *Views\Home\Index.cshtml*.)</span></span>

<span data-ttu-id="b04a7-166">Editing the Web.config file is only one example of scenarios in which the ability to read and edit files on your Azure web app make troubleshooting easier.</span><span class="sxs-lookup"><span data-stu-id="b04a7-166">Editing the Web.config file is only one example of scenarios in which the ability to read and edit files on your Azure web app make troubleshooting easier.</span></span>

## <a name="remotedebug"></a><span data-ttu-id="b04a7-167">Remote debugging web apps</span><span class="sxs-lookup"><span data-stu-id="b04a7-167">Remote debugging web apps</span></span>
<span data-ttu-id="b04a7-168">If the detailed error message doesn't provide enough information, and you can't re-create the error locally, another way to troubleshoot is to run in debug mode remotely.</span><span class="sxs-lookup"><span data-stu-id="b04a7-168">If the detailed error message doesn't provide enough information, and you can't re-create the error locally, another way to troubleshoot is to run in debug mode remotely.</span></span> <span data-ttu-id="b04a7-169">You can set breakpoints, manipulate memory directly, step through code, and even change the code path.</span><span class="sxs-lookup"><span data-stu-id="b04a7-169">You can set breakpoints, manipulate memory directly, step through code, and even change the code path.</span></span>

<span data-ttu-id="b04a7-170">Remote debugging does not work in Express editions of Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b04a7-170">Remote debugging does not work in Express editions of Visual Studio.</span></span>

<span data-ttu-id="b04a7-171">This section shows how to debug remotely using the project you create in [Getting started with Azure and ASP.NET][GetStarted].</span><span class="sxs-lookup"><span data-stu-id="b04a7-171">This section shows how to debug remotely using the project you create in [Getting started with Azure and ASP.NET][GetStarted].</span></span>

1. <span data-ttu-id="b04a7-172">Open the web project that you created in [Getting started with Azure and ASP.NET][GetStarted].</span><span class="sxs-lookup"><span data-stu-id="b04a7-172">Open the web project that you created in [Getting started with Azure and ASP.NET][GetStarted].</span></span>
2. <span data-ttu-id="b04a7-173">Open *Controllers\HomeController.cs*.</span><span class="sxs-lookup"><span data-stu-id="b04a7-173">Open *Controllers\HomeController.cs*.</span></span>
3. <span data-ttu-id="b04a7-174">Delete the `About()` method and insert the following code in its place.</span><span class="sxs-lookup"><span data-stu-id="b04a7-174">Delete the `About()` method and insert the following code in its place.</span></span>

        public ActionResult About()
        {
            string currentTime = DateTime.Now.ToLongTimeString();
            ViewBag.Message = "The current time is " + currentTime;
            return View();
        }
4. <span data-ttu-id="b04a7-175">[Set a breakpoint](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) on the `ViewBag.Message` line.</span><span class="sxs-lookup"><span data-stu-id="b04a7-175">[Set a breakpoint](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) on the `ViewBag.Message` line.</span></span>
5. <span data-ttu-id="b04a7-176">In **Solution Explorer**, right-click the project, and click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-176">In **Solution Explorer**, right-click the project, and click **Publish**.</span></span>
6. <span data-ttu-id="b04a7-177">In the **Profile** drop-down list, select the same profile that you used in [Getting started with Azure and ASP.NET][GetStarted].</span><span class="sxs-lookup"><span data-stu-id="b04a7-177">In the **Profile** drop-down list, select the same profile that you used in [Getting started with Azure and ASP.NET][GetStarted].</span></span>
7. <span data-ttu-id="b04a7-178">Click the **Settings** tab, and change **Configuration** to **Debug**, and then click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-178">Click the **Settings** tab, and change **Configuration** to **Debug**, and then click **Publish**.</span></span>

    ![Publish in debug mode](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-publishdebug.png)
8. <span data-ttu-id="b04a7-180">After deployment finishes and your browser opens to the Azure URL of your web app, close the browser.</span><span class="sxs-lookup"><span data-stu-id="b04a7-180">After deployment finishes and your browser opens to the Azure URL of your web app, close the browser.</span></span>
9. <span data-ttu-id="b04a7-181">In **Server Explorer**, right-click your web app, and then click **Attach Debugger**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-181">In **Server Explorer**, right-click your web app, and then click **Attach Debugger**.</span></span>

    ![Attach debugger](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-attachdebugger.png)

    <span data-ttu-id="b04a7-183">The browser automatically opens to your home page running in Azure.</span><span class="sxs-lookup"><span data-stu-id="b04a7-183">The browser automatically opens to your home page running in Azure.</span></span> <span data-ttu-id="b04a7-184">You might have to wait 20 seconds or so while Azure sets up the server for debugging.</span><span class="sxs-lookup"><span data-stu-id="b04a7-184">You might have to wait 20 seconds or so while Azure sets up the server for debugging.</span></span> <span data-ttu-id="b04a7-185">This delay only happens the first time you run in debug mode on a web app.</span><span class="sxs-lookup"><span data-stu-id="b04a7-185">This delay only happens the first time you run in debug mode on a web app.</span></span> <span data-ttu-id="b04a7-186">Subsequent times within the next 48 hours when you start debugging again there won't be a delay.</span><span class="sxs-lookup"><span data-stu-id="b04a7-186">Subsequent times within the next 48 hours when you start debugging again there won't be a delay.</span></span>

    <span data-ttu-id="b04a7-187">**Note:** If you have any trouble starting the debugger, try to do it by using **Cloud Explorer** instead of **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-187">**Note:** If you have any trouble starting the debugger, try to do it by using **Cloud Explorer** instead of **Server Explorer**.</span></span>
10. <span data-ttu-id="b04a7-188">Click **About** in the menu.</span><span class="sxs-lookup"><span data-stu-id="b04a7-188">Click **About** in the menu.</span></span>

     <span data-ttu-id="b04a7-189">Visual Studio stops on the breakpoint, and the code is running in Azure, not on your local computer.</span><span class="sxs-lookup"><span data-stu-id="b04a7-189">Visual Studio stops on the breakpoint, and the code is running in Azure, not on your local computer.</span></span>
11. <span data-ttu-id="b04a7-190">Hover over the `currentTime` variable to see the time value.</span><span class="sxs-lookup"><span data-stu-id="b04a7-190">Hover over the `currentTime` variable to see the time value.</span></span>

     ![View variable in debug mode running in Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugviewinwa.png)

     <span data-ttu-id="b04a7-192">The time you see is the Azure server time, which may be in a different time zone than your local computer.</span><span class="sxs-lookup"><span data-stu-id="b04a7-192">The time you see is the Azure server time, which may be in a different time zone than your local computer.</span></span>
12. <span data-ttu-id="b04a7-193">Enter a new value for the `currentTime` variable, such as "Now running in Azure".</span><span class="sxs-lookup"><span data-stu-id="b04a7-193">Enter a new value for the `currentTime` variable, such as "Now running in Azure".</span></span>
13. <span data-ttu-id="b04a7-194">Press F5 to continue running.</span><span class="sxs-lookup"><span data-stu-id="b04a7-194">Press F5 to continue running.</span></span>

     <span data-ttu-id="b04a7-195">The About page running in Azure displays the new value that you entered into the currentTime variable.</span><span class="sxs-lookup"><span data-stu-id="b04a7-195">The About page running in Azure displays the new value that you entered into the currentTime variable.</span></span>

     ![About page with new value](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugchangeinwa.png)

## <a name="remotedebugwj"></a> <span data-ttu-id="b04a7-197">Remote debugging WebJobs</span><span class="sxs-lookup"><span data-stu-id="b04a7-197">Remote debugging WebJobs</span></span>
<span data-ttu-id="b04a7-198">This section shows how to debug remotely using the project and web app you create in [Get Started with the Azure WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="b04a7-198">This section shows how to debug remotely using the project and web app you create in [Get Started with the Azure WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

<span data-ttu-id="b04a7-199">The features shown in this section are available only in Visual Studio 2013 with Update 4 or later.</span><span class="sxs-lookup"><span data-stu-id="b04a7-199">The features shown in this section are available only in Visual Studio 2013 with Update 4 or later.</span></span>

<span data-ttu-id="b04a7-200">Remote debugging only works with continuous WebJobs.</span><span class="sxs-lookup"><span data-stu-id="b04a7-200">Remote debugging only works with continuous WebJobs.</span></span> <span data-ttu-id="b04a7-201">Scheduled and on-demand WebJobs don't support debugging.</span><span class="sxs-lookup"><span data-stu-id="b04a7-201">Scheduled and on-demand WebJobs don't support debugging.</span></span>

1. <span data-ttu-id="b04a7-202">Open the web project that you created in [Get Started with the Azure WebJobs SDK][GetStartedWJ].</span><span class="sxs-lookup"><span data-stu-id="b04a7-202">Open the web project that you created in [Get Started with the Azure WebJobs SDK][GetStartedWJ].</span></span>
2. <span data-ttu-id="b04a7-203">In the ContosoAdsWebJob project, open *Functions.cs*.</span><span class="sxs-lookup"><span data-stu-id="b04a7-203">In the ContosoAdsWebJob project, open *Functions.cs*.</span></span>
3. <span data-ttu-id="b04a7-204">[Set a breakpoint](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) on the first statement in the `GnerateThumbnail` method.</span><span class="sxs-lookup"><span data-stu-id="b04a7-204">[Set a breakpoint](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) on the first statement in the `GnerateThumbnail` method.</span></span>

    ![Set breakpoint](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/wjbreakpoint.png)
4. <span data-ttu-id="b04a7-206">In **Solution Explorer**, right-click the web project (not the WebJob project), and click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-206">In **Solution Explorer**, right-click the web project (not the WebJob project), and click **Publish**.</span></span>
5. <span data-ttu-id="b04a7-207">In the **Profile** drop-down list, select the same profile that you used in [Get Started with the Azure WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="b04a7-207">In the **Profile** drop-down list, select the same profile that you used in [Get Started with the Azure WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>
6. <span data-ttu-id="b04a7-208">Click the **Settings** tab, and change **Configuration** to **Debug**, and then click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-208">Click the **Settings** tab, and change **Configuration** to **Debug**, and then click **Publish**.</span></span>

    <span data-ttu-id="b04a7-209">Visual Studio deploys the web and WebJob projects, and your browser opens to the Azure URL of your web app.</span><span class="sxs-lookup"><span data-stu-id="b04a7-209">Visual Studio deploys the web and WebJob projects, and your browser opens to the Azure URL of your web app.</span></span>
7. <span data-ttu-id="b04a7-210">In **Server Explorer** expand **Azure > App Service > your resource group > your web app > WebJobs > Continuous**, and then right-click **ContosoAdsWebJob**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-210">In **Server Explorer** expand **Azure > App Service > your resource group > your web app > WebJobs > Continuous**, and then right-click **ContosoAdsWebJob**.</span></span>
8. <span data-ttu-id="b04a7-211">Click **Attach Debugger**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-211">Click **Attach Debugger**.</span></span>

    ![Attach debugger](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/wjattach.png)

    <span data-ttu-id="b04a7-213">The browser automatically opens to your home page running in Azure.</span><span class="sxs-lookup"><span data-stu-id="b04a7-213">The browser automatically opens to your home page running in Azure.</span></span> <span data-ttu-id="b04a7-214">You might have to wait 20 seconds or so while Azure sets up the server for debugging.</span><span class="sxs-lookup"><span data-stu-id="b04a7-214">You might have to wait 20 seconds or so while Azure sets up the server for debugging.</span></span> <span data-ttu-id="b04a7-215">This delay only happens the first time you run in debug mode on a web app.</span><span class="sxs-lookup"><span data-stu-id="b04a7-215">This delay only happens the first time you run in debug mode on a web app.</span></span> <span data-ttu-id="b04a7-216">The next time you attach the debugger there won't be a delay, if you do it within 48 hours.</span><span class="sxs-lookup"><span data-stu-id="b04a7-216">The next time you attach the debugger there won't be a delay, if you do it within 48 hours.</span></span>
9. <span data-ttu-id="b04a7-217">In the web browser that is opened to the Contoso Ads home page, create a new ad.</span><span class="sxs-lookup"><span data-stu-id="b04a7-217">In the web browser that is opened to the Contoso Ads home page, create a new ad.</span></span>

    <span data-ttu-id="b04a7-218">Creating an ad causes a queue message to be created, which will be picked up by the WebJob and processed.</span><span class="sxs-lookup"><span data-stu-id="b04a7-218">Creating an ad causes a queue message to be created, which will be picked up by the WebJob and processed.</span></span> <span data-ttu-id="b04a7-219">When the WebJobs SDK calls the function to process the queue message, the code will hit your breakpoint.</span><span class="sxs-lookup"><span data-stu-id="b04a7-219">When the WebJobs SDK calls the function to process the queue message, the code will hit your breakpoint.</span></span>
10. <span data-ttu-id="b04a7-220">When the debugger breaks at your breakpoint, you can examine and change variable values while the program is running the cloud.</span><span class="sxs-lookup"><span data-stu-id="b04a7-220">When the debugger breaks at your breakpoint, you can examine and change variable values while the program is running the cloud.</span></span> <span data-ttu-id="b04a7-221">In the following illustration the debugger shows the contents of the blobInfo object that was passed to the GenerateThumbnail method.</span><span class="sxs-lookup"><span data-stu-id="b04a7-221">In the following illustration the debugger shows the contents of the blobInfo object that was passed to the GenerateThumbnail method.</span></span>

     ![blobInfo object in debugger](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/blobinfo.png)
11. <span data-ttu-id="b04a7-223">Press F5 to continue running.</span><span class="sxs-lookup"><span data-stu-id="b04a7-223">Press F5 to continue running.</span></span>

     <span data-ttu-id="b04a7-224">The GenerateThumbnail method finishes creating the thumbnail.</span><span class="sxs-lookup"><span data-stu-id="b04a7-224">The GenerateThumbnail method finishes creating the thumbnail.</span></span>
12. <span data-ttu-id="b04a7-225">In the browser, refresh the Index page and you see the thumbnail.</span><span class="sxs-lookup"><span data-stu-id="b04a7-225">In the browser, refresh the Index page and you see the thumbnail.</span></span>
13. <span data-ttu-id="b04a7-226">In Visual Studio, press SHIFT+F5 to stop debugging.</span><span class="sxs-lookup"><span data-stu-id="b04a7-226">In Visual Studio, press SHIFT+F5 to stop debugging.</span></span>
14. <span data-ttu-id="b04a7-227">In **Server Explorer**, right-click the ContosoAdsWebJob node and click **View Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-227">In **Server Explorer**, right-click the ContosoAdsWebJob node and click **View Dashboard**.</span></span>
15. <span data-ttu-id="b04a7-228">Sign in with your Azure credentials, and then click the WebJob name to go to the page for your WebJob.</span><span class="sxs-lookup"><span data-stu-id="b04a7-228">Sign in with your Azure credentials, and then click the WebJob name to go to the page for your WebJob.</span></span>

     ![Click ContosoAdsWebJob](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/clickcaw.png)

     <span data-ttu-id="b04a7-230">The Dashboard shows that the GenerateThumbnail function executed recently.</span><span class="sxs-lookup"><span data-stu-id="b04a7-230">The Dashboard shows that the GenerateThumbnail function executed recently.</span></span>

     <span data-ttu-id="b04a7-231">(The next time you click **View Dashboard**, you don't have to sign in, and the browser goes directly to the page for your WebJob.)</span><span class="sxs-lookup"><span data-stu-id="b04a7-231">(The next time you click **View Dashboard**, you don't have to sign in, and the browser goes directly to the page for your WebJob.)</span></span>
16. <span data-ttu-id="b04a7-232">Click the function name to see details about the function execution.</span><span class="sxs-lookup"><span data-stu-id="b04a7-232">Click the function name to see details about the function execution.</span></span>

     ![Function details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/funcdetails.png)

<span data-ttu-id="b04a7-234">If your function [wrote logs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs), you could click **ToggleOutput** to see them.</span><span class="sxs-lookup"><span data-stu-id="b04a7-234">If your function [wrote logs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs), you could click **ToggleOutput** to see them.</span></span>

## <a name="notes-about-remote-debugging"></a><span data-ttu-id="b04a7-235">Notes about remote debugging</span><span class="sxs-lookup"><span data-stu-id="b04a7-235">Notes about remote debugging</span></span>
* <span data-ttu-id="b04a7-236">Running in debug mode in production is not recommended.</span><span class="sxs-lookup"><span data-stu-id="b04a7-236">Running in debug mode in production is not recommended.</span></span> <span data-ttu-id="b04a7-237">If your production web app is not scaled out to multiple server instances, debugging will prevent the web server from responding to other requests.</span><span class="sxs-lookup"><span data-stu-id="b04a7-237">If your production web app is not scaled out to multiple server instances, debugging will prevent the web server from responding to other requests.</span></span> <span data-ttu-id="b04a7-238">If you do have multiple web server instances, when you attach to the debugger you'll get a random instance, and you have no way to ensure that subsequent browser requests will go to that instance.</span><span class="sxs-lookup"><span data-stu-id="b04a7-238">If you do have multiple web server instances, when you attach to the debugger you'll get a random instance, and you have no way to ensure that subsequent browser requests will go to that instance.</span></span> <span data-ttu-id="b04a7-239">Also, you typically don't deploy a debug build to production, and compiler optimizations for release builds might make it impossible to show what is happening line by line in your source code.</span><span class="sxs-lookup"><span data-stu-id="b04a7-239">Also, you typically don't deploy a debug build to production, and compiler optimizations for release builds might make it impossible to show what is happening line by line in your source code.</span></span> <span data-ttu-id="b04a7-240">For troubleshooting production problems, your best resource is application tracing and web server logs.</span><span class="sxs-lookup"><span data-stu-id="b04a7-240">For troubleshooting production problems, your best resource is application tracing and web server logs.</span></span>
* <span data-ttu-id="b04a7-241">Avoid long stops at breakpoints when remote debugging.</span><span class="sxs-lookup"><span data-stu-id="b04a7-241">Avoid long stops at breakpoints when remote debugging.</span></span> <span data-ttu-id="b04a7-242">Azure treats a process that is stopped for longer than a few minutes as an unresponsive process, and shuts it down.</span><span class="sxs-lookup"><span data-stu-id="b04a7-242">Azure treats a process that is stopped for longer than a few minutes as an unresponsive process, and shuts it down.</span></span>
* <span data-ttu-id="b04a7-243">While you're debugging, the server is sending data to Visual Studio, which could affect bandwidth charges.</span><span class="sxs-lookup"><span data-stu-id="b04a7-243">While you're debugging, the server is sending data to Visual Studio, which could affect bandwidth charges.</span></span> <span data-ttu-id="b04a7-244">For information about bandwidth rates, see [Azure Pricing](https://azure.microsoft.com/pricing/calculator/).</span><span class="sxs-lookup"><span data-stu-id="b04a7-244">For information about bandwidth rates, see [Azure Pricing](https://azure.microsoft.com/pricing/calculator/).</span></span>
* <span data-ttu-id="b04a7-245">Make sure that the `debug` attribute of the `compilation` element in the *Web.config* file is set to true.</span><span class="sxs-lookup"><span data-stu-id="b04a7-245">Make sure that the `debug` attribute of the `compilation` element in the *Web.config* file is set to true.</span></span> <span data-ttu-id="b04a7-246">It is set to true by default when you publish a debug build configuration.</span><span class="sxs-lookup"><span data-stu-id="b04a7-246">It is set to true by default when you publish a debug build configuration.</span></span>

        <system.web>
          <compilation debug="true" targetFramework="4.5" />
          <httpRuntime targetFramework="4.5" />
        </system.web>
* <span data-ttu-id="b04a7-247">If you find that the debugger won't step into code that you want to debug, you might have to change the Just My Code setting.</span><span class="sxs-lookup"><span data-stu-id="b04a7-247">If you find that the debugger won't step into code that you want to debug, you might have to change the Just My Code setting.</span></span>  <span data-ttu-id="b04a7-248">For more information, see [Restrict stepping to Just My Code](http://msdn.microsoft.com/library/vstudio/y740d9d3.aspx#BKMK_Restrict_stepping_to_Just_My_Code).</span><span class="sxs-lookup"><span data-stu-id="b04a7-248">For more information, see [Restrict stepping to Just My Code](http://msdn.microsoft.com/library/vstudio/y740d9d3.aspx#BKMK_Restrict_stepping_to_Just_My_Code).</span></span>
* <span data-ttu-id="b04a7-249">A timer starts on the server when you enable the remote debugging feature, and after 48 hours the feature is automatically turned off.</span><span class="sxs-lookup"><span data-stu-id="b04a7-249">A timer starts on the server when you enable the remote debugging feature, and after 48 hours the feature is automatically turned off.</span></span> <span data-ttu-id="b04a7-250">This 48 hour limit is done for security and performance reasons.</span><span class="sxs-lookup"><span data-stu-id="b04a7-250">This 48 hour limit is done for security and performance reasons.</span></span> <span data-ttu-id="b04a7-251">You can easily turn the feature back on as many times as you like.</span><span class="sxs-lookup"><span data-stu-id="b04a7-251">You can easily turn the feature back on as many times as you like.</span></span> <span data-ttu-id="b04a7-252">We recommend leaving it disabled when you are not actively debugging.</span><span class="sxs-lookup"><span data-stu-id="b04a7-252">We recommend leaving it disabled when you are not actively debugging.</span></span>
* <span data-ttu-id="b04a7-253">You can manually attach the debugger to any process, not only the web app process (w3wp.exe).</span><span class="sxs-lookup"><span data-stu-id="b04a7-253">You can manually attach the debugger to any process, not only the web app process (w3wp.exe).</span></span> <span data-ttu-id="b04a7-254">For more information about how to use debug mode in Visual Studio, see [Debugging in Visual Studio](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx).</span><span class="sxs-lookup"><span data-stu-id="b04a7-254">For more information about how to use debug mode in Visual Studio, see [Debugging in Visual Studio](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx).</span></span>

## <a name="logsoverview"></a><span data-ttu-id="b04a7-255">Diagnostic logs overview</span><span class="sxs-lookup"><span data-stu-id="b04a7-255">Diagnostic logs overview</span></span>
<span data-ttu-id="b04a7-256">An ASP.NET application that runs in an Azure web app can create the following kinds of logs:</span><span class="sxs-lookup"><span data-stu-id="b04a7-256">An ASP.NET application that runs in an Azure web app can create the following kinds of logs:</span></span>

* <span data-ttu-id="b04a7-257">**Application tracing logs**</span><span class="sxs-lookup"><span data-stu-id="b04a7-257">**Application tracing logs**</span></span><br/>
  <span data-ttu-id="b04a7-258">The application creates these logs by calling methods of the [System.Diagnostics.Trace](http://msdn.microsoft.com/library/system.diagnostics.trace.aspx) class.</span><span class="sxs-lookup"><span data-stu-id="b04a7-258">The application creates these logs by calling methods of the [System.Diagnostics.Trace](http://msdn.microsoft.com/library/system.diagnostics.trace.aspx) class.</span></span>
* <span data-ttu-id="b04a7-259">**Web server logs**</span><span class="sxs-lookup"><span data-stu-id="b04a7-259">**Web server logs**</span></span><br/>
  <span data-ttu-id="b04a7-260">The web server creates a log entry for every HTTP request to the web app.</span><span class="sxs-lookup"><span data-stu-id="b04a7-260">The web server creates a log entry for every HTTP request to the web app.</span></span>
* <span data-ttu-id="b04a7-261">**Detailed error message logs**</span><span class="sxs-lookup"><span data-stu-id="b04a7-261">**Detailed error message logs**</span></span><br/>
  <span data-ttu-id="b04a7-262">The web server creates an HTML page with some additional information for failed HTTP requests (those that result in status code 400 or greater).</span><span class="sxs-lookup"><span data-stu-id="b04a7-262">The web server creates an HTML page with some additional information for failed HTTP requests (those that result in status code 400 or greater).</span></span>
* <span data-ttu-id="b04a7-263">**Failed request tracing logs**</span><span class="sxs-lookup"><span data-stu-id="b04a7-263">**Failed request tracing logs**</span></span><br/>
  <span data-ttu-id="b04a7-264">The web server creates an XML file with detailed tracing information for failed HTTP requests.</span><span class="sxs-lookup"><span data-stu-id="b04a7-264">The web server creates an XML file with detailed tracing information for failed HTTP requests.</span></span> <span data-ttu-id="b04a7-265">The web server also provides an XSL file to format the XML in a browser.</span><span class="sxs-lookup"><span data-stu-id="b04a7-265">The web server also provides an XSL file to format the XML in a browser.</span></span>

<span data-ttu-id="b04a7-266">Logging affects web app performance, so Azure gives you the ability to enable or disable each type of log as needed.</span><span class="sxs-lookup"><span data-stu-id="b04a7-266">Logging affects web app performance, so Azure gives you the ability to enable or disable each type of log as needed.</span></span> <span data-ttu-id="b04a7-267">For application logs, you can specify that only logs above a certain severity level should be written.</span><span class="sxs-lookup"><span data-stu-id="b04a7-267">For application logs, you can specify that only logs above a certain severity level should be written.</span></span> <span data-ttu-id="b04a7-268">When you create a new web app, by default all logging is disabled.</span><span class="sxs-lookup"><span data-stu-id="b04a7-268">When you create a new web app, by default all logging is disabled.</span></span>

<span data-ttu-id="b04a7-269">Logs are written to files in a *LogFiles* folder in the file system of your web app and are accessible via FTP.</span><span class="sxs-lookup"><span data-stu-id="b04a7-269">Logs are written to files in a *LogFiles* folder in the file system of your web app and are accessible via FTP.</span></span> <span data-ttu-id="b04a7-270">Web server logs and application logs can also be written to an Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="b04a7-270">Web server logs and application logs can also be written to an Azure Storage account.</span></span> <span data-ttu-id="b04a7-271">You can retain a greater volume of logs in a storage account than is possible in the file system.</span><span class="sxs-lookup"><span data-stu-id="b04a7-271">You can retain a greater volume of logs in a storage account than is possible in the file system.</span></span> <span data-ttu-id="b04a7-272">You're limited to a maximum of 100 megabytes of logs when you use the file system.</span><span class="sxs-lookup"><span data-stu-id="b04a7-272">You're limited to a maximum of 100 megabytes of logs when you use the file system.</span></span> <span data-ttu-id="b04a7-273">(File system logs are only for short-term retention.</span><span class="sxs-lookup"><span data-stu-id="b04a7-273">(File system logs are only for short-term retention.</span></span> <span data-ttu-id="b04a7-274">Azure deletes old log files to make room for new ones after the limit is reached.)</span><span class="sxs-lookup"><span data-stu-id="b04a7-274">Azure deletes old log files to make room for new ones after the limit is reached.)</span></span>  

## <a name="apptracelogs"></a><span data-ttu-id="b04a7-275">Create and view application trace logs</span><span class="sxs-lookup"><span data-stu-id="b04a7-275">Create and view application trace logs</span></span>
<span data-ttu-id="b04a7-276">In this section you'll do the following tasks:</span><span class="sxs-lookup"><span data-stu-id="b04a7-276">In this section you'll do the following tasks:</span></span>

* <span data-ttu-id="b04a7-277">Add tracing statements to the web project that you created in [Get started with Azure and ASP.NET][GetStarted].</span><span class="sxs-lookup"><span data-stu-id="b04a7-277">Add tracing statements to the web project that you created in [Get started with Azure and ASP.NET][GetStarted].</span></span>
* <span data-ttu-id="b04a7-278">View the logs when you run the project locally.</span><span class="sxs-lookup"><span data-stu-id="b04a7-278">View the logs when you run the project locally.</span></span>
* <span data-ttu-id="b04a7-279">View the logs as they are generated by the application running in Azure.</span><span class="sxs-lookup"><span data-stu-id="b04a7-279">View the logs as they are generated by the application running in Azure.</span></span>

<span data-ttu-id="b04a7-280">For information about how to create application logs in WebJobs, see [How to work with Azure queue storage using the WebJobs SDK - How to write logs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs).</span><span class="sxs-lookup"><span data-stu-id="b04a7-280">For information about how to create application logs in WebJobs, see [How to work with Azure queue storage using the WebJobs SDK - How to write logs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs).</span></span> <span data-ttu-id="b04a7-281">The following instructions for viewing logs and controlling how they're stored in Azure apply also to application logs created by WebJobs.</span><span class="sxs-lookup"><span data-stu-id="b04a7-281">The following instructions for viewing logs and controlling how they're stored in Azure apply also to application logs created by WebJobs.</span></span>

### <a name="add-tracing-statements-to-the-application"></a><span data-ttu-id="b04a7-282">Add tracing statements to the application</span><span class="sxs-lookup"><span data-stu-id="b04a7-282">Add tracing statements to the application</span></span>
1. <span data-ttu-id="b04a7-283">Open *Controllers\HomeController.cs*, and replace the `Index`, `About`, and `Contact` methods with the following code in order to add `Trace` statements and a `using` statement for `System.Diagnostics`:</span><span class="sxs-lookup"><span data-stu-id="b04a7-283">Open *Controllers\HomeController.cs*, and replace the `Index`, `About`, and `Contact` methods with the following code in order to add `Trace` statements and a `using` statement for `System.Diagnostics`:</span></span>

        public ActionResult Index()
        {
            Trace.WriteLine("Entering Index method");
            ViewBag.Message = "Modify this template to jump-start your ASP.NET MVC application.";
            Trace.TraceInformation("Displaying the Index page at " + DateTime.Now.ToLongTimeString());
            Trace.WriteLine("Leaving Index method");
            return View();
        }

        public ActionResult About()
        {
            Trace.WriteLine("Entering About method");
            ViewBag.Message = "Your app description page.";
            Trace.TraceWarning("Transient error on the About page at " + DateTime.Now.ToShortTimeString());
            Trace.WriteLine("Leaving About method");
            return View();
        }

        public ActionResult Contact()
        {
            Trace.WriteLine("Entering Contact method");
            ViewBag.Message = "Your contact page.";
            Trace.TraceError("Fatal error on the Contact page at " + DateTime.Now.ToLongTimeString());
            Trace.WriteLine("Leaving Contact method");
            return View();
        }        
2. <span data-ttu-id="b04a7-284">Add a `using System.Diagnostics;` statement to the top of the file.</span><span class="sxs-lookup"><span data-stu-id="b04a7-284">Add a `using System.Diagnostics;` statement to the top of the file.</span></span>

### <a name="view-the-tracing-output-locally"></a><span data-ttu-id="b04a7-285">View the tracing output locally</span><span class="sxs-lookup"><span data-stu-id="b04a7-285">View the tracing output locally</span></span>
1. <span data-ttu-id="b04a7-286">Press F5 to run the application in debug mode.</span><span class="sxs-lookup"><span data-stu-id="b04a7-286">Press F5 to run the application in debug mode.</span></span>

    <span data-ttu-id="b04a7-287">The default trace listener writes all trace output to the **Output** window, along with other Debug output.</span><span class="sxs-lookup"><span data-stu-id="b04a7-287">The default trace listener writes all trace output to the **Output** window, along with other Debug output.</span></span> <span data-ttu-id="b04a7-288">The following illustration shows the output from the trace statements that you added to the `Index` method.</span><span class="sxs-lookup"><span data-stu-id="b04a7-288">The following illustration shows the output from the trace statements that you added to the `Index` method.</span></span>

    ![Tracing in Debug window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugtracing.png)

    <span data-ttu-id="b04a7-290">The following steps show how to view trace output in a web page, without compiling in debug mode.</span><span class="sxs-lookup"><span data-stu-id="b04a7-290">The following steps show how to view trace output in a web page, without compiling in debug mode.</span></span>
2. <span data-ttu-id="b04a7-291">Open the application Web.config file (the one located in the project folder) and add a `<system.diagnostics>` element at the end of the file just before the closing `</configuration>` element:</span><span class="sxs-lookup"><span data-stu-id="b04a7-291">Open the application Web.config file (the one located in the project folder) and add a `<system.diagnostics>` element at the end of the file just before the closing `</configuration>` element:</span></span>

          <system.diagnostics>
            <trace>
              <listeners>
                <add name="WebPageTraceListener"
                    type="System.Web.WebPageTraceListener,
                    System.Web,
                    Version=4.0.0.0,
                    Culture=neutral,
                    PublicKeyToken=b03f5f7f11d50a3a" />
              </listeners>
            </trace>
          </system.diagnostics>

    <span data-ttu-id="b04a7-292">The `WebPageTraceListener` lets you view trace output by browsing to `/trace.axd`.</span><span class="sxs-lookup"><span data-stu-id="b04a7-292">The `WebPageTraceListener` lets you view trace output by browsing to `/trace.axd`.</span></span>
3. <span data-ttu-id="b04a7-293">Add a <a href="http://msdn.microsoft.com/library/vstudio/6915t83k(v=vs.100).aspx">trace element</a> under `<system.web>` in the Web.config file, such as the following example:</span><span class="sxs-lookup"><span data-stu-id="b04a7-293">Add a <a href="http://msdn.microsoft.com/library/vstudio/6915t83k(v=vs.100).aspx">trace element</a> under `<system.web>` in the Web.config file, such as the following example:</span></span>

        <trace enabled="true" writeToDiagnosticsTrace="true" mostRecent="true" pageOutput="false" />
4. <span data-ttu-id="b04a7-294">Press CTRL+F5 to run the application.</span><span class="sxs-lookup"><span data-stu-id="b04a7-294">Press CTRL+F5 to run the application.</span></span>
5. <span data-ttu-id="b04a7-295">In the address bar of the browser window, add *trace.axd* to the URL, and then press Enter (the URL will be similar to http://localhost:53370/trace.axd).</span><span class="sxs-lookup"><span data-stu-id="b04a7-295">In the address bar of the browser window, add *trace.axd* to the URL, and then press Enter (the URL will be similar to http://localhost:53370/trace.axd).</span></span>
6. <span data-ttu-id="b04a7-296">On the **Application Trace** page, click **View Details** on the first line (not the BrowserLink line).</span><span class="sxs-lookup"><span data-stu-id="b04a7-296">On the **Application Trace** page, click **View Details** on the first line (not the BrowserLink line).</span></span>

    ![trace.axd](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-traceaxd1.png)

    <span data-ttu-id="b04a7-298">The **Request Details** page appears, and in the **Trace Information** section you see the output from the trace statements that you added to the `Index` method.</span><span class="sxs-lookup"><span data-stu-id="b04a7-298">The **Request Details** page appears, and in the **Trace Information** section you see the output from the trace statements that you added to the `Index` method.</span></span>

    ![trace.axd](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-traceaxd2.png)

    <span data-ttu-id="b04a7-300">By default, `trace.axd` is only available locally.</span><span class="sxs-lookup"><span data-stu-id="b04a7-300">By default, `trace.axd` is only available locally.</span></span> <span data-ttu-id="b04a7-301">If you wanted to make it available from a remote web app, you could add `localOnly="false"` to the `trace` element in the *Web.config* file, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="b04a7-301">If you wanted to make it available from a remote web app, you could add `localOnly="false"` to the `trace` element in the *Web.config* file, as shown in the following example:</span></span>

        <trace enabled="true" writeToDiagnosticsTrace="true" localOnly="false" mostRecent="true" pageOutput="false" />

    <span data-ttu-id="b04a7-302">However, enabling `trace.axd` in a production web app is generally not recommended for security reasons, and in the following sections you'll see an easier way to read tracing logs in an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="b04a7-302">However, enabling `trace.axd` in a production web app is generally not recommended for security reasons, and in the following sections you'll see an easier way to read tracing logs in an Azure web app.</span></span>

### <a name="view-the-tracing-output-in-azure"></a><span data-ttu-id="b04a7-303">View the tracing output in Azure</span><span class="sxs-lookup"><span data-stu-id="b04a7-303">View the tracing output in Azure</span></span>
1. <span data-ttu-id="b04a7-304">In **Solution Explorer**, right-click the web project and click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-304">In **Solution Explorer**, right-click the web project and click **Publish**.</span></span>
2. <span data-ttu-id="b04a7-305">In the **Publish Web** dialog box, click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-305">In the **Publish Web** dialog box, click **Publish**.</span></span>

    <span data-ttu-id="b04a7-306">After Visual Studio publishes your update, it opens a browser window to your home page (assuming you didn't clear **Destination URL** on the **Connection** tab).</span><span class="sxs-lookup"><span data-stu-id="b04a7-306">After Visual Studio publishes your update, it opens a browser window to your home page (assuming you didn't clear **Destination URL** on the **Connection** tab).</span></span>
3. <span data-ttu-id="b04a7-307">In **Server Explorer**, right-click your web app and select **View Streaming Logs**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-307">In **Server Explorer**, right-click your web app and select **View Streaming Logs**.</span></span>

    ![View Streaming Logs in context menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-viewlogsmenu.png)

    <span data-ttu-id="b04a7-309">The **Output** window shows that you are connected to the log-streaming service, and adds a notification line each minute that goes by without a log to display.</span><span class="sxs-lookup"><span data-stu-id="b04a7-309">The **Output** window shows that you are connected to the log-streaming service, and adds a notification line each minute that goes by without a log to display.</span></span>

    ![View Streaming Logs in context menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-nologsyet.png)
4. <span data-ttu-id="b04a7-311">In the browser window that shows your application home page, click **Contact**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-311">In the browser window that shows your application home page, click **Contact**.</span></span>

    <span data-ttu-id="b04a7-312">Within a few seconds the output from the error-level trace you added to the `Contact` method appears in the **Output** window.</span><span class="sxs-lookup"><span data-stu-id="b04a7-312">Within a few seconds the output from the error-level trace you added to the `Contact` method appears in the **Output** window.</span></span>

    ![Error trace in Output window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-errortrace.png)

    <span data-ttu-id="b04a7-314">Visual Studio is only showing error-level traces because that is the default setting when you enable the log monitoring service.</span><span class="sxs-lookup"><span data-stu-id="b04a7-314">Visual Studio is only showing error-level traces because that is the default setting when you enable the log monitoring service.</span></span> <span data-ttu-id="b04a7-315">When you create a new Azure web app, all logging is disabled by default, as you saw when you opened the settings page earlier:</span><span class="sxs-lookup"><span data-stu-id="b04a7-315">When you create a new Azure web app, all logging is disabled by default, as you saw when you opened the settings page earlier:</span></span>

    ![Application Logging off](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-apploggingoff.png)

    <span data-ttu-id="b04a7-317">However, when you selected **View Streaming Logs**, Visual Studio automatically changed **Application Logging(File System)** to **Error**, which means error-level logs get reported.</span><span class="sxs-lookup"><span data-stu-id="b04a7-317">However, when you selected **View Streaming Logs**, Visual Studio automatically changed **Application Logging(File System)** to **Error**, which means error-level logs get reported.</span></span> <span data-ttu-id="b04a7-318">In order to see all of your tracing logs, you can change this setting to **Verbose**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-318">In order to see all of your tracing logs, you can change this setting to **Verbose**.</span></span> <span data-ttu-id="b04a7-319">When you select a severity level lower than error, all logs for higher severity levels are also reported.</span><span class="sxs-lookup"><span data-stu-id="b04a7-319">When you select a severity level lower than error, all logs for higher severity levels are also reported.</span></span> <span data-ttu-id="b04a7-320">So when you select verbose, you also see information, warning, and error logs.</span><span class="sxs-lookup"><span data-stu-id="b04a7-320">So when you select verbose, you also see information, warning, and error logs.</span></span>  

1. <span data-ttu-id="b04a7-321">In **Server Explorer**, right-click the web app, and then click **View Settings** as you did earlier.</span><span class="sxs-lookup"><span data-stu-id="b04a7-321">In **Server Explorer**, right-click the web app, and then click **View Settings** as you did earlier.</span></span>
2. <span data-ttu-id="b04a7-322">Change **Application Logging (File System)** to **Verbose**, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-322">Change **Application Logging (File System)** to **Verbose**, and then click **Save**.</span></span>

    ![Setting trace level to Verbose](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-applogverbose.png)
3. <span data-ttu-id="b04a7-324">In the browser window that is now showing your **Contact** page, click **Home**, then click **About**, and then click **Contact**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-324">In the browser window that is now showing your **Contact** page, click **Home**, then click **About**, and then click **Contact**.</span></span>

    <span data-ttu-id="b04a7-325">Within a few seconds, the **Output** window shows all of your tracing output.</span><span class="sxs-lookup"><span data-stu-id="b04a7-325">Within a few seconds, the **Output** window shows all of your tracing output.</span></span>

    ![Verbose trace output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-verbosetraces.png)

    <span data-ttu-id="b04a7-327">In this section you enabled and disabled logging by using Azure web app settings.</span><span class="sxs-lookup"><span data-stu-id="b04a7-327">In this section you enabled and disabled logging by using Azure web app settings.</span></span> <span data-ttu-id="b04a7-328">You can also enable and disable trace listeners by modifying the Web.config file.</span><span class="sxs-lookup"><span data-stu-id="b04a7-328">You can also enable and disable trace listeners by modifying the Web.config file.</span></span> <span data-ttu-id="b04a7-329">However, modifying the Web.config file causes the app domain to recycle, while enabling logging via the web app configuration doesn't do that.</span><span class="sxs-lookup"><span data-stu-id="b04a7-329">However, modifying the Web.config file causes the app domain to recycle, while enabling logging via the web app configuration doesn't do that.</span></span> <span data-ttu-id="b04a7-330">If the problem takes a long time to reproduce, or is intermittent, recycling the app domain might "fix" it and force you to wait until it happens again.</span><span class="sxs-lookup"><span data-stu-id="b04a7-330">If the problem takes a long time to reproduce, or is intermittent, recycling the app domain might "fix" it and force you to wait until it happens again.</span></span> <span data-ttu-id="b04a7-331">Enabling diagnostics in Azure doesn't do this, so you can start capturing error information immediately.</span><span class="sxs-lookup"><span data-stu-id="b04a7-331">Enabling diagnostics in Azure doesn't do this, so you can start capturing error information immediately.</span></span>

### <a name="output-window-features"></a><span data-ttu-id="b04a7-332">Output window features</span><span class="sxs-lookup"><span data-stu-id="b04a7-332">Output window features</span></span>
<span data-ttu-id="b04a7-333">The **Azure Logs** tab of the **Output** Window has several buttons and a text box:</span><span class="sxs-lookup"><span data-stu-id="b04a7-333">The **Azure Logs** tab of the **Output** Window has several buttons and a text box:</span></span>

![Logs tab buttons](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-icons.png)

<span data-ttu-id="b04a7-335">These perform the following functions:</span><span class="sxs-lookup"><span data-stu-id="b04a7-335">These perform the following functions:</span></span>

* <span data-ttu-id="b04a7-336">Clear the **Output** window.</span><span class="sxs-lookup"><span data-stu-id="b04a7-336">Clear the **Output** window.</span></span>
* <span data-ttu-id="b04a7-337">Enable or disable word wrap.</span><span class="sxs-lookup"><span data-stu-id="b04a7-337">Enable or disable word wrap.</span></span>
* <span data-ttu-id="b04a7-338">Start or stop monitoring logs.</span><span class="sxs-lookup"><span data-stu-id="b04a7-338">Start or stop monitoring logs.</span></span>
* <span data-ttu-id="b04a7-339">Specify which logs to monitor.</span><span class="sxs-lookup"><span data-stu-id="b04a7-339">Specify which logs to monitor.</span></span>
* <span data-ttu-id="b04a7-340">Download logs.</span><span class="sxs-lookup"><span data-stu-id="b04a7-340">Download logs.</span></span>
* <span data-ttu-id="b04a7-341">Filter logs based on a search string or a regular expression.</span><span class="sxs-lookup"><span data-stu-id="b04a7-341">Filter logs based on a search string or a regular expression.</span></span>
* <span data-ttu-id="b04a7-342">Close the **Output** window.</span><span class="sxs-lookup"><span data-stu-id="b04a7-342">Close the **Output** window.</span></span>

<span data-ttu-id="b04a7-343">If you enter a search string or regular expression, Visual Studio filters logging information at the client.</span><span class="sxs-lookup"><span data-stu-id="b04a7-343">If you enter a search string or regular expression, Visual Studio filters logging information at the client.</span></span> <span data-ttu-id="b04a7-344">That means you can enter the criteria after the logs are displayed in the **Output** window and you can change filtering criteria without having to regenerate the logs.</span><span class="sxs-lookup"><span data-stu-id="b04a7-344">That means you can enter the criteria after the logs are displayed in the **Output** window and you can change filtering criteria without having to regenerate the logs.</span></span>

## <a name="webserverlogs"></a><span data-ttu-id="b04a7-345">View web server logs</span><span class="sxs-lookup"><span data-stu-id="b04a7-345">View web server logs</span></span>
<span data-ttu-id="b04a7-346">Web server logs record all HTTP activity for the web app.</span><span class="sxs-lookup"><span data-stu-id="b04a7-346">Web server logs record all HTTP activity for the web app.</span></span> <span data-ttu-id="b04a7-347">In order to see them in the **Output** window you have to enable them for the web app and tell Visual Studio that you want to monitor them.</span><span class="sxs-lookup"><span data-stu-id="b04a7-347">In order to see them in the **Output** window you have to enable them for the web app and tell Visual Studio that you want to monitor them.</span></span>

1. <span data-ttu-id="b04a7-348">In the **Azure Web App Configuration** tab that you opened from **Server Explorer**, change Web Server Logging to **On**, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-348">In the **Azure Web App Configuration** tab that you opened from **Server Explorer**, change Web Server Logging to **On**, and then click **Save**.</span></span>

    ![Enable web server logging](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-webserverloggingon.png)
2. <span data-ttu-id="b04a7-350">In the **Output** Window, click the **Specify which Azure logs to monitor** button.</span><span class="sxs-lookup"><span data-stu-id="b04a7-350">In the **Output** Window, click the **Specify which Azure logs to monitor** button.</span></span>

    ![Specify which Azure logs to monitor](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-specifylogs.png)
3. <span data-ttu-id="b04a7-352">In the **Azure Logging Options** dialog box, select **Web server logs**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-352">In the **Azure Logging Options** dialog box, select **Web server logs**, and then click **OK**.</span></span>

    ![Monitor web server logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-monitorwslogson.png)
4. <span data-ttu-id="b04a7-354">In the browser window that shows the web app, click **Home**, then click **About**, and then click **Contact**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-354">In the browser window that shows the web app, click **Home**, then click **About**, and then click **Contact**.</span></span>

    <span data-ttu-id="b04a7-355">The application logs generally appear first, followed by the web server logs.</span><span class="sxs-lookup"><span data-stu-id="b04a7-355">The application logs generally appear first, followed by the web server logs.</span></span> <span data-ttu-id="b04a7-356">You might have to wait a while for the logs to appear.</span><span class="sxs-lookup"><span data-stu-id="b04a7-356">You might have to wait a while for the logs to appear.</span></span>

    ![Web server logs in Output window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-wslogs.png)

<span data-ttu-id="b04a7-358">By default, when you first enable web server logs by using Visual Studio, Azure writes the logs to the file system.</span><span class="sxs-lookup"><span data-stu-id="b04a7-358">By default, when you first enable web server logs by using Visual Studio, Azure writes the logs to the file system.</span></span> <span data-ttu-id="b04a7-359">As an alternative, you can use the Azure portal to specify that web server logs should be written to a blob container in a storage account.</span><span class="sxs-lookup"><span data-stu-id="b04a7-359">As an alternative, you can use the Azure portal to specify that web server logs should be written to a blob container in a storage account.</span></span>

<span data-ttu-id="b04a7-360">If you use the portal to enable web server logging to an Azure storage account, and then disable logging in Visual Studio, when you re-enable logging in Visual Studio your storage account settings are restored.</span><span class="sxs-lookup"><span data-stu-id="b04a7-360">If you use the portal to enable web server logging to an Azure storage account, and then disable logging in Visual Studio, when you re-enable logging in Visual Studio your storage account settings are restored.</span></span>

## <a name="detailederrorlogs"></a><span data-ttu-id="b04a7-361">View detailed error message logs</span><span class="sxs-lookup"><span data-stu-id="b04a7-361">View detailed error message logs</span></span>
<span data-ttu-id="b04a7-362">Detailed error logs provide some additional information about HTTP requests that result in error response codes (400 or above).</span><span class="sxs-lookup"><span data-stu-id="b04a7-362">Detailed error logs provide some additional information about HTTP requests that result in error response codes (400 or above).</span></span> <span data-ttu-id="b04a7-363">In order to see them in the **Output** window, you have to enable them for the web app and tell Visual Studio that you want to monitor them.</span><span class="sxs-lookup"><span data-stu-id="b04a7-363">In order to see them in the **Output** window, you have to enable them for the web app and tell Visual Studio that you want to monitor them.</span></span>

1. <span data-ttu-id="b04a7-364">In the **Azure Web App Configuration** tab that you opened from **Server Explorer**, change **Detailed Error Messages** to **On**, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-364">In the **Azure Web App Configuration** tab that you opened from **Server Explorer**, change **Detailed Error Messages** to **On**, and then click **Save**.</span></span>

    ![Enable detailed error messages](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailedlogson.png)
2. <span data-ttu-id="b04a7-366">In the **Output** Window, click the **Specify which Azure logs to monitor** button.</span><span class="sxs-lookup"><span data-stu-id="b04a7-366">In the **Output** Window, click the **Specify which Azure logs to monitor** button.</span></span>
3. <span data-ttu-id="b04a7-367">In the **Azure Logging Options** dialog box, click **All logs**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-367">In the **Azure Logging Options** dialog box, click **All logs**, and then click **OK**.</span></span>

    ![Monitor all logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-monitorall.png)
4. <span data-ttu-id="b04a7-369">In the address bar of the browser window, add an extra character to the URL to cause a 404 error (for example, `http://localhost:53370/Home/Contactx`), and press Enter.</span><span class="sxs-lookup"><span data-stu-id="b04a7-369">In the address bar of the browser window, add an extra character to the URL to cause a 404 error (for example, `http://localhost:53370/Home/Contactx`), and press Enter.</span></span>

    <span data-ttu-id="b04a7-370">After several seconds the detailed error log appears in the Visual Studio **Output** window.</span><span class="sxs-lookup"><span data-stu-id="b04a7-370">After several seconds the detailed error log appears in the Visual Studio **Output** window.</span></span>

    ![Detailed error log in Output window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailederrorlog.png)

    <span data-ttu-id="b04a7-372">Control+click the link to see the log output formatted in a browser:</span><span class="sxs-lookup"><span data-stu-id="b04a7-372">Control+click the link to see the log output formatted in a browser:</span></span>

    ![Detailed error log in browser window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailederrorloginbrowser.png)

## <a name="downloadlogs"></a><span data-ttu-id="b04a7-374">Download file system logs</span><span class="sxs-lookup"><span data-stu-id="b04a7-374">Download file system logs</span></span>
<span data-ttu-id="b04a7-375">Any logs that you can monitor in the **Output** window can also be downloaded as a *.zip* file.</span><span class="sxs-lookup"><span data-stu-id="b04a7-375">Any logs that you can monitor in the **Output** window can also be downloaded as a *.zip* file.</span></span>

1. <span data-ttu-id="b04a7-376">In the **Output** window, click **Download Streaming Logs**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-376">In the **Output** window, click **Download Streaming Logs**.</span></span>

    ![Logs tab buttons](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-downloadicon.png)

    <span data-ttu-id="b04a7-378">File Explorer opens to your *Downloads* folder with the downloaded file selected.</span><span class="sxs-lookup"><span data-stu-id="b04a7-378">File Explorer opens to your *Downloads* folder with the downloaded file selected.</span></span>

    ![Downloaded file](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-downloadedfile.png)
2. <span data-ttu-id="b04a7-380">Extract the *.zip* file, and you see the following folder structure:</span><span class="sxs-lookup"><span data-stu-id="b04a7-380">Extract the *.zip* file, and you see the following folder structure:</span></span>

    ![Downloaded file](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-logfilefolders.png)

   * <span data-ttu-id="b04a7-382">Application tracing logs are in *.txt* files in the *LogFiles\Application* folder.</span><span class="sxs-lookup"><span data-stu-id="b04a7-382">Application tracing logs are in *.txt* files in the *LogFiles\Application* folder.</span></span>
   * <span data-ttu-id="b04a7-383">Web server logs are in *.log* files in the *LogFiles\http\RawLogs* folder.</span><span class="sxs-lookup"><span data-stu-id="b04a7-383">Web server logs are in *.log* files in the *LogFiles\http\RawLogs* folder.</span></span> <span data-ttu-id="b04a7-384">You can use a tool such as [Log Parser](http://www.microsoft.com/download/details.aspx?displaylang=en&id=24659) to view and manipulate these files.</span><span class="sxs-lookup"><span data-stu-id="b04a7-384">You can use a tool such as [Log Parser](http://www.microsoft.com/download/details.aspx?displaylang=en&id=24659) to view and manipulate these files.</span></span>
   * <span data-ttu-id="b04a7-385">Detailed error message logs are in *.html* files in the *LogFiles\DetailedErrors* folder.</span><span class="sxs-lookup"><span data-stu-id="b04a7-385">Detailed error message logs are in *.html* files in the *LogFiles\DetailedErrors* folder.</span></span>

     <span data-ttu-id="b04a7-386">(The *deployments* folder is for files created by source control publishing; it doesn't have anything related to Visual Studio publishing.</span><span class="sxs-lookup"><span data-stu-id="b04a7-386">(The *deployments* folder is for files created by source control publishing; it doesn't have anything related to Visual Studio publishing.</span></span> <span data-ttu-id="b04a7-387">The *Git* folder is for traces related to source control publishing and the log file streaming service.)</span><span class="sxs-lookup"><span data-stu-id="b04a7-387">The *Git* folder is for traces related to source control publishing and the log file streaming service.)</span></span>  

## <a name="storagelogs"></a><span data-ttu-id="b04a7-388">View storage logs</span><span class="sxs-lookup"><span data-stu-id="b04a7-388">View storage logs</span></span>
<span data-ttu-id="b04a7-389">Application tracing logs can also be sent to an Azure storage account, and you can view them in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b04a7-389">Application tracing logs can also be sent to an Azure storage account, and you can view them in Visual Studio.</span></span> <span data-ttu-id="b04a7-390">To do that you'll create a storage account, enable storage logs in the classic portal, and view them in the **Logs** tab of the **Azure Web App** window.</span><span class="sxs-lookup"><span data-stu-id="b04a7-390">To do that you'll create a storage account, enable storage logs in the classic portal, and view them in the **Logs** tab of the **Azure Web App** window.</span></span>

<span data-ttu-id="b04a7-391">You can send logs to any or all of three destinations:</span><span class="sxs-lookup"><span data-stu-id="b04a7-391">You can send logs to any or all of three destinations:</span></span>

* <span data-ttu-id="b04a7-392">The file system.</span><span class="sxs-lookup"><span data-stu-id="b04a7-392">The file system.</span></span>
* <span data-ttu-id="b04a7-393">Storage account tables.</span><span class="sxs-lookup"><span data-stu-id="b04a7-393">Storage account tables.</span></span>
* <span data-ttu-id="b04a7-394">Storage account blobs.</span><span class="sxs-lookup"><span data-stu-id="b04a7-394">Storage account blobs.</span></span>

<span data-ttu-id="b04a7-395">You can specify a different severity level for each destination.</span><span class="sxs-lookup"><span data-stu-id="b04a7-395">You can specify a different severity level for each destination.</span></span>

<span data-ttu-id="b04a7-396">Tables make it easy to view details of logs online, and they support streaming; you can query logs in tables and see new logs as they are being created.</span><span class="sxs-lookup"><span data-stu-id="b04a7-396">Tables make it easy to view details of logs online, and they support streaming; you can query logs in tables and see new logs as they are being created.</span></span> <span data-ttu-id="b04a7-397">Blobs make it easy to download logs in files and to analyze them using HDInsight, because HDInsight knows how to work with blob storage.</span><span class="sxs-lookup"><span data-stu-id="b04a7-397">Blobs make it easy to download logs in files and to analyze them using HDInsight, because HDInsight knows how to work with blob storage.</span></span> <span data-ttu-id="b04a7-398">For more information, see **Hadoop and MapReduce** in [Data Storage Options (Building Real-World Cloud Apps with Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options).</span><span class="sxs-lookup"><span data-stu-id="b04a7-398">For more information, see **Hadoop and MapReduce** in [Data Storage Options (Building Real-World Cloud Apps with Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options).</span></span>

<span data-ttu-id="b04a7-399">You currently have file system logs set to verbose level; the following steps walk you through setting up information level logs to go to storage account tables.</span><span class="sxs-lookup"><span data-stu-id="b04a7-399">You currently have file system logs set to verbose level; the following steps walk you through setting up information level logs to go to storage account tables.</span></span> <span data-ttu-id="b04a7-400">Information level means all logs created by calling `Trace.TraceInformation`, `Trace.TraceWarning`, and `Trace.TraceError` will be displayed, but not logs created by calling `Trace.WriteLine`.</span><span class="sxs-lookup"><span data-stu-id="b04a7-400">Information level means all logs created by calling `Trace.TraceInformation`, `Trace.TraceWarning`, and `Trace.TraceError` will be displayed, but not logs created by calling `Trace.WriteLine`.</span></span>

<span data-ttu-id="b04a7-401">Storage accounts offer more storage and longer-lasting retention for logs compared to the file system.</span><span class="sxs-lookup"><span data-stu-id="b04a7-401">Storage accounts offer more storage and longer-lasting retention for logs compared to the file system.</span></span> <span data-ttu-id="b04a7-402">Another advantage of sending application tracing logs to storage is that you get some additional information with each log that you don't get from file system logs.</span><span class="sxs-lookup"><span data-stu-id="b04a7-402">Another advantage of sending application tracing logs to storage is that you get some additional information with each log that you don't get from file system logs.</span></span>

1. <span data-ttu-id="b04a7-403">Right-click **Storage** under the Azure node, and then click **Create Storage Account**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-403">Right-click **Storage** under the Azure node, and then click **Create Storage Account**.</span></span>

![Create Storage Account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/createstor.png)

1. <span data-ttu-id="b04a7-405">In the **Create Storage Account** dialog, enter a name for the storage account.</span><span class="sxs-lookup"><span data-stu-id="b04a7-405">In the **Create Storage Account** dialog, enter a name for the storage account.</span></span>

    <span data-ttu-id="b04a7-406">The name must be must be unique (no other Azure storage account can have the same name).</span><span class="sxs-lookup"><span data-stu-id="b04a7-406">The name must be must be unique (no other Azure storage account can have the same name).</span></span> <span data-ttu-id="b04a7-407">If the name you enter is already in use you'll get a chance to change it.</span><span class="sxs-lookup"><span data-stu-id="b04a7-407">If the name you enter is already in use you'll get a chance to change it.</span></span>

    <span data-ttu-id="b04a7-408">The URL to access your storage account will be *{name}*.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="b04a7-408">The URL to access your storage account will be *{name}*.core.windows.net.</span></span>
2. <span data-ttu-id="b04a7-409">Set the **Region or Affinity Group** drop-down list to the region closest to you.</span><span class="sxs-lookup"><span data-stu-id="b04a7-409">Set the **Region or Affinity Group** drop-down list to the region closest to you.</span></span>

    <span data-ttu-id="b04a7-410">This setting specifies which Azure datacenter will host your storage account.</span><span class="sxs-lookup"><span data-stu-id="b04a7-410">This setting specifies which Azure datacenter will host your storage account.</span></span> <span data-ttu-id="b04a7-411">For this tutorial your choice won't make a noticeable difference, but for a production web app you want your web server and your storage account to be in the same region to minimize latency and data egress charges.</span><span class="sxs-lookup"><span data-stu-id="b04a7-411">For this tutorial your choice won't make a noticeable difference, but for a production web app you want your web server and your storage account to be in the same region to minimize latency and data egress charges.</span></span> <span data-ttu-id="b04a7-412">The web app (which you'll create later) should run in a region as close as possible to the browsers accessing your web app in order to minimize latency.</span><span class="sxs-lookup"><span data-stu-id="b04a7-412">The web app (which you'll create later) should run in a region as close as possible to the browsers accessing your web app in order to minimize latency.</span></span>
3. <span data-ttu-id="b04a7-413">Set the **Replication** drop-down list to **Locally redundant**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-413">Set the **Replication** drop-down list to **Locally redundant**.</span></span>
   
    <span data-ttu-id="b04a7-414">When geo-replication is enabled for a storage account, the stored content is replicated to a secondary datacenter to enable failover to that location in case of a major disaster in the primary location.</span><span class="sxs-lookup"><span data-stu-id="b04a7-414">When geo-replication is enabled for a storage account, the stored content is replicated to a secondary datacenter to enable failover to that location in case of a major disaster in the primary location.</span></span> <span data-ttu-id="b04a7-415">Geo-replication can incur additional costs.</span><span class="sxs-lookup"><span data-stu-id="b04a7-415">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="b04a7-416">For test and development accounts, you generally don't want to pay for geo-replication.</span><span class="sxs-lookup"><span data-stu-id="b04a7-416">For test and development accounts, you generally don't want to pay for geo-replication.</span></span> <span data-ttu-id="b04a7-417">For more information, see [Create, manage, or delete a storage account](../storage/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="b04a7-417">For more information, see [Create, manage, or delete a storage account](../storage/storage-create-storage-account.md).</span></span>
4. <span data-ttu-id="b04a7-418">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-418">Click **Create**.</span></span>

    ![New storage account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/newstorage.png)    
5. <span data-ttu-id="b04a7-420">In the Visual Studio **Azure Web App** window, click the **Logs** tab, and then click **Configure Logging in Management Portal**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-420">In the Visual Studio **Azure Web App** window, click the **Logs** tab, and then click **Configure Logging in Management Portal**.</span></span>

    <span data-ttu-id="b04a7-421"><!-- todo:screenshot of new portal if the VS page link goes to new portal --> ![Configure logging](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-configlogging.png)</span><span class="sxs-lookup"><span data-stu-id="b04a7-421"><!-- todo:screenshot of new portal if the VS page link goes to new portal --> ![Configure logging](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-configlogging.png)</span></span>

    <span data-ttu-id="b04a7-422">This opens the **Configure** tab in the classic portal for your web app.</span><span class="sxs-lookup"><span data-stu-id="b04a7-422">This opens the **Configure** tab in the classic portal for your web app.</span></span>
6. <span data-ttu-id="b04a7-423">In the classic portal's **Configure** tab, scroll down to the application diagnostics section, and then change **Application Logging (Table Storage)** to **On**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-423">In the classic portal's **Configure** tab, scroll down to the application diagnostics section, and then change **Application Logging (Table Storage)** to **On**.</span></span>
7. <span data-ttu-id="b04a7-424">Change **Logging Level** to **Information**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-424">Change **Logging Level** to **Information**.</span></span>
8. <span data-ttu-id="b04a7-425">Click **Manage Table Storage**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-425">Click **Manage Table Storage**.</span></span>

    ![Click Manage TableStorage](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-stgsettingsmgmtportal.png)

    <span data-ttu-id="b04a7-427">In the **Manage table storage for application diagnostics** box, you can choose your storage account if you have more than one.</span><span class="sxs-lookup"><span data-stu-id="b04a7-427">In the **Manage table storage for application diagnostics** box, you can choose your storage account if you have more than one.</span></span> <span data-ttu-id="b04a7-428">You can create a new table or use an existing one.</span><span class="sxs-lookup"><span data-stu-id="b04a7-428">You can create a new table or use an existing one.</span></span>

    ![Manage table storage](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-choosestorageacct.png)
9. <span data-ttu-id="b04a7-430">In the **Manage table storage for application diagnostics** box click the check mark to close the box.</span><span class="sxs-lookup"><span data-stu-id="b04a7-430">In the **Manage table storage for application diagnostics** box click the check mark to close the box.</span></span>
10. <span data-ttu-id="b04a7-431">In the classic portal's **Configure** tab, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-431">In the classic portal's **Configure** tab, click **Save**.</span></span>
11. <span data-ttu-id="b04a7-432">In the browser window that displays the application web app, click **Home**, then click **About**, and then click **Contact**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-432">In the browser window that displays the application web app, click **Home**, then click **About**, and then click **Contact**.</span></span>

     <span data-ttu-id="b04a7-433">The logging information produced by browsing these web pages will be written to the storage account.</span><span class="sxs-lookup"><span data-stu-id="b04a7-433">The logging information produced by browsing these web pages will be written to the storage account.</span></span>
12. <span data-ttu-id="b04a7-434">In the **Logs** tab of the **Azure Web App** window in Visual Studio, click **Refresh** under **Diagnostic Summary**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-434">In the **Logs** tab of the **Azure Web App** window in Visual Studio, click **Refresh** under **Diagnostic Summary**.</span></span>

     ![Click Refresh](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-refreshstorage.png)

     <span data-ttu-id="b04a7-436">The **Diagnostic Summary** section shows logs for the last 15 minutes by default.</span><span class="sxs-lookup"><span data-stu-id="b04a7-436">The **Diagnostic Summary** section shows logs for the last 15 minutes by default.</span></span> <span data-ttu-id="b04a7-437">You can change the period to see more logs.</span><span class="sxs-lookup"><span data-stu-id="b04a7-437">You can change the period to see more logs.</span></span>

     <span data-ttu-id="b04a7-438">(If you get a "table not found" error, verify that you browsed to the pages that do the tracing after you enabled **Application Logging (Storage)** and after you clicked **Save**.)</span><span class="sxs-lookup"><span data-stu-id="b04a7-438">(If you get a "table not found" error, verify that you browsed to the pages that do the tracing after you enabled **Application Logging (Storage)** and after you clicked **Save**.)</span></span>

     ![Storage logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-storagelogs.png)

     <span data-ttu-id="b04a7-440">Notice that in this view you see **Process ID** and **Thread ID** for each log, which you don't get in the file system logs.</span><span class="sxs-lookup"><span data-stu-id="b04a7-440">Notice that in this view you see **Process ID** and **Thread ID** for each log, which you don't get in the file system logs.</span></span> <span data-ttu-id="b04a7-441">You can see additional fields by viewing the Azure storage table directly.</span><span class="sxs-lookup"><span data-stu-id="b04a7-441">You can see additional fields by viewing the Azure storage table directly.</span></span>
13. <span data-ttu-id="b04a7-442">Click **View all application logs**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-442">Click **View all application logs**.</span></span>

     <span data-ttu-id="b04a7-443">The trace log table appears in the Azure storage table viewer.</span><span class="sxs-lookup"><span data-stu-id="b04a7-443">The trace log table appears in the Azure storage table viewer.</span></span>

     <span data-ttu-id="b04a7-444">(If you get a "sequence contains no elements" error, open **Server Explorer**, expand the node for your storage account under the **Azure** node, and then right-click **Tables** and click **Refresh**.)</span><span class="sxs-lookup"><span data-stu-id="b04a7-444">(If you get a "sequence contains no elements" error, open **Server Explorer**, expand the node for your storage account under the **Azure** node, and then right-click **Tables** and click **Refresh**.)</span></span>

     ![Storage logs in table view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-tracelogtableview.png)

     <span data-ttu-id="b04a7-446">This view shows additional fields you don't see in any other views.</span><span class="sxs-lookup"><span data-stu-id="b04a7-446">This view shows additional fields you don't see in any other views.</span></span> <span data-ttu-id="b04a7-447">This view also enables you to filter logs by using special Query Builder UI for constructing a query.</span><span class="sxs-lookup"><span data-stu-id="b04a7-447">This view also enables you to filter logs by using special Query Builder UI for constructing a query.</span></span> <span data-ttu-id="b04a7-448">For more information, see Working with Table Resources - Filtering Entities in [Browsing Storage Resources with Server Explorer](http://msdn.microsoft.com/library/ff683677.aspx).</span><span class="sxs-lookup"><span data-stu-id="b04a7-448">For more information, see Working with Table Resources - Filtering Entities in [Browsing Storage Resources with Server Explorer](http://msdn.microsoft.com/library/ff683677.aspx).</span></span>
14. <span data-ttu-id="b04a7-449">To look at the details for a single row, double-click one of the rows.</span><span class="sxs-lookup"><span data-stu-id="b04a7-449">To look at the details for a single row, double-click one of the rows.</span></span>

     ![Trace table in Server Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-tracetablerow.png)

## <a name="failedrequestlogs"></a><span data-ttu-id="b04a7-451">View failed request tracing logs</span><span class="sxs-lookup"><span data-stu-id="b04a7-451">View failed request tracing logs</span></span>
<span data-ttu-id="b04a7-452">Failed request tracing logs are useful when you need to understand the details of how IIS is handling an HTTP request, in scenarios such as URL rewriting or authentication problems.</span><span class="sxs-lookup"><span data-stu-id="b04a7-452">Failed request tracing logs are useful when you need to understand the details of how IIS is handling an HTTP request, in scenarios such as URL rewriting or authentication problems.</span></span>

<span data-ttu-id="b04a7-453">Azure web apps use the same failed request tracing functionality that has been available with IIS 7.0 and later.</span><span class="sxs-lookup"><span data-stu-id="b04a7-453">Azure web apps use the same failed request tracing functionality that has been available with IIS 7.0 and later.</span></span> <span data-ttu-id="b04a7-454">You don't have access to the IIS settings that configure which errors get logged, however.</span><span class="sxs-lookup"><span data-stu-id="b04a7-454">You don't have access to the IIS settings that configure which errors get logged, however.</span></span> <span data-ttu-id="b04a7-455">When you enable failed request tracing, all errors are captured.</span><span class="sxs-lookup"><span data-stu-id="b04a7-455">When you enable failed request tracing, all errors are captured.</span></span>

<span data-ttu-id="b04a7-456">You can enable failed request tracing by using Visual Studio, but you can't view them in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b04a7-456">You can enable failed request tracing by using Visual Studio, but you can't view them in Visual Studio.</span></span> <span data-ttu-id="b04a7-457">These logs are XML files.</span><span class="sxs-lookup"><span data-stu-id="b04a7-457">These logs are XML files.</span></span> <span data-ttu-id="b04a7-458">The streaming log service only monitors files that are deemed readable in plain text mode:  *.txt*, *.html*, and *.log* files.</span><span class="sxs-lookup"><span data-stu-id="b04a7-458">The streaming log service only monitors files that are deemed readable in plain text mode:  *.txt*, *.html*, and *.log* files.</span></span>

<span data-ttu-id="b04a7-459">You can view failed request tracing logs in a browser directly via FTP or locally after using an FTP tool to download them to your local computer.</span><span class="sxs-lookup"><span data-stu-id="b04a7-459">You can view failed request tracing logs in a browser directly via FTP or locally after using an FTP tool to download them to your local computer.</span></span> <span data-ttu-id="b04a7-460">In this section you'll view them in a browser directly.</span><span class="sxs-lookup"><span data-stu-id="b04a7-460">In this section you'll view them in a browser directly.</span></span>

1. <span data-ttu-id="b04a7-461">In the **Configuration** tab of the **Azure Web App** window that you opened from **Server Explorer**, change **Failed Request Tracing** to **On**, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-461">In the **Configuration** tab of the **Azure Web App** window that you opened from **Server Explorer**, change **Failed Request Tracing** to **On**, and then click **Save**.</span></span>

    ![Enable failed request tracing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-failedrequeston.png)
2. <span data-ttu-id="b04a7-463">In the address bar of the browser window that shows the web app, add an extra character to the URL and click Enter to cause a 404 error.</span><span class="sxs-lookup"><span data-stu-id="b04a7-463">In the address bar of the browser window that shows the web app, add an extra character to the URL and click Enter to cause a 404 error.</span></span>

    <span data-ttu-id="b04a7-464">This causes a failed request tracing log to be created, and the following steps show how to view or download the log.</span><span class="sxs-lookup"><span data-stu-id="b04a7-464">This causes a failed request tracing log to be created, and the following steps show how to view or download the log.</span></span>
3. <span data-ttu-id="b04a7-465">In Visual Studio, in the **Configuration** tab of the **Azure Web App** window, click **Open in Management Portal**.</span><span class="sxs-lookup"><span data-stu-id="b04a7-465">In Visual Studio, in the **Configuration** tab of the **Azure Web App** window, click **Open in Management Portal**.</span></span>
4. <span data-ttu-id="b04a7-466">In the [Azure Portal](https://portal.azure.com) **Settings** blade for your web app, click **Deployment credentials**, and then enter a new user name and password.</span><span class="sxs-lookup"><span data-stu-id="b04a7-466">In the [Azure Portal](https://portal.azure.com) **Settings** blade for your web app, click **Deployment credentials**, and then enter a new user name and password.</span></span>

    ![New FTP user name and password](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-enterftpcredentials.png)

    <span data-ttu-id="b04a7-468">\*\*When you log in, you have to use the full user name with the web app name prefixed to it.</span><span class="sxs-lookup"><span data-stu-id="b04a7-468">\*\*When you log in, you have to use the full user name with the web app name prefixed to it.</span></span> <span data-ttu-id="b04a7-469">For example, if you enter "myid" as a user name and the site is "myexample", you log in as "myexample\myid".</span><span class="sxs-lookup"><span data-stu-id="b04a7-469">For example, if you enter "myid" as a user name and the site is "myexample", you log in as "myexample\myid".</span></span>
5. <span data-ttu-id="b04a7-470">In a new browser window, go to the URL that is shown under **FTP hostname** or **FTPS hostname** in the **Web App** blade for your web app.</span><span class="sxs-lookup"><span data-stu-id="b04a7-470">In a new browser window, go to the URL that is shown under **FTP hostname** or **FTPS hostname** in the **Web App** blade for your web app.</span></span>
6. <span data-ttu-id="b04a7-471">Log in using the FTP credentials that you created earlier (including the web app name prefix for the user name).</span><span class="sxs-lookup"><span data-stu-id="b04a7-471">Log in using the FTP credentials that you created earlier (including the web app name prefix for the user name).</span></span>

    <span data-ttu-id="b04a7-472">The browser shows the root folder of the web app.</span><span class="sxs-lookup"><span data-stu-id="b04a7-472">The browser shows the root folder of the web app.</span></span>
7. <span data-ttu-id="b04a7-473">Open the *LogFiles* folder.</span><span class="sxs-lookup"><span data-stu-id="b04a7-473">Open the *LogFiles* folder.</span></span>

    ![Open LogFiles folder](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-logfilesfolder.png)
8. <span data-ttu-id="b04a7-475">Open the folder that is named W3SVC plus a numeric value.</span><span class="sxs-lookup"><span data-stu-id="b04a7-475">Open the folder that is named W3SVC plus a numeric value.</span></span>

    ![Open W3SVC folder](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-w3svcfolder.png)

    <span data-ttu-id="b04a7-477">The folder contains XML files for any errors that have been logged after you enabled failed request tracing, and an XSL file that a browser can use to format the XML.</span><span class="sxs-lookup"><span data-stu-id="b04a7-477">The folder contains XML files for any errors that have been logged after you enabled failed request tracing, and an XSL file that a browser can use to format the XML.</span></span>

    ![W3SVC folder](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-w3svcfoldercontents.png)
9. <span data-ttu-id="b04a7-479">Click the XML file for the failed request that you want to see tracing information for.</span><span class="sxs-lookup"><span data-stu-id="b04a7-479">Click the XML file for the failed request that you want to see tracing information for.</span></span>

    <span data-ttu-id="b04a7-480">The following illustration shows part of the tracing information for a sample error.</span><span class="sxs-lookup"><span data-stu-id="b04a7-480">The following illustration shows part of the tracing information for a sample error.</span></span>

    ![Failed request tracing in browser](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-troubleshoot-visual-studio/tws-failedrequestinbrowser.png)

## <a name="nextsteps"></a><span data-ttu-id="b04a7-482">Next Steps</span><span class="sxs-lookup"><span data-stu-id="b04a7-482">Next Steps</span></span>
<span data-ttu-id="b04a7-483">You've seen how Visual Studio makes it easy to view logs created by an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="b04a7-483">You've seen how Visual Studio makes it easy to view logs created by an Azure web app.</span></span> <span data-ttu-id="b04a7-484">The following sections provide links to more resources on related topics:</span><span class="sxs-lookup"><span data-stu-id="b04a7-484">The following sections provide links to more resources on related topics:</span></span>

* <span data-ttu-id="b04a7-485">Azure web app troubleshooting</span><span class="sxs-lookup"><span data-stu-id="b04a7-485">Azure web app troubleshooting</span></span>
* <span data-ttu-id="b04a7-486">Debugging in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b04a7-486">Debugging in Visual Studio</span></span>
* <span data-ttu-id="b04a7-487">Remote debugging in Azure</span><span class="sxs-lookup"><span data-stu-id="b04a7-487">Remote debugging in Azure</span></span>
* <span data-ttu-id="b04a7-488">Tracing in ASP.NET applications</span><span class="sxs-lookup"><span data-stu-id="b04a7-488">Tracing in ASP.NET applications</span></span>
* <span data-ttu-id="b04a7-489">Analyzing web server logs</span><span class="sxs-lookup"><span data-stu-id="b04a7-489">Analyzing web server logs</span></span>
* <span data-ttu-id="b04a7-490">Analyzing failed request tracing logs</span><span class="sxs-lookup"><span data-stu-id="b04a7-490">Analyzing failed request tracing logs</span></span>
* <span data-ttu-id="b04a7-491">Debugging Cloud Services</span><span class="sxs-lookup"><span data-stu-id="b04a7-491">Debugging Cloud Services</span></span>

### <a name="azure-web-app-troubleshooting"></a><span data-ttu-id="b04a7-492">Azure web app troubleshooting</span><span class="sxs-lookup"><span data-stu-id="b04a7-492">Azure web app troubleshooting</span></span>
<span data-ttu-id="b04a7-493">For more information about troubleshooting web apps in Azure App Service, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="b04a7-493">For more information about troubleshooting web apps in Azure App Service, see the following resources:</span></span>

* [<span data-ttu-id="b04a7-494">How to monitor web apps</span><span class="sxs-lookup"><span data-stu-id="b04a7-494">How to monitor web apps</span></span>](/manage/services/web-sites/how-to-monitor-websites/)
* <span data-ttu-id="b04a7-495">[Investigating Memory Leaks in Azure Web Apps with Visual Studio 2013](http://blogs.msdn.com/b/visualstudioalm/archive/2013/12/20/investigating-memory-leaks-in-azure-web-sites-with-visual-studio-2013.aspx).</span><span class="sxs-lookup"><span data-stu-id="b04a7-495">[Investigating Memory Leaks in Azure Web Apps with Visual Studio 2013](http://blogs.msdn.com/b/visualstudioalm/archive/2013/12/20/investigating-memory-leaks-in-azure-web-sites-with-visual-studio-2013.aspx).</span></span> <span data-ttu-id="b04a7-496">Microsoft ALM blog post about Visual Studio features for analyzing managed memory issues.</span><span class="sxs-lookup"><span data-stu-id="b04a7-496">Microsoft ALM blog post about Visual Studio features for analyzing managed memory issues.</span></span>
* <span data-ttu-id="b04a7-497">[Azure web apps online tools you should know about](https://azure.microsoft.com/blog/2014/03/28/windows-azure-websites-online-tools-you-should-know-about-2/).</span><span class="sxs-lookup"><span data-stu-id="b04a7-497">[Azure web apps online tools you should know about](https://azure.microsoft.com/blog/2014/03/28/windows-azure-websites-online-tools-you-should-know-about-2/).</span></span> <span data-ttu-id="b04a7-498">Blog post by Amit Apple.</span><span class="sxs-lookup"><span data-stu-id="b04a7-498">Blog post by Amit Apple.</span></span>

<span data-ttu-id="b04a7-499">For help with a specific troubleshooting question, start a thread in one of the following forums:</span><span class="sxs-lookup"><span data-stu-id="b04a7-499">For help with a specific troubleshooting question, start a thread in one of the following forums:</span></span>

* <span data-ttu-id="b04a7-500">[The Azure forum on the ASP.NET site](http://forums.asp.net/1247.aspx/1?Azure+and+ASP+NET).</span><span class="sxs-lookup"><span data-stu-id="b04a7-500">[The Azure forum on the ASP.NET site](http://forums.asp.net/1247.aspx/1?Azure+and+ASP+NET).</span></span>
* <span data-ttu-id="b04a7-501">[The Azure forum on MSDN](http://social.msdn.microsoft.com/Forums/windowsazure/).</span><span class="sxs-lookup"><span data-stu-id="b04a7-501">[The Azure forum on MSDN](http://social.msdn.microsoft.com/Forums/windowsazure/).</span></span>
* <span data-ttu-id="b04a7-502">[StackOverflow.com](http://www.stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="b04a7-502">[StackOverflow.com](http://www.stackoverflow.com).</span></span>

### <a name="debugging-in-visual-studio"></a><span data-ttu-id="b04a7-503">Debugging in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b04a7-503">Debugging in Visual Studio</span></span>
<span data-ttu-id="b04a7-504">For more information about how to use debug mode in Visual Studio, see the [Debugging in Visual Studio](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx) MSDN topic and [Debugging Tips with Visual Studio 2010](http://weblogs.asp.net/scottgu/archive/2010/08/18/debugging-tips-with-visual-studio-2010.aspx).</span><span class="sxs-lookup"><span data-stu-id="b04a7-504">For more information about how to use debug mode in Visual Studio, see the [Debugging in Visual Studio](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx) MSDN topic and [Debugging Tips with Visual Studio 2010](http://weblogs.asp.net/scottgu/archive/2010/08/18/debugging-tips-with-visual-studio-2010.aspx).</span></span>

### <a name="remote-debugging-in-azure"></a><span data-ttu-id="b04a7-505">Remote debugging in Azure</span><span class="sxs-lookup"><span data-stu-id="b04a7-505">Remote debugging in Azure</span></span>
<span data-ttu-id="b04a7-506">For more information about remote debugging for Azure web apps and WebJobs, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="b04a7-506">For more information about remote debugging for Azure web apps and WebJobs, see the following resources:</span></span>

* <span data-ttu-id="b04a7-507">[Introduction to Remote Debugging Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/05/06/introduction-to-remote-debugging-on-azure-web-sites/).</span><span class="sxs-lookup"><span data-stu-id="b04a7-507">[Introduction to Remote Debugging Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/05/06/introduction-to-remote-debugging-on-azure-web-sites/).</span></span>
* [<span data-ttu-id="b04a7-508">Introduction to Remote Debugging Azure App Service Web Apps part 2 - Inside Remote debugging</span><span class="sxs-lookup"><span data-stu-id="b04a7-508">Introduction to Remote Debugging Azure App Service Web Apps part 2 - Inside Remote debugging</span></span>](https://azure.microsoft.com/blog/2014/05/07/introduction-to-remote-debugging-azure-web-sites-part-2-inside-remote-debugging/)
* [<span data-ttu-id="b04a7-509">Introduction to Remote Debugging on Azure App Service Web Apps part 3 - Multi-Instance environment and GIT</span><span class="sxs-lookup"><span data-stu-id="b04a7-509">Introduction to Remote Debugging on Azure App Service Web Apps part 3 - Multi-Instance environment and GIT</span></span>](https://azure.microsoft.com/blog/2014/05/08/introduction-to-remote-debugging-on-azure-web-sites-part-3-multi-instance-environment-and-git/)
* [<span data-ttu-id="b04a7-510">WebJobs Debugging (video)</span><span class="sxs-lookup"><span data-stu-id="b04a7-510">WebJobs Debugging (video)</span></span>](https://www.youtube.com/watch?v=ncQm9q5ZFZs&list=UU_SjTh-ZltPmTYzAybypB-g&index=1)

<span data-ttu-id="b04a7-511">If your web app uses an Azure Web API or Mobile Services back-end and you need to debug that, see [Debugging .NET Backend in Visual Studio](http://blogs.msdn.com/b/azuremobile/archive/2014/03/14/debugging-net-backend-in-visual-studio.aspx).</span><span class="sxs-lookup"><span data-stu-id="b04a7-511">If your web app uses an Azure Web API or Mobile Services back-end and you need to debug that, see [Debugging .NET Backend in Visual Studio](http://blogs.msdn.com/b/azuremobile/archive/2014/03/14/debugging-net-backend-in-visual-studio.aspx).</span></span>

### <a name="tracing-in-aspnet-applications"></a><span data-ttu-id="b04a7-512">Tracing in ASP.NET applications</span><span class="sxs-lookup"><span data-stu-id="b04a7-512">Tracing in ASP.NET applications</span></span>
<span data-ttu-id="b04a7-513">There are no thorough and up-to-date introductions to ASP.NET tracing available on the Internet.</span><span class="sxs-lookup"><span data-stu-id="b04a7-513">There are no thorough and up-to-date introductions to ASP.NET tracing available on the Internet.</span></span> <span data-ttu-id="b04a7-514">The best you can do is get started with old introductory materials written for Web Forms because MVC didn't exist yet, and supplement that with newer blog posts that focus on specific issues.</span><span class="sxs-lookup"><span data-stu-id="b04a7-514">The best you can do is get started with old introductory materials written for Web Forms because MVC didn't exist yet, and supplement that with newer blog posts that focus on specific issues.</span></span> <span data-ttu-id="b04a7-515">Some good places to start are the following resources:</span><span class="sxs-lookup"><span data-stu-id="b04a7-515">Some good places to start are the following resources:</span></span>

* <span data-ttu-id="b04a7-516">[Monitoring and Telemetry (Building Real-World Cloud Apps with Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry).</span><span class="sxs-lookup"><span data-stu-id="b04a7-516">[Monitoring and Telemetry (Building Real-World Cloud Apps with Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry).</span></span><br>
  <span data-ttu-id="b04a7-517">E-book chapter with recommendations for tracing in Azure cloud applications.</span><span class="sxs-lookup"><span data-stu-id="b04a7-517">E-book chapter with recommendations for tracing in Azure cloud applications.</span></span>
* [<span data-ttu-id="b04a7-518">ASP.NET Tracing</span><span class="sxs-lookup"><span data-stu-id="b04a7-518">ASP.NET Tracing</span></span>](http://msdn.microsoft.com/library/ms972204.aspx)<br/>
  <span data-ttu-id="b04a7-519">Old but still a good resource for a basic introduction to the subject.</span><span class="sxs-lookup"><span data-stu-id="b04a7-519">Old but still a good resource for a basic introduction to the subject.</span></span>
* [<span data-ttu-id="b04a7-520">Trace Listeners</span><span class="sxs-lookup"><span data-stu-id="b04a7-520">Trace Listeners</span></span>](http://msdn.microsoft.com/library/4y5y10s7.aspx)<br/>
  <span data-ttu-id="b04a7-521">Information about trace listeners but doesn't mention the [WebPageTraceListener](http://msdn.microsoft.com/library/system.web.webpagetracelistener.aspx).</span><span class="sxs-lookup"><span data-stu-id="b04a7-521">Information about trace listeners but doesn't mention the [WebPageTraceListener](http://msdn.microsoft.com/library/system.web.webpagetracelistener.aspx).</span></span>
* [<span data-ttu-id="b04a7-522">Walkthrough: Integrating ASP.NET Tracing with System.Diagnostics Tracing</span><span class="sxs-lookup"><span data-stu-id="b04a7-522">Walkthrough: Integrating ASP.NET Tracing with System.Diagnostics Tracing</span></span>](http://msdn.microsoft.com/library/b0ectfxd.aspx)<br/>
  <span data-ttu-id="b04a7-523">This too is old, but includes some additional information that the introductory article doesn't cover.</span><span class="sxs-lookup"><span data-stu-id="b04a7-523">This too is old, but includes some additional information that the introductory article doesn't cover.</span></span>
* [<span data-ttu-id="b04a7-524">Tracing in ASP.NET MVC Razor Views</span><span class="sxs-lookup"><span data-stu-id="b04a7-524">Tracing in ASP.NET MVC Razor Views</span></span>](http://blogs.msdn.com/b/webdev/archive/2013/07/16/tracing-in-asp-net-mvc-razor-views.aspx)<br/>
  <span data-ttu-id="b04a7-525">Besides tracing in Razor views, the post also explains how to create an error filter in order to log all unhandled exceptions in an MVC application.</span><span class="sxs-lookup"><span data-stu-id="b04a7-525">Besides tracing in Razor views, the post also explains how to create an error filter in order to log all unhandled exceptions in an MVC application.</span></span> <span data-ttu-id="b04a7-526">For information about how to log all unhandled exceptions in a Web Forms application, see the Global.asax example in [Complete Example for Error Handlers](http://msdn.microsoft.com/library/bb397417.aspx) on MSDN.</span><span class="sxs-lookup"><span data-stu-id="b04a7-526">For information about how to log all unhandled exceptions in a Web Forms application, see the Global.asax example in [Complete Example for Error Handlers](http://msdn.microsoft.com/library/bb397417.aspx) on MSDN.</span></span> <span data-ttu-id="b04a7-527">In either MVC or Web Forms, if you want to log certain exceptions but let the default framework handling take effect for them, you can catch and rethrow as in the following example:</span><span class="sxs-lookup"><span data-stu-id="b04a7-527">In either MVC or Web Forms, if you want to log certain exceptions but let the default framework handling take effect for them, you can catch and rethrow as in the following example:</span></span>

        try
        {
           // Your code that might cause an exception to be thrown.
        }
        catch (Exception ex)
        {
            Trace.TraceError("Exception: " + ex.ToString());
            throw;
        }
* [<span data-ttu-id="b04a7-528">Streaming Diagnostics Trace Logging from the Azure Command Line (plus Glimpse!)</span><span class="sxs-lookup"><span data-stu-id="b04a7-528">Streaming Diagnostics Trace Logging from the Azure Command Line (plus Glimpse!)</span></span>](http://www.hanselman.com/blog/StreamingDiagnosticsTraceLoggingFromTheAzureCommandLinePlusGlimpse.aspx)<br/>
  <span data-ttu-id="b04a7-529">How to use the command line to do what this tutorial shows how to do in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b04a7-529">How to use the command line to do what this tutorial shows how to do in Visual Studio.</span></span> <span data-ttu-id="b04a7-530">[Glimpse](http://www.hanselman.com/blog/IfYoureNotUsingGlimpseWithASPNETForDebuggingAndProfilingYoureMissingOut.aspx) is a tool for debugging ASP.NET applications.</span><span class="sxs-lookup"><span data-stu-id="b04a7-530">[Glimpse](http://www.hanselman.com/blog/IfYoureNotUsingGlimpseWithASPNETForDebuggingAndProfilingYoureMissingOut.aspx) is a tool for debugging ASP.NET applications.</span></span>
* <span data-ttu-id="b04a7-531">[Using Web Apps Logging and Diagnostics - with David Ebbo](/documentation/videos/azure-web-site-logging-and-diagnostics/) and [Streaming Logs from Web Apps - with David Ebbo](/documentation/videos/log-streaming-with-azure-web-sites/)</span><span class="sxs-lookup"><span data-stu-id="b04a7-531">[Using Web Apps Logging and Diagnostics - with David Ebbo](/documentation/videos/azure-web-site-logging-and-diagnostics/) and [Streaming Logs from Web Apps - with David Ebbo](/documentation/videos/log-streaming-with-azure-web-sites/)</span></span><br>
  <span data-ttu-id="b04a7-532">Videos by Scott Hanselman and David Ebbo.</span><span class="sxs-lookup"><span data-stu-id="b04a7-532">Videos by Scott Hanselman and David Ebbo.</span></span>

<span data-ttu-id="b04a7-533">For error logging, an alternative to writing your own tracing code is to use an open-source logging framework such as [ELMAH](http://nuget.org/packages/elmah/).</span><span class="sxs-lookup"><span data-stu-id="b04a7-533">For error logging, an alternative to writing your own tracing code is to use an open-source logging framework such as [ELMAH](http://nuget.org/packages/elmah/).</span></span> <span data-ttu-id="b04a7-534">For more information, see [Scott Hanselman's blog posts about ELMAH](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx).</span><span class="sxs-lookup"><span data-stu-id="b04a7-534">For more information, see [Scott Hanselman's blog posts about ELMAH](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx).</span></span>

<span data-ttu-id="b04a7-535">Also, note that you don't have to use ASP.NET or System.Diagnostics tracing if you want to get streaming logs from Azure.</span><span class="sxs-lookup"><span data-stu-id="b04a7-535">Also, note that you don't have to use ASP.NET or System.Diagnostics tracing if you want to get streaming logs from Azure.</span></span> <span data-ttu-id="b04a7-536">The Azure web app streaming log service will stream any *.txt*, *.html*, or *.log* file that it finds in the *LogFiles* folder.</span><span class="sxs-lookup"><span data-stu-id="b04a7-536">The Azure web app streaming log service will stream any *.txt*, *.html*, or *.log* file that it finds in the *LogFiles* folder.</span></span> <span data-ttu-id="b04a7-537">Therefore, you could create your own logging system that writes to the file system of the web app, and your file will be automatically streamed and downloaded.</span><span class="sxs-lookup"><span data-stu-id="b04a7-537">Therefore, you could create your own logging system that writes to the file system of the web app, and your file will be automatically streamed and downloaded.</span></span> <span data-ttu-id="b04a7-538">All you have to do is write application code that creates files in the *d:\home\logfiles* folder.</span><span class="sxs-lookup"><span data-stu-id="b04a7-538">All you have to do is write application code that creates files in the *d:\home\logfiles* folder.</span></span>

### <a name="analyzing-web-server-logs"></a><span data-ttu-id="b04a7-539">Analyzing web server logs</span><span class="sxs-lookup"><span data-stu-id="b04a7-539">Analyzing web server logs</span></span>
<span data-ttu-id="b04a7-540">For more information about analyzing web server logs, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="b04a7-540">For more information about analyzing web server logs, see the following resources:</span></span>

* [<span data-ttu-id="b04a7-541">LogParser</span><span class="sxs-lookup"><span data-stu-id="b04a7-541">LogParser</span></span>](http://www.microsoft.com/download/details.aspx?id=24659)<br/>
  <span data-ttu-id="b04a7-542">A tool for viewing data in web server logs (*.log* files).</span><span class="sxs-lookup"><span data-stu-id="b04a7-542">A tool for viewing data in web server logs (*.log* files).</span></span>
* [<span data-ttu-id="b04a7-543">Troubleshooting IIS Performance Issues or Application Errors using LogParser </span><span class="sxs-lookup"><span data-stu-id="b04a7-543">Troubleshooting IIS Performance Issues or Application Errors using LogParser </span></span>](http://www.iis.net/learn/troubleshoot/performance-issues/troubleshooting-iis-performance-issues-or-application-errors-using-logparser)<br/>
  <span data-ttu-id="b04a7-544">An introduction to the Log Parser tool that you can use to analyze web server logs.</span><span class="sxs-lookup"><span data-stu-id="b04a7-544">An introduction to the Log Parser tool that you can use to analyze web server logs.</span></span>
* [<span data-ttu-id="b04a7-545">Blog posts by Robert McMurray on using LogParser</span><span class="sxs-lookup"><span data-stu-id="b04a7-545">Blog posts by Robert McMurray on using LogParser</span></span>](http://blogs.msdn.com/b/robert_mcmurray/archive/tags/logparser/)<br/>
* [<span data-ttu-id="b04a7-546">The HTTP status code in IIS 7.0, IIS 7.5, and IIS 8.0</span><span class="sxs-lookup"><span data-stu-id="b04a7-546">The HTTP status code in IIS 7.0, IIS 7.5, and IIS 8.0</span></span>](http://support.microsoft.com/kb/943891)

### <a name="analyzing-failed-request-tracing-logs"></a><span data-ttu-id="b04a7-547">Analyzing failed request tracing logs</span><span class="sxs-lookup"><span data-stu-id="b04a7-547">Analyzing failed request tracing logs</span></span>
<span data-ttu-id="b04a7-548">The Microsoft TechNet website includes a [Using Failed Request Tracing](http://www.iis.net/learn/troubleshoot/using-failed-request-tracing) section which may be helpful for understanding how to use these logs.</span><span class="sxs-lookup"><span data-stu-id="b04a7-548">The Microsoft TechNet website includes a [Using Failed Request Tracing](http://www.iis.net/learn/troubleshoot/using-failed-request-tracing) section which may be helpful for understanding how to use these logs.</span></span> <span data-ttu-id="b04a7-549">However, this documentation focuses mainly on configuring failed request tracing in IIS, which you can't do in Azure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="b04a7-549">However, this documentation focuses mainly on configuring failed request tracing in IIS, which you can't do in Azure Web Apps.</span></span>

[GetStarted]: app-service-web-get-started-dotnet.md
[GetStartedWJ]: websites-dotnet-webjobs-sdk.md





















































