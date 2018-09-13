---
title: Develop and deploy WebJobs using Visual Studio - Azure
description: Learn how to develop and deploy Azure WebJobs to Azure App Service using Visual Studio.
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
ms.custom: vs-azure
ms.workload: azure-vs
ms.date: 09/12/2017
ms.author: glenga;david.ebbo;suwatch;pbatum;naren.soni
ms.openlocfilehash: 64fdb6dceb1ca10e68411f95c310fdd9a2e25202
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867462"
---
# <a name="develop-and-deploy-webjobs-using-visual-studio---azure-app-service"></a><span data-ttu-id="33091-103">Develop and deploy WebJobs using Visual Studio - Azure App Service</span><span class="sxs-lookup"><span data-stu-id="33091-103">Develop and deploy WebJobs using Visual Studio - Azure App Service</span></span>

## <a name="overview"></a><span data-ttu-id="33091-104">Overview</span><span class="sxs-lookup"><span data-stu-id="33091-104">Overview</span></span>

<span data-ttu-id="33091-105">This topic explains how to use Visual Studio to deploy a Console Application project to a web app in [App Service](app-service-web-overview.md) as an [Azure WebJob](http://go.microsoft.com/fwlink/?LinkId=390226).</span><span class="sxs-lookup"><span data-stu-id="33091-105">This topic explains how to use Visual Studio to deploy a Console Application project to a web app in [App Service](app-service-web-overview.md) as an [Azure WebJob](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span> <span data-ttu-id="33091-106">For information about how to deploy WebJobs by using the [Azure portal](https://portal.azure.com), see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="33091-106">For information about how to deploy WebJobs by using the [Azure portal](https://portal.azure.com), see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

<span data-ttu-id="33091-107">When Visual Studio deploys a WebJobs-enabled Console Application project, it performs two tasks:</span><span class="sxs-lookup"><span data-stu-id="33091-107">When Visual Studio deploys a WebJobs-enabled Console Application project, it performs two tasks:</span></span>

* <span data-ttu-id="33091-108">Copies runtime files to the appropriate folder in the web app (*App_Data/jobs/continuous* for continuous WebJobs, *App_Data/jobs/triggered* for scheduled and on-demand WebJobs).</span><span class="sxs-lookup"><span data-stu-id="33091-108">Copies runtime files to the appropriate folder in the web app (*App_Data/jobs/continuous* for continuous WebJobs, *App_Data/jobs/triggered* for scheduled and on-demand WebJobs).</span></span>
* <span data-ttu-id="33091-109">Sets up [Azure Scheduler](https://docs.microsoft.com/azure/scheduler/) jobs for WebJobs that are scheduled to run at particular times.</span><span class="sxs-lookup"><span data-stu-id="33091-109">Sets up [Azure Scheduler](https://docs.microsoft.com/azure/scheduler/) jobs for WebJobs that are scheduled to run at particular times.</span></span> <span data-ttu-id="33091-110">(This is not needed for continuous WebJobs.)</span><span class="sxs-lookup"><span data-stu-id="33091-110">(This is not needed for continuous WebJobs.)</span></span>

<span data-ttu-id="33091-111">A WebJobs-enabled project has the following items added to it:</span><span class="sxs-lookup"><span data-stu-id="33091-111">A WebJobs-enabled project has the following items added to it:</span></span>

* <span data-ttu-id="33091-112">The [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package.</span><span class="sxs-lookup"><span data-stu-id="33091-112">The [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package.</span></span>
* <span data-ttu-id="33091-113">A [webjob-publish-settings.json](#publishsettings) file that contains deployment and scheduler settings.</span><span class="sxs-lookup"><span data-stu-id="33091-113">A [webjob-publish-settings.json](#publishsettings) file that contains deployment and scheduler settings.</span></span> 

![Diagram showing what is added to a Console App to enable deployment as a WebJob](./media/websites-dotnet-deploy-webjobs/convert.png)

<span data-ttu-id="33091-115">You can add these items to an existing Console Application project or use a template to create a new WebJobs-enabled Console Application project.</span><span class="sxs-lookup"><span data-stu-id="33091-115">You can add these items to an existing Console Application project or use a template to create a new WebJobs-enabled Console Application project.</span></span> 

<span data-ttu-id="33091-116">You can deploy a project as a WebJob by itself, or link it to a web project so that it automatically deploys whenever you deploy the web project.</span><span class="sxs-lookup"><span data-stu-id="33091-116">You can deploy a project as a WebJob by itself, or link it to a web project so that it automatically deploys whenever you deploy the web project.</span></span> <span data-ttu-id="33091-117">To link projects, Visual Studio includes the name of the WebJobs-enabled project in a [webjobs-list.json](#webjobslist) file in the web project.</span><span class="sxs-lookup"><span data-stu-id="33091-117">To link projects, Visual Studio includes the name of the WebJobs-enabled project in a [webjobs-list.json](#webjobslist) file in the web project.</span></span>

![Diagram showing WebJob project linking to web project](./media/websites-dotnet-deploy-webjobs/link.png)

## <a name="prerequisites"></a><span data-ttu-id="33091-119">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="33091-119">Prerequisites</span></span>

<span data-ttu-id="33091-120">If you're using Visual Studio 2015, install the [Azure SDK for .NET (Visual Studio 2015)](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="33091-120">If you're using Visual Studio 2015, install the [Azure SDK for .NET (Visual Studio 2015)](https://azure.microsoft.com/downloads/).</span></span>

<span data-ttu-id="33091-121">If you're using Visual Studio 2017, install the [Azure development workload](https://docs.microsoft.com/visualstudio/install/install-visual-studio#step-4---select-workloads).</span><span class="sxs-lookup"><span data-stu-id="33091-121">If you're using Visual Studio 2017, install the [Azure development workload](https://docs.microsoft.com/visualstudio/install/install-visual-studio#step-4---select-workloads).</span></span>

## <a id="convert"></a> <span data-ttu-id="33091-122">Enable WebJobs deployment for an existing Console Application project</span><span class="sxs-lookup"><span data-stu-id="33091-122">Enable WebJobs deployment for an existing Console Application project</span></span>

<span data-ttu-id="33091-123">You have two options:</span><span class="sxs-lookup"><span data-stu-id="33091-123">You have two options:</span></span>

* <span data-ttu-id="33091-124">[Enable automatic deployment with a web project](#convertlink).</span><span class="sxs-lookup"><span data-stu-id="33091-124">[Enable automatic deployment with a web project](#convertlink).</span></span>

  <span data-ttu-id="33091-125">Configure an existing Console Application project so that it automatically deploys as a WebJob when you deploy a web project.</span><span class="sxs-lookup"><span data-stu-id="33091-125">Configure an existing Console Application project so that it automatically deploys as a WebJob when you deploy a web project.</span></span> <span data-ttu-id="33091-126">Use this option when you want to run your WebJob in the same web app in which you run the related web application.</span><span class="sxs-lookup"><span data-stu-id="33091-126">Use this option when you want to run your WebJob in the same web app in which you run the related web application.</span></span>

* <span data-ttu-id="33091-127">[Enable deployment without a web project](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="33091-127">[Enable deployment without a web project](#convertnolink).</span></span>

  <span data-ttu-id="33091-128">Configure an existing Console Application project to deploy as a WebJob by itself, with no link to a web project.</span><span class="sxs-lookup"><span data-stu-id="33091-128">Configure an existing Console Application project to deploy as a WebJob by itself, with no link to a web project.</span></span> <span data-ttu-id="33091-129">Use this option when you want to run a WebJob in a web app by itself, with no web application running in the web app.</span><span class="sxs-lookup"><span data-stu-id="33091-129">Use this option when you want to run a WebJob in a web app by itself, with no web application running in the web app.</span></span> <span data-ttu-id="33091-130">You might want to do this in order to be able to scale your WebJob resources independently of your web application resources.</span><span class="sxs-lookup"><span data-stu-id="33091-130">You might want to do this in order to be able to scale your WebJob resources independently of your web application resources.</span></span>

### <a id="convertlink"></a> <span data-ttu-id="33091-131">Enable automatic WebJobs deployment with a web project</span><span class="sxs-lookup"><span data-stu-id="33091-131">Enable automatic WebJobs deployment with a web project</span></span>

1. <span data-ttu-id="33091-132">Right-click the web project in **Solution Explorer**, and then click **Add** > **Existing Project as Azure WebJob**.</span><span class="sxs-lookup"><span data-stu-id="33091-132">Right-click the web project in **Solution Explorer**, and then click **Add** > **Existing Project as Azure WebJob**.</span></span>
   
    ![Existing Project as Azure WebJob](./media/websites-dotnet-deploy-webjobs/eawj.png)
   
    <span data-ttu-id="33091-134">The [Add Azure WebJob](#configure) dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="33091-134">The [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="33091-135">In the **Project name** drop-down list, select the Console Application project to add as a WebJob.</span><span class="sxs-lookup"><span data-stu-id="33091-135">In the **Project name** drop-down list, select the Console Application project to add as a WebJob.</span></span>
   
    ![Selecting project in Add Azure WebJob dialog](./media/websites-dotnet-deploy-webjobs/aaw1.png)
3. <span data-ttu-id="33091-137">Complete the [Add Azure WebJob](#configure) dialog, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="33091-137">Complete the [Add Azure WebJob](#configure) dialog, and then click **OK**.</span></span> 

### <a id="convertnolink"></a> <span data-ttu-id="33091-138">Enable WebJobs deployment without a web project</span><span class="sxs-lookup"><span data-stu-id="33091-138">Enable WebJobs deployment without a web project</span></span>
1. <span data-ttu-id="33091-139">Right-click the Console Application project in **Solution Explorer**, and then click **Publish as Azure WebJob...**.</span><span class="sxs-lookup"><span data-stu-id="33091-139">Right-click the Console Application project in **Solution Explorer**, and then click **Publish as Azure WebJob...**.</span></span> 
   
    ![Publish as Azure WebJob](./media/websites-dotnet-deploy-webjobs/paw.png)
   
    <span data-ttu-id="33091-141">The [Add Azure WebJob](#configure) dialog box appears, with the project selected in the **Project name** box.</span><span class="sxs-lookup"><span data-stu-id="33091-141">The [Add Azure WebJob](#configure) dialog box appears, with the project selected in the **Project name** box.</span></span>
2. <span data-ttu-id="33091-142">Complete the [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="33091-142">Complete the [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>
   
   <span data-ttu-id="33091-143">The **Publish Web** wizard appears.</span><span class="sxs-lookup"><span data-stu-id="33091-143">The **Publish Web** wizard appears.</span></span>  <span data-ttu-id="33091-144">If you do not want to publish immediately, close the wizard.</span><span class="sxs-lookup"><span data-stu-id="33091-144">If you do not want to publish immediately, close the wizard.</span></span> <span data-ttu-id="33091-145">The settings that you've entered are saved for when you do want to [deploy the project](#deploy).</span><span class="sxs-lookup"><span data-stu-id="33091-145">The settings that you've entered are saved for when you do want to [deploy the project](#deploy).</span></span>

## <a id="create"></a><span data-ttu-id="33091-146">Create a new WebJobs-enabled project</span><span class="sxs-lookup"><span data-stu-id="33091-146">Create a new WebJobs-enabled project</span></span>
<span data-ttu-id="33091-147">To create a new WebJobs-enabled project, you can use the Console Application project template and enable WebJobs deployment as explained in [the previous section](#convert).</span><span class="sxs-lookup"><span data-stu-id="33091-147">To create a new WebJobs-enabled project, you can use the Console Application project template and enable WebJobs deployment as explained in [the previous section](#convert).</span></span> <span data-ttu-id="33091-148">As an alternative, you can use the WebJobs new-project template:</span><span class="sxs-lookup"><span data-stu-id="33091-148">As an alternative, you can use the WebJobs new-project template:</span></span>

* [<span data-ttu-id="33091-149">Use the WebJobs new-project template for an independent WebJob</span><span class="sxs-lookup"><span data-stu-id="33091-149">Use the WebJobs new-project template for an independent WebJob</span></span>](#createnolink)
  
    <span data-ttu-id="33091-150">Create a project and configure it to deploy by itself as a WebJob, with no link to a web project.</span><span class="sxs-lookup"><span data-stu-id="33091-150">Create a project and configure it to deploy by itself as a WebJob, with no link to a web project.</span></span> <span data-ttu-id="33091-151">Use this option when you want to run a WebJob in a web app by itself, with no web application running in the web app.</span><span class="sxs-lookup"><span data-stu-id="33091-151">Use this option when you want to run a WebJob in a web app by itself, with no web application running in the web app.</span></span> <span data-ttu-id="33091-152">You might want to do this in order to be able to scale your WebJob resources independently of your web application resources.</span><span class="sxs-lookup"><span data-stu-id="33091-152">You might want to do this in order to be able to scale your WebJob resources independently of your web application resources.</span></span>
* [<span data-ttu-id="33091-153">Use the WebJobs new-project template for a WebJob linked to a web project</span><span class="sxs-lookup"><span data-stu-id="33091-153">Use the WebJobs new-project template for a WebJob linked to a web project</span></span>](#createlink)
  
    <span data-ttu-id="33091-154">Create a project that is configured to deploy automatically as a WebJob when a web project in the same solution is deployed.</span><span class="sxs-lookup"><span data-stu-id="33091-154">Create a project that is configured to deploy automatically as a WebJob when a web project in the same solution is deployed.</span></span> <span data-ttu-id="33091-155">Use this option when you want to run your WebJob in the same web app in which you run the related web application.</span><span class="sxs-lookup"><span data-stu-id="33091-155">Use this option when you want to run your WebJob in the same web app in which you run the related web application.</span></span>

> [!NOTE]
> <span data-ttu-id="33091-156">The WebJobs new-project template automatically installs NuGet packages and includes code in *Program.cs* for the [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span><span class="sxs-lookup"><span data-stu-id="33091-156">The WebJobs new-project template automatically installs NuGet packages and includes code in *Program.cs* for the [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span></span> <span data-ttu-id="33091-157">If you don't want to use the WebJobs SDK, remove or change the `host.RunAndBlock` statement in *Program.cs*.</span><span class="sxs-lookup"><span data-stu-id="33091-157">If you don't want to use the WebJobs SDK, remove or change the `host.RunAndBlock` statement in *Program.cs*.</span></span>
> 
> 

### <a id="createnolink"></a> <span data-ttu-id="33091-158">Use the WebJobs new-project template for an independent WebJob</span><span class="sxs-lookup"><span data-stu-id="33091-158">Use the WebJobs new-project template for an independent WebJob</span></span>
1. <span data-ttu-id="33091-159">Click **File** > **New Project**, and then in the **New Project** dialog box click **Cloud** > **Azure WebJob (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="33091-159">Click **File** > **New Project**, and then in the **New Project** dialog box click **Cloud** > **Azure WebJob (.NET Framework)**.</span></span>
   
    ![New Project dialog showing WebJob template](./media/websites-dotnet-deploy-webjobs/np.png)
2. <span data-ttu-id="33091-161">Follow the directions shown earlier to [make the Console Application project an independent WebJobs project](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="33091-161">Follow the directions shown earlier to [make the Console Application project an independent WebJobs project](#convertnolink).</span></span>

### <a id="createlink"></a> <span data-ttu-id="33091-162">Use the WebJobs new-project template for a WebJob linked to a web project</span><span class="sxs-lookup"><span data-stu-id="33091-162">Use the WebJobs new-project template for a WebJob linked to a web project</span></span>
1. <span data-ttu-id="33091-163">Right-click the web project in **Solution Explorer**, and then click **Add** > **New Azure WebJob Project**.</span><span class="sxs-lookup"><span data-stu-id="33091-163">Right-click the web project in **Solution Explorer**, and then click **Add** > **New Azure WebJob Project**.</span></span>
   
    ![New Azure WebJob Project menu entry](./media/websites-dotnet-deploy-webjobs/nawj.png)
   
    <span data-ttu-id="33091-165">The [Add Azure WebJob](#configure) dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="33091-165">The [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="33091-166">Complete the [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="33091-166">Complete the [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>

## <a id="configure"></a><span data-ttu-id="33091-167">The Add Azure WebJob dialog</span><span class="sxs-lookup"><span data-stu-id="33091-167">The Add Azure WebJob dialog</span></span>
<span data-ttu-id="33091-168">The **Add Azure WebJob** dialog lets you enter the WebJob name and run mode setting for your WebJob.</span><span class="sxs-lookup"><span data-stu-id="33091-168">The **Add Azure WebJob** dialog lets you enter the WebJob name and run mode setting for your WebJob.</span></span> 

![Add Azure WebJob dialog](./media/websites-dotnet-deploy-webjobs/aaw2.png)

<span data-ttu-id="33091-170">The fields in this dialog correspond to fields on the **Add WebJob** dialog of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="33091-170">The fields in this dialog correspond to fields on the **Add WebJob** dialog of the Azure portal.</span></span> <span data-ttu-id="33091-171">For more information, see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="33091-171">For more information, see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

> [!NOTE]
> * <span data-ttu-id="33091-172">For information about command-line deployment, see [Enabling Command-line or Continuous Delivery of Azure WebJobs](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span><span class="sxs-lookup"><span data-stu-id="33091-172">For information about command-line deployment, see [Enabling Command-line or Continuous Delivery of Azure WebJobs](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span></span>
> * <span data-ttu-id="33091-173">If you deploy a WebJob and then decide you want to change the type of WebJob and redeploy, you'll need to delete the *webjobs-publish-settings.json* file.</span><span class="sxs-lookup"><span data-stu-id="33091-173">If you deploy a WebJob and then decide you want to change the type of WebJob and redeploy, you'll need to delete the *webjobs-publish-settings.json* file.</span></span> <span data-ttu-id="33091-174">This will make Visual Studio show the publishing options again, so you can change the type of WebJob.</span><span class="sxs-lookup"><span data-stu-id="33091-174">This will make Visual Studio show the publishing options again, so you can change the type of WebJob.</span></span>
> * <span data-ttu-id="33091-175">If you deploy a WebJob and later change the run mode from continuous to non-continuous or vice versa, Visual Studio creates a new WebJob in Azure when you redeploy.</span><span class="sxs-lookup"><span data-stu-id="33091-175">If you deploy a WebJob and later change the run mode from continuous to non-continuous or vice versa, Visual Studio creates a new WebJob in Azure when you redeploy.</span></span> <span data-ttu-id="33091-176">If you change other scheduling settings but leave run mode the same or switch between Scheduled and On Demand, Visual Studio updates the existing job rather than create a new one.</span><span class="sxs-lookup"><span data-stu-id="33091-176">If you change other scheduling settings but leave run mode the same or switch between Scheduled and On Demand, Visual Studio updates the existing job rather than create a new one.</span></span>
> 
> 

## <a id="publishsettings"></a><span data-ttu-id="33091-177">webjob-publish-settings.json</span><span class="sxs-lookup"><span data-stu-id="33091-177">webjob-publish-settings.json</span></span>
<span data-ttu-id="33091-178">When you configure a Console Application for WebJobs deployment, Visual Studio installs the [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package and stores scheduling information in a *webjob-publish-settings.json* file in the project *Properties* folder of the WebJobs project.</span><span class="sxs-lookup"><span data-stu-id="33091-178">When you configure a Console Application for WebJobs deployment, Visual Studio installs the [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package and stores scheduling information in a *webjob-publish-settings.json* file in the project *Properties* folder of the WebJobs project.</span></span> <span data-ttu-id="33091-179">Here is an example of that file:</span><span class="sxs-lookup"><span data-stu-id="33091-179">Here is an example of that file:</span></span>

        {
          "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
          "webJobName": "WebJob1",
          "startTime": "null",
          "endTime": "null",
          "jobRecurrenceFrequency": "null",
          "interval": null,
          "runMode": "Continuous"
        }

<span data-ttu-id="33091-180">You can edit this file directly, and Visual Studio provides IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="33091-180">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="33091-181">The file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) and can be viewed there.</span><span class="sxs-lookup"><span data-stu-id="33091-181">The file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) and can be viewed there.</span></span>  

## <a id="webjobslist"></a><span data-ttu-id="33091-182">webjobs-list.json</span><span class="sxs-lookup"><span data-stu-id="33091-182">webjobs-list.json</span></span>
<span data-ttu-id="33091-183">When you link a WebJobs-enabled project to a web project, Visual Studio stores the name of the WebJobs project in a *webjobs-list.json* file in the web project's *Properties* folder.</span><span class="sxs-lookup"><span data-stu-id="33091-183">When you link a WebJobs-enabled project to a web project, Visual Studio stores the name of the WebJobs project in a *webjobs-list.json* file in the web project's *Properties* folder.</span></span> <span data-ttu-id="33091-184">The list might contain multiple WebJobs projects, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="33091-184">The list might contain multiple WebJobs projects, as shown in the following example:</span></span>

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

<span data-ttu-id="33091-185">You can edit this file directly, and Visual Studio provides IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="33091-185">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="33091-186">The file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) and can be viewed there.</span><span class="sxs-lookup"><span data-stu-id="33091-186">The file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) and can be viewed there.</span></span>

## <a id="deploy"></a><span data-ttu-id="33091-187">Deploy a WebJobs project</span><span class="sxs-lookup"><span data-stu-id="33091-187">Deploy a WebJobs project</span></span>
<span data-ttu-id="33091-188">A WebJobs project that you have linked to a web project deploys automatically with the web project.</span><span class="sxs-lookup"><span data-stu-id="33091-188">A WebJobs project that you have linked to a web project deploys automatically with the web project.</span></span> <span data-ttu-id="33091-189">For information about web project deployment, see **How-to guides** > **Deploy app** in the left navigation.</span><span class="sxs-lookup"><span data-stu-id="33091-189">For information about web project deployment, see **How-to guides** > **Deploy app** in the left navigation.</span></span>

<span data-ttu-id="33091-190">To deploy a WebJobs project by itself, right-click the project in **Solution Explorer** and click **Publish as Azure WebJob...**.</span><span class="sxs-lookup"><span data-stu-id="33091-190">To deploy a WebJobs project by itself, right-click the project in **Solution Explorer** and click **Publish as Azure WebJob...**.</span></span> 

![Publish as Azure WebJob](./media/websites-dotnet-deploy-webjobs/paw.png)

<span data-ttu-id="33091-192">For an independent WebJob, the same **Publish Web** wizard that is used for web projects appears, but with fewer settings available to change.</span><span class="sxs-lookup"><span data-stu-id="33091-192">For an independent WebJob, the same **Publish Web** wizard that is used for web projects appears, but with fewer settings available to change.</span></span>
