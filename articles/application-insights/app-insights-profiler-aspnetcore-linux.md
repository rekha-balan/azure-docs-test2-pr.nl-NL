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
# <a name="profile-aspnet-core-azure-linux-web-apps-with-application-insights-profiler"></a>Profile ASP.NET Core Azure Linux web apps with Application Insights Profiler

This feature is currently in preview.

Find out how much time is spent in each method of your live web application when using [Application Insights](app-insights-overview.md). Application Insights Profiler is now available for ASP.NET Core web apps that are hosted in Linux on Azure App Service. This guide provides step-by-step instructions on how the Profiler traces can be collected for ASP.NET Core Linux web apps.

After you complete this walkthrough, your app can collect Profiler traces like the traces that are shown in the image. In this example, the Profiler trace indicates that a particular web request is slow because of time spent waiting. The *hot path* in the code that's slowing the app is marked by a flame icon. The **About** method in the **HomeController** section is slowing the web app because the method is calling the **Thread.Sleep** function.

![Profiler traces](./media/app-insights-profiler-aspnetcore-linux/profiler-traces.png)

## <a name="prerequisites"></a>Prerequisites
The following instructions apply to all Windows, Linux, and Mac development environments:

* Install the [.NET Core SDK 2.1.2 or later](https://www.microsoft.com/net/download/windows/build).
* Install Git by following the instructions at [Getting Started - Installing Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).

## <a name="set-up-the-project-locally"></a>Set up the project locally

1. Open a Command Prompt window on your machine. The following instructions work for all Windows, Linux, and Mac development environments.

2. Create an ASP.NET Core MVC web application:

    ```
    dotnet new mvc -n LinuxProfilerTest
    ```

3. Change the working directory to the root folder for the project.

4. Add the NuGet package to collect the Profiler traces:

    ```
    dotnet add package Microsoft.ApplicationInsights.Profiler.AspNetCore
    ```

5. Add a line of code in the **HomeController.cs** section to randomly delay a few seconds:

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

6. Save and commit your changes to the local repository:

    ```
        git init
        git add .
        git commit -m "first commit"
    ```

## <a name="create-the-linux-web-app-to-host-your-project"></a>Create the Linux web app to host your project

1. Create the web app environment by using App Service on Linux:

    ![Create the Linux web app](./media/app-insights-profiler-aspnetcore-linux/create-linux-appservice.png)

2. Create the deployment credentials:

    > [!NOTE]
    > Record your password to use later when deploying your web app.

    ![Create the deployment credentials](./media/app-insights-profiler-aspnetcore-linux/create-deployment-credentials.png)

3. Choose the deployment options. Set up a local Git repository in the web app by following the instructions on the Azure portal. A Git repository is automatically created.

    ![Set up the Git repository](./media/app-insights-profiler-aspnetcore-linux/setup-git-repo.png)

For more deployment options, see [this article](https://docs.microsoft.com/azure/app-service/containers/choose-deployment-type).

## <a name="deploy-your-project"></a>Deploy your project

1. In your Command Prompt window, browse to the root folder for your project. Add a Git remote repository to point to the repository on App Service:

    ```
    git remote add azure https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git
    ```

    * Use the **username** that you used to create the deployment credentials.
    * Use the **app name** that you used to create the web app by using App Service on Linux.

2. Deploy the project by pushing the changes to Azure:

    ```
    git push azure master
    ```

You should see output similar to the following example:

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

## <a name="add-application-insights-to-monitor-your-web-apps"></a>Add Application Insights to monitor your web apps

1. [Create an Application Insights resource](./app-insights-create-new-resource.md).

2. Copy the **iKey** value of the Application Insights resource and set the following settings in your web apps:

    ```
    APPINSIGHTS_INSTRUMENTATIONKEY: [YOUR_APPINSIGHTS_KEY]
    ASPNETCORE_HOSTINGSTARTUPASSEMBLIES: Microsoft.ApplicationInsights.Profiler.AspNetCore
    ```

    ![Configure the app settings](./media/app-insights-profiler-aspnetcore-linux/set-appsettings.png)

    When the app settings are changed, the site automatically restarts. After the new settings are applied, the Profiler immediately runs for two minutes. The Profiler then runs for two minutes every hour.

3. Generate some traffic to your website. You can generate traffic by refreshing the site **About** page a few times.

4. Wait two to five minutes for the events to aggregate to Application Insights.

5. Browse to the Application Insights **Performance** pane in the Azure portal. You can view the Profiler traces at the bottom right of the pane.

    ![View Profiler traces](./media/app-insights-profiler-aspnetcore-linux/view-traces.png)

## <a name="known-issues"></a>Known issues

### <a name="the-enable-action-in-the-profiler-configuration-pane-doesnt-work"></a>The Enable action in the Profiler Configuration pane doesn't work

> [!NOTE]
> If you host your app by using App Service on Linux, you don't need to re-enable the Profiler in the **Performance** pane in the Application Insights portal. You can include the NuGet package in your project and set the Application Insights **iKey** value in your web app settings to enable the Profiler.

If you follow the enablement workflow for [Application Insights Profiler for Windows](./app-insights-profiler.md) and select **Enable** in the **Configure Profiler** pane, you receive an error. The enable action tries to install the Windows version of the Profiler agent on the Linux environment.

We're working on a resolution for this issue.

![Don't try to re-enable the Profiler in the Performance pane](./media/app-insights-profiler-aspnetcore-linux/issue-enable-profiler.png)


## <a name="next-steps"></a>Next steps
If you use custom containers that are hosted by Azure App Service, follow the instructions in [ Enable Service Profiler for a containerized ASP.NET Core application](https://github.com/Microsoft/ApplicationInsights-Profiler-AspNetCore/tree/master/examples/EnableServiceProfilerForContainerApp) to enable Application Insights Profiler.

Report any issues or suggestions to the Application Insights GitHub repository: [ApplicationInsights-Profiler-AspNetCore: Issues](https://github.com/Microsoft/ApplicationInsights-Profiler-AspNetCore/issues).