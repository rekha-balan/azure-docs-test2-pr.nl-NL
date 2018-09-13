---
title: Troubleshoot a web app in Azure App Service using Visual Studio
description: Learn how to troubleshoot an Azure web app by using remote debugging, tracing, and logging tools that are built in to Visual Studio 2013.
services: app-service
documentationcenter: .net
author: cephalin
manager: cfowler
editor: ''
ms.assetid: def8e481-7803-4371-aa55-64025d116c97
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/29/2016
ms.author: cephalin
ms.openlocfilehash: ba84d297420ca5a9b75b4cfa432373d3070e0d01
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869969"
---
# <a name="troubleshoot-a-web-app-in-azure-app-service-using-visual-studio"></a><span data-ttu-id="d673f-103">Troubleshoot a web app in Azure App Service using Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d673f-103">Troubleshoot a web app in Azure App Service using Visual Studio</span></span>
## <a name="overview"></a><span data-ttu-id="d673f-104">Overview</span><span class="sxs-lookup"><span data-stu-id="d673f-104">Overview</span></span>
<span data-ttu-id="d673f-105">This tutorial shows how to use Visual Studio tools to help debug a web app in [App Service](http://go.microsoft.com/fwlink/?LinkId=529714), by running in [debug mode](https://docs.microsoft.com/visualstudio/debugger/) remotely or by viewing application logs and web server logs.</span><span class="sxs-lookup"><span data-stu-id="d673f-105">This tutorial shows how to use Visual Studio tools to help debug a web app in [App Service](http://go.microsoft.com/fwlink/?LinkId=529714), by running in [debug mode](https://docs.microsoft.com/visualstudio/debugger/) remotely or by viewing application logs and web server logs.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="d673f-106">You'll learn:</span><span class="sxs-lookup"><span data-stu-id="d673f-106">You'll learn:</span></span>

* <span data-ttu-id="d673f-107">Which Azure web app management functions are available in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d673f-107">Which Azure web app management functions are available in Visual Studio.</span></span>
* <span data-ttu-id="d673f-108">How to use Visual Studio remote view to make quick changes in a remote web app.</span><span class="sxs-lookup"><span data-stu-id="d673f-108">How to use Visual Studio remote view to make quick changes in a remote web app.</span></span>
* <span data-ttu-id="d673f-109">How to run debug mode remotely while a project is running in Azure, both for a web app and for a WebJob.</span><span class="sxs-lookup"><span data-stu-id="d673f-109">How to run debug mode remotely while a project is running in Azure, both for a web app and for a WebJob.</span></span>
* <span data-ttu-id="d673f-110">How to create application trace logs and view them while the application is creating them.</span><span class="sxs-lookup"><span data-stu-id="d673f-110">How to create application trace logs and view them while the application is creating them.</span></span>
* <span data-ttu-id="d673f-111">How to view web server logs, including detailed error messages and failed request tracing.</span><span class="sxs-lookup"><span data-stu-id="d673f-111">How to view web server logs, including detailed error messages and failed request tracing.</span></span>
* <span data-ttu-id="d673f-112">How to send diagnostic logs to an Azure Storage account and view them there.</span><span class="sxs-lookup"><span data-stu-id="d673f-112">How to send diagnostic logs to an Azure Storage account and view them there.</span></span>

<span data-ttu-id="d673f-113">If you have Visual Studio Ultimate, you can also use [IntelliTrace](http://msdn.microsoft.com/library/vstudio/dd264915.aspx) for debugging.</span><span class="sxs-lookup"><span data-stu-id="d673f-113">If you have Visual Studio Ultimate, you can also use [IntelliTrace](http://msdn.microsoft.com/library/vstudio/dd264915.aspx) for debugging.</span></span> <span data-ttu-id="d673f-114">IntelliTrace is not covered in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="d673f-114">IntelliTrace is not covered in this tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d673f-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d673f-115">Prerequisites</span></span>
<span data-ttu-id="d673f-116">This tutorial works with the development environment, web project, and Azure web app that you set up in [Get started with Azure and ASP.NET](app-service-web-get-started-dotnet-framework.md).</span><span class="sxs-lookup"><span data-stu-id="d673f-116">This tutorial works with the development environment, web project, and Azure web app that you set up in [Get started with Azure and ASP.NET](app-service-web-get-started-dotnet-framework.md).</span></span> <span data-ttu-id="d673f-117">For the WebJobs sections, you'll need the application that you create in [Get Started with the Azure WebJobs SDK][GetStartedWJ].</span><span class="sxs-lookup"><span data-stu-id="d673f-117">For the WebJobs sections, you'll need the application that you create in [Get Started with the Azure WebJobs SDK][GetStartedWJ].</span></span>

<span data-ttu-id="d673f-118">The code samples shown in this tutorial are for a C# MVC web application, but the troubleshooting procedures are the same for Visual Basic and Web Forms applications.</span><span class="sxs-lookup"><span data-stu-id="d673f-118">The code samples shown in this tutorial are for a C# MVC web application, but the troubleshooting procedures are the same for Visual Basic and Web Forms applications.</span></span>

<span data-ttu-id="d673f-119">The tutorial assumes you're using Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="d673f-119">The tutorial assumes you're using Visual Studio 2017.</span></span> 

<span data-ttu-id="d673f-120">The streaming logs feature only works for applications that target .NET Framework 4 or later.</span><span class="sxs-lookup"><span data-stu-id="d673f-120">The streaming logs feature only works for applications that target .NET Framework 4 or later.</span></span>

## <a name="sitemanagement"></a><span data-ttu-id="d673f-121">Web app configuration and management</span><span class="sxs-lookup"><span data-stu-id="d673f-121">Web app configuration and management</span></span>
<span data-ttu-id="d673f-122">Visual Studio provides access to a subset of the web app management functions and configuration settings available in the [Azure portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span><span class="sxs-lookup"><span data-stu-id="d673f-122">Visual Studio provides access to a subset of the web app management functions and configuration settings available in the [Azure portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="d673f-123">In this section, you'll see what's available by using **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="d673f-123">In this section, you'll see what's available by using **Server Explorer**.</span></span> <span data-ttu-id="d673f-124">To see the latest Azure integration features, try out **Cloud Explorer** also.</span><span class="sxs-lookup"><span data-stu-id="d673f-124">To see the latest Azure integration features, try out **Cloud Explorer** also.</span></span> <span data-ttu-id="d673f-125">You can open both windows from the **View** menu.</span><span class="sxs-lookup"><span data-stu-id="d673f-125">You can open both windows from the **View** menu.</span></span>

1. <span data-ttu-id="d673f-126">If you aren't already signed in to Azure in Visual Studio, right-click **Azure** and select Connect to **Microsoft Azure Subscription** in **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="d673f-126">If you aren't already signed in to Azure in Visual Studio, right-click **Azure** and select Connect to **Microsoft Azure Subscription** in **Server Explorer**.</span></span>

    <span data-ttu-id="d673f-127">An alternative is to install a management certificate that enables access to your account.</span><span class="sxs-lookup"><span data-stu-id="d673f-127">An alternative is to install a management certificate that enables access to your account.</span></span> <span data-ttu-id="d673f-128">If you choose to install a certificate, right-click the **Azure** node in **Server Explorer**, and then select **Manage and Filter Subscriptions** in the context menu.</span><span class="sxs-lookup"><span data-stu-id="d673f-128">If you choose to install a certificate, right-click the **Azure** node in **Server Explorer**, and then select **Manage and Filter Subscriptions** in the context menu.</span></span> <span data-ttu-id="d673f-129">In the **Manage Microsoft Azure Subscriptions** dialog box, click the **Certificates** tab, and then click **Import**.</span><span class="sxs-lookup"><span data-stu-id="d673f-129">In the **Manage Microsoft Azure Subscriptions** dialog box, click the **Certificates** tab, and then click **Import**.</span></span> <span data-ttu-id="d673f-130">Follow the directions to download and then import a subscription file (also called a *.publishsettings* file) for your Azure account.</span><span class="sxs-lookup"><span data-stu-id="d673f-130">Follow the directions to download and then import a subscription file (also called a *.publishsettings* file) for your Azure account.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d673f-131">If you download a subscription file, save it to a folder outside your source code directories (for example, in the Downloads folder), and then delete it once the import has completed.</span><span class="sxs-lookup"><span data-stu-id="d673f-131">If you download a subscription file, save it to a folder outside your source code directories (for example, in the Downloads folder), and then delete it once the import has completed.</span></span> <span data-ttu-id="d673f-132">A malicious user who gains access to the subscription file can edit, create, and delete your Azure services.</span><span class="sxs-lookup"><span data-stu-id="d673f-132">A malicious user who gains access to the subscription file can edit, create, and delete your Azure services.</span></span>
   >
   >

    <span data-ttu-id="d673f-133">For more information about connecting to Azure resources from Visual Studio, see [Manage Accounts, Subscriptions, and Administrative Roles](http://go.microsoft.com/fwlink/?LinkId=324796#BKMK_AccountVCert).</span><span class="sxs-lookup"><span data-stu-id="d673f-133">For more information about connecting to Azure resources from Visual Studio, see [Manage Accounts, Subscriptions, and Administrative Roles](http://go.microsoft.com/fwlink/?LinkId=324796#BKMK_AccountVCert).</span></span>
2. <span data-ttu-id="d673f-134">In **Server Explorer**, expand **Azure** and expand **App Service**.</span><span class="sxs-lookup"><span data-stu-id="d673f-134">In **Server Explorer**, expand **Azure** and expand **App Service**.</span></span>
3. <span data-ttu-id="d673f-135">Expand the resource group that includes the web app that you created in [Create an ASP.NET web app in Azure](app-service-web-get-started-dotnet-framework.md), and then right-click the web app node and click **View Settings**.</span><span class="sxs-lookup"><span data-stu-id="d673f-135">Expand the resource group that includes the web app that you created in [Create an ASP.NET web app in Azure](app-service-web-get-started-dotnet-framework.md), and then right-click the web app node and click **View Settings**.</span></span>

    ![View Settings in Server Explorer](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-viewsettings.png)

    <span data-ttu-id="d673f-137">The **Azure Web App** tab appears, and you can see there the web app management and configuration tasks that are available in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d673f-137">The **Azure Web App** tab appears, and you can see there the web app management and configuration tasks that are available in Visual Studio.</span></span>

    ![Azure Web App window](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-configtab.png)

    <span data-ttu-id="d673f-139">In this tutorial, you'll use the logging and tracing drop-downs.</span><span class="sxs-lookup"><span data-stu-id="d673f-139">In this tutorial, you'll use the logging and tracing drop-downs.</span></span> <span data-ttu-id="d673f-140">You'll also use remote debugging but you'll use a different method to enable it.</span><span class="sxs-lookup"><span data-stu-id="d673f-140">You'll also use remote debugging but you'll use a different method to enable it.</span></span>

    <span data-ttu-id="d673f-141">For information about the App Settings and Connection Strings boxes in this window, see [Azure Web Apps: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span><span class="sxs-lookup"><span data-stu-id="d673f-141">For information about the App Settings and Connection Strings boxes in this window, see [Azure Web Apps: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span>

    <span data-ttu-id="d673f-142">If you want to perform a web app management task that can't be done in this window, click **Open in Management Portal** to open a browser window to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d673f-142">If you want to perform a web app management task that can't be done in this window, click **Open in Management Portal** to open a browser window to the Azure portal.</span></span>

## <a name="remoteview"></a><span data-ttu-id="d673f-143">Access web app files in Server Explorer</span><span class="sxs-lookup"><span data-stu-id="d673f-143">Access web app files in Server Explorer</span></span>
<span data-ttu-id="d673f-144">You typically deploy a web project with the `customErrors` flag in the Web.config file set to `On` or `RemoteOnly`, which means you don't get a helpful error message when something goes wrong.</span><span class="sxs-lookup"><span data-stu-id="d673f-144">You typically deploy a web project with the `customErrors` flag in the Web.config file set to `On` or `RemoteOnly`, which means you don't get a helpful error message when something goes wrong.</span></span> <span data-ttu-id="d673f-145">For many errors, all you get is a page like one of the following ones:</span><span class="sxs-lookup"><span data-stu-id="d673f-145">For many errors, all you get is a page like one of the following ones:</span></span>

<span data-ttu-id="d673f-146">**Server Error in '/' Application:**</span><span class="sxs-lookup"><span data-stu-id="d673f-146">**Server Error in '/' Application:**</span></span>

![Unhelpful error page](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror.png)

<span data-ttu-id="d673f-148">**An error occurred:**</span><span class="sxs-lookup"><span data-stu-id="d673f-148">**An error occurred:**</span></span>

![Unhelpful error page](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror1.png)

<span data-ttu-id="d673f-150">**The website cannot display the page**</span><span class="sxs-lookup"><span data-stu-id="d673f-150">**The website cannot display the page**</span></span>

![Unhelpful error page](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror2.png)

<span data-ttu-id="d673f-152">Frequently the easiest way to find the cause of the error is to enable detailed error messages, which the first of the preceding screenshots explains how to do.</span><span class="sxs-lookup"><span data-stu-id="d673f-152">Frequently the easiest way to find the cause of the error is to enable detailed error messages, which the first of the preceding screenshots explains how to do.</span></span> <span data-ttu-id="d673f-153">That requires a change in the deployed Web.config file.</span><span class="sxs-lookup"><span data-stu-id="d673f-153">That requires a change in the deployed Web.config file.</span></span> <span data-ttu-id="d673f-154">You could edit the *Web.config* file in the project and redeploy the project, or create a [Web.config transform](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) and deploy a debug build, but there's a quicker way: in **Solution Explorer**, you can directly view and edit files in the remote web app by using the *remote view* feature.</span><span class="sxs-lookup"><span data-stu-id="d673f-154">You could edit the *Web.config* file in the project and redeploy the project, or create a [Web.config transform](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) and deploy a debug build, but there's a quicker way: in **Solution Explorer**, you can directly view and edit files in the remote web app by using the *remote view* feature.</span></span>

1. <span data-ttu-id="d673f-155">In **Server Explorer**, expand **Azure**, expand **App Service**, expand the resource group that your web app is located in, and then expand the node for your web app.</span><span class="sxs-lookup"><span data-stu-id="d673f-155">In **Server Explorer**, expand **Azure**, expand **App Service**, expand the resource group that your web app is located in, and then expand the node for your web app.</span></span>

    <span data-ttu-id="d673f-156">You see nodes that give you access to the web app's content files and log files.</span><span class="sxs-lookup"><span data-stu-id="d673f-156">You see nodes that give you access to the web app's content files and log files.</span></span>
2. <span data-ttu-id="d673f-157">Expand the **Files** node, and double-click the *Web.config* file.</span><span class="sxs-lookup"><span data-stu-id="d673f-157">Expand the **Files** node, and double-click the *Web.config* file.</span></span>

    ![Open Web.config](./media/web-sites-dotnet-troubleshoot-visual-studio/webconfig.png)

    <span data-ttu-id="d673f-159">Visual Studio opens the Web.config file from the remote web app and shows [Remote] next to the file name in the title bar.</span><span class="sxs-lookup"><span data-stu-id="d673f-159">Visual Studio opens the Web.config file from the remote web app and shows [Remote] next to the file name in the title bar.</span></span>
3. <span data-ttu-id="d673f-160">Add the following line to the `system.web` element:</span><span class="sxs-lookup"><span data-stu-id="d673f-160">Add the following line to the `system.web` element:</span></span>

    `<customErrors mode="Off"></customErrors>`

    ![Edit Web.config](./media/web-sites-dotnet-troubleshoot-visual-studio/webconfigedit.png)
4. <span data-ttu-id="d673f-162">Refresh the browser that is showing the unhelpful error message, and now you get a detailed error message, such as the following example:</span><span class="sxs-lookup"><span data-stu-id="d673f-162">Refresh the browser that is showing the unhelpful error message, and now you get a detailed error message, such as the following example:</span></span>

    ![Detailed error message](./media/web-sites-dotnet-troubleshoot-visual-studio/detailederror.png)

    <span data-ttu-id="d673f-164">(The error shown was created by adding the line shown in red to *Views\Home\Index.cshtml*.)</span><span class="sxs-lookup"><span data-stu-id="d673f-164">(The error shown was created by adding the line shown in red to *Views\Home\Index.cshtml*.)</span></span>

<span data-ttu-id="d673f-165">Editing the Web.config file is only one example of scenarios in which the ability to read and edit files on your Azure web app make troubleshooting easier.</span><span class="sxs-lookup"><span data-stu-id="d673f-165">Editing the Web.config file is only one example of scenarios in which the ability to read and edit files on your Azure web app make troubleshooting easier.</span></span>

## <a name="remotedebug"></a><span data-ttu-id="d673f-166">Remote debugging web apps</span><span class="sxs-lookup"><span data-stu-id="d673f-166">Remote debugging web apps</span></span>
<span data-ttu-id="d673f-167">If the detailed error message doesn't provide enough information, and you can't re-create the error locally, another way to troubleshoot is to run in debug mode remotely.</span><span class="sxs-lookup"><span data-stu-id="d673f-167">If the detailed error message doesn't provide enough information, and you can't re-create the error locally, another way to troubleshoot is to run in debug mode remotely.</span></span> <span data-ttu-id="d673f-168">You can set breakpoints, manipulate memory directly, step through code, and even change the code path.</span><span class="sxs-lookup"><span data-stu-id="d673f-168">You can set breakpoints, manipulate memory directly, step through code, and even change the code path.</span></span>

<span data-ttu-id="d673f-169">Remote debugging does not work in Express editions of Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d673f-169">Remote debugging does not work in Express editions of Visual Studio.</span></span>

<span data-ttu-id="d673f-170">This section shows how to debug remotely using the project you create in [Create an ASP.NET web app in Azure](app-service-web-get-started-dotnet-framework.md).</span><span class="sxs-lookup"><span data-stu-id="d673f-170">This section shows how to debug remotely using the project you create in [Create an ASP.NET web app in Azure](app-service-web-get-started-dotnet-framework.md).</span></span>

1. <span data-ttu-id="d673f-171">Open the web project that you created in [Create an ASP.NET web app in Azure](app-service-web-get-started-dotnet-framework.md).</span><span class="sxs-lookup"><span data-stu-id="d673f-171">Open the web project that you created in [Create an ASP.NET web app in Azure](app-service-web-get-started-dotnet-framework.md).</span></span>

2. <span data-ttu-id="d673f-172">Open *Controllers\HomeController.cs*.</span><span class="sxs-lookup"><span data-stu-id="d673f-172">Open *Controllers\HomeController.cs*.</span></span>

3. <span data-ttu-id="d673f-173">Delete the `About()` method and insert the following code in its place.</span><span class="sxs-lookup"><span data-stu-id="d673f-173">Delete the `About()` method and insert the following code in its place.</span></span>

``` c#
public ActionResult About()
{
    string currentTime = DateTime.Now.ToLongTimeString();
    ViewBag.Message = "The current time is " + currentTime;
    return View();
}
```

4. <span data-ttu-id="d673f-174">[Set a breakpoint](https://docs.microsoft.com/visualstudio/debugger/) on the `ViewBag.Message` line.</span><span class="sxs-lookup"><span data-stu-id="d673f-174">[Set a breakpoint](https://docs.microsoft.com/visualstudio/debugger/) on the `ViewBag.Message` line.</span></span>

5. <span data-ttu-id="d673f-175">In **Solution Explorer**, right-click the project, and click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="d673f-175">In **Solution Explorer**, right-click the project, and click **Publish**.</span></span>

6. <span data-ttu-id="d673f-176">In the **Profile** drop-down list, select the same profile that you used in [Create an ASP.NET web app in Azure](app-service-web-get-started-dotnet-framework.md).</span><span class="sxs-lookup"><span data-stu-id="d673f-176">In the **Profile** drop-down list, select the same profile that you used in [Create an ASP.NET web app in Azure](app-service-web-get-started-dotnet-framework.md).</span></span> <span data-ttu-id="d673f-177">Then, click Settings.</span><span class="sxs-lookup"><span data-stu-id="d673f-177">Then, click Settings.</span></span>

7. <span data-ttu-id="d673f-178">In the **Publish** dialog, click the **Settings** tab, and then change **Configuration** to **Debug**, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="d673f-178">In the **Publish** dialog, click the **Settings** tab, and then change **Configuration** to **Debug**, and then click **Save**.</span></span>

    ![Publish in debug mode](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-publishdebug.png)

8. <span data-ttu-id="d673f-180">Click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="d673f-180">Click **Publish**.</span></span> <span data-ttu-id="d673f-181">After deployment finishes and your browser opens to the Azure URL of your web app, close the browser.</span><span class="sxs-lookup"><span data-stu-id="d673f-181">After deployment finishes and your browser opens to the Azure URL of your web app, close the browser.</span></span>

9. <span data-ttu-id="d673f-182">In **Server Explorer**, right-click your web app, and then click **Attach Debugger**.</span><span class="sxs-lookup"><span data-stu-id="d673f-182">In **Server Explorer**, right-click your web app, and then click **Attach Debugger**.</span></span>

    ![Attach debugger](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-attachdebugger.png)

    <span data-ttu-id="d673f-184">The browser automatically opens to your home page running in Azure.</span><span class="sxs-lookup"><span data-stu-id="d673f-184">The browser automatically opens to your home page running in Azure.</span></span> <span data-ttu-id="d673f-185">You might have to wait 20 seconds or so while Azure sets up the server for debugging.</span><span class="sxs-lookup"><span data-stu-id="d673f-185">You might have to wait 20 seconds or so while Azure sets up the server for debugging.</span></span> <span data-ttu-id="d673f-186">This delay only happens the first time you run in debug mode on a web app in a 48-hour period.</span><span class="sxs-lookup"><span data-stu-id="d673f-186">This delay only happens the first time you run in debug mode on a web app in a 48-hour period.</span></span> <span data-ttu-id="d673f-187">When you start debugging again in the same period, there isn't a delay.</span><span class="sxs-lookup"><span data-stu-id="d673f-187">When you start debugging again in the same period, there isn't a delay.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d673f-188">If you have any trouble starting the debugger, try to do it by using **Cloud Explorer** instead of **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="d673f-188">If you have any trouble starting the debugger, try to do it by using **Cloud Explorer** instead of **Server Explorer**.</span></span>
    >

10. <span data-ttu-id="d673f-189">Click **About** in the menu.</span><span class="sxs-lookup"><span data-stu-id="d673f-189">Click **About** in the menu.</span></span>

     <span data-ttu-id="d673f-190">Visual Studio stops on the breakpoint, and the code is running in Azure, not on your local computer.</span><span class="sxs-lookup"><span data-stu-id="d673f-190">Visual Studio stops on the breakpoint, and the code is running in Azure, not on your local computer.</span></span>

11. <span data-ttu-id="d673f-191">Hover over the `currentTime` variable to see the time value.</span><span class="sxs-lookup"><span data-stu-id="d673f-191">Hover over the `currentTime` variable to see the time value.</span></span>

     ![View variable in debug mode running in Azure](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugviewinwa.png)

     <span data-ttu-id="d673f-193">The time you see is the Azure server time, which may be in a different time zone than your local computer.</span><span class="sxs-lookup"><span data-stu-id="d673f-193">The time you see is the Azure server time, which may be in a different time zone than your local computer.</span></span>

12. <span data-ttu-id="d673f-194">Enter a new value for the `currentTime` variable, such as "Now running in Azure".</span><span class="sxs-lookup"><span data-stu-id="d673f-194">Enter a new value for the `currentTime` variable, such as "Now running in Azure".</span></span>

13. <span data-ttu-id="d673f-195">Press F5 to continue running.</span><span class="sxs-lookup"><span data-stu-id="d673f-195">Press F5 to continue running.</span></span>

     <span data-ttu-id="d673f-196">The About page running in Azure displays the new value that you entered into the currentTime variable.</span><span class="sxs-lookup"><span data-stu-id="d673f-196">The About page running in Azure displays the new value that you entered into the currentTime variable.</span></span>

     ![About page with new value](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugchangeinwa.png)

## <a name="remotedebugwj"></a> <span data-ttu-id="d673f-198">Remote debugging WebJobs</span><span class="sxs-lookup"><span data-stu-id="d673f-198">Remote debugging WebJobs</span></span>
<span data-ttu-id="d673f-199">This section shows how to debug remotely using the project and web app you create in [Get Started with the Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/wiki).</span><span class="sxs-lookup"><span data-stu-id="d673f-199">This section shows how to debug remotely using the project and web app you create in [Get Started with the Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/wiki).</span></span>

<span data-ttu-id="d673f-200">The features shown in this section are available only in Visual Studio 2013 with Update 4 or later.</span><span class="sxs-lookup"><span data-stu-id="d673f-200">The features shown in this section are available only in Visual Studio 2013 with Update 4 or later.</span></span>

<span data-ttu-id="d673f-201">Remote debugging only works with continuous WebJobs.</span><span class="sxs-lookup"><span data-stu-id="d673f-201">Remote debugging only works with continuous WebJobs.</span></span> <span data-ttu-id="d673f-202">Scheduled and on-demand WebJobs don't support debugging.</span><span class="sxs-lookup"><span data-stu-id="d673f-202">Scheduled and on-demand WebJobs don't support debugging.</span></span>

1. <span data-ttu-id="d673f-203">Open the web project that you created in [Get Started with the Azure WebJobs SDK][GetStartedWJ].</span><span class="sxs-lookup"><span data-stu-id="d673f-203">Open the web project that you created in [Get Started with the Azure WebJobs SDK][GetStartedWJ].</span></span>

2. <span data-ttu-id="d673f-204">In the ContosoAdsWebJob project, open *Functions.cs*.</span><span class="sxs-lookup"><span data-stu-id="d673f-204">In the ContosoAdsWebJob project, open *Functions.cs*.</span></span>

3. <span data-ttu-id="d673f-205">[Set a breakpoint](https://docs.microsoft.com/visualstudio/debugger/) on the first statement in the `GnerateThumbnail` method.</span><span class="sxs-lookup"><span data-stu-id="d673f-205">[Set a breakpoint](https://docs.microsoft.com/visualstudio/debugger/) on the first statement in the `GnerateThumbnail` method.</span></span>

    ![Set breakpoint](./media/web-sites-dotnet-troubleshoot-visual-studio/wjbreakpoint.png)

4. <span data-ttu-id="d673f-207">In **Solution Explorer**, right-click the web project (not the WebJob project), and click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="d673f-207">In **Solution Explorer**, right-click the web project (not the WebJob project), and click **Publish**.</span></span>

5. <span data-ttu-id="d673f-208">In the **Profile** drop-down list, select the same profile that you used in [Get Started with the Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/wiki).</span><span class="sxs-lookup"><span data-stu-id="d673f-208">In the **Profile** drop-down list, select the same profile that you used in [Get Started with the Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/wiki).</span></span>

6. <span data-ttu-id="d673f-209">Click the **Settings** tab, and change **Configuration** to **Debug**, and then click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="d673f-209">Click the **Settings** tab, and change **Configuration** to **Debug**, and then click **Publish**.</span></span>

    <span data-ttu-id="d673f-210">Visual Studio deploys the web and WebJob projects, and your browser opens to the Azure URL of your web app.</span><span class="sxs-lookup"><span data-stu-id="d673f-210">Visual Studio deploys the web and WebJob projects, and your browser opens to the Azure URL of your web app.</span></span>

7. <span data-ttu-id="d673f-211">In **Server Explorer**, expand **Azure > App Service > your resource group > your web app > WebJobs > Continuous**, and then right-click **ContosoAdsWebJob**.</span><span class="sxs-lookup"><span data-stu-id="d673f-211">In **Server Explorer**, expand **Azure > App Service > your resource group > your web app > WebJobs > Continuous**, and then right-click **ContosoAdsWebJob**.</span></span>

8. <span data-ttu-id="d673f-212">Click **Attach Debugger**.</span><span class="sxs-lookup"><span data-stu-id="d673f-212">Click **Attach Debugger**.</span></span>

    ![Attach debugger](./media/web-sites-dotnet-troubleshoot-visual-studio/wjattach.png)

    <span data-ttu-id="d673f-214">The browser automatically opens to your home page running in Azure.</span><span class="sxs-lookup"><span data-stu-id="d673f-214">The browser automatically opens to your home page running in Azure.</span></span> <span data-ttu-id="d673f-215">You might have to wait 20 seconds or so while Azure sets up the server for debugging.</span><span class="sxs-lookup"><span data-stu-id="d673f-215">You might have to wait 20 seconds or so while Azure sets up the server for debugging.</span></span> <span data-ttu-id="d673f-216">This delay only happens the first time you run in debug mode on a web app in a 48-hour period.</span><span class="sxs-lookup"><span data-stu-id="d673f-216">This delay only happens the first time you run in debug mode on a web app in a 48-hour period.</span></span> <span data-ttu-id="d673f-217">When you start debugging again in the same period, there isn't a delay.</span><span class="sxs-lookup"><span data-stu-id="d673f-217">When you start debugging again in the same period, there isn't a delay.</span></span>

9. <span data-ttu-id="d673f-218">In the web browser that is opened to the Contoso Ads home page, create a new ad.</span><span class="sxs-lookup"><span data-stu-id="d673f-218">In the web browser that is opened to the Contoso Ads home page, create a new ad.</span></span>

    <span data-ttu-id="d673f-219">Creating an ad causes a queue message to be created, which is picked up by the WebJob and processed.</span><span class="sxs-lookup"><span data-stu-id="d673f-219">Creating an ad causes a queue message to be created, which is picked up by the WebJob and processed.</span></span> <span data-ttu-id="d673f-220">When the WebJobs SDK calls the function to process the queue message, the code hits your breakpoint.</span><span class="sxs-lookup"><span data-stu-id="d673f-220">When the WebJobs SDK calls the function to process the queue message, the code hits your breakpoint.</span></span>

10. <span data-ttu-id="d673f-221">When the debugger breaks at your breakpoint, you can examine and change variable values while the program is running the cloud.</span><span class="sxs-lookup"><span data-stu-id="d673f-221">When the debugger breaks at your breakpoint, you can examine and change variable values while the program is running the cloud.</span></span> <span data-ttu-id="d673f-222">In the following illustration, the debugger shows the contents of the blobInfo object that was passed to the `GenerateThumbnail` method.</span><span class="sxs-lookup"><span data-stu-id="d673f-222">In the following illustration, the debugger shows the contents of the blobInfo object that was passed to the `GenerateThumbnail` method.</span></span>

     ![blobInfo object in debugger](./media/web-sites-dotnet-troubleshoot-visual-studio/blobinfo.png)

11. <span data-ttu-id="d673f-224">Press F5 to continue running.</span><span class="sxs-lookup"><span data-stu-id="d673f-224">Press F5 to continue running.</span></span>

     <span data-ttu-id="d673f-225">The `GenerateThumbnail` method finishes creating the thumbnail.</span><span class="sxs-lookup"><span data-stu-id="d673f-225">The `GenerateThumbnail` method finishes creating the thumbnail.</span></span>

12. <span data-ttu-id="d673f-226">In the browser, refresh the Index page and you see the thumbnail.</span><span class="sxs-lookup"><span data-stu-id="d673f-226">In the browser, refresh the Index page and you see the thumbnail.</span></span>

13. <span data-ttu-id="d673f-227">In Visual Studio, press SHIFT+F5 to stop debugging.</span><span class="sxs-lookup"><span data-stu-id="d673f-227">In Visual Studio, press SHIFT+F5 to stop debugging.</span></span>

14. <span data-ttu-id="d673f-228">In **Server Explorer**, right-click the ContosoAdsWebJob node and click **View Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="d673f-228">In **Server Explorer**, right-click the ContosoAdsWebJob node and click **View Dashboard**.</span></span>

15. <span data-ttu-id="d673f-229">Sign in with your Azure credentials, and then click the WebJob name to go to the page for your WebJob.</span><span class="sxs-lookup"><span data-stu-id="d673f-229">Sign in with your Azure credentials, and then click the WebJob name to go to the page for your WebJob.</span></span>

     ![Click ContosoAdsWebJob](./media/web-sites-dotnet-troubleshoot-visual-studio/clickcaw.png)

     <span data-ttu-id="d673f-231">The Dashboard shows that the `GenerateThumbnail` function executed recently.</span><span class="sxs-lookup"><span data-stu-id="d673f-231">The Dashboard shows that the `GenerateThumbnail` function executed recently.</span></span>

     <span data-ttu-id="d673f-232">(The next time you click **View Dashboard**, you don't have to sign in, and the browser goes directly to the page for your WebJob.)</span><span class="sxs-lookup"><span data-stu-id="d673f-232">(The next time you click **View Dashboard**, you don't have to sign in, and the browser goes directly to the page for your WebJob.)</span></span>

16. <span data-ttu-id="d673f-233">Click the function name to see details about the function execution.</span><span class="sxs-lookup"><span data-stu-id="d673f-233">Click the function name to see details about the function execution.</span></span>

     ![Function details](./media/web-sites-dotnet-troubleshoot-visual-studio/funcdetails.png)

<span data-ttu-id="d673f-235">If your function [wrote logs](https://github.com/Azure/azure-webjobs-sdk/wiki), you could click **ToggleOutput** to see them.</span><span class="sxs-lookup"><span data-stu-id="d673f-235">If your function [wrote logs](https://github.com/Azure/azure-webjobs-sdk/wiki), you could click **ToggleOutput** to see them.</span></span>

## <a name="notes-about-remote-debugging"></a><span data-ttu-id="d673f-236">Notes about remote debugging</span><span class="sxs-lookup"><span data-stu-id="d673f-236">Notes about remote debugging</span></span>

* <span data-ttu-id="d673f-237">Running in debug mode in production is not recommended.</span><span class="sxs-lookup"><span data-stu-id="d673f-237">Running in debug mode in production is not recommended.</span></span> <span data-ttu-id="d673f-238">If your production web app is not scaled out to multiple server instances, debugging prevents the web server from responding to other requests.</span><span class="sxs-lookup"><span data-stu-id="d673f-238">If your production web app is not scaled out to multiple server instances, debugging prevents the web server from responding to other requests.</span></span> <span data-ttu-id="d673f-239">If you do have multiple web server instances, when you attach to the debugger, you get a random instance, and you have no way to ensure that subsequent browser requests go to the same instance.</span><span class="sxs-lookup"><span data-stu-id="d673f-239">If you do have multiple web server instances, when you attach to the debugger, you get a random instance, and you have no way to ensure that subsequent browser requests go to the same instance.</span></span> <span data-ttu-id="d673f-240">Also, you typically don't deploy a debug build to production, and compiler optimizations for release builds might make it impossible to show what is happening line by line in your source code.</span><span class="sxs-lookup"><span data-stu-id="d673f-240">Also, you typically don't deploy a debug build to production, and compiler optimizations for release builds might make it impossible to show what is happening line by line in your source code.</span></span> <span data-ttu-id="d673f-241">For troubleshooting production problems, your best resource is application tracing and web server logs.</span><span class="sxs-lookup"><span data-stu-id="d673f-241">For troubleshooting production problems, your best resource is application tracing and web server logs.</span></span>
* <span data-ttu-id="d673f-242">Avoid long stops at breakpoints when remote debugging.</span><span class="sxs-lookup"><span data-stu-id="d673f-242">Avoid long stops at breakpoints when remote debugging.</span></span> <span data-ttu-id="d673f-243">Azure treats a process that is stopped for longer than a few minutes as an unresponsive process, and shuts it down.</span><span class="sxs-lookup"><span data-stu-id="d673f-243">Azure treats a process that is stopped for longer than a few minutes as an unresponsive process, and shuts it down.</span></span>
* <span data-ttu-id="d673f-244">While you're debugging, the server is sending data to Visual Studio, which could affect bandwidth charges.</span><span class="sxs-lookup"><span data-stu-id="d673f-244">While you're debugging, the server is sending data to Visual Studio, which could affect bandwidth charges.</span></span> <span data-ttu-id="d673f-245">For information about bandwidth rates, see [Azure Pricing](https://azure.microsoft.com/pricing/calculator/).</span><span class="sxs-lookup"><span data-stu-id="d673f-245">For information about bandwidth rates, see [Azure Pricing](https://azure.microsoft.com/pricing/calculator/).</span></span>
* <span data-ttu-id="d673f-246">Make sure that the `debug` attribute of the `compilation` element in the *Web.config* file is set to true.</span><span class="sxs-lookup"><span data-stu-id="d673f-246">Make sure that the `debug` attribute of the `compilation` element in the *Web.config* file is set to true.</span></span> <span data-ttu-id="d673f-247">It is set to true by default when you publish a debug build configuration.</span><span class="sxs-lookup"><span data-stu-id="d673f-247">It is set to true by default when you publish a debug build configuration.</span></span>

``` xml
<system.web>
  <compilation debug="true" targetFramework="4.5" />
  <httpRuntime targetFramework="4.5" />
</system.web>
```
* <span data-ttu-id="d673f-248">If you find that the debugger doesn't step into the code that you want to debug, you might have to change the Just My Code setting.</span><span class="sxs-lookup"><span data-stu-id="d673f-248">If you find that the debugger doesn't step into the code that you want to debug, you might have to change the Just My Code setting.</span></span>  <span data-ttu-id="d673f-249">For more information, see [Specify whether to debug only user code using Just My Code in Visual Studio](https://docs.microsoft.com/visualstudio/debugger/just-my-code).</span><span class="sxs-lookup"><span data-stu-id="d673f-249">For more information, see [Specify whether to debug only user code using Just My Code in Visual Studio](https://docs.microsoft.com/visualstudio/debugger/just-my-code).</span></span>
* <span data-ttu-id="d673f-250">A timer starts on the server when you enable the remote debugging feature, and after 48 hours the feature is automatically turned off.</span><span class="sxs-lookup"><span data-stu-id="d673f-250">A timer starts on the server when you enable the remote debugging feature, and after 48 hours the feature is automatically turned off.</span></span> <span data-ttu-id="d673f-251">This 48-hour limit is done for security and performance reasons.</span><span class="sxs-lookup"><span data-stu-id="d673f-251">This 48-hour limit is done for security and performance reasons.</span></span> <span data-ttu-id="d673f-252">You can easily turn the feature back on as many times as you like.</span><span class="sxs-lookup"><span data-stu-id="d673f-252">You can easily turn the feature back on as many times as you like.</span></span> <span data-ttu-id="d673f-253">We recommend leaving it disabled when you are not actively debugging.</span><span class="sxs-lookup"><span data-stu-id="d673f-253">We recommend leaving it disabled when you are not actively debugging.</span></span>
* <span data-ttu-id="d673f-254">You can manually attach the debugger to any process, not only the web app process (w3wp.exe).</span><span class="sxs-lookup"><span data-stu-id="d673f-254">You can manually attach the debugger to any process, not only the web app process (w3wp.exe).</span></span> <span data-ttu-id="d673f-255">For more information about how to use debug mode in Visual Studio, see [Debugging in Visual Studio](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx).</span><span class="sxs-lookup"><span data-stu-id="d673f-255">For more information about how to use debug mode in Visual Studio, see [Debugging in Visual Studio](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx).</span></span>

## <a name="logsoverview"></a><span data-ttu-id="d673f-256">Diagnostic logs overview</span><span class="sxs-lookup"><span data-stu-id="d673f-256">Diagnostic logs overview</span></span>
<span data-ttu-id="d673f-257">An ASP.NET application that runs in an Azure web app can create the following kinds of logs:</span><span class="sxs-lookup"><span data-stu-id="d673f-257">An ASP.NET application that runs in an Azure web app can create the following kinds of logs:</span></span>

* <span data-ttu-id="d673f-258">**Application tracing logs**</span><span class="sxs-lookup"><span data-stu-id="d673f-258">**Application tracing logs**</span></span><br/>
  <span data-ttu-id="d673f-259">The application creates these logs by calling methods of the [System.Diagnostics.Trace](http://msdn.microsoft.com/library/system.diagnostics.trace.aspx) class.</span><span class="sxs-lookup"><span data-stu-id="d673f-259">The application creates these logs by calling methods of the [System.Diagnostics.Trace](http://msdn.microsoft.com/library/system.diagnostics.trace.aspx) class.</span></span>
* <span data-ttu-id="d673f-260">**Web server logs**</span><span class="sxs-lookup"><span data-stu-id="d673f-260">**Web server logs**</span></span><br/>
  <span data-ttu-id="d673f-261">The web server creates a log entry for every HTTP request to the web app.</span><span class="sxs-lookup"><span data-stu-id="d673f-261">The web server creates a log entry for every HTTP request to the web app.</span></span>
* <span data-ttu-id="d673f-262">**Detailed error message logs**</span><span class="sxs-lookup"><span data-stu-id="d673f-262">**Detailed error message logs**</span></span><br/>
  <span data-ttu-id="d673f-263">The web server creates an HTML page with some additional information for failed HTTP requests (requests that result in status code 400 or greater).</span><span class="sxs-lookup"><span data-stu-id="d673f-263">The web server creates an HTML page with some additional information for failed HTTP requests (requests that result in status code 400 or greater).</span></span>
* <span data-ttu-id="d673f-264">**Failed request tracing logs**</span><span class="sxs-lookup"><span data-stu-id="d673f-264">**Failed request tracing logs**</span></span><br/>
  <span data-ttu-id="d673f-265">The web server creates an XML file with detailed tracing information for failed HTTP requests.</span><span class="sxs-lookup"><span data-stu-id="d673f-265">The web server creates an XML file with detailed tracing information for failed HTTP requests.</span></span> <span data-ttu-id="d673f-266">The web server also provides an XSL file to format the XML in a browser.</span><span class="sxs-lookup"><span data-stu-id="d673f-266">The web server also provides an XSL file to format the XML in a browser.</span></span>

<span data-ttu-id="d673f-267">Logging affects web app performance, so Azure gives you the ability to enable or disable each type of log as needed.</span><span class="sxs-lookup"><span data-stu-id="d673f-267">Logging affects web app performance, so Azure gives you the ability to enable or disable each type of log as needed.</span></span> <span data-ttu-id="d673f-268">For application logs, you can specify that only logs above a certain severity level should be written.</span><span class="sxs-lookup"><span data-stu-id="d673f-268">For application logs, you can specify that only logs above a certain severity level should be written.</span></span> <span data-ttu-id="d673f-269">When you create a new web app, by default all logging is disabled.</span><span class="sxs-lookup"><span data-stu-id="d673f-269">When you create a new web app, by default all logging is disabled.</span></span>

<span data-ttu-id="d673f-270">Logs are written to files in a *LogFiles* folder in the file system of your web app and are accessible via FTP.</span><span class="sxs-lookup"><span data-stu-id="d673f-270">Logs are written to files in a *LogFiles* folder in the file system of your web app and are accessible via FTP.</span></span> <span data-ttu-id="d673f-271">Web server logs and application logs can also be written to an Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="d673f-271">Web server logs and application logs can also be written to an Azure Storage account.</span></span> <span data-ttu-id="d673f-272">You can retain a greater volume of logs in a storage account than is possible in the file system.</span><span class="sxs-lookup"><span data-stu-id="d673f-272">You can retain a greater volume of logs in a storage account than is possible in the file system.</span></span> <span data-ttu-id="d673f-273">You're limited to a maximum of 100 megabytes of logs when you use the file system.</span><span class="sxs-lookup"><span data-stu-id="d673f-273">You're limited to a maximum of 100 megabytes of logs when you use the file system.</span></span> <span data-ttu-id="d673f-274">(File system logs are only for short-term retention.</span><span class="sxs-lookup"><span data-stu-id="d673f-274">(File system logs are only for short-term retention.</span></span> <span data-ttu-id="d673f-275">Azure deletes old log files to make room for new ones after the limit is reached.)</span><span class="sxs-lookup"><span data-stu-id="d673f-275">Azure deletes old log files to make room for new ones after the limit is reached.)</span></span>  

## <a name="apptracelogs"></a><span data-ttu-id="d673f-276">Create and view application trace logs</span><span class="sxs-lookup"><span data-stu-id="d673f-276">Create and view application trace logs</span></span>
<span data-ttu-id="d673f-277">In this section, you do the following tasks:</span><span class="sxs-lookup"><span data-stu-id="d673f-277">In this section, you do the following tasks:</span></span>

* <span data-ttu-id="d673f-278">Add tracing statements to the web project that you created in [Get started with Azure and ASP.NET](app-service-web-get-started-dotnet-framework.md).</span><span class="sxs-lookup"><span data-stu-id="d673f-278">Add tracing statements to the web project that you created in [Get started with Azure and ASP.NET](app-service-web-get-started-dotnet-framework.md).</span></span>
* <span data-ttu-id="d673f-279">View the logs when you run the project locally.</span><span class="sxs-lookup"><span data-stu-id="d673f-279">View the logs when you run the project locally.</span></span>
* <span data-ttu-id="d673f-280">View the logs as they are generated by the application running in Azure.</span><span class="sxs-lookup"><span data-stu-id="d673f-280">View the logs as they are generated by the application running in Azure.</span></span>

<span data-ttu-id="d673f-281">For information about how to create application logs in WebJobs, see [How to work with Azure queue storage using the WebJobs SDK - How to write logs](https://github.com/Azure/azure-webjobs-sdk/wiki).</span><span class="sxs-lookup"><span data-stu-id="d673f-281">For information about how to create application logs in WebJobs, see [How to work with Azure queue storage using the WebJobs SDK - How to write logs](https://github.com/Azure/azure-webjobs-sdk/wiki).</span></span> <span data-ttu-id="d673f-282">The following instructions for viewing logs and controlling how they're stored in Azure apply also to application logs created by WebJobs.</span><span class="sxs-lookup"><span data-stu-id="d673f-282">The following instructions for viewing logs and controlling how they're stored in Azure apply also to application logs created by WebJobs.</span></span>

### <a name="add-tracing-statements-to-the-application"></a><span data-ttu-id="d673f-283">Add tracing statements to the application</span><span class="sxs-lookup"><span data-stu-id="d673f-283">Add tracing statements to the application</span></span>
1. <span data-ttu-id="d673f-284">Open *Controllers\HomeController.cs*, and replace the `Index`, `About`, and `Contact` methods with the following code in order to add `Trace` statements and a `using` statement for `System.Diagnostics`:</span><span class="sxs-lookup"><span data-stu-id="d673f-284">Open *Controllers\HomeController.cs*, and replace the `Index`, `About`, and `Contact` methods with the following code in order to add `Trace` statements and a `using` statement for `System.Diagnostics`:</span></span>

```c#
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
```

2. <span data-ttu-id="d673f-285">Add a `using System.Diagnostics;` statement to the top of the file.</span><span class="sxs-lookup"><span data-stu-id="d673f-285">Add a `using System.Diagnostics;` statement to the top of the file.</span></span>

### <a name="view-the-tracing-output-locally"></a><span data-ttu-id="d673f-286">View the tracing output locally</span><span class="sxs-lookup"><span data-stu-id="d673f-286">View the tracing output locally</span></span>
1. <span data-ttu-id="d673f-287">Press F5 to run the application in debug mode.</span><span class="sxs-lookup"><span data-stu-id="d673f-287">Press F5 to run the application in debug mode.</span></span>

    <span data-ttu-id="d673f-288">The default trace listener writes all trace output to the **Output** window, along with other Debug output.</span><span class="sxs-lookup"><span data-stu-id="d673f-288">The default trace listener writes all trace output to the **Output** window, along with other Debug output.</span></span> <span data-ttu-id="d673f-289">The following illustration shows the output from the trace statements that you added to the `Index` method.</span><span class="sxs-lookup"><span data-stu-id="d673f-289">The following illustration shows the output from the trace statements that you added to the `Index` method.</span></span>

    ![Tracing in Debug window](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugtracing.png)

    <span data-ttu-id="d673f-291">The following steps show how to view trace output in a web page, without compiling in debug mode.</span><span class="sxs-lookup"><span data-stu-id="d673f-291">The following steps show how to view trace output in a web page, without compiling in debug mode.</span></span>
2. <span data-ttu-id="d673f-292">Open the application Web.config file (the one located in the project folder) and add a `<system.diagnostics>` element at the end of the file just before the closing `</configuration>` element:</span><span class="sxs-lookup"><span data-stu-id="d673f-292">Open the application Web.config file (the one located in the project folder) and add a `<system.diagnostics>` element at the end of the file just before the closing `</configuration>` element:</span></span>

``` xml
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
```

<span data-ttu-id="d673f-293">The `WebPageTraceListener` lets you view trace output by browsing to `/trace.axd`.</span><span class="sxs-lookup"><span data-stu-id="d673f-293">The `WebPageTraceListener` lets you view trace output by browsing to `/trace.axd`.</span></span>
3. <span data-ttu-id="d673f-294">Add a <a href="http://msdn.microsoft.com/library/vstudio/6915t83k(v=vs.100).aspx">trace element</a> under `<system.web>` in the Web.config file, such as the following example:</span><span class="sxs-lookup"><span data-stu-id="d673f-294">Add a <a href="http://msdn.microsoft.com/library/vstudio/6915t83k(v=vs.100).aspx">trace element</a> under `<system.web>` in the Web.config file, such as the following example:</span></span>

``` xml
<trace enabled="true" writeToDiagnosticsTrace="true" mostRecent="true" pageOutput="false" />
```       

4. <span data-ttu-id="d673f-295">Press CTRL+F5 to run the application.</span><span class="sxs-lookup"><span data-stu-id="d673f-295">Press CTRL+F5 to run the application.</span></span>
5. <span data-ttu-id="d673f-296">In the address bar of the browser window, add *trace.axd* to the URL, and then press Enter (the URL is similar to http://localhost:53370/trace.axd).</span><span class="sxs-lookup"><span data-stu-id="d673f-296">In the address bar of the browser window, add *trace.axd* to the URL, and then press Enter (the URL is similar to http://localhost:53370/trace.axd).</span></span>
6. <span data-ttu-id="d673f-297">On the **Application Trace** page, click **View Details** on the first line (not the BrowserLink line).</span><span class="sxs-lookup"><span data-stu-id="d673f-297">On the **Application Trace** page, click **View Details** on the first line (not the BrowserLink line).</span></span>

    ![trace.axd](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-traceaxd1.png)

    <span data-ttu-id="d673f-299">The **Request Details** page appears, and in the **Trace Information** section you see the output from the trace statements that you added to the `Index` method.</span><span class="sxs-lookup"><span data-stu-id="d673f-299">The **Request Details** page appears, and in the **Trace Information** section you see the output from the trace statements that you added to the `Index` method.</span></span>

    ![trace.axd](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-traceaxd2.png)

    <span data-ttu-id="d673f-301">By default, `trace.axd` is only available locally.</span><span class="sxs-lookup"><span data-stu-id="d673f-301">By default, `trace.axd` is only available locally.</span></span> <span data-ttu-id="d673f-302">If you wanted to make it available from a remote web app, you could add `localOnly="false"` to the `trace` element in the *Web.config* file, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="d673f-302">If you wanted to make it available from a remote web app, you could add `localOnly="false"` to the `trace` element in the *Web.config* file, as shown in the following example:</span></span>

        <trace enabled="true" writeToDiagnosticsTrace="true" localOnly="false" mostRecent="true" pageOutput="false" />

    <span data-ttu-id="d673f-303">However, enabling `trace.axd` in a production web app is not recommended for security reasons.</span><span class="sxs-lookup"><span data-stu-id="d673f-303">However, enabling `trace.axd` in a production web app is not recommended for security reasons.</span></span> <span data-ttu-id="d673f-304">In the following sections, you'll see an easier way to read tracing logs in an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="d673f-304">In the following sections, you'll see an easier way to read tracing logs in an Azure web app.</span></span>

### <a name="view-the-tracing-output-in-azure"></a><span data-ttu-id="d673f-305">View the tracing output in Azure</span><span class="sxs-lookup"><span data-stu-id="d673f-305">View the tracing output in Azure</span></span>
1. <span data-ttu-id="d673f-306">In **Solution Explorer**, right-click the web project and click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="d673f-306">In **Solution Explorer**, right-click the web project and click **Publish**.</span></span>
2. <span data-ttu-id="d673f-307">In the **Publish Web** dialog box, click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="d673f-307">In the **Publish Web** dialog box, click **Publish**.</span></span>

    <span data-ttu-id="d673f-308">After Visual Studio publishes your update, it opens a browser window to your home page (assuming you didn't clear **Destination URL** on the **Connection** tab).</span><span class="sxs-lookup"><span data-stu-id="d673f-308">After Visual Studio publishes your update, it opens a browser window to your home page (assuming you didn't clear **Destination URL** on the **Connection** tab).</span></span>
3. <span data-ttu-id="d673f-309">In **Server Explorer**, right-click your web app and select **View Streaming Logs**.</span><span class="sxs-lookup"><span data-stu-id="d673f-309">In **Server Explorer**, right-click your web app and select **View Streaming Logs**.</span></span>

    ![View Streaming Logs in context menu](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-viewlogsmenu.png)

    <span data-ttu-id="d673f-311">The **Output** window shows that you are connected to the log-streaming service, and adds a notification line each minute that goes by without a log to display.</span><span class="sxs-lookup"><span data-stu-id="d673f-311">The **Output** window shows that you are connected to the log-streaming service, and adds a notification line each minute that goes by without a log to display.</span></span>

    ![View Streaming Logs in context menu](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-nologsyet.png)
4. <span data-ttu-id="d673f-313">In the browser window that shows your application home page, click **Contact**.</span><span class="sxs-lookup"><span data-stu-id="d673f-313">In the browser window that shows your application home page, click **Contact**.</span></span>

    <span data-ttu-id="d673f-314">Within a few seconds, the output from the error-level trace you added to the `Contact` method appears in the **Output** window.</span><span class="sxs-lookup"><span data-stu-id="d673f-314">Within a few seconds, the output from the error-level trace you added to the `Contact` method appears in the **Output** window.</span></span>

    ![Error trace in Output window](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-errortrace.png)

    <span data-ttu-id="d673f-316">Visual Studio is only showing error-level traces because that is the default setting when you enable the log monitoring service.</span><span class="sxs-lookup"><span data-stu-id="d673f-316">Visual Studio is only showing error-level traces because that is the default setting when you enable the log monitoring service.</span></span> <span data-ttu-id="d673f-317">When you create a new Azure web app, all logging is disabled by default, as you saw when you opened the settings page earlier:</span><span class="sxs-lookup"><span data-stu-id="d673f-317">When you create a new Azure web app, all logging is disabled by default, as you saw when you opened the settings page earlier:</span></span>

    ![Application Logging off](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-apploggingoff.png)

    <span data-ttu-id="d673f-319">However, when you selected **View Streaming Logs**, Visual Studio automatically changed **Application Logging(File System)** to **Error**, which means error-level logs get reported.</span><span class="sxs-lookup"><span data-stu-id="d673f-319">However, when you selected **View Streaming Logs**, Visual Studio automatically changed **Application Logging(File System)** to **Error**, which means error-level logs get reported.</span></span> <span data-ttu-id="d673f-320">In order to see all of your tracing logs, you can change this setting to **Verbose**.</span><span class="sxs-lookup"><span data-stu-id="d673f-320">In order to see all of your tracing logs, you can change this setting to **Verbose**.</span></span> <span data-ttu-id="d673f-321">When you select a severity level lower than error, all logs for higher severity levels are also reported.</span><span class="sxs-lookup"><span data-stu-id="d673f-321">When you select a severity level lower than error, all logs for higher severity levels are also reported.</span></span> <span data-ttu-id="d673f-322">So when you select verbose, you also see information, warning, and error logs.</span><span class="sxs-lookup"><span data-stu-id="d673f-322">So when you select verbose, you also see information, warning, and error logs.</span></span>  

1. <span data-ttu-id="d673f-323">In **Server Explorer**, right-click the web app, and then click **View Settings** as you did earlier.</span><span class="sxs-lookup"><span data-stu-id="d673f-323">In **Server Explorer**, right-click the web app, and then click **View Settings** as you did earlier.</span></span>
2. <span data-ttu-id="d673f-324">Change **Application Logging (File System)** to **Verbose**, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="d673f-324">Change **Application Logging (File System)** to **Verbose**, and then click **Save**.</span></span>

    ![Setting trace level to Verbose](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-applogverbose.png)
3. <span data-ttu-id="d673f-326">In the browser window that is now showing your **Contact** page, click **Home**, then click **About**, and then click **Contact**.</span><span class="sxs-lookup"><span data-stu-id="d673f-326">In the browser window that is now showing your **Contact** page, click **Home**, then click **About**, and then click **Contact**.</span></span>

    <span data-ttu-id="d673f-327">Within a few seconds, the **Output** window shows all of your tracing output.</span><span class="sxs-lookup"><span data-stu-id="d673f-327">Within a few seconds, the **Output** window shows all of your tracing output.</span></span>

    ![Verbose trace output](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-verbosetraces.png)

    <span data-ttu-id="d673f-329">In this section, you enabled and disabled logging by using Azure web app settings.</span><span class="sxs-lookup"><span data-stu-id="d673f-329">In this section, you enabled and disabled logging by using Azure web app settings.</span></span> <span data-ttu-id="d673f-330">You can also enable and disable trace listeners by modifying the Web.config file.</span><span class="sxs-lookup"><span data-stu-id="d673f-330">You can also enable and disable trace listeners by modifying the Web.config file.</span></span> <span data-ttu-id="d673f-331">However, modifying the Web.config file causes the app domain to recycle, while enabling logging via the web app configuration doesn't do that.</span><span class="sxs-lookup"><span data-stu-id="d673f-331">However, modifying the Web.config file causes the app domain to recycle, while enabling logging via the web app configuration doesn't do that.</span></span> <span data-ttu-id="d673f-332">If the problem takes a long time to reproduce, or is intermittent, recycling the app domain might "fix" it and force you to wait until it happens again.</span><span class="sxs-lookup"><span data-stu-id="d673f-332">If the problem takes a long time to reproduce, or is intermittent, recycling the app domain might "fix" it and force you to wait until it happens again.</span></span> <span data-ttu-id="d673f-333">Enabling diagnostics in Azure lets you start capturing error information immediately without recycling the app domain.</span><span class="sxs-lookup"><span data-stu-id="d673f-333">Enabling diagnostics in Azure lets you start capturing error information immediately without recycling the app domain.</span></span>

### <a name="output-window-features"></a><span data-ttu-id="d673f-334">Output window features</span><span class="sxs-lookup"><span data-stu-id="d673f-334">Output window features</span></span>
<span data-ttu-id="d673f-335">The **Microsoft Azure Logs** tab of the **Output** Window has several buttons and a text box:</span><span class="sxs-lookup"><span data-stu-id="d673f-335">The **Microsoft Azure Logs** tab of the **Output** Window has several buttons and a text box:</span></span>

![Logs tab buttons](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-icons.png)

<span data-ttu-id="d673f-337">These perform the following functions:</span><span class="sxs-lookup"><span data-stu-id="d673f-337">These perform the following functions:</span></span>

* <span data-ttu-id="d673f-338">Clear the **Output** window.</span><span class="sxs-lookup"><span data-stu-id="d673f-338">Clear the **Output** window.</span></span>
* <span data-ttu-id="d673f-339">Enable or disable word wrap.</span><span class="sxs-lookup"><span data-stu-id="d673f-339">Enable or disable word wrap.</span></span>
* <span data-ttu-id="d673f-340">Start or stop monitoring logs.</span><span class="sxs-lookup"><span data-stu-id="d673f-340">Start or stop monitoring logs.</span></span>
* <span data-ttu-id="d673f-341">Specify which logs to monitor.</span><span class="sxs-lookup"><span data-stu-id="d673f-341">Specify which logs to monitor.</span></span>
* <span data-ttu-id="d673f-342">Download logs.</span><span class="sxs-lookup"><span data-stu-id="d673f-342">Download logs.</span></span>
* <span data-ttu-id="d673f-343">Filter logs based on a search string or a regular expression.</span><span class="sxs-lookup"><span data-stu-id="d673f-343">Filter logs based on a search string or a regular expression.</span></span>
* <span data-ttu-id="d673f-344">Close the **Output** window.</span><span class="sxs-lookup"><span data-stu-id="d673f-344">Close the **Output** window.</span></span>

<span data-ttu-id="d673f-345">If you enter a search string or regular expression, Visual Studio filters logging information at the client.</span><span class="sxs-lookup"><span data-stu-id="d673f-345">If you enter a search string or regular expression, Visual Studio filters logging information at the client.</span></span> <span data-ttu-id="d673f-346">That means you can enter the criteria after the logs are displayed in the **Output** window and you can change filtering criteria without having to regenerate the logs.</span><span class="sxs-lookup"><span data-stu-id="d673f-346">That means you can enter the criteria after the logs are displayed in the **Output** window and you can change filtering criteria without having to regenerate the logs.</span></span>

## <a name="webserverlogs"></a><span data-ttu-id="d673f-347">View web server logs</span><span class="sxs-lookup"><span data-stu-id="d673f-347">View web server logs</span></span>
<span data-ttu-id="d673f-348">Web server logs record all HTTP activity for the web app.</span><span class="sxs-lookup"><span data-stu-id="d673f-348">Web server logs record all HTTP activity for the web app.</span></span> <span data-ttu-id="d673f-349">In order to see them in the **Output** window, you must enable them for the web app and tell Visual Studio that you want to monitor them.</span><span class="sxs-lookup"><span data-stu-id="d673f-349">In order to see them in the **Output** window, you must enable them for the web app and tell Visual Studio that you want to monitor them.</span></span>

1. <span data-ttu-id="d673f-350">In the **Azure Web App Configuration** tab that you opened from **Server Explorer**, change Web Server Logging to **On**, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="d673f-350">In the **Azure Web App Configuration** tab that you opened from **Server Explorer**, change Web Server Logging to **On**, and then click **Save**.</span></span>

    ![Enable web server logging](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-webserverloggingon.png)
2. <span data-ttu-id="d673f-352">In the **Output** Window, click the **Specify which Microsoft Azure logs to monitor** button.</span><span class="sxs-lookup"><span data-stu-id="d673f-352">In the **Output** Window, click the **Specify which Microsoft Azure logs to monitor** button.</span></span>

    ![Specify which Azure logs to monitor](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-specifylogs.png)
3. <span data-ttu-id="d673f-354">In the **Microsoft Azure Logging Options** dialog box, select **Web server logs**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="d673f-354">In the **Microsoft Azure Logging Options** dialog box, select **Web server logs**, and then click **OK**.</span></span>

    ![Monitor web server logs](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-monitorwslogson.png)
4. <span data-ttu-id="d673f-356">In the browser window that shows the web app, click **Home**, then click **About**, and then click **Contact**.</span><span class="sxs-lookup"><span data-stu-id="d673f-356">In the browser window that shows the web app, click **Home**, then click **About**, and then click **Contact**.</span></span>

    <span data-ttu-id="d673f-357">The application logs generally appear first, followed by the web server logs.</span><span class="sxs-lookup"><span data-stu-id="d673f-357">The application logs generally appear first, followed by the web server logs.</span></span> <span data-ttu-id="d673f-358">You might have to wait a while for the logs to appear.</span><span class="sxs-lookup"><span data-stu-id="d673f-358">You might have to wait a while for the logs to appear.</span></span>

    ![Web server logs in Output window](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-wslogs.png)

<span data-ttu-id="d673f-360">By default, when you first enable web server logs by using Visual Studio, Azure writes the logs to the file system.</span><span class="sxs-lookup"><span data-stu-id="d673f-360">By default, when you first enable web server logs by using Visual Studio, Azure writes the logs to the file system.</span></span> <span data-ttu-id="d673f-361">As an alternative, you can use the Azure portal to specify that web server logs should be written to a blob container in a storage account.</span><span class="sxs-lookup"><span data-stu-id="d673f-361">As an alternative, you can use the Azure portal to specify that web server logs should be written to a blob container in a storage account.</span></span>

<span data-ttu-id="d673f-362">If you use the portal to enable web server logging to an Azure storage account, and then disable logging in Visual Studio, when you re-enable logging in Visual Studio your storage account settings are restored.</span><span class="sxs-lookup"><span data-stu-id="d673f-362">If you use the portal to enable web server logging to an Azure storage account, and then disable logging in Visual Studio, when you re-enable logging in Visual Studio your storage account settings are restored.</span></span>

## <a name="detailederrorlogs"></a><span data-ttu-id="d673f-363">View detailed error message logs</span><span class="sxs-lookup"><span data-stu-id="d673f-363">View detailed error message logs</span></span>
<span data-ttu-id="d673f-364">Detailed error logs provide some additional information about HTTP requests that result in error response codes (400 or above).</span><span class="sxs-lookup"><span data-stu-id="d673f-364">Detailed error logs provide some additional information about HTTP requests that result in error response codes (400 or above).</span></span> <span data-ttu-id="d673f-365">In order to see them in the **Output** window, you have to enable them for the web app and tell Visual Studio that you want to monitor them.</span><span class="sxs-lookup"><span data-stu-id="d673f-365">In order to see them in the **Output** window, you have to enable them for the web app and tell Visual Studio that you want to monitor them.</span></span>

1. <span data-ttu-id="d673f-366">In the **Azure Web App Configuration** tab that you opened from **Server Explorer**, change **Detailed Error Messages** to **On**, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="d673f-366">In the **Azure Web App Configuration** tab that you opened from **Server Explorer**, change **Detailed Error Messages** to **On**, and then click **Save**.</span></span>

    ![Enable detailed error messages](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailedlogson.png)

2. <span data-ttu-id="d673f-368">In the **Output** Window, click the **Specify which Microsoft Azure logs to monitor** button.</span><span class="sxs-lookup"><span data-stu-id="d673f-368">In the **Output** Window, click the **Specify which Microsoft Azure logs to monitor** button.</span></span>

3. <span data-ttu-id="d673f-369">In the **Microsoft Azure Logging Options** dialog box, click **All logs**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="d673f-369">In the **Microsoft Azure Logging Options** dialog box, click **All logs**, and then click **OK**.</span></span>

    ![Monitor all logs](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-monitorall.png)

4. <span data-ttu-id="d673f-371">In the address bar of the browser window, add an extra character to the URL to cause a 404 error (for example, `http://localhost:53370/Home/Contactx`), and press Enter.</span><span class="sxs-lookup"><span data-stu-id="d673f-371">In the address bar of the browser window, add an extra character to the URL to cause a 404 error (for example, `http://localhost:53370/Home/Contactx`), and press Enter.</span></span>

    <span data-ttu-id="d673f-372">After several seconds, the detailed error log appears in the Visual Studio **Output** window.</span><span class="sxs-lookup"><span data-stu-id="d673f-372">After several seconds, the detailed error log appears in the Visual Studio **Output** window.</span></span>

    ![Detailed error log - Output window](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailederrorlog.png)

    <span data-ttu-id="d673f-374">Control+click the link to see the log output formatted in a browser:</span><span class="sxs-lookup"><span data-stu-id="d673f-374">Control+click the link to see the log output formatted in a browser:</span></span>

    ![Detailed error log - browser window](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailederrorloginbrowser.png)

## <a name="downloadlogs"></a><span data-ttu-id="d673f-376">Download file system logs</span><span class="sxs-lookup"><span data-stu-id="d673f-376">Download file system logs</span></span>
<span data-ttu-id="d673f-377">Any logs that you can monitor in the **Output** window can also be downloaded as a *.zip* file.</span><span class="sxs-lookup"><span data-stu-id="d673f-377">Any logs that you can monitor in the **Output** window can also be downloaded as a *.zip* file.</span></span>

1. <span data-ttu-id="d673f-378">In the **Output** window, click **Download Streaming Logs**.</span><span class="sxs-lookup"><span data-stu-id="d673f-378">In the **Output** window, click **Download Streaming Logs**.</span></span>

    ![Logs tab buttons](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-downloadicon.png)

    <span data-ttu-id="d673f-380">File Explorer opens to your *Downloads* folder with the downloaded file selected.</span><span class="sxs-lookup"><span data-stu-id="d673f-380">File Explorer opens to your *Downloads* folder with the downloaded file selected.</span></span>

    ![Downloaded file](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-downloadedfile.png)
2. <span data-ttu-id="d673f-382">Extract the *.zip* file, and you see the following folder structure:</span><span class="sxs-lookup"><span data-stu-id="d673f-382">Extract the *.zip* file, and you see the following folder structure:</span></span>

    ![Downloaded file](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-logfilefolders.png)

   * <span data-ttu-id="d673f-384">Application tracing logs are in *.txt* files in the *LogFiles\Application* folder.</span><span class="sxs-lookup"><span data-stu-id="d673f-384">Application tracing logs are in *.txt* files in the *LogFiles\Application* folder.</span></span>
   * <span data-ttu-id="d673f-385">Web server logs are in *.log* files in the *LogFiles\http\RawLogs* folder.</span><span class="sxs-lookup"><span data-stu-id="d673f-385">Web server logs are in *.log* files in the *LogFiles\http\RawLogs* folder.</span></span> <span data-ttu-id="d673f-386">You can use a tool such as [Log Parser](http://www.microsoft.com/download/details.aspx?displaylang=en&id=24659) to view and manipulate these files.</span><span class="sxs-lookup"><span data-stu-id="d673f-386">You can use a tool such as [Log Parser](http://www.microsoft.com/download/details.aspx?displaylang=en&id=24659) to view and manipulate these files.</span></span>
   * <span data-ttu-id="d673f-387">Detailed error message logs are in *.html* files in the *LogFiles\DetailedErrors* folder.</span><span class="sxs-lookup"><span data-stu-id="d673f-387">Detailed error message logs are in *.html* files in the *LogFiles\DetailedErrors* folder.</span></span>

    <span data-ttu-id="d673f-388">(The *deployments* folder is for files created by source control publishing; it doesn't have anything related to Visual Studio publishing.</span><span class="sxs-lookup"><span data-stu-id="d673f-388">(The *deployments* folder is for files created by source control publishing; it doesn't have anything related to Visual Studio publishing.</span></span> <span data-ttu-id="d673f-389">The *Git* folder is for traces related to source control publishing and the log file streaming service.)</span><span class="sxs-lookup"><span data-stu-id="d673f-389">The *Git* folder is for traces related to source control publishing and the log file streaming service.)</span></span>  

<!-- ## <a name="storagelogs"></a>View storage logs
Application tracing logs can also be sent to an Azure storage account, and you can view them in Visual Studio. To do that you'll create a storage account, enable storage logs in the Azure portal, and view them in the **Logs** tab of the **Azure Web App** window.

You can send logs to any or all of three destinations:

* The file system.
* Storage account tables.
* Storage account blobs.

You can specify a different severity level for each destination.

Tables make it easy to view details of logs online, and they support streaming; you can query logs in tables and see new logs as they are being created. Blobs make it easy to download logs in files and to analyze them using HDInsight, because HDInsight knows how to work with blob storage. For more information, see **Hadoop and MapReduce** in [Data Storage Options (Building Real-World Cloud Apps with Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options).

You currently have file system logs set to verbose level; the following steps walk you through setting up information level logs to go to storage account tables. Information level means all logs created by calling `Trace.TraceInformation`, `Trace.TraceWarning`, and `Trace.TraceError` will be displayed, but not logs created by calling `Trace.WriteLine`.

Storage accounts offer more storage and longer-lasting retention for logs compared to the file system. Another advantage of sending application tracing logs to storage is that you get some additional information with each log that you don't get from file system logs.

1. Right-click **Storage** under the Azure node, and then click **Create Storage Account**.

![Create Storage Account](./media/web-sites-dotnet-troubleshoot-visual-studio/createstor.png)

1. In the **Create Storage Account** dialog, enter a name for the storage account.

    The name must be must be unique (no other Azure storage account can have the same name). If the name you enter is already in use you'll get a chance to change it.

    The URL to access your storage account will be *{name}*.core.windows.net.
2. Set the **Region or Affinity Group** drop-down list to the region closest to you.

    This setting specifies which Azure datacenter will host your storage account. For this tutorial your choice won't make a noticeable difference, but for a production web app you want your web server and your storage account to be in the same region to minimize latency and data egress charges. The web app (which you'll create later) should run in a region as close as possible to the browsers accessing your web app in order to minimize latency.
3. Set the **Replication** drop-down list to **Locally redundant**.
   
    When geo-replication is enabled for a storage account, the stored content is replicated to a secondary datacenter to enable failover to that location in case of a major disaster in the primary location. Geo-replication can incur additional costs. For test and development accounts, you generally don't want to pay for geo-replication. For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).
4. Click **Create**.

    ![New storage account](./media/web-sites-dotnet-troubleshoot-visual-studio/newstorage.png)    
5. In the Visual Studio **Azure Web App** window, click the **Logs** tab, and then click **Configure Logging in Management Portal**.

     <!-- todo:screenshot of new portal if the VS page link goes to new portal -- >
    ![Configure logging](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-configlogging.png)

    This opens the **Configure** tab in the portal for your web app.
6. In the portal's **Configure** tab, scroll down to the application diagnostics section, and then change **Application Logging (Table Storage)** to **On**.
7. Change **Logging Level** to **Information**.
8. Click **Manage Table Storage**.

    ![Click Manage TableStorage](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-stgsettingsmgmtportal.png)

    In the **Manage table storage for application diagnostics** box, you can choose your storage account if you have more than one. You can create a new table or use an existing one.

    ![Manage table storage](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-choosestorageacct.png)
9. In the **Manage table storage for application diagnostics** box, click the check mark to close the box.
10. In the portal's **Configure** tab, click **Save**.
11. In the browser window that displays the application web app, click **Home**, then click **About**, and then click **Contact**.

     The logging information produced by browsing these web pages is written to the storage account.
12. In the **Logs** tab of the **Azure Web App** window in Visual Studio, click **Refresh** under **Diagnostic Summary**.

     ![Click Refresh](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-refreshstorage.png)

     The **Diagnostic Summary** section shows logs for the last 15 minutes by default. You can change the period to see more logs.

     (If you get a "table not found" error, verify that you browsed to the pages that do the tracing after you enabled **Application Logging (Storage)** and after you clicked **Save**.)

     ![Storage logs](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-storagelogs.png)

     Notice that in this view you see **Process ID** and **Thread ID** for each log, which you don't get in the file system logs. You can see additional fields by viewing the Azure storage table directly.
13. Click **View all application logs**.

     The trace log table appears in the Azure storage table viewer.

     (If you get a "sequence contains no elements" error, open **Server Explorer**, expand the node for your storage account under the **Azure** node, and then right-click **Tables** and click **Refresh**.)

     ![Storage logs in table view](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-tracelogtableview.png)

     This view shows additional fields you don't see in any other views. This view also enables you to filter logs by using special Query Builder UI for constructing a query. For more information, see Working with Table Resources - Filtering Entities in [Browsing Storage Resources with Server Explorer](http://msdn.microsoft.com/library/ff683677.aspx).
14. To look at the details for a single row, double-click one of the rows.

     ![Trace table in Server Explorer](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-tracetablerow.png)
 -->
## <a name="failedrequestlogs"></a><span data-ttu-id="d673f-390">View failed request tracing logs</span><span class="sxs-lookup"><span data-stu-id="d673f-390">View failed request tracing logs</span></span>
<span data-ttu-id="d673f-391">Failed request tracing logs are useful when you need to understand the details of how IIS is handling an HTTP request, in scenarios such as URL rewriting or authentication problems.</span><span class="sxs-lookup"><span data-stu-id="d673f-391">Failed request tracing logs are useful when you need to understand the details of how IIS is handling an HTTP request, in scenarios such as URL rewriting or authentication problems.</span></span>

<span data-ttu-id="d673f-392">Azure web apps use the same failed request tracing functionality that has been available with IIS 7.0 and later.</span><span class="sxs-lookup"><span data-stu-id="d673f-392">Azure web apps use the same failed request tracing functionality that has been available with IIS 7.0 and later.</span></span> <span data-ttu-id="d673f-393">You don't have access to the IIS settings that configure which errors get logged, however.</span><span class="sxs-lookup"><span data-stu-id="d673f-393">You don't have access to the IIS settings that configure which errors get logged, however.</span></span> <span data-ttu-id="d673f-394">When you enable failed request tracing, all errors are captured.</span><span class="sxs-lookup"><span data-stu-id="d673f-394">When you enable failed request tracing, all errors are captured.</span></span>

<span data-ttu-id="d673f-395">You can enable failed request tracing by using Visual Studio, but you can't view them in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d673f-395">You can enable failed request tracing by using Visual Studio, but you can't view them in Visual Studio.</span></span> <span data-ttu-id="d673f-396">These logs are XML files.</span><span class="sxs-lookup"><span data-stu-id="d673f-396">These logs are XML files.</span></span> <span data-ttu-id="d673f-397">The streaming log service only monitors files that are deemed readable in plain text mode:  *.txt*, *.html*, and *.log* files.</span><span class="sxs-lookup"><span data-stu-id="d673f-397">The streaming log service only monitors files that are deemed readable in plain text mode:  *.txt*, *.html*, and *.log* files.</span></span>

<span data-ttu-id="d673f-398">You can view failed request tracing logs in a browser directly via FTP or locally after using an FTP tool to download them to your local computer.</span><span class="sxs-lookup"><span data-stu-id="d673f-398">You can view failed request tracing logs in a browser directly via FTP or locally after using an FTP tool to download them to your local computer.</span></span> <span data-ttu-id="d673f-399">In this section, you'll view them in a browser directly.</span><span class="sxs-lookup"><span data-stu-id="d673f-399">In this section, you'll view them in a browser directly.</span></span>

1. <span data-ttu-id="d673f-400">In the **Configuration** tab of the **Azure Web App** window that you opened from **Server Explorer**, change **Failed Request Tracing** to **On**, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="d673f-400">In the **Configuration** tab of the **Azure Web App** window that you opened from **Server Explorer**, change **Failed Request Tracing** to **On**, and then click **Save**.</span></span>

    ![Enable failed request tracing](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-failedrequeston.png)
2. <span data-ttu-id="d673f-402">In the address bar of the browser window that shows the web app, add an extra character to the URL and click Enter to cause a 404 error.</span><span class="sxs-lookup"><span data-stu-id="d673f-402">In the address bar of the browser window that shows the web app, add an extra character to the URL and click Enter to cause a 404 error.</span></span>

    <span data-ttu-id="d673f-403">This causes a failed request tracing log to be created, and the following steps show how to view or download the log.</span><span class="sxs-lookup"><span data-stu-id="d673f-403">This causes a failed request tracing log to be created, and the following steps show how to view or download the log.</span></span>

3. <span data-ttu-id="d673f-404">In Visual Studio, in the **Configuration** tab of the **Azure Web App** window, click **Open in Management Portal**.</span><span class="sxs-lookup"><span data-stu-id="d673f-404">In Visual Studio, in the **Configuration** tab of the **Azure Web App** window, click **Open in Management Portal**.</span></span>

4. <span data-ttu-id="d673f-405">In the [Azure portal](https://portal.azure.com) **Settings** page for your web app, click **Deployment credentials**, and then enter a new user name and password.</span><span class="sxs-lookup"><span data-stu-id="d673f-405">In the [Azure portal](https://portal.azure.com) **Settings** page for your web app, click **Deployment credentials**, and then enter a new user name and password.</span></span>

    ![New FTP user name and password](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-enterftpcredentials.png)

    > [!NOTE]
    > <span data-ttu-id="d673f-407">When you log in, you have to use the full user name with the web app name prefixed to it.</span><span class="sxs-lookup"><span data-stu-id="d673f-407">When you log in, you have to use the full user name with the web app name prefixed to it.</span></span> <span data-ttu-id="d673f-408">For example, if you enter "myid" as a user name and the site is "myexample", you log in as "myexample\myid".</span><span class="sxs-lookup"><span data-stu-id="d673f-408">For example, if you enter "myid" as a user name and the site is "myexample", you log in as "myexample\myid".</span></span>
    >

5. <span data-ttu-id="d673f-409">In a new browser window, go to the URL that is shown under **FTP hostname** or **FTPS hostname** in the **Overview** page for your web app.</span><span class="sxs-lookup"><span data-stu-id="d673f-409">In a new browser window, go to the URL that is shown under **FTP hostname** or **FTPS hostname** in the **Overview** page for your web app.</span></span>

6. <span data-ttu-id="d673f-410">Log in using the FTP credentials that you created earlier (including the web app name prefix for the user name).</span><span class="sxs-lookup"><span data-stu-id="d673f-410">Log in using the FTP credentials that you created earlier (including the web app name prefix for the user name).</span></span>

    <span data-ttu-id="d673f-411">The browser shows the root folder of the web app.</span><span class="sxs-lookup"><span data-stu-id="d673f-411">The browser shows the root folder of the web app.</span></span>

7. <span data-ttu-id="d673f-412">Open the *LogFiles* folder.</span><span class="sxs-lookup"><span data-stu-id="d673f-412">Open the *LogFiles* folder.</span></span>

    ![Open LogFiles folder](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-logfilesfolder.png)

8. <span data-ttu-id="d673f-414">Open the folder that is named W3SVC plus a numeric value.</span><span class="sxs-lookup"><span data-stu-id="d673f-414">Open the folder that is named W3SVC plus a numeric value.</span></span>

    ![Open W3SVC folder](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-w3svcfolder.png)

    <span data-ttu-id="d673f-416">The folder contains XML files for any errors that have been logged after you enabled failed request tracing, and an XSL file that a browser can use to format the XML.</span><span class="sxs-lookup"><span data-stu-id="d673f-416">The folder contains XML files for any errors that have been logged after you enabled failed request tracing, and an XSL file that a browser can use to format the XML.</span></span>

    ![W3SVC folder](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-w3svcfoldercontents.png)

9. <span data-ttu-id="d673f-418">Click the XML file for the failed request that you want to see tracing information for.</span><span class="sxs-lookup"><span data-stu-id="d673f-418">Click the XML file for the failed request that you want to see tracing information for.</span></span>

    <span data-ttu-id="d673f-419">The following illustration shows part of the tracing information for a sample error.</span><span class="sxs-lookup"><span data-stu-id="d673f-419">The following illustration shows part of the tracing information for a sample error.</span></span>

    ![Failed request tracing in browser](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-failedrequestinbrowser.png)

## <a name="nextsteps"></a><span data-ttu-id="d673f-421">Next Steps</span><span class="sxs-lookup"><span data-stu-id="d673f-421">Next Steps</span></span>
<span data-ttu-id="d673f-422">You've seen how Visual Studio makes it easy to view logs created by an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="d673f-422">You've seen how Visual Studio makes it easy to view logs created by an Azure web app.</span></span> <span data-ttu-id="d673f-423">The following sections provide links to more resources on related topics:</span><span class="sxs-lookup"><span data-stu-id="d673f-423">The following sections provide links to more resources on related topics:</span></span>

* <span data-ttu-id="d673f-424">Azure web app troubleshooting</span><span class="sxs-lookup"><span data-stu-id="d673f-424">Azure web app troubleshooting</span></span>
* <span data-ttu-id="d673f-425">Debugging in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d673f-425">Debugging in Visual Studio</span></span>
* <span data-ttu-id="d673f-426">Remote debugging in Azure</span><span class="sxs-lookup"><span data-stu-id="d673f-426">Remote debugging in Azure</span></span>
* <span data-ttu-id="d673f-427">Tracing in ASP.NET applications</span><span class="sxs-lookup"><span data-stu-id="d673f-427">Tracing in ASP.NET applications</span></span>
* <span data-ttu-id="d673f-428">Analyzing web server logs</span><span class="sxs-lookup"><span data-stu-id="d673f-428">Analyzing web server logs</span></span>
* <span data-ttu-id="d673f-429">Analyzing failed request tracing logs</span><span class="sxs-lookup"><span data-stu-id="d673f-429">Analyzing failed request tracing logs</span></span>
* <span data-ttu-id="d673f-430">Debugging Cloud Services</span><span class="sxs-lookup"><span data-stu-id="d673f-430">Debugging Cloud Services</span></span>

### <a name="azure-web-app-troubleshooting"></a><span data-ttu-id="d673f-431">Azure web app troubleshooting</span><span class="sxs-lookup"><span data-stu-id="d673f-431">Azure web app troubleshooting</span></span>
<span data-ttu-id="d673f-432">For more information about troubleshooting web apps in Azure App Service, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="d673f-432">For more information about troubleshooting web apps in Azure App Service, see the following resources:</span></span>

* [<span data-ttu-id="d673f-433">How to monitor web apps</span><span class="sxs-lookup"><span data-stu-id="d673f-433">How to monitor web apps</span></span>](web-sites-monitor.md)
* <span data-ttu-id="d673f-434">[Investigating Memory Leaks in Azure Web Apps with Visual Studio 2013](http://blogs.msdn.com/b/visualstudioalm/archive/2013/12/20/investigating-memory-leaks-in-azure-web-sites-with-visual-studio-2013.aspx).</span><span class="sxs-lookup"><span data-stu-id="d673f-434">[Investigating Memory Leaks in Azure Web Apps with Visual Studio 2013](http://blogs.msdn.com/b/visualstudioalm/archive/2013/12/20/investigating-memory-leaks-in-azure-web-sites-with-visual-studio-2013.aspx).</span></span> <span data-ttu-id="d673f-435">Microsoft ALM blog post about Visual Studio features for analyzing managed memory issues.</span><span class="sxs-lookup"><span data-stu-id="d673f-435">Microsoft ALM blog post about Visual Studio features for analyzing managed memory issues.</span></span>
* <span data-ttu-id="d673f-436">[Azure web apps online tools you should know about](https://azure.microsoft.com/blog/2014/03/28/windows-azure-websites-online-tools-you-should-know-about-2/).</span><span class="sxs-lookup"><span data-stu-id="d673f-436">[Azure web apps online tools you should know about](https://azure.microsoft.com/blog/2014/03/28/windows-azure-websites-online-tools-you-should-know-about-2/).</span></span> <span data-ttu-id="d673f-437">Blog post by Amit Apple.</span><span class="sxs-lookup"><span data-stu-id="d673f-437">Blog post by Amit Apple.</span></span>

<span data-ttu-id="d673f-438">For help with a specific troubleshooting question, start a thread in one of the following forums:</span><span class="sxs-lookup"><span data-stu-id="d673f-438">For help with a specific troubleshooting question, start a thread in one of the following forums:</span></span>

* <span data-ttu-id="d673f-439">[The Azure forum on the ASP.NET site](http://forums.asp.net/1247.aspx/1?Azure+and+ASP+NET).</span><span class="sxs-lookup"><span data-stu-id="d673f-439">[The Azure forum on the ASP.NET site](http://forums.asp.net/1247.aspx/1?Azure+and+ASP+NET).</span></span>
* <span data-ttu-id="d673f-440">[The Azure forum on MSDN](http://social.msdn.microsoft.com/Forums/windowsazure/).</span><span class="sxs-lookup"><span data-stu-id="d673f-440">[The Azure forum on MSDN](http://social.msdn.microsoft.com/Forums/windowsazure/).</span></span>
* <span data-ttu-id="d673f-441">[StackOverflow.com](http://www.stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="d673f-441">[StackOverflow.com](http://www.stackoverflow.com).</span></span>

### <a name="debugging-in-visual-studio"></a><span data-ttu-id="d673f-442">Debugging in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d673f-442">Debugging in Visual Studio</span></span>
<span data-ttu-id="d673f-443">For more information about how to use debug mode in Visual Studio, see [Debugging in Visual Studio](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx) and [Debugging Tips with Visual Studio 2010](http://weblogs.asp.net/scottgu/archive/2010/08/18/debugging-tips-with-visual-studio-2010.aspx).</span><span class="sxs-lookup"><span data-stu-id="d673f-443">For more information about how to use debug mode in Visual Studio, see [Debugging in Visual Studio](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx) and [Debugging Tips with Visual Studio 2010](http://weblogs.asp.net/scottgu/archive/2010/08/18/debugging-tips-with-visual-studio-2010.aspx).</span></span>

### <a name="remote-debugging-in-azure"></a><span data-ttu-id="d673f-444">Remote debugging in Azure</span><span class="sxs-lookup"><span data-stu-id="d673f-444">Remote debugging in Azure</span></span>
<span data-ttu-id="d673f-445">For more information about remote debugging for Azure web apps and WebJobs, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="d673f-445">For more information about remote debugging for Azure web apps and WebJobs, see the following resources:</span></span>

* <span data-ttu-id="d673f-446">[Introduction to Remote Debugging Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/05/06/introduction-to-remote-debugging-on-azure-web-sites/).</span><span class="sxs-lookup"><span data-stu-id="d673f-446">[Introduction to Remote Debugging Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/05/06/introduction-to-remote-debugging-on-azure-web-sites/).</span></span>
* [<span data-ttu-id="d673f-447">Introduction to Remote Debugging Azure App Service Web Apps part 2 - Inside Remote debugging</span><span class="sxs-lookup"><span data-stu-id="d673f-447">Introduction to Remote Debugging Azure App Service Web Apps part 2 - Inside Remote debugging</span></span>](https://azure.microsoft.com/blog/2014/05/07/introduction-to-remote-debugging-azure-web-sites-part-2-inside-remote-debugging/)
* [<span data-ttu-id="d673f-448">Introduction to Remote Debugging on Azure App Service Web Apps part 3 - Multi-Instance environment and GIT</span><span class="sxs-lookup"><span data-stu-id="d673f-448">Introduction to Remote Debugging on Azure App Service Web Apps part 3 - Multi-Instance environment and GIT</span></span>](https://azure.microsoft.com/blog/2014/05/08/introduction-to-remote-debugging-on-azure-web-sites-part-3-multi-instance-environment-and-git/)
* [<span data-ttu-id="d673f-449">WebJobs Debugging (video)</span><span class="sxs-lookup"><span data-stu-id="d673f-449">WebJobs Debugging (video)</span></span>](https://www.youtube.com/watch?v=ncQm9q5ZFZs&list=UU_SjTh-ZltPmTYzAybypB-g&index=1)

<span data-ttu-id="d673f-450">If your web app uses an Azure Web API or Mobile Services back-end and you need to debug that, see [Debugging .NET Backend in Visual Studio](http://blogs.msdn.com/b/azuremobile/archive/2014/03/14/debugging-net-backend-in-visual-studio.aspx).</span><span class="sxs-lookup"><span data-stu-id="d673f-450">If your web app uses an Azure Web API or Mobile Services back-end and you need to debug that, see [Debugging .NET Backend in Visual Studio](http://blogs.msdn.com/b/azuremobile/archive/2014/03/14/debugging-net-backend-in-visual-studio.aspx).</span></span>

### <a name="tracing-in-aspnet-applications"></a><span data-ttu-id="d673f-451">Tracing in ASP.NET applications</span><span class="sxs-lookup"><span data-stu-id="d673f-451">Tracing in ASP.NET applications</span></span>
<span data-ttu-id="d673f-452">There are no thorough and up-to-date introductions to ASP.NET tracing available on the Internet.</span><span class="sxs-lookup"><span data-stu-id="d673f-452">There are no thorough and up-to-date introductions to ASP.NET tracing available on the Internet.</span></span> <span data-ttu-id="d673f-453">The best you can do is get started with old introductory materials written for Web Forms because MVC didn't exist yet, and supplement that with newer blog posts that focus on specific issues.</span><span class="sxs-lookup"><span data-stu-id="d673f-453">The best you can do is get started with old introductory materials written for Web Forms because MVC didn't exist yet, and supplement that with newer blog posts that focus on specific issues.</span></span> <span data-ttu-id="d673f-454">Some good places to start are the following resources:</span><span class="sxs-lookup"><span data-stu-id="d673f-454">Some good places to start are the following resources:</span></span>

* <span data-ttu-id="d673f-455">[Monitoring and Telemetry (Building Real-World Cloud Apps with Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry).</span><span class="sxs-lookup"><span data-stu-id="d673f-455">[Monitoring and Telemetry (Building Real-World Cloud Apps with Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry).</span></span><br>
  <span data-ttu-id="d673f-456">E-book chapter with recommendations for tracing in Azure cloud applications.</span><span class="sxs-lookup"><span data-stu-id="d673f-456">E-book chapter with recommendations for tracing in Azure cloud applications.</span></span>
* [<span data-ttu-id="d673f-457">ASP.NET Tracing</span><span class="sxs-lookup"><span data-stu-id="d673f-457">ASP.NET Tracing</span></span>](http://msdn.microsoft.com/library/ms972204.aspx)<br/>
  <span data-ttu-id="d673f-458">Old but still a good resource for a basic introduction to the subject.</span><span class="sxs-lookup"><span data-stu-id="d673f-458">Old but still a good resource for a basic introduction to the subject.</span></span>
* [<span data-ttu-id="d673f-459">Trace Listeners</span><span class="sxs-lookup"><span data-stu-id="d673f-459">Trace Listeners</span></span>](http://msdn.microsoft.com/library/4y5y10s7.aspx)<br/>
  <span data-ttu-id="d673f-460">Information about trace listeners but doesn't mention the [WebPageTraceListener](http://msdn.microsoft.com/library/system.web.webpagetracelistener.aspx).</span><span class="sxs-lookup"><span data-stu-id="d673f-460">Information about trace listeners but doesn't mention the [WebPageTraceListener](http://msdn.microsoft.com/library/system.web.webpagetracelistener.aspx).</span></span>
* [<span data-ttu-id="d673f-461">Walkthrough: Integrating ASP.NET Tracing with System.Diagnostics Tracing</span><span class="sxs-lookup"><span data-stu-id="d673f-461">Walkthrough: Integrating ASP.NET Tracing with System.Diagnostics Tracing</span></span>](http://msdn.microsoft.com/library/b0ectfxd.aspx)<br/>
  <span data-ttu-id="d673f-462">This article is also old, but includes some additional information that the introductory article doesn't cover.</span><span class="sxs-lookup"><span data-stu-id="d673f-462">This article is also old, but includes some additional information that the introductory article doesn't cover.</span></span>
* [<span data-ttu-id="d673f-463">Tracing in ASP.NET MVC Razor Views</span><span class="sxs-lookup"><span data-stu-id="d673f-463">Tracing in ASP.NET MVC Razor Views</span></span>](http://blogs.msdn.com/b/webdev/archive/2013/07/16/tracing-in-asp-net-mvc-razor-views.aspx)<br/>
  <span data-ttu-id="d673f-464">Besides tracing in Razor views, the post also explains how to create an error filter in order to log all unhandled exceptions in an MVC application.</span><span class="sxs-lookup"><span data-stu-id="d673f-464">Besides tracing in Razor views, the post also explains how to create an error filter in order to log all unhandled exceptions in an MVC application.</span></span> <span data-ttu-id="d673f-465">For information about how to log all unhandled exceptions in a Web Forms application, see the Global.asax example in [Complete Example for Error Handlers](http://msdn.microsoft.com/library/bb397417.aspx) on MSDN.</span><span class="sxs-lookup"><span data-stu-id="d673f-465">For information about how to log all unhandled exceptions in a Web Forms application, see the Global.asax example in [Complete Example for Error Handlers](http://msdn.microsoft.com/library/bb397417.aspx) on MSDN.</span></span> <span data-ttu-id="d673f-466">In either MVC or Web Forms, if you want to log certain exceptions but let the default framework handling take effect for them, you can catch and rethrow as in the following example:</span><span class="sxs-lookup"><span data-stu-id="d673f-466">In either MVC or Web Forms, if you want to log certain exceptions but let the default framework handling take effect for them, you can catch and rethrow as in the following example:</span></span>

``` c#
try
{
   // Your code that might cause an exception to be thrown.
}
catch (Exception ex)
{
    Trace.TraceError("Exception: " + ex.ToString());
    throw;
}
```

* [<span data-ttu-id="d673f-467">Streaming Diagnostics Trace Logging from the Azure Command Line (plus Glimpse!)</span><span class="sxs-lookup"><span data-stu-id="d673f-467">Streaming Diagnostics Trace Logging from the Azure Command Line (plus Glimpse!)</span></span>](http://www.hanselman.com/blog/StreamingDiagnosticsTraceLoggingFromTheAzureCommandLinePlusGlimpse.aspx)<br/>
  <span data-ttu-id="d673f-468">How to use the command line to do what this tutorial shows how to do in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d673f-468">How to use the command line to do what this tutorial shows how to do in Visual Studio.</span></span> <span data-ttu-id="d673f-469">[Glimpse](http://www.hanselman.com/blog/IfYoureNotUsingGlimpseWithASPNETForDebuggingAndProfilingYoureMissingOut.aspx) is a tool for debugging ASP.NET applications.</span><span class="sxs-lookup"><span data-stu-id="d673f-469">[Glimpse](http://www.hanselman.com/blog/IfYoureNotUsingGlimpseWithASPNETForDebuggingAndProfilingYoureMissingOut.aspx) is a tool for debugging ASP.NET applications.</span></span>
* <span data-ttu-id="d673f-470">[Using Web Apps Logging and Diagnostics - with David Ebbo](https://azure.microsoft.com/documentation/videos/azure-web-site-logging-and-diagnostics/) and [Streaming Logs from Web Apps - with David Ebbo](https://azure.microsoft.com/documentation/videos/log-streaming-with-azure-web-sites/)</span><span class="sxs-lookup"><span data-stu-id="d673f-470">[Using Web Apps Logging and Diagnostics - with David Ebbo](https://azure.microsoft.com/documentation/videos/azure-web-site-logging-and-diagnostics/) and [Streaming Logs from Web Apps - with David Ebbo](https://azure.microsoft.com/documentation/videos/log-streaming-with-azure-web-sites/)</span></span><br>
  <span data-ttu-id="d673f-471">Videos by Scott Hanselman and David Ebbo.</span><span class="sxs-lookup"><span data-stu-id="d673f-471">Videos by Scott Hanselman and David Ebbo.</span></span>

<span data-ttu-id="d673f-472">For error logging, an alternative to writing your own tracing code is to use an open-source logging framework such as [ELMAH](http://nuget.org/packages/elmah/).</span><span class="sxs-lookup"><span data-stu-id="d673f-472">For error logging, an alternative to writing your own tracing code is to use an open-source logging framework such as [ELMAH](http://nuget.org/packages/elmah/).</span></span> <span data-ttu-id="d673f-473">For more information, see [Scott Hanselman's blog posts about ELMAH](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx).</span><span class="sxs-lookup"><span data-stu-id="d673f-473">For more information, see [Scott Hanselman's blog posts about ELMAH](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx).</span></span>

<span data-ttu-id="d673f-474">Also, you don't need to use ASP.NET or `System.Diagnostics` tracing to get streaming logs from Azure.</span><span class="sxs-lookup"><span data-stu-id="d673f-474">Also, you don't need to use ASP.NET or `System.Diagnostics` tracing to get streaming logs from Azure.</span></span> <span data-ttu-id="d673f-475">The Azure web app streaming log service streams any *.txt*, *.html*, or *.log* file that it finds in the *LogFiles* folder.</span><span class="sxs-lookup"><span data-stu-id="d673f-475">The Azure web app streaming log service streams any *.txt*, *.html*, or *.log* file that it finds in the *LogFiles* folder.</span></span> <span data-ttu-id="d673f-476">Therefore, you could create your own logging system that writes to the file system of the web app, and your file is automatically streamed and downloaded.</span><span class="sxs-lookup"><span data-stu-id="d673f-476">Therefore, you could create your own logging system that writes to the file system of the web app, and your file is automatically streamed and downloaded.</span></span> <span data-ttu-id="d673f-477">All you have to do is write application code that creates files in the *d:\home\logfiles* folder.</span><span class="sxs-lookup"><span data-stu-id="d673f-477">All you have to do is write application code that creates files in the *d:\home\logfiles* folder.</span></span>

### <a name="analyzing-web-server-logs"></a><span data-ttu-id="d673f-478">Analyzing web server logs</span><span class="sxs-lookup"><span data-stu-id="d673f-478">Analyzing web server logs</span></span>
<span data-ttu-id="d673f-479">For more information about analyzing web server logs, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="d673f-479">For more information about analyzing web server logs, see the following resources:</span></span>

* [<span data-ttu-id="d673f-480">LogParser</span><span class="sxs-lookup"><span data-stu-id="d673f-480">LogParser</span></span>](http://www.microsoft.com/download/details.aspx?id=24659)<br/>
  <span data-ttu-id="d673f-481">A tool for viewing data in web server logs (*.log* files).</span><span class="sxs-lookup"><span data-stu-id="d673f-481">A tool for viewing data in web server logs (*.log* files).</span></span>
* [<span data-ttu-id="d673f-482">Troubleshooting IIS Performance Issues or Application Errors using LogParser </span><span class="sxs-lookup"><span data-stu-id="d673f-482">Troubleshooting IIS Performance Issues or Application Errors using LogParser </span></span>](http://www.iis.net/learn/troubleshoot/performance-issues/troubleshooting-iis-performance-issues-or-application-errors-using-logparser)<br/>
  <span data-ttu-id="d673f-483">An introduction to the Log Parser tool that you can use to analyze web server logs.</span><span class="sxs-lookup"><span data-stu-id="d673f-483">An introduction to the Log Parser tool that you can use to analyze web server logs.</span></span>
* [<span data-ttu-id="d673f-484">Blog posts by Robert McMurray on using LogParser</span><span class="sxs-lookup"><span data-stu-id="d673f-484">Blog posts by Robert McMurray on using LogParser</span></span>](http://blogs.msdn.com/b/robert_mcmurray/archive/tags/logparser/)<br/>
* [<span data-ttu-id="d673f-485">The HTTP status code in IIS 7.0, IIS 7.5, and IIS 8.0</span><span class="sxs-lookup"><span data-stu-id="d673f-485">The HTTP status code in IIS 7.0, IIS 7.5, and IIS 8.0</span></span>](http://support.microsoft.com/kb/943891)

### <a name="analyzing-failed-request-tracing-logs"></a><span data-ttu-id="d673f-486">Analyzing failed request tracing logs</span><span class="sxs-lookup"><span data-stu-id="d673f-486">Analyzing failed request tracing logs</span></span>
<span data-ttu-id="d673f-487">The Microsoft TechNet website includes a [Using Failed Request Tracing](http://www.iis.net/learn/troubleshoot/using-failed-request-tracing) section, which may be helpful for understanding how to use these logs.</span><span class="sxs-lookup"><span data-stu-id="d673f-487">The Microsoft TechNet website includes a [Using Failed Request Tracing](http://www.iis.net/learn/troubleshoot/using-failed-request-tracing) section, which may be helpful for understanding how to use these logs.</span></span> <span data-ttu-id="d673f-488">However, this documentation focuses mainly on configuring failed request tracing in IIS, which you can't do in Azure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="d673f-488">However, this documentation focuses mainly on configuring failed request tracing in IIS, which you can't do in Azure Web Apps.</span></span>

[GetStarted]: app-service-web-get-started-dotnet.md
[GetStartedWJ]: https://github.com/Azure/azure-webjobs-sdk/wiki
