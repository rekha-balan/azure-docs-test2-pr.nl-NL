---
title: Deploy WebJobs using Visual Studio
description: Learn how to deploy Azure WebJobs to Azure App Service Web Apps using Visual Studio.
services: app-service
documentationcenter: ''
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: a3a9d320-1201-4ac8-9398-b4c9535ba755
ms.service: app-service
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2016
ms.author: glenga
ms.openlocfilehash: 1f9879551edef04843f189ea9127a9a6b1018f8f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553884"
---
# <a name="deploy-webjobs-using-visual-studio"></a><span data-ttu-id="404c1-103">Deploy WebJobs using Visual Studio</span><span class="sxs-lookup"><span data-stu-id="404c1-103">Deploy WebJobs using Visual Studio</span></span>
## <a name="overview"></a><span data-ttu-id="404c1-104">Overview</span><span class="sxs-lookup"><span data-stu-id="404c1-104">Overview</span></span>
<span data-ttu-id="404c1-105">This topic explains how to use Visual Studio to deploy a Console Application project to a web app in [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) as an [Azure WebJob](http://go.microsoft.com/fwlink/?LinkId=390226).</span><span class="sxs-lookup"><span data-stu-id="404c1-105">This topic explains how to use Visual Studio to deploy a Console Application project to a web app in [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) as an [Azure WebJob](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span> <span data-ttu-id="404c1-106">For information about how to deploy WebJobs by using the [Azure Portal](https://portal.azure.com), see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="404c1-106">For information about how to deploy WebJobs by using the [Azure Portal](https://portal.azure.com), see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

<span data-ttu-id="404c1-107">When Visual Studio deploys a WebJobs-enabled Console Application project, it performs two tasks:</span><span class="sxs-lookup"><span data-stu-id="404c1-107">When Visual Studio deploys a WebJobs-enabled Console Application project, it performs two tasks:</span></span>

* <span data-ttu-id="404c1-108">Copies runtime files to the appropriate folder in the web app (*App_Data/jobs/continuous* for continuous WebJobs, *App_Data/jobs/triggered* for scheduled and on-demand WebJobs).</span><span class="sxs-lookup"><span data-stu-id="404c1-108">Copies runtime files to the appropriate folder in the web app (*App_Data/jobs/continuous* for continuous WebJobs, *App_Data/jobs/triggered* for scheduled and on-demand WebJobs).</span></span>
* <span data-ttu-id="404c1-109">Sets up [Azure Scheduler jobs](#scheduler) for WebJobs that are scheduled to run at particular times.</span><span class="sxs-lookup"><span data-stu-id="404c1-109">Sets up [Azure Scheduler jobs](#scheduler) for WebJobs that are scheduled to run at particular times.</span></span> <span data-ttu-id="404c1-110">(This is not needed for continuous WebJobs.)</span><span class="sxs-lookup"><span data-stu-id="404c1-110">(This is not needed for continuous WebJobs.)</span></span>

<span data-ttu-id="404c1-111">A WebJobs-enabled project has the following items added to it:</span><span class="sxs-lookup"><span data-stu-id="404c1-111">A WebJobs-enabled project has the following items added to it:</span></span>

* <span data-ttu-id="404c1-112">The [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package.</span><span class="sxs-lookup"><span data-stu-id="404c1-112">The [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package.</span></span>
* <span data-ttu-id="404c1-113">A [webjob-publish-settings.json](#publishsettings) file that contains deployment and scheduler settings.</span><span class="sxs-lookup"><span data-stu-id="404c1-113">A [webjob-publish-settings.json](#publishsettings) file that contains deployment and scheduler settings.</span></span> 

![Diagram showing what is added to a Console App to enable deployment as a WebJob](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-deploy-webjobs/convert.png)

<span data-ttu-id="404c1-115">You can add these items to an existing Console Application project or use a template to create a new WebJobs-enabled Console Application project.</span><span class="sxs-lookup"><span data-stu-id="404c1-115">You can add these items to an existing Console Application project or use a template to create a new WebJobs-enabled Console Application project.</span></span> 

<span data-ttu-id="404c1-116">You can deploy a project as a WebJob by itself, or link it to a web project so that it automatically deploys whenever you deploy the web project.</span><span class="sxs-lookup"><span data-stu-id="404c1-116">You can deploy a project as a WebJob by itself, or link it to a web project so that it automatically deploys whenever you deploy the web project.</span></span> <span data-ttu-id="404c1-117">To link projects, Visual Studio includes the name of the WebJobs-enabled project in a [webjobs-list.json](#webjobslist) file in the web project.</span><span class="sxs-lookup"><span data-stu-id="404c1-117">To link projects, Visual Studio includes the name of the WebJobs-enabled project in a [webjobs-list.json](#webjobslist) file in the web project.</span></span>

![Diagram showing WebJob project linking to web project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-deploy-webjobs/link.png)

## <a name="prerequisites"></a><span data-ttu-id="404c1-119">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="404c1-119">Prerequisites</span></span>
<span data-ttu-id="404c1-120">WebJobs deployment features are available in Visual Studio 2015 when you install the Azure SDK for .NET:</span><span class="sxs-lookup"><span data-stu-id="404c1-120">WebJobs deployment features are available in Visual Studio 2015 when you install the Azure SDK for .NET:</span></span>

* <span data-ttu-id="404c1-121">[Azure SDK for .NET (Visual Studio 2015)](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="404c1-121">[Azure SDK for .NET (Visual Studio 2015)](http://go.microsoft.com/fwlink/?linkid=518003).</span></span>

## <a id="convert"></a><span data-ttu-id="404c1-122">Enable WebJobs deployment for an existing Console Application project</span><span class="sxs-lookup"><span data-stu-id="404c1-122">Enable WebJobs deployment for an existing Console Application project</span></span>
<span data-ttu-id="404c1-123">You have two options:</span><span class="sxs-lookup"><span data-stu-id="404c1-123">You have two options:</span></span>

* <span data-ttu-id="404c1-124">[Enable automatic deployment with a web project](#convertlink).</span><span class="sxs-lookup"><span data-stu-id="404c1-124">[Enable automatic deployment with a web project](#convertlink).</span></span>
  
    <span data-ttu-id="404c1-125">Configure an existing Console Application project so that it automatically deploys as a WebJob when you deploy a web project.</span><span class="sxs-lookup"><span data-stu-id="404c1-125">Configure an existing Console Application project so that it automatically deploys as a WebJob when you deploy a web project.</span></span> <span data-ttu-id="404c1-126">Use this option when you want to run your WebJob in the same web app in which you run the related web application.</span><span class="sxs-lookup"><span data-stu-id="404c1-126">Use this option when you want to run your WebJob in the same web app in which you run the related web application.</span></span>
* <span data-ttu-id="404c1-127">[Enable deployment without a web project](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="404c1-127">[Enable deployment without a web project](#convertnolink).</span></span>
  
    <span data-ttu-id="404c1-128">Configure an existing Console Application project to deploy as a WebJob by itself, with no link to a web project.</span><span class="sxs-lookup"><span data-stu-id="404c1-128">Configure an existing Console Application project to deploy as a WebJob by itself, with no link to a web project.</span></span> <span data-ttu-id="404c1-129">Use this option when you want to run a WebJob in a web app by itself, with no web application running in the web app.</span><span class="sxs-lookup"><span data-stu-id="404c1-129">Use this option when you want to run a WebJob in a web app by itself, with no web application running in the web app.</span></span> <span data-ttu-id="404c1-130">You might want to do this in order to be able to scale your WebJob resources independently of your web application resources.</span><span class="sxs-lookup"><span data-stu-id="404c1-130">You might want to do this in order to be able to scale your WebJob resources independently of your web application resources.</span></span>

### <a id="convertlink"></a> <span data-ttu-id="404c1-131">Enable automatic WebJobs deployment with a web project</span><span class="sxs-lookup"><span data-stu-id="404c1-131">Enable automatic WebJobs deployment with a web project</span></span>
1. <span data-ttu-id="404c1-132">Right-click the web project in **Solution Explorer**, and then click **Add** > **Existing Project as Azure WebJob**.</span><span class="sxs-lookup"><span data-stu-id="404c1-132">Right-click the web project in **Solution Explorer**, and then click **Add** > **Existing Project as Azure WebJob**.</span></span>
   
    ![Existing Project as Azure WebJob](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-deploy-webjobs/eawj.png)
   
    <span data-ttu-id="404c1-134">The [Add Azure WebJob](#configure) dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="404c1-134">The [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="404c1-135">In the **Project name** drop-down list, select the Console Application project to add as a WebJob.</span><span class="sxs-lookup"><span data-stu-id="404c1-135">In the **Project name** drop-down list, select the Console Application project to add as a WebJob.</span></span>
   
    ![Selecting project in Add Azure WebJob dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-deploy-webjobs/aaw1.png)
3. <span data-ttu-id="404c1-137">Complete the [Add Azure WebJob](#configure) dialog, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="404c1-137">Complete the [Add Azure WebJob](#configure) dialog, and then click **OK**.</span></span> 

### <a id="convertnolink"></a> <span data-ttu-id="404c1-138">Enable WebJobs deployment without a web project</span><span class="sxs-lookup"><span data-stu-id="404c1-138">Enable WebJobs deployment without a web project</span></span>
1. <span data-ttu-id="404c1-139">Right-click the Console Application project in **Solution Explorer**, and then click **Publish as Azure WebJob**.</span><span class="sxs-lookup"><span data-stu-id="404c1-139">Right-click the Console Application project in **Solution Explorer**, and then click **Publish as Azure WebJob**.</span></span> 
   
    ![Publish as Azure WebJob](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-deploy-webjobs/paw.png)
   
    <span data-ttu-id="404c1-141">The [Add Azure WebJob](#configure) dialog box appears, with the project selected in the **Project name** box.</span><span class="sxs-lookup"><span data-stu-id="404c1-141">The [Add Azure WebJob](#configure) dialog box appears, with the project selected in the **Project name** box.</span></span>
2. <span data-ttu-id="404c1-142">Complete the [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="404c1-142">Complete the [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>
   
   <span data-ttu-id="404c1-143">The **Publish Web** wizard appears.</span><span class="sxs-lookup"><span data-stu-id="404c1-143">The **Publish Web** wizard appears.</span></span>  <span data-ttu-id="404c1-144">If you don't want to publish immediately, close the wizard.</span><span class="sxs-lookup"><span data-stu-id="404c1-144">If you don't want to publish immediately, close the wizard.</span></span> <span data-ttu-id="404c1-145">The settings that you've entered are saved for when you do want to [deploy the project](#deploy).</span><span class="sxs-lookup"><span data-stu-id="404c1-145">The settings that you've entered are saved for when you do want to [deploy the project](#deploy).</span></span>

## <a id="create"></a><span data-ttu-id="404c1-146">Create a new WebJobs-enabled project</span><span class="sxs-lookup"><span data-stu-id="404c1-146">Create a new WebJobs-enabled project</span></span>
<span data-ttu-id="404c1-147">To create a new WebJobs-enabled project, you can use the Console Application project template and enable WebJobs deployment as explained in [the previous section](#convert).</span><span class="sxs-lookup"><span data-stu-id="404c1-147">To create a new WebJobs-enabled project, you can use the Console Application project template and enable WebJobs deployment as explained in [the previous section](#convert).</span></span> <span data-ttu-id="404c1-148">As an alternative, you can use the WebJobs new-project template:</span><span class="sxs-lookup"><span data-stu-id="404c1-148">As an alternative, you can use the WebJobs new-project template:</span></span>

* [<span data-ttu-id="404c1-149">Use the WebJobs new-project template for an independent WebJob</span><span class="sxs-lookup"><span data-stu-id="404c1-149">Use the WebJobs new-project template for an independent WebJob</span></span>](#createnolink)
  
    <span data-ttu-id="404c1-150">Create a project and configure it to deploy by itself as a WebJob, with no link to a web project.</span><span class="sxs-lookup"><span data-stu-id="404c1-150">Create a project and configure it to deploy by itself as a WebJob, with no link to a web project.</span></span> <span data-ttu-id="404c1-151">Use this option when you want to run a WebJob in a web app by itself, with no web application running in the web app.</span><span class="sxs-lookup"><span data-stu-id="404c1-151">Use this option when you want to run a WebJob in a web app by itself, with no web application running in the web app.</span></span> <span data-ttu-id="404c1-152">You might want to do this in order to be able to scale your WebJob resources independently of your web application resources.</span><span class="sxs-lookup"><span data-stu-id="404c1-152">You might want to do this in order to be able to scale your WebJob resources independently of your web application resources.</span></span>
* [<span data-ttu-id="404c1-153">Use the WebJobs new-project template for a WebJob linked to a web project</span><span class="sxs-lookup"><span data-stu-id="404c1-153">Use the WebJobs new-project template for a WebJob linked to a web project</span></span>](#createlink)
  
    <span data-ttu-id="404c1-154">Create a project that is configured to deploy automatically as a WebJob when a web project in the same solution is deployed.</span><span class="sxs-lookup"><span data-stu-id="404c1-154">Create a project that is configured to deploy automatically as a WebJob when a web project in the same solution is deployed.</span></span> <span data-ttu-id="404c1-155">Use this option when you want to run your WebJob in the same web app in which you run the related web application.</span><span class="sxs-lookup"><span data-stu-id="404c1-155">Use this option when you want to run your WebJob in the same web app in which you run the related web application.</span></span>

> [!NOTE]
> <span data-ttu-id="404c1-156">The WebJobs new-project template automatically installs NuGet packages and includes code in *Program.cs* for the [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span><span class="sxs-lookup"><span data-stu-id="404c1-156">The WebJobs new-project template automatically installs NuGet packages and includes code in *Program.cs* for the [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span></span> <span data-ttu-id="404c1-157">If you don't want to use the WebJobs SDK, or want to use a scheduled rather than continuous WebJob, remove or change the `host.RunAndBlock` statement in *Program.cs*.</span><span class="sxs-lookup"><span data-stu-id="404c1-157">If you don't want to use the WebJobs SDK, or want to use a scheduled rather than continuous WebJob, remove or change the `host.RunAndBlock` statement in *Program.cs*.</span></span>
> 
> 

### <a id="createnolink"></a> <span data-ttu-id="404c1-158">Use the WebJobs new-project template for an independent WebJob</span><span class="sxs-lookup"><span data-stu-id="404c1-158">Use the WebJobs new-project template for an independent WebJob</span></span>
1. <span data-ttu-id="404c1-159">Click **File** > **New Project**, and then in the **New Project** dialog box click **Cloud** > **Microsoft Azure WebJob**.</span><span class="sxs-lookup"><span data-stu-id="404c1-159">Click **File** > **New Project**, and then in the **New Project** dialog box click **Cloud** > **Microsoft Azure WebJob**.</span></span>
   
    ![New Project dialog showing WebJob template](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-deploy-webjobs/np.png)
2. <span data-ttu-id="404c1-161">Follow the directions shown earlier to [make the Console Application project an independent WebJobs project](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="404c1-161">Follow the directions shown earlier to [make the Console Application project an independent WebJobs project](#convertnolink).</span></span>

### <a id="createlink"></a> <span data-ttu-id="404c1-162">Use the WebJobs new-project template for a WebJob linked to a web project</span><span class="sxs-lookup"><span data-stu-id="404c1-162">Use the WebJobs new-project template for a WebJob linked to a web project</span></span>
1. <span data-ttu-id="404c1-163">Right-click the web project in **Solution Explorer**, and then click **Add** > **New Azure WebJob Project**.</span><span class="sxs-lookup"><span data-stu-id="404c1-163">Right-click the web project in **Solution Explorer**, and then click **Add** > **New Azure WebJob Project**.</span></span>
   
    ![New Azure WebJob Project menu entry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-deploy-webjobs/nawj.png)
   
    <span data-ttu-id="404c1-165">The [Add Azure WebJob](#configure) dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="404c1-165">The [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="404c1-166">Complete the [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="404c1-166">Complete the [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>

## <a id="configure"></a><span data-ttu-id="404c1-167">The Add Azure WebJob dialog</span><span class="sxs-lookup"><span data-stu-id="404c1-167">The Add Azure WebJob dialog</span></span>
<span data-ttu-id="404c1-168">The **Add Azure WebJob** dialog enables you to enter WebJob name and scheduling settings for your WebJob.</span><span class="sxs-lookup"><span data-stu-id="404c1-168">The **Add Azure WebJob** dialog enables you to enter WebJob name and scheduling settings for your WebJob.</span></span> 

![Add Azure WebJob dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-deploy-webjobs/aaw2.png)

<span data-ttu-id="404c1-170">The fields in this dialog correspond to fields on the **New Job** dialog of the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="404c1-170">The fields in this dialog correspond to fields on the **New Job** dialog of the Azure Portal.</span></span> <span data-ttu-id="404c1-171">For more information, see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="404c1-171">For more information, see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

<span data-ttu-id="404c1-172">For a scheduled WebJob (not for continuous WebJobs), Visual Studio creates an [Azure Scheduler](/services/scheduler/) job collection if one doesn't exist yet, and it creates a job in the collection:</span><span class="sxs-lookup"><span data-stu-id="404c1-172">For a scheduled WebJob (not for continuous WebJobs), Visual Studio creates an [Azure Scheduler](/services/scheduler/) job collection if one doesn't exist yet, and it creates a job in the collection:</span></span>

* <span data-ttu-id="404c1-173">The scheduler job collection is named *WebJobs-{regionname}* where *{regionname}* refers to the region the web app is hosted in.</span><span class="sxs-lookup"><span data-stu-id="404c1-173">The scheduler job collection is named *WebJobs-{regionname}* where *{regionname}* refers to the region the web app is hosted in.</span></span> <span data-ttu-id="404c1-174">For example: WebJobs-WestUS.</span><span class="sxs-lookup"><span data-stu-id="404c1-174">For example: WebJobs-WestUS.</span></span>
* <span data-ttu-id="404c1-175">The scheduler job is named *{webappname}-{webjobname}*.</span><span class="sxs-lookup"><span data-stu-id="404c1-175">The scheduler job is named *{webappname}-{webjobname}*.</span></span> <span data-ttu-id="404c1-176">For example: MyWebApp-MyWebJob.</span><span class="sxs-lookup"><span data-stu-id="404c1-176">For example: MyWebApp-MyWebJob.</span></span> 

> [!NOTE]
> * <span data-ttu-id="404c1-177">For information about command-line deployment, see [Enabling Command-line or Continuous Delivery of Azure WebJobs](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span><span class="sxs-lookup"><span data-stu-id="404c1-177">For information about command-line deployment, see [Enabling Command-line or Continuous Delivery of Azure WebJobs](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span></span>
> * <span data-ttu-id="404c1-178">If you configure a **Recurring Job** and set recurrence frequency to a number of minutes, the Azure Scheduler service is not free.</span><span class="sxs-lookup"><span data-stu-id="404c1-178">If you configure a **Recurring Job** and set recurrence frequency to a number of minutes, the Azure Scheduler service is not free.</span></span> <span data-ttu-id="404c1-179">Other frequencies (hours, days, and so forth) are free.</span><span class="sxs-lookup"><span data-stu-id="404c1-179">Other frequencies (hours, days, and so forth) are free.</span></span>
> * <span data-ttu-id="404c1-180">If you deploy a WebJob and then decide you want to change the type of WebJob and redeploy, you'll need to delete the webjobs-publish-settings.json file.</span><span class="sxs-lookup"><span data-stu-id="404c1-180">If you deploy a WebJob and then decide you want to change the type of WebJob and redeploy, you'll need to delete the webjobs-publish-settings.json file.</span></span> <span data-ttu-id="404c1-181">This will make Visual Studio show the publishing options again, so you can change the type of WebJob.</span><span class="sxs-lookup"><span data-stu-id="404c1-181">This will make Visual Studio show the publishing options again, so you can change the type of WebJob.</span></span>
> * <span data-ttu-id="404c1-182">If you deploy a WebJob and later change the run mode from continuous to non-continuous or vice versa, Visual Studio creates a new WebJob in Azure when you redeploy.</span><span class="sxs-lookup"><span data-stu-id="404c1-182">If you deploy a WebJob and later change the run mode from continuous to non-continuous or vice versa, Visual Studio creates a new WebJob in Azure when you redeploy.</span></span> <span data-ttu-id="404c1-183">If you change other scheduling settings but leave run mode the same or switch between Scheduled and On Demand, Visual Studio updates the existing job rather than create a new one.</span><span class="sxs-lookup"><span data-stu-id="404c1-183">If you change other scheduling settings but leave run mode the same or switch between Scheduled and On Demand, Visual Studio updates the existing job rather than create a new one.</span></span>
> 
> 

## <a id="publishsettings"></a><span data-ttu-id="404c1-184">webjob-publish-settings.json</span><span class="sxs-lookup"><span data-stu-id="404c1-184">webjob-publish-settings.json</span></span>
<span data-ttu-id="404c1-185">When you configure a Console Application for WebJobs deployment, Visual Studio installs the [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package and stores scheduling information in a *webjob-publish-settings.json* file in the project *Properties* folder of the WebJobs project.</span><span class="sxs-lookup"><span data-stu-id="404c1-185">When you configure a Console Application for WebJobs deployment, Visual Studio installs the [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package and stores scheduling information in a *webjob-publish-settings.json* file in the project *Properties* folder of the WebJobs project.</span></span> <span data-ttu-id="404c1-186">Here is an example of that file:</span><span class="sxs-lookup"><span data-stu-id="404c1-186">Here is an example of that file:</span></span>

        {
          "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
          "webJobName": "WebJob1",
          "startTime": "2014-06-23T00:00:00-08:00",
          "endTime": "2014-06-27T00:00:00-08:00",
          "jobRecurrenceFrequency": "Minute",
          "interval": 5,
          "runMode": "Scheduled"
        }

<span data-ttu-id="404c1-187">You can edit this file directly, and Visual Studio provides IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="404c1-187">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="404c1-188">The file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) and can be viewed there.</span><span class="sxs-lookup"><span data-stu-id="404c1-188">The file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) and can be viewed there.</span></span>  

> [!NOTE]
> * <span data-ttu-id="404c1-189">If you configure a **Recurring Job** and set recurrence frequency to a number of minutes, the Azure Scheduler service is not free.</span><span class="sxs-lookup"><span data-stu-id="404c1-189">If you configure a **Recurring Job** and set recurrence frequency to a number of minutes, the Azure Scheduler service is not free.</span></span> <span data-ttu-id="404c1-190">Other frequencies (hours, days, and so forth) are free.</span><span class="sxs-lookup"><span data-stu-id="404c1-190">Other frequencies (hours, days, and so forth) are free.</span></span>
> 
> 

## <a id="webjobslist"></a><span data-ttu-id="404c1-191">webjobs-list.json</span><span class="sxs-lookup"><span data-stu-id="404c1-191">webjobs-list.json</span></span>
<span data-ttu-id="404c1-192">When you link a WebJobs-enabled project to a web project, Visual Studio stores the name of the WebJobs project in a *webjobs-list.json* file in the web project's *Properties* folder.</span><span class="sxs-lookup"><span data-stu-id="404c1-192">When you link a WebJobs-enabled project to a web project, Visual Studio stores the name of the WebJobs project in a *webjobs-list.json* file in the web project's *Properties* folder.</span></span> <span data-ttu-id="404c1-193">The list may contain multiple WebJobs projects, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="404c1-193">The list may contain multiple WebJobs projects, as shown in the following example:</span></span>

        {
          "$schema": "http://schemastore.org/schemas/json/webjobs-list.json",
          "WebJobs": [
            {
              "filePath": "../ConsoleApplication1/ConsoleApplication1.csproj"
            },
            {
              "filePath": "../WebJob1/WebJob1.csproj"
            }
          ]
        }

<span data-ttu-id="404c1-194">You can edit this file directly, and Visual Studio provides IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="404c1-194">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="404c1-195">The file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) and can be viewed there.</span><span class="sxs-lookup"><span data-stu-id="404c1-195">The file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) and can be viewed there.</span></span>

## <a id="deploy"></a><span data-ttu-id="404c1-196">Deploy a WebJobs project</span><span class="sxs-lookup"><span data-stu-id="404c1-196">Deploy a WebJobs project</span></span>
<span data-ttu-id="404c1-197">A WebJobs project that you have linked to a web project deploys automatically with the web project.</span><span class="sxs-lookup"><span data-stu-id="404c1-197">A WebJobs project that you have linked to a web project deploys automatically with the web project.</span></span> <span data-ttu-id="404c1-198">For information about web project deployment, see [How to deploy to Web Apps](web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="404c1-198">For information about web project deployment, see [How to deploy to Web Apps](web-sites-deploy.md).</span></span>

<span data-ttu-id="404c1-199">To deploy a WebJobs project by itself, right-click the project in **Solution Explorer**, and click **Publish as Azure WebJob**.</span><span class="sxs-lookup"><span data-stu-id="404c1-199">To deploy a WebJobs project by itself, right-click the project in **Solution Explorer**, and click **Publish as Azure WebJob**.</span></span> 

![Publish as Azure WebJob](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/websites-dotnet-deploy-webjobs/paw.png)

<span data-ttu-id="404c1-201">For an independent WebJob, the same **Publish Web** wizard that is used for web projects appears, but with fewer settings available to change.</span><span class="sxs-lookup"><span data-stu-id="404c1-201">For an independent WebJob, the same **Publish Web** wizard that is used for web projects appears, but with fewer settings available to change.</span></span>

## <a id="nextsteps"></a><span data-ttu-id="404c1-202">Next Steps</span><span class="sxs-lookup"><span data-stu-id="404c1-202">Next Steps</span></span>
<span data-ttu-id="404c1-203">This article has explained how to deploy WebJobs by using Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="404c1-203">This article has explained how to deploy WebJobs by using Visual Studio.</span></span> <span data-ttu-id="404c1-204">For more information about how to deploy Azure WebJobs, see [Azure WebJobs - Recommended Resources - Deployment](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span><span class="sxs-lookup"><span data-stu-id="404c1-204">For more information about how to deploy Azure WebJobs, see [Azure WebJobs - Recommended Resources - Deployment](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span></span>










