---
title: Profile ASP.NET Core Azure Linux web apps with Application Insights Profiler | Microsoft Docs
description: A conceptual overview and step-by-step tutorial on how to use Application Insights Profiler.
services: application-insights
documentationcenter: ''
author: mrbullwinkle
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: conceptual
ms.date: 02/23/2018
ms.author: mbullwin
ms.openlocfilehash: 6fcc11b0120c9d19cfc1482100ac68d04c9d625d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869614"
---
# <a name="profile-aspnet-core-azure-linux-web-apps-with-application-insights-profiler"></a><span data-ttu-id="5624b-103">Profile ASP.NET Core Azure Linux web apps with Application Insights Profiler</span><span class="sxs-lookup"><span data-stu-id="5624b-103">Profile ASP.NET Core Azure Linux web apps with Application Insights Profiler</span></span>

<span data-ttu-id="5624b-104">This feature is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="5624b-104">This feature is currently in preview.</span></span>

<span data-ttu-id="5624b-105">Find out how much time is spent in each method of your live web application when using [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5624b-105">Find out how much time is spent in each method of your live web application when using [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="5624b-106">Application Insights Profiler is now available for ASP.NET Core web apps that are hosted in Linux on Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="5624b-106">Application Insights Profiler is now available for ASP.NET Core web apps that are hosted in Linux on Azure App Service.</span></span> <span data-ttu-id="5624b-107">This guide provides step-by-step instructions on how the Profiler traces can be collected for ASP.NET Core Linux web apps.</span><span class="sxs-lookup"><span data-stu-id="5624b-107">This guide provides step-by-step instructions on how the Profiler traces can be collected for ASP.NET Core Linux web apps.</span></span>

<span data-ttu-id="5624b-108">After you complete this walkthrough, your app can collect Profiler traces like the traces that are shown in the image.</span><span class="sxs-lookup"><span data-stu-id="5624b-108">After you complete this walkthrough, your app can collect Profiler traces like the traces that are shown in the image.</span></span> <span data-ttu-id="5624b-109">In this example, the Profiler trace indicates that a particular web request is slow because of time spent waiting.</span><span class="sxs-lookup"><span data-stu-id="5624b-109">In this example, the Profiler trace indicates that a particular web request is slow because of time spent waiting.</span></span> <span data-ttu-id="5624b-110">The *hot path* in the code that's slowing the app is marked by a flame icon.</span><span class="sxs-lookup"><span data-stu-id="5624b-110">The *hot path* in the code that's slowing the app is marked by a flame icon.</span></span> <span data-ttu-id="5624b-111">The **About** method in the **HomeController** section is slowing the web app because the method is calling the **Thread.Sleep** function.</span><span class="sxs-lookup"><span data-stu-id="5624b-111">The **About** method in the **HomeController** section is slowing the web app because the method is calling the **Thread.Sleep** function.</span></span>

![Profiler traces](./media/app-insights-profiler-aspnetcore-linux/profiler-traces.png)

## <a name="prerequisites"></a><span data-ttu-id="5624b-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5624b-113">Prerequisites</span></span>
<span data-ttu-id="5624b-114">The following instructions apply to all Windows, Linux, and Mac development environments:</span><span class="sxs-lookup"><span data-stu-id="5624b-114">The following instructions apply to all Windows, Linux, and Mac development environments:</span></span>

* <span data-ttu-id="5624b-115">Install the [.NET Core SDK 2.1.2 or later](https://www.microsoft.com/net/download/windows/build).</span><span class="sxs-lookup"><span data-stu-id="5624b-115">Install the [.NET Core SDK 2.1.2 or later](https://www.microsoft.com/net/download/windows/build).</span></span>
* <span data-ttu-id="5624b-116">Install Git by following the instructions at [Getting Started - Installing Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).</span><span class="sxs-lookup"><span data-stu-id="5624b-116">Install Git by following the instructions at [Getting Started - Installing Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).</span></span>

## <a name="set-up-the-project-locally"></a><span data-ttu-id="5624b-117">Set up the project locally</span><span class="sxs-lookup"><span data-stu-id="5624b-117">Set up the project locally</span></span>

1. <span data-ttu-id="5624b-118">Open a Command Prompt window on your machine.</span><span class="sxs-lookup"><span data-stu-id="5624b-118">Open a Command Prompt window on your machine.</span></span> <span data-ttu-id="5624b-119">The following instructions work for all Windows, Linux, and Mac development environments.</span><span class="sxs-lookup"><span data-stu-id="5624b-119">The following instructions work for all Windows, Linux, and Mac development environments.</span></span>

2. <span data-ttu-id="5624b-120">Create an ASP.NET Core MVC web application:</span><span class="sxs-lookup"><span data-stu-id="5624b-120">Create an ASP.NET Core MVC web application:</span></span>

    ```
    dotnet new mvc -n LinuxProfilerTest
    ```

3. <span data-ttu-id="5624b-121">Change the working directory to the root folder for the project.</span><span class="sxs-lookup"><span data-stu-id="5624b-121">Change the working directory to the root folder for the project.</span></span>

4. <span data-ttu-id="5624b-122">Add the NuGet package to collect the Profiler traces:</span><span class="sxs-lookup"><span data-stu-id="5624b-122">Add the NuGet package to collect the Profiler traces:</span></span>

    ```
    dotnet add package Microsoft.ApplicationInsights.Profiler.AspNetCore
    ```

5. <span data-ttu-id="5624b-123">Add a line of code in the **HomeController.cs** section to randomly delay a few seconds:</span><span class="sxs-lookup"><span data-stu-id="5624b-123">Add a line of code in the **HomeController.cs** section to randomly delay a few seconds:</span></span>

    ```csharp
        using System.Threading;
        ...

        public IActionResult About()
            {
                Random r = new Random();
                int delay = r.Next(5000, 10000);
                Thread.Sleep(delay);
                return View();
            }
    ```

6. <span data-ttu-id="5624b-124">Save and commit your changes to the local repository:</span><span class="sxs-lookup"><span data-stu-id="5624b-124">Save and commit your changes to the local repository:</span></span>

    ```
        git init
        git add .
        git commit -m "first commit"
    ```

## <a name="create-the-linux-web-app-to-host-your-project"></a><span data-ttu-id="5624b-125">Create the Linux web app to host your project</span><span class="sxs-lookup"><span data-stu-id="5624b-125">Create the Linux web app to host your project</span></span>

1. <span data-ttu-id="5624b-126">Create the web app environment by using App Service on Linux:</span><span class="sxs-lookup"><span data-stu-id="5624b-126">Create the web app environment by using App Service on Linux:</span></span>

    ![Create the Linux web app](./media/app-insights-profiler-aspnetcore-linux/create-linux-appservice.png)

2. <span data-ttu-id="5624b-128">Create the deployment credentials:</span><span class="sxs-lookup"><span data-stu-id="5624b-128">Create the deployment credentials:</span></span>

    > [!NOTE]
    > <span data-ttu-id="5624b-129">Record your password to use later when deploying your web app.</span><span class="sxs-lookup"><span data-stu-id="5624b-129">Record your password to use later when deploying your web app.</span></span>

    ![Create the deployment credentials](./media/app-insights-profiler-aspnetcore-linux/create-deployment-credentials.png)

3. <span data-ttu-id="5624b-131">Choose the deployment options.</span><span class="sxs-lookup"><span data-stu-id="5624b-131">Choose the deployment options.</span></span> <span data-ttu-id="5624b-132">Set up a local Git repository in the web app by following the instructions on the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="5624b-132">Set up a local Git repository in the web app by following the instructions on the Azure portal.</span></span> <span data-ttu-id="5624b-133">A Git repository is automatically created.</span><span class="sxs-lookup"><span data-stu-id="5624b-133">A Git repository is automatically created.</span></span>

    ![Set up the Git repository](./media/app-insights-profiler-aspnetcore-linux/setup-git-repo.png)

<span data-ttu-id="5624b-135">For more deployment options, see [this article](https://docs.microsoft.com/azure/app-service/containers/choose-deployment-type).</span><span class="sxs-lookup"><span data-stu-id="5624b-135">For more deployment options, see [this article](https://docs.microsoft.com/azure/app-service/containers/choose-deployment-type).</span></span>

## <a name="deploy-your-project"></a><span data-ttu-id="5624b-136">Deploy your project</span><span class="sxs-lookup"><span data-stu-id="5624b-136">Deploy your project</span></span>

1. <span data-ttu-id="5624b-137">In your Command Prompt window, browse to the root folder for your project.</span><span class="sxs-lookup"><span data-stu-id="5624b-137">In your Command Prompt window, browse to the root folder for your project.</span></span> <span data-ttu-id="5624b-138">Add a Git remote repository to point to the repository on App Service:</span><span class="sxs-lookup"><span data-stu-id="5624b-138">Add a Git remote repository to point to the repository on App Service:</span></span>

    ```
    git remote add azure https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git
    ```

    * <span data-ttu-id="5624b-139">Use the **username** that you used to create the deployment credentials.</span><span class="sxs-lookup"><span data-stu-id="5624b-139">Use the **username** that you used to create the deployment credentials.</span></span>
    * <span data-ttu-id="5624b-140">Use the **app name** that you used to create the web app by using App Service on Linux.</span><span class="sxs-lookup"><span data-stu-id="5624b-140">Use the **app name** that you used to create the web app by using App Service on Linux.</span></span>

2. <span data-ttu-id="5624b-141">Deploy the project by pushing the changes to Azure:</span><span class="sxs-lookup"><span data-stu-id="5624b-141">Deploy the project by pushing the changes to Azure:</span></span>

    ```
    git push azure master
    ```

<span data-ttu-id="5624b-142">You should see output similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="5624b-142">You should see output similar to the following example:</span></span>

    ```
    Counting objects: 9, done.
    Delta compression using up to 8 threads.
    Compressing objects: 100% (8/8), done.
    Writing objects: 100% (9/9), 1.78 KiB | 911.00 KiB/s, done.
    Total 9 (delta 3), reused 0 (delta 0)
    remote: Updating branch 'master'.
    remote: Updating submodules.
    remote: Preparing deployment for commit id 'd7369a99d7'.
    remote: Generating deployment script.
    remote: Running deployment command...
    remote: Handling ASP.NET Core Web Application deployment.
    remote: ......
    remote:   Restoring packages for /home/site/repository/EventPipeExampleLinux.csproj...
    remote: .
    remote:   Installing Newtonsoft.Json 10.0.3.
    remote:   Installing Microsoft.ApplicationInsights.Profiler.Core 1.1.0-LKG
    …

    ```

## <a name="add-application-insights-to-monitor-your-web-apps"></a><span data-ttu-id="5624b-143">Add Application Insights to monitor your web apps</span><span class="sxs-lookup"><span data-stu-id="5624b-143">Add Application Insights to monitor your web apps</span></span>

1. <span data-ttu-id="5624b-144">[Create an Application Insights resource](./app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="5624b-144">[Create an Application Insights resource](./app-insights-create-new-resource.md).</span></span>

2. <span data-ttu-id="5624b-145">Copy the **iKey** value of the Application Insights resource and set the following settings in your web apps:</span><span class="sxs-lookup"><span data-stu-id="5624b-145">Copy the **iKey** value of the Application Insights resource and set the following settings in your web apps:</span></span>

    ```
    APPINSIGHTS_INSTRUMENTATIONKEY: [YOUR_APPINSIGHTS_KEY]
    ASPNETCORE_HOSTINGSTARTUPASSEMBLIES: Microsoft.ApplicationInsights.Profiler.AspNetCore
    ```

    ![Configure the app settings](./media/app-insights-profiler-aspnetcore-linux/set-appsettings.png)

    <span data-ttu-id="5624b-147">When the app settings are changed, the site automatically restarts.</span><span class="sxs-lookup"><span data-stu-id="5624b-147">When the app settings are changed, the site automatically restarts.</span></span> <span data-ttu-id="5624b-148">After the new settings are applied, the Profiler immediately runs for two minutes.</span><span class="sxs-lookup"><span data-stu-id="5624b-148">After the new settings are applied, the Profiler immediately runs for two minutes.</span></span> <span data-ttu-id="5624b-149">The Profiler then runs for two minutes every hour.</span><span class="sxs-lookup"><span data-stu-id="5624b-149">The Profiler then runs for two minutes every hour.</span></span>

3. <span data-ttu-id="5624b-150">Generate some traffic to your website.</span><span class="sxs-lookup"><span data-stu-id="5624b-150">Generate some traffic to your website.</span></span> <span data-ttu-id="5624b-151">You can generate traffic by refreshing the site **About** page a few times.</span><span class="sxs-lookup"><span data-stu-id="5624b-151">You can generate traffic by refreshing the site **About** page a few times.</span></span>

4. <span data-ttu-id="5624b-152">Wait two to five minutes for the events to aggregate to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="5624b-152">Wait two to five minutes for the events to aggregate to Application Insights.</span></span>

5. <span data-ttu-id="5624b-153">Browse to the Application Insights **Performance** pane in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="5624b-153">Browse to the Application Insights **Performance** pane in the Azure portal.</span></span> <span data-ttu-id="5624b-154">You can view the Profiler traces at the bottom right of the pane.</span><span class="sxs-lookup"><span data-stu-id="5624b-154">You can view the Profiler traces at the bottom right of the pane.</span></span>

    ![View Profiler traces](./media/app-insights-profiler-aspnetcore-linux/view-traces.png)

## <a name="known-issues"></a><span data-ttu-id="5624b-156">Known issues</span><span class="sxs-lookup"><span data-stu-id="5624b-156">Known issues</span></span>

### <a name="the-enable-action-in-the-profiler-configuration-pane-doesnt-work"></a><span data-ttu-id="5624b-157">The Enable action in the Profiler Configuration pane doesn't work</span><span class="sxs-lookup"><span data-stu-id="5624b-157">The Enable action in the Profiler Configuration pane doesn't work</span></span>

> [!NOTE]
> <span data-ttu-id="5624b-158">If you host your app by using App Service on Linux, you don't need to re-enable the Profiler in the **Performance** pane in the Application Insights portal.</span><span class="sxs-lookup"><span data-stu-id="5624b-158">If you host your app by using App Service on Linux, you don't need to re-enable the Profiler in the **Performance** pane in the Application Insights portal.</span></span> <span data-ttu-id="5624b-159">You can include the NuGet package in your project and set the Application Insights **iKey** value in your web app settings to enable the Profiler.</span><span class="sxs-lookup"><span data-stu-id="5624b-159">You can include the NuGet package in your project and set the Application Insights **iKey** value in your web app settings to enable the Profiler.</span></span>

<span data-ttu-id="5624b-160">If you follow the enablement workflow for [Application Insights Profiler for Windows](./app-insights-profiler.md) and select **Enable** in the **Configure Profiler** pane, you receive an error.</span><span class="sxs-lookup"><span data-stu-id="5624b-160">If you follow the enablement workflow for [Application Insights Profiler for Windows](./app-insights-profiler.md) and select **Enable** in the **Configure Profiler** pane, you receive an error.</span></span> <span data-ttu-id="5624b-161">The enable action tries to install the Windows version of the Profiler agent on the Linux environment.</span><span class="sxs-lookup"><span data-stu-id="5624b-161">The enable action tries to install the Windows version of the Profiler agent on the Linux environment.</span></span>

<span data-ttu-id="5624b-162">We're working on a resolution for this issue.</span><span class="sxs-lookup"><span data-stu-id="5624b-162">We're working on a resolution for this issue.</span></span>

![Don't try to re-enable the Profiler in the Performance pane](./media/app-insights-profiler-aspnetcore-linux/issue-enable-profiler.png)


## <a name="next-steps"></a><span data-ttu-id="5624b-164">Next steps</span><span class="sxs-lookup"><span data-stu-id="5624b-164">Next steps</span></span>
<span data-ttu-id="5624b-165">If you use custom containers that are hosted by Azure App Service, follow the instructions in [ Enable Service Profiler for a containerized ASP.NET Core application](https://github.com/Microsoft/ApplicationInsights-Profiler-AspNetCore/tree/master/examples/EnableServiceProfilerForContainerApp) to enable Application Insights Profiler.</span><span class="sxs-lookup"><span data-stu-id="5624b-165">If you use custom containers that are hosted by Azure App Service, follow the instructions in [ Enable Service Profiler for a containerized ASP.NET Core application](https://github.com/Microsoft/ApplicationInsights-Profiler-AspNetCore/tree/master/examples/EnableServiceProfilerForContainerApp) to enable Application Insights Profiler.</span></span>

<span data-ttu-id="5624b-166">Report any issues or suggestions to the Application Insights GitHub repository: [ApplicationInsights-Profiler-AspNetCore: Issues](https://github.com/Microsoft/ApplicationInsights-Profiler-AspNetCore/issues).</span><span class="sxs-lookup"><span data-stu-id="5624b-166">Report any issues or suggestions to the Application Insights GitHub repository: [ApplicationInsights-Profiler-AspNetCore: Issues](https://github.com/Microsoft/ApplicationInsights-Profiler-AspNetCore/issues).</span></span>
