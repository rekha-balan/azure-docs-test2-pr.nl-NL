---
title: Flighting deployment (beta testing) in Azure App Service
description: Learn how to flight new features in your app or beta test your updates in this end-to-end tutorial. It brings together App Service features like continuous publishing, slots, traffic routing, and Application Insights integration.
services: app-service\web
documentationcenter: ''
author: cephalin
manager: erikre
editor: ''
ms.assetid: 17953c51-38f8-442d-bb0b-f69c1542f0e9
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/02/2016
ms.author: cephalin
ms.openlocfilehash: a9dd63737115b829b53a68ec1c23ebf172cbf913
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552297"
---
# <a name="flighting-deployment-beta-testing-in-azure-app-service"></a><span data-ttu-id="abcc3-104">Flighting deployment (beta testing) in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="abcc3-104">Flighting deployment (beta testing) in Azure App Service</span></span>
<span data-ttu-id="abcc3-105">This tutorial shows you how to do *flighting deployments* by integrating the various capabilities of [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) and [Azure Application Insights](/services/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="abcc3-105">This tutorial shows you how to do *flighting deployments* by integrating the various capabilities of [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) and [Azure Application Insights](/services/application-insights/).</span></span>

<span data-ttu-id="abcc3-106">*Flighting* is a deployment process that validates a new feature or change with a limited number of real customers, and is a major testing in production scenario.</span><span class="sxs-lookup"><span data-stu-id="abcc3-106">*Flighting* is a deployment process that validates a new feature or change with a limited number of real customers, and is a major testing in production scenario.</span></span> <span data-ttu-id="abcc3-107">It is akin to beta testing and is sometimes known as "controlled test flight".</span><span class="sxs-lookup"><span data-stu-id="abcc3-107">It is akin to beta testing and is sometimes known as "controlled test flight".</span></span> <span data-ttu-id="abcc3-108">Many large enterprises with a web presence use this approach to get early validation on their app updates in their practice of [agile development](https://en.wikipedia.org/wiki/Agile_software_development).</span><span class="sxs-lookup"><span data-stu-id="abcc3-108">Many large enterprises with a web presence use this approach to get early validation on their app updates in their practice of [agile development](https://en.wikipedia.org/wiki/Agile_software_development).</span></span> <span data-ttu-id="abcc3-109">Azure App Service enables you to integrate test in production with continous publishing and Application Insights to implement the same DevOps scenario.</span><span class="sxs-lookup"><span data-stu-id="abcc3-109">Azure App Service enables you to integrate test in production with continous publishing and Application Insights to implement the same DevOps scenario.</span></span> <span data-ttu-id="abcc3-110">Benefits of this approach include:</span><span class="sxs-lookup"><span data-stu-id="abcc3-110">Benefits of this approach include:</span></span>

* <span data-ttu-id="abcc3-111">**Gain real feedback *before* updates are released to production** - The only thing better than gaining feedback as soon as you release is gaining feedback before you release.</span><span class="sxs-lookup"><span data-stu-id="abcc3-111">**Gain real feedback *before* updates are released to production** - The only thing better than gaining feedback as soon as you release is gaining feedback before you release.</span></span> <span data-ttu-id="abcc3-112">You can test updates with real user traffic and behaviors as early as you desire in the product life cycle.</span><span class="sxs-lookup"><span data-stu-id="abcc3-112">You can test updates with real user traffic and behaviors as early as you desire in the product life cycle.</span></span>
* <span data-ttu-id="abcc3-113">**Enhance [continuous test-driven development (CTDD)](https://en.wikipedia.org/wiki/Continuous_test-driven_development)** - By integrating test in production with continuous integration and instrumentation with Application Insights, user validation happens early and automatically in your product life cycle.</span><span class="sxs-lookup"><span data-stu-id="abcc3-113">**Enhance [continuous test-driven development (CTDD)](https://en.wikipedia.org/wiki/Continuous_test-driven_development)** - By integrating test in production with continuous integration and instrumentation with Application Insights, user validation happens early and automatically in your product life cycle.</span></span> <span data-ttu-id="abcc3-114">This helps reduce time investments in manual test execution.</span><span class="sxs-lookup"><span data-stu-id="abcc3-114">This helps reduce time investments in manual test execution.</span></span>
* <span data-ttu-id="abcc3-115">**Optimize test workflow** - By automating test in production with continuous monitoring instrumentation, you can potentially accomplish the goals of various kinds of tests in a single process, such as [integration](https://en.wikipedia.org/wiki/Integration_testing), [regression](https://en.wikipedia.org/wiki/Regression_testing), [usability](https://en.wikipedia.org/wiki/Usability_testing), accessibility, localization, [performance](https://en.wikipedia.org/wiki/Software_performance_testing), [security](https://en.wikipedia.org/wiki/Security_testing), and [acceptance](https://en.wikipedia.org/wiki/Acceptance_testing).</span><span class="sxs-lookup"><span data-stu-id="abcc3-115">**Optimize test workflow** - By automating test in production with continuous monitoring instrumentation, you can potentially accomplish the goals of various kinds of tests in a single process, such as [integration](https://en.wikipedia.org/wiki/Integration_testing), [regression](https://en.wikipedia.org/wiki/Regression_testing), [usability](https://en.wikipedia.org/wiki/Usability_testing), accessibility, localization, [performance](https://en.wikipedia.org/wiki/Software_performance_testing), [security](https://en.wikipedia.org/wiki/Security_testing), and [acceptance](https://en.wikipedia.org/wiki/Acceptance_testing).</span></span>

<span data-ttu-id="abcc3-116">A flighting deployment is not just about routing live traffic.</span><span class="sxs-lookup"><span data-stu-id="abcc3-116">A flighting deployment is not just about routing live traffic.</span></span> <span data-ttu-id="abcc3-117">In such a deployment you want to gain insight as quickly as possible, whether it be an unexpected bug, performance degradation, user experience issues.</span><span class="sxs-lookup"><span data-stu-id="abcc3-117">In such a deployment you want to gain insight as quickly as possible, whether it be an unexpected bug, performance degradation, user experience issues.</span></span> <span data-ttu-id="abcc3-118">Remember, you are dealing with real customers.</span><span class="sxs-lookup"><span data-stu-id="abcc3-118">Remember, you are dealing with real customers.</span></span> <span data-ttu-id="abcc3-119">So to do it right, you must make sure that you have set up your flighting deployment to gather all the data you need in order to make an informed decision for your next step.</span><span class="sxs-lookup"><span data-stu-id="abcc3-119">So to do it right, you must make sure that you have set up your flighting deployment to gather all the data you need in order to make an informed decision for your next step.</span></span> <span data-ttu-id="abcc3-120">This tutorial shows you how to collect data with Application Insights, but you can use New Relic or other technologies that suits your scenario.</span><span class="sxs-lookup"><span data-stu-id="abcc3-120">This tutorial shows you how to collect data with Application Insights, but you can use New Relic or other technologies that suits your scenario.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="abcc3-121">What you will do</span><span class="sxs-lookup"><span data-stu-id="abcc3-121">What you will do</span></span>
<span data-ttu-id="abcc3-122">In this tutorial, you will learn how to bring the following scenarios together to test your App Service app in production:</span><span class="sxs-lookup"><span data-stu-id="abcc3-122">In this tutorial, you will learn how to bring the following scenarios together to test your App Service app in production:</span></span>

* <span data-ttu-id="abcc3-123">[Route production traffic](app-service-web-test-in-production-get-start.md) to your beta app</span><span class="sxs-lookup"><span data-stu-id="abcc3-123">[Route production traffic](app-service-web-test-in-production-get-start.md) to your beta app</span></span>
* <span data-ttu-id="abcc3-124">[Instrument your app](../application-insights/app-insights-web-track-usage.md) to obtain useful metrics</span><span class="sxs-lookup"><span data-stu-id="abcc3-124">[Instrument your app](../application-insights/app-insights-web-track-usage.md) to obtain useful metrics</span></span>
* <span data-ttu-id="abcc3-125">Continuously deploy your beta app and track live app metrics</span><span class="sxs-lookup"><span data-stu-id="abcc3-125">Continuously deploy your beta app and track live app metrics</span></span>
* <span data-ttu-id="abcc3-126">Compare metrics between the production app and the beta app to see how code changes translate to results</span><span class="sxs-lookup"><span data-stu-id="abcc3-126">Compare metrics between the production app and the beta app to see how code changes translate to results</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="abcc3-127">What you will need</span><span class="sxs-lookup"><span data-stu-id="abcc3-127">What you will need</span></span>
* <span data-ttu-id="abcc3-128">An Azure account</span><span class="sxs-lookup"><span data-stu-id="abcc3-128">An Azure account</span></span>
* <span data-ttu-id="abcc3-129">A [GitHub](https://github.com/) account</span><span class="sxs-lookup"><span data-stu-id="abcc3-129">A [GitHub](https://github.com/) account</span></span>
* <span data-ttu-id="abcc3-130">Visual Studio 2015 - you can download the [Community edition](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="abcc3-130">Visual Studio 2015 - you can download the [Community edition](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx).</span></span>
* <span data-ttu-id="abcc3-131">Git Shell (installed with [GitHub for Windows](https://windows.github.com/)) - this enables you to run both the Git and PowerShell commands in the same session</span><span class="sxs-lookup"><span data-stu-id="abcc3-131">Git Shell (installed with [GitHub for Windows](https://windows.github.com/)) - this enables you to run both the Git and PowerShell commands in the same session</span></span>
* <span data-ttu-id="abcc3-132">Latest [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi) bits</span><span class="sxs-lookup"><span data-stu-id="abcc3-132">Latest [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi) bits</span></span>
* <span data-ttu-id="abcc3-133">Basic understanding of the following:</span><span class="sxs-lookup"><span data-stu-id="abcc3-133">Basic understanding of the following:</span></span>
  * <span data-ttu-id="abcc3-134">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) template deployment (see [Deploy a complex application predictably in Azure](app-service-deploy-complex-application-predictably.md))</span><span class="sxs-lookup"><span data-stu-id="abcc3-134">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) template deployment (see [Deploy a complex application predictably in Azure](app-service-deploy-complex-application-predictably.md))</span></span>
  * [<span data-ttu-id="abcc3-135">Git</span><span class="sxs-lookup"><span data-stu-id="abcc3-135">Git</span></span>](http://git-scm.com/documentation)
  * [<span data-ttu-id="abcc3-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="abcc3-136">PowerShell</span></span>](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> <span data-ttu-id="abcc3-137">You need an Azure account to complete this tutorial:</span><span class="sxs-lookup"><span data-stu-id="abcc3-137">You need an Azure account to complete this tutorial:</span></span>
>
> * <span data-ttu-id="abcc3-138">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services, such as Web Apps.</span><span class="sxs-lookup"><span data-stu-id="abcc3-138">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services, such as Web Apps.</span></span>
> * <span data-ttu-id="abcc3-139">You can [activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your Visual Studio subscription gives you credits every month that you can use for paid Azure services.</span><span class="sxs-lookup"><span data-stu-id="abcc3-139">You can [activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your Visual Studio subscription gives you credits every month that you can use for paid Azure services.</span></span>
>
> <span data-ttu-id="abcc3-140">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="abcc3-140">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="abcc3-141">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="abcc3-141">No credit cards required; no commitments.</span></span>
>
>

## <a name="set-up-your-production-web-app"></a><span data-ttu-id="abcc3-142">Set up your production web app</span><span class="sxs-lookup"><span data-stu-id="abcc3-142">Set up your production web app</span></span>
> [!NOTE]
> <span data-ttu-id="abcc3-143">The script used in this tutorial will automatically configure continuous publishing from your GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="abcc3-143">The script used in this tutorial will automatically configure continuous publishing from your GitHub repository.</span></span> <span data-ttu-id="abcc3-144">This requires that your GitHub credentials are already stored in Azure, otherwise the scripted deployment will fail when attempting to configure source control settings for the web apps.</span><span class="sxs-lookup"><span data-stu-id="abcc3-144">This requires that your GitHub credentials are already stored in Azure, otherwise the scripted deployment will fail when attempting to configure source control settings for the web apps.</span></span>
>
> <span data-ttu-id="abcc3-145">To store your GitHub credentials in Azure, create a web app in the [Azure Portal](https://portal.azure.com/) and [configure GitHub deployment](app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="abcc3-145">To store your GitHub credentials in Azure, create a web app in the [Azure Portal](https://portal.azure.com/) and [configure GitHub deployment](app-service-continuous-deployment.md).</span></span> <span data-ttu-id="abcc3-146">You only need to do this once.</span><span class="sxs-lookup"><span data-stu-id="abcc3-146">You only need to do this once.</span></span>
>
>

<span data-ttu-id="abcc3-147">In a typical DevOps scenario, you have an application that’s running live in Azure, and you want to make changes to it through continuous publishing.</span><span class="sxs-lookup"><span data-stu-id="abcc3-147">In a typical DevOps scenario, you have an application that’s running live in Azure, and you want to make changes to it through continuous publishing.</span></span> <span data-ttu-id="abcc3-148">In this scenario, you will deploy to production a template that you have developed and tested.</span><span class="sxs-lookup"><span data-stu-id="abcc3-148">In this scenario, you will deploy to production a template that you have developed and tested.</span></span>

1. <span data-ttu-id="abcc3-149">Create your own fork of the [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) repository.</span><span class="sxs-lookup"><span data-stu-id="abcc3-149">Create your own fork of the [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) repository.</span></span> <span data-ttu-id="abcc3-150">For information on creating your fork, see [Fork a Repo](https://help.github.com/articles/fork-a-repo/).</span><span class="sxs-lookup"><span data-stu-id="abcc3-150">For information on creating your fork, see [Fork a Repo](https://help.github.com/articles/fork-a-repo/).</span></span> <span data-ttu-id="abcc3-151">Once your fork is created, you can see it in your browser.</span><span class="sxs-lookup"><span data-stu-id="abcc3-151">Once your fork is created, you can see it in your browser.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-agile-software-development/production-1-private-repo.png)
2. <span data-ttu-id="abcc3-152">Open a Git Shell session.</span><span class="sxs-lookup"><span data-stu-id="abcc3-152">Open a Git Shell session.</span></span> <span data-ttu-id="abcc3-153">If you don't have Git Shell yet, install [GitHub for Windows](https://windows.github.com/) now.</span><span class="sxs-lookup"><span data-stu-id="abcc3-153">If you don't have Git Shell yet, install [GitHub for Windows](https://windows.github.com/) now.</span></span>
3. <span data-ttu-id="abcc3-154">Create a local clone of your fork by executing the following command:</span><span class="sxs-lookup"><span data-stu-id="abcc3-154">Create a local clone of your fork by executing the following command:</span></span>

     <span data-ttu-id="abcc3-155">git clone https://github.com/<your_fork>/ToDoApp.git</span><span class="sxs-lookup"><span data-stu-id="abcc3-155">git clone https://github.com/<your_fork>/ToDoApp.git</span></span>
4. <span data-ttu-id="abcc3-156">Once you have your local clone, navigate to *&lt;repository_root>* \ARMTemplates, and run the deploy.ps1 script with a unique suffix, as shown below:</span><span class="sxs-lookup"><span data-stu-id="abcc3-156">Once you have your local clone, navigate to *&lt;repository_root>* \ARMTemplates, and run the deploy.ps1 script with a unique suffix, as shown below:</span></span>

     <span data-ttu-id="abcc3-157">.\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git -ResourceGroupSuffix <your_suffix></span><span class="sxs-lookup"><span data-stu-id="abcc3-157">.\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git -ResourceGroupSuffix <your_suffix></span></span>
5. <span data-ttu-id="abcc3-158">When prompted, type in the desired username and password for database access.</span><span class="sxs-lookup"><span data-stu-id="abcc3-158">When prompted, type in the desired username and password for database access.</span></span> <span data-ttu-id="abcc3-159">Remember your database credentials because you will need to specify them again when updating the resource group.</span><span class="sxs-lookup"><span data-stu-id="abcc3-159">Remember your database credentials because you will need to specify them again when updating the resource group.</span></span>

   <span data-ttu-id="abcc3-160">You should see the provisioning progress of various Azure resources.</span><span class="sxs-lookup"><span data-stu-id="abcc3-160">You should see the provisioning progress of various Azure resources.</span></span> <span data-ttu-id="abcc3-161">When deployment completes, the script will launch the application in the browser and give you a friendly beep.</span><span class="sxs-lookup"><span data-stu-id="abcc3-161">When deployment completes, the script will launch the application in the browser and give you a friendly beep.</span></span>
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-test-in-production-controlled-test-flight/00.1-app-in-browser.png)
6. <span data-ttu-id="abcc3-162">Back in your Git Shell session, run:</span><span class="sxs-lookup"><span data-stu-id="abcc3-162">Back in your Git Shell session, run:</span></span>

     <span data-ttu-id="abcc3-163">.\swap –Name ToDoApp<your_suffix></span><span class="sxs-lookup"><span data-stu-id="abcc3-163">.\swap –Name ToDoApp<your_suffix></span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-test-in-production-controlled-test-flight/00.2-swap-to-production.png)
7. <span data-ttu-id="abcc3-164">When the script finishes, go back to browse to the frontend’s address (http://ToDoApp*&lt;your_suffix>*.azurewebsites.net/) to see the application running in production.</span><span class="sxs-lookup"><span data-stu-id="abcc3-164">When the script finishes, go back to browse to the frontend’s address (http://ToDoApp*&lt;your_suffix>*.azurewebsites.net/) to see the application running in production.</span></span>
8. <span data-ttu-id="abcc3-165">Log into the [Azure Portal](https://portal.azure.com/) and take a look at what’s created.</span><span class="sxs-lookup"><span data-stu-id="abcc3-165">Log into the [Azure Portal](https://portal.azure.com/) and take a look at what’s created.</span></span>

   <span data-ttu-id="abcc3-166">You should be able to see two web apps in the same resource group, one with the `Api` suffix in the name.</span><span class="sxs-lookup"><span data-stu-id="abcc3-166">You should be able to see two web apps in the same resource group, one with the `Api` suffix in the name.</span></span> <span data-ttu-id="abcc3-167">If you look at the resource group view, you will also see the SQL Database and server, the App Service plan, and the staging slots for the web apps.</span><span class="sxs-lookup"><span data-stu-id="abcc3-167">If you look at the resource group view, you will also see the SQL Database and server, the App Service plan, and the staging slots for the web apps.</span></span> <span data-ttu-id="abcc3-168">Browse through the different resources and compare them with *&lt;repository_root>* \ARMTemplates\ProdAndStage.json to see how they are configured in the template.</span><span class="sxs-lookup"><span data-stu-id="abcc3-168">Browse through the different resources and compare them with *&lt;repository_root>* \ARMTemplates\ProdAndStage.json to see how they are configured in the template.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-test-in-production-controlled-test-flight/00.3-resource-group-view.png)

<span data-ttu-id="abcc3-169">You have set up the production app.</span><span class="sxs-lookup"><span data-stu-id="abcc3-169">You have set up the production app.</span></span>  <span data-ttu-id="abcc3-170">Now, let's imagine that you receive feedback that usability is poor for the app.</span><span class="sxs-lookup"><span data-stu-id="abcc3-170">Now, let's imagine that you receive feedback that usability is poor for the app.</span></span> <span data-ttu-id="abcc3-171">So you decide to investigate.</span><span class="sxs-lookup"><span data-stu-id="abcc3-171">So you decide to investigate.</span></span> <span data-ttu-id="abcc3-172">You're going to instrument your app to give you feedback.</span><span class="sxs-lookup"><span data-stu-id="abcc3-172">You're going to instrument your app to give you feedback.</span></span>

## <a name="investigate-instrument-your-client-app-for-monitoringmetrics"></a><span data-ttu-id="abcc3-173">Investigate: Instrument your client app for monitoring/metrics</span><span class="sxs-lookup"><span data-stu-id="abcc3-173">Investigate: Instrument your client app for monitoring/metrics</span></span>
1. <span data-ttu-id="abcc3-174">Open *&lt;repository_root>* \src\MultiChannelToDo.sln in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="abcc3-174">Open *&lt;repository_root>* \src\MultiChannelToDo.sln in Visual Studio.</span></span>
2. <span data-ttu-id="abcc3-175">Restore all Nuget packages by right-clicking solution > **Manage NuGet Packages for Solution** > **Restore**.</span><span class="sxs-lookup"><span data-stu-id="abcc3-175">Restore all Nuget packages by right-clicking solution > **Manage NuGet Packages for Solution** > **Restore**.</span></span>
3. <span data-ttu-id="abcc3-176">Right-click **MultiChannelToDo.Web** > **Add Application Insights Telemetry** > **Configure Settings** > Change resource group to ToDoApp*&lt;your_suffix>* > **Add Application Insights to Project**.</span><span class="sxs-lookup"><span data-stu-id="abcc3-176">Right-click **MultiChannelToDo.Web** > **Add Application Insights Telemetry** > **Configure Settings** > Change resource group to ToDoApp*&lt;your_suffix>* > **Add Application Insights to Project**.</span></span>
4. <span data-ttu-id="abcc3-177">In the Azure Portal, open the blade for the **MultiChannelToDo.Web** Application Insight resource.</span><span class="sxs-lookup"><span data-stu-id="abcc3-177">In the Azure Portal, open the blade for the **MultiChannelToDo.Web** Application Insight resource.</span></span> <span data-ttu-id="abcc3-178">Then in the **Application health** part, click **Learn how to collect browser page load data** > copy code.</span><span class="sxs-lookup"><span data-stu-id="abcc3-178">Then in the **Application health** part, click **Learn how to collect browser page load data** > copy code.</span></span>
5. <span data-ttu-id="abcc3-179">Add the copied JS instrumentation code to *&lt;repository_root>* \src\MultiChannelToDo.Web\app\Index.cshtml, just before the closing `<heading>` tag.</span><span class="sxs-lookup"><span data-stu-id="abcc3-179">Add the copied JS instrumentation code to *&lt;repository_root>* \src\MultiChannelToDo.Web\app\Index.cshtml, just before the closing `<heading>` tag.</span></span> <span data-ttu-id="abcc3-180">It should contain the unique instrumentation key of your Application Insight resource.</span><span class="sxs-lookup"><span data-stu-id="abcc3-180">It should contain the unique instrumentation key of your Application Insight resource.</span></span>

        <script type="text/javascript">
        var appInsights=window.appInsights||function(config){
            function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
        }({
            instrumentationKey:"<your_unique_instrumentation_key>"
        });

        window.appInsights=appInsights;
        appInsights.trackPageView();
        </script>
6. <span data-ttu-id="abcc3-181">Send custom events to Application Insights for mouse clicks by adding the following code to the bottom of body:</span><span class="sxs-lookup"><span data-stu-id="abcc3-181">Send custom events to Application Insights for mouse clicks by adding the following code to the bottom of body:</span></span>

       <script>
           $(document.body).find("*").click(function(event) {

               appInsights.trackEvent(event.target.tagName + ": " + event.target.className);
           });
       </script>

   <span data-ttu-id="abcc3-182">This JavaScript snippet sends a custom event to Application Insights every time a user clicks anywhere in the web app.</span><span class="sxs-lookup"><span data-stu-id="abcc3-182">This JavaScript snippet sends a custom event to Application Insights every time a user clicks anywhere in the web app.</span></span>
7. <span data-ttu-id="abcc3-183">In Git Shell, commit and push your changes to your fork in GitHub.</span><span class="sxs-lookup"><span data-stu-id="abcc3-183">In Git Shell, commit and push your changes to your fork in GitHub.</span></span> <span data-ttu-id="abcc3-184">Then, wait for clients to refresh browser.</span><span class="sxs-lookup"><span data-stu-id="abcc3-184">Then, wait for clients to refresh browser.</span></span>

       git add -A :/
       git commit -m "add AI configuration for client app"
       git push origin master
8. <span data-ttu-id="abcc3-185">Swap the deployed app changes to production:</span><span class="sxs-lookup"><span data-stu-id="abcc3-185">Swap the deployed app changes to production:</span></span>

     <span data-ttu-id="abcc3-186">.\swap –Name ToDoApp<your_suffix></span><span class="sxs-lookup"><span data-stu-id="abcc3-186">.\swap –Name ToDoApp<your_suffix></span></span>
9. <span data-ttu-id="abcc3-187">Browse to the Application Insights resource that you configured.</span><span class="sxs-lookup"><span data-stu-id="abcc3-187">Browse to the Application Insights resource that you configured.</span></span> <span data-ttu-id="abcc3-188">Click Custom events.</span><span class="sxs-lookup"><span data-stu-id="abcc3-188">Click Custom events.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-test-in-production-controlled-test-flight/01-custom-events.png)

   <span data-ttu-id="abcc3-189">If you don't see metrics for custom events, wait a few minutes and click **Refresh**.</span><span class="sxs-lookup"><span data-stu-id="abcc3-189">If you don't see metrics for custom events, wait a few minutes and click **Refresh**.</span></span>

<span data-ttu-id="abcc3-190">Suppose you see a chart like below:</span><span class="sxs-lookup"><span data-stu-id="abcc3-190">Suppose you see a chart like below:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-test-in-production-controlled-test-flight/02-custom-events-chart-view.png)

<span data-ttu-id="abcc3-191">And the event grid below it:</span><span class="sxs-lookup"><span data-stu-id="abcc3-191">And the event grid below it:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-test-in-production-controlled-test-flight/03-custom-event-grid-view.png)

<span data-ttu-id="abcc3-192">According to your ToDoApp application code, the **BUTTON** event corresponds to the submit button, and the **INPUT** event corresponds to the textbox.</span><span class="sxs-lookup"><span data-stu-id="abcc3-192">According to your ToDoApp application code, the **BUTTON** event corresponds to the submit button, and the **INPUT** event corresponds to the textbox.</span></span> <span data-ttu-id="abcc3-193">So far, things make sense.</span><span class="sxs-lookup"><span data-stu-id="abcc3-193">So far, things make sense.</span></span> <span data-ttu-id="abcc3-194">However, it looks like there's a good amount of clicks and very few clicks on the to-do items (the **LI** events).</span><span class="sxs-lookup"><span data-stu-id="abcc3-194">However, it looks like there's a good amount of clicks and very few clicks on the to-do items (the **LI** events).</span></span>

<span data-ttu-id="abcc3-195">Based on this, you form your hypothesis that some users are confused which part of the UI is clickable and it is because the cursor is styled for text selection when it hovers on the list items and their icons.</span><span class="sxs-lookup"><span data-stu-id="abcc3-195">Based on this, you form your hypothesis that some users are confused which part of the UI is clickable and it is because the cursor is styled for text selection when it hovers on the list items and their icons.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-test-in-production-controlled-test-flight/04-to-do-list-item-ui.png)

<span data-ttu-id="abcc3-196">This might be a contrived example.</span><span class="sxs-lookup"><span data-stu-id="abcc3-196">This might be a contrived example.</span></span> <span data-ttu-id="abcc3-197">Nevertheless, you're going to make an improvement to your app, and then perform a flighting deployment to get usability feedback from live customers.</span><span class="sxs-lookup"><span data-stu-id="abcc3-197">Nevertheless, you're going to make an improvement to your app, and then perform a flighting deployment to get usability feedback from live customers.</span></span>

### <a name="instrument-your-server-app-for-monitoringmetrics"></a><span data-ttu-id="abcc3-198">Instrument your server app for monitoring/metrics</span><span class="sxs-lookup"><span data-stu-id="abcc3-198">Instrument your server app for monitoring/metrics</span></span>
<span data-ttu-id="abcc3-199">This is a tangent since the scenario demonstrated in this tutorial only deals with the client app.</span><span class="sxs-lookup"><span data-stu-id="abcc3-199">This is a tangent since the scenario demonstrated in this tutorial only deals with the client app.</span></span> <span data-ttu-id="abcc3-200">However, for completeness you will set up the server-side app.</span><span class="sxs-lookup"><span data-stu-id="abcc3-200">However, for completeness you will set up the server-side app.</span></span>

1. <span data-ttu-id="abcc3-201">Right-click **MultiChannelToDo** > **Add Application Insights Telemetry** > **Configure Settings** > Change resource group to ToDoApp*&lt;your_suffix>* > **Add Application Insights to Project**.</span><span class="sxs-lookup"><span data-stu-id="abcc3-201">Right-click **MultiChannelToDo** > **Add Application Insights Telemetry** > **Configure Settings** > Change resource group to ToDoApp*&lt;your_suffix>* > **Add Application Insights to Project**.</span></span>
2. <span data-ttu-id="abcc3-202">In Git Shell, commit and push your changes to your fork in GitHub.</span><span class="sxs-lookup"><span data-stu-id="abcc3-202">In Git Shell, commit and push your changes to your fork in GitHub.</span></span> <span data-ttu-id="abcc3-203">Then, wait for clients to refresh browser.</span><span class="sxs-lookup"><span data-stu-id="abcc3-203">Then, wait for clients to refresh browser.</span></span>

       git add -A :/
       git commit -m "add AI configuration for server app"
       git push origin master
3. <span data-ttu-id="abcc3-204">Swap the deployed app changes to production:</span><span class="sxs-lookup"><span data-stu-id="abcc3-204">Swap the deployed app changes to production:</span></span>

     <span data-ttu-id="abcc3-205">.\swap –Name ToDoApp<your_suffix></span><span class="sxs-lookup"><span data-stu-id="abcc3-205">.\swap –Name ToDoApp<your_suffix></span></span>

<span data-ttu-id="abcc3-206">That's it!</span><span class="sxs-lookup"><span data-stu-id="abcc3-206">That's it!</span></span>

## <a name="investigate-add-slot-specific-tags-to-your-client-app-metrics"></a><span data-ttu-id="abcc3-207">Investigate: Add slot-specific tags to your client app metrics</span><span class="sxs-lookup"><span data-stu-id="abcc3-207">Investigate: Add slot-specific tags to your client app metrics</span></span>
<span data-ttu-id="abcc3-208">In this section, you will configure the different deployment slots to send slot-specific telemetry to the same Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="abcc3-208">In this section, you will configure the different deployment slots to send slot-specific telemetry to the same Application Insights resource.</span></span> <span data-ttu-id="abcc3-209">This way, you can compare telemetry data between traffic from different slots (deployment environments) to easily see the effect of your app changes.</span><span class="sxs-lookup"><span data-stu-id="abcc3-209">This way, you can compare telemetry data between traffic from different slots (deployment environments) to easily see the effect of your app changes.</span></span> <span data-ttu-id="abcc3-210">At the same time, you can separate the production traffic from the rest so you can continue to monitor your production app as needed.</span><span class="sxs-lookup"><span data-stu-id="abcc3-210">At the same time, you can separate the production traffic from the rest so you can continue to monitor your production app as needed.</span></span>

<span data-ttu-id="abcc3-211">Since you're gathering data on client behavior, you will [add a telemetry initializer to your JavaScript code](../application-insights/app-insights-api-filtering-sampling.md) in index.cshtml.</span><span class="sxs-lookup"><span data-stu-id="abcc3-211">Since you're gathering data on client behavior, you will [add a telemetry initializer to your JavaScript code](../application-insights/app-insights-api-filtering-sampling.md) in index.cshtml.</span></span> <span data-ttu-id="abcc3-212">If you want to test server-side performance, for example, you can also do similarly in your server code (see [Application Insights API for custom events and metrics](../application-insights/app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="abcc3-212">If you want to test server-side performance, for example, you can also do similarly in your server code (see [Application Insights API for custom events and metrics](../application-insights/app-insights-api-custom-events-metrics.md).</span></span>

1. <span data-ttu-id="abcc3-213">First, add the code bewteen the two `//` comments below in the JavaScript block that you added to the `<heading>` tag earlier.</span><span class="sxs-lookup"><span data-stu-id="abcc3-213">First, add the code bewteen the two `//` comments below in the JavaScript block that you added to the `<heading>` tag earlier.</span></span>

        window.appInsights = appInsights;

        // Begin new code
        appInsights.queue.push(function () {
            appInsights.context.addTelemetryInitializer(function (envelope) {
                var telemetryItem = envelope.data.baseData;
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["Environment"] = "@System.Configuration.ConfigurationManager.AppSettings["environment"]";
            });
        });
        // End new code

        appInsights.trackPageView();

    <span data-ttu-id="abcc3-214">This initializer code causes the `appInsights` object to add the a custom property called `Environment` to every piece of telemetry it sends.</span><span class="sxs-lookup"><span data-stu-id="abcc3-214">This initializer code causes the `appInsights` object to add the a custom property called `Environment` to every piece of telemetry it sends.</span></span>
2. <span data-ttu-id="abcc3-215">Next, add this custom property as a [slot setting](web-sites-staged-publishing.md#AboutConfiguration) for your web app in Azure.</span><span class="sxs-lookup"><span data-stu-id="abcc3-215">Next, add this custom property as a [slot setting](web-sites-staged-publishing.md#AboutConfiguration) for your web app in Azure.</span></span> <span data-ttu-id="abcc3-216">To do this, run the following commands in your Git Shell session.</span><span class="sxs-lookup"><span data-stu-id="abcc3-216">To do this, run the following commands in your Git Shell session.</span></span>

        $app = Get-AzureWebsite -Name todoapp<your_suffix> -Slot production
        $app.AppSettings.Add("environment", "Production")
        $app.SlotStickyAppSettingNames.Add("environment")
        $app | Set-AzureWebsite -Name todoapp<your_suffix> -Slot production

    <span data-ttu-id="abcc3-217">The Web.config in your project already defines the `environment` app setting.</span><span class="sxs-lookup"><span data-stu-id="abcc3-217">The Web.config in your project already defines the `environment` app setting.</span></span> <span data-ttu-id="abcc3-218">With this setting, when you test the app locally, your metrics will be tagged with `VS Debugger`.</span><span class="sxs-lookup"><span data-stu-id="abcc3-218">With this setting, when you test the app locally, your metrics will be tagged with `VS Debugger`.</span></span> <span data-ttu-id="abcc3-219">However, when you push your changes to Azure, Azure will find and use the `environment` app setting in the web app's configuration instead, and your metrics will be tagged with `Production`.</span><span class="sxs-lookup"><span data-stu-id="abcc3-219">However, when you push your changes to Azure, Azure will find and use the `environment` app setting in the web app's configuration instead, and your metrics will be tagged with `Production`.</span></span>
3. <span data-ttu-id="abcc3-220">Commit and push your code changes to your fork on GitHub, and then wait for your users to use the new app (need to refresh the browser).</span><span class="sxs-lookup"><span data-stu-id="abcc3-220">Commit and push your code changes to your fork on GitHub, and then wait for your users to use the new app (need to refresh the browser).</span></span> <span data-ttu-id="abcc3-221">It takes about 15 minutes for the new property to show up in your Application Insights `MultiChannelToDo.Web` resource.</span><span class="sxs-lookup"><span data-stu-id="abcc3-221">It takes about 15 minutes for the new property to show up in your Application Insights `MultiChannelToDo.Web` resource.</span></span>

        git add -A :/
        git commit -m "add environment property to AI events for client app"
        git push origin master
4. <span data-ttu-id="abcc3-222">Now, go to the **Custom events** blade again and filter the metrics on `Environment=Production`.</span><span class="sxs-lookup"><span data-stu-id="abcc3-222">Now, go to the **Custom events** blade again and filter the metrics on `Environment=Production`.</span></span> <span data-ttu-id="abcc3-223">You should now be able to see all the new custom events in the production slot with this filter.</span><span class="sxs-lookup"><span data-stu-id="abcc3-223">You should now be able to see all the new custom events in the production slot with this filter.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-test-in-production-controlled-test-flight/05-filter-on-production-environment.png)
5. <span data-ttu-id="abcc3-224">Click the **Favorites** button to save the current Metrics Explorer settings to something like **Custom events: Production**.</span><span class="sxs-lookup"><span data-stu-id="abcc3-224">Click the **Favorites** button to save the current Metrics Explorer settings to something like **Custom events: Production**.</span></span> <span data-ttu-id="abcc3-225">You can easily switch between this view and a deployment slot view later.</span><span class="sxs-lookup"><span data-stu-id="abcc3-225">You can easily switch between this view and a deployment slot view later.</span></span>

   > [!TIP]
   > <span data-ttu-id="abcc3-226">For even more powerful analytics, consider [integrating your Application Insights resource with Power BI](../application-insights/app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="abcc3-226">For even more powerful analytics, consider [integrating your Application Insights resource with Power BI](../application-insights/app-insights-export-power-bi.md).</span></span>
   >
   >

### <a name="add-slot-specific-tags-to-your-server-app-metrics"></a><span data-ttu-id="abcc3-227">Add slot-specific tags to your server app metrics</span><span class="sxs-lookup"><span data-stu-id="abcc3-227">Add slot-specific tags to your server app metrics</span></span>
<span data-ttu-id="abcc3-228">Again, for completeness you will set up the server-side app.</span><span class="sxs-lookup"><span data-stu-id="abcc3-228">Again, for completeness you will set up the server-side app.</span></span> <span data-ttu-id="abcc3-229">Unlike the client app which is instrumented in JavaScript, slot-specific tags for the server app is instrumented with .NET code.</span><span class="sxs-lookup"><span data-stu-id="abcc3-229">Unlike the client app which is instrumented in JavaScript, slot-specific tags for the server app is instrumented with .NET code.</span></span>

1. <span data-ttu-id="abcc3-230">Open *&lt;repository_root>* \src\MultiChannelToDo\Global.asax.cs.</span><span class="sxs-lookup"><span data-stu-id="abcc3-230">Open *&lt;repository_root>* \src\MultiChannelToDo\Global.asax.cs.</span></span> <span data-ttu-id="abcc3-231">Add the code block below, just before the closing namespace curly brace.</span><span class="sxs-lookup"><span data-stu-id="abcc3-231">Add the code block below, just before the closing namespace curly brace.</span></span>

        namespace MultiChannelToDo
        {
                ...

                // Begin new code
            public class ConfigInitializer
            : ITelemetryInitializer
            {
                void ITelemetryInitializer.Initialize(ITelemetry telemetry)
                {
                    telemetry.Context.Properties["Environment"] = System.Configuration.ConfigurationManager.AppSettings["environment"];
                }
            }
                // End new code
        }
2. <span data-ttu-id="abcc3-232">Correct the name resolution errors by adding the `using` statements below to the beginning of the file:</span><span class="sxs-lookup"><span data-stu-id="abcc3-232">Correct the name resolution errors by adding the `using` statements below to the beginning of the file:</span></span>

        using Microsoft.ApplicationInsights.Channel;
        using Microsoft.ApplicationInsights.Extensibility;
3. <span data-ttu-id="abcc3-233">Add the code below to the beginning of the `Application_Start()` method:</span><span class="sxs-lookup"><span data-stu-id="abcc3-233">Add the code below to the beginning of the `Application_Start()` method:</span></span>

        TelemetryConfiguration.Active.TelemetryInitializers.Add(new ConfigInitializer());
4. <span data-ttu-id="abcc3-234">Commit and push your code changes to your fork on GitHub, and then wait for your users to use the new app (need to refresh the browser).</span><span class="sxs-lookup"><span data-stu-id="abcc3-234">Commit and push your code changes to your fork on GitHub, and then wait for your users to use the new app (need to refresh the browser).</span></span> <span data-ttu-id="abcc3-235">It takes about 15 minutes for the new property to show up in your Application Insights `MultiChannelToDo` resource.</span><span class="sxs-lookup"><span data-stu-id="abcc3-235">It takes about 15 minutes for the new property to show up in your Application Insights `MultiChannelToDo` resource.</span></span>

        git add -A :/
        git commit -m "add environment property to AI events for server app"
        git push origin master

## <a name="update-set-up-your-beta-branch"></a><span data-ttu-id="abcc3-236">Update: Set up your beta branch</span><span class="sxs-lookup"><span data-stu-id="abcc3-236">Update: Set up your beta branch</span></span>
1. <span data-ttu-id="abcc3-237">Open *&lt;repository_root>* \ARMTemplates\ProdAndStagetest.json and find the `appsettings` resources (search for `"name": "appsettings"`).</span><span class="sxs-lookup"><span data-stu-id="abcc3-237">Open *&lt;repository_root>* \ARMTemplates\ProdAndStagetest.json and find the `appsettings` resources (search for `"name": "appsettings"`).</span></span> <span data-ttu-id="abcc3-238">There are 4 of them, one for each slot.</span><span class="sxs-lookup"><span data-stu-id="abcc3-238">There are 4 of them, one for each slot.</span></span>
2. <span data-ttu-id="abcc3-239">For each `appsettings` resource, add an  `"environment": "[parameters('slotName')]"` app setting to the end of the `properties` array.</span><span class="sxs-lookup"><span data-stu-id="abcc3-239">For each `appsettings` resource, add an  `"environment": "[parameters('slotName')]"` app setting to the end of the `properties` array.</span></span> <span data-ttu-id="abcc3-240">Don't forget to end the previous line with a comma.</span><span class="sxs-lookup"><span data-stu-id="abcc3-240">Don't forget to end the previous line with a comma.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-test-in-production-controlled-test-flight/06-arm-app-setting-with-slot-name.png)

    <span data-ttu-id="abcc3-241">You have just added the `environment` app setting to all the slots in the template.</span><span class="sxs-lookup"><span data-stu-id="abcc3-241">You have just added the `environment` app setting to all the slots in the template.</span></span>
3. <span data-ttu-id="abcc3-242">In the same file, find the `slotconfignames` resources (search for `"name": "slotconfignames"`).</span><span class="sxs-lookup"><span data-stu-id="abcc3-242">In the same file, find the `slotconfignames` resources (search for `"name": "slotconfignames"`).</span></span> <span data-ttu-id="abcc3-243">There are 2 of them, one for each app.</span><span class="sxs-lookup"><span data-stu-id="abcc3-243">There are 2 of them, one for each app.</span></span>
4. <span data-ttu-id="abcc3-244">For each `slotconfignames` resource, add `"environment"` to the end of the `appSettingNames` array.</span><span class="sxs-lookup"><span data-stu-id="abcc3-244">For each `slotconfignames` resource, add `"environment"` to the end of the `appSettingNames` array.</span></span> <span data-ttu-id="abcc3-245">Don't forget to end the previous line with a comma.</span><span class="sxs-lookup"><span data-stu-id="abcc3-245">Don't forget to end the previous line with a comma.</span></span>

    <span data-ttu-id="abcc3-246">You have just made the `environment` app setting stick to its respective deployment slot for both apps.</span><span class="sxs-lookup"><span data-stu-id="abcc3-246">You have just made the `environment` app setting stick to its respective deployment slot for both apps.</span></span>  
5. <span data-ttu-id="abcc3-247">In your Git Shell session, run the following commands with the same resource group suffix that you used before.</span><span class="sxs-lookup"><span data-stu-id="abcc3-247">In your Git Shell session, run the following commands with the same resource group suffix that you used before.</span></span>

        git checkout -b beta
        git push origin beta
        .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch beta
6. <span data-ttu-id="abcc3-248">When prompted, specify the same SQL database credentials as before.</span><span class="sxs-lookup"><span data-stu-id="abcc3-248">When prompted, specify the same SQL database credentials as before.</span></span> <span data-ttu-id="abcc3-249">Then, when asked to update the resource group, type `Y`, then `ENTER`.</span><span class="sxs-lookup"><span data-stu-id="abcc3-249">Then, when asked to update the resource group, type `Y`, then `ENTER`.</span></span>

    <span data-ttu-id="abcc3-250">Once the script finishes, all your resources in the original resource group are retained, but a new slot named "beta" is created in it with the same configuration as the "Staging" slot that was created in the beginning.</span><span class="sxs-lookup"><span data-stu-id="abcc3-250">Once the script finishes, all your resources in the original resource group are retained, but a new slot named "beta" is created in it with the same configuration as the "Staging" slot that was created in the beginning.</span></span>

   > [!NOTE]
   > <span data-ttu-id="abcc3-251">This method of creating different deployment environments is different from the method in [Agile software development with Azure App Service](app-service-agile-software-development.md).</span><span class="sxs-lookup"><span data-stu-id="abcc3-251">This method of creating different deployment environments is different from the method in [Agile software development with Azure App Service](app-service-agile-software-development.md).</span></span> <span data-ttu-id="abcc3-252">Here, you create deployment environments with deployment slots, where as there you create deployment environments with resource groups.</span><span class="sxs-lookup"><span data-stu-id="abcc3-252">Here, you create deployment environments with deployment slots, where as there you create deployment environments with resource groups.</span></span> <span data-ttu-id="abcc3-253">Managing deployment environments with resource groups enables you to keep the production environment off-limits to developers, but it's not easy to do testing in production, which you can do easily with slots.</span><span class="sxs-lookup"><span data-stu-id="abcc3-253">Managing deployment environments with resource groups enables you to keep the production environment off-limits to developers, but it's not easy to do testing in production, which you can do easily with slots.</span></span>
   >
   >

<span data-ttu-id="abcc3-254">If you wish, you can also create an alpha app by running</span><span class="sxs-lookup"><span data-stu-id="abcc3-254">If you wish, you can also create an alpha app by running</span></span>

    git checkout -b alpha
    git push origin alpha
    .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch alpha

<span data-ttu-id="abcc3-255">For this tutorial, you will just keep using your beta app.</span><span class="sxs-lookup"><span data-stu-id="abcc3-255">For this tutorial, you will just keep using your beta app.</span></span>

## <a name="update-push-your-updates-to-the-beta-app"></a><span data-ttu-id="abcc3-256">Update: Push your updates to the beta app</span><span class="sxs-lookup"><span data-stu-id="abcc3-256">Update: Push your updates to the beta app</span></span>
<span data-ttu-id="abcc3-257">Back to your app that you want to improve.</span><span class="sxs-lookup"><span data-stu-id="abcc3-257">Back to your app that you want to improve.</span></span>

1. <span data-ttu-id="abcc3-258">Make sure you're now in your beta branch</span><span class="sxs-lookup"><span data-stu-id="abcc3-258">Make sure you're now in your beta branch</span></span>

        git checkout beta
2. <span data-ttu-id="abcc3-259">In *&lt;repository_root>* \src\MultiChannelToDo.Web\app\Index.cshtml, find the `<li>` tag and add the `style="cursor:pointer"` attribute, as shown below.</span><span class="sxs-lookup"><span data-stu-id="abcc3-259">In *&lt;repository_root>* \src\MultiChannelToDo.Web\app\Index.cshtml, find the `<li>` tag and add the `style="cursor:pointer"` attribute, as shown below.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-test-in-production-controlled-test-flight/07-change-cursor-style-on-li.png)
3. <span data-ttu-id="abcc3-260">commit and push to Azure.</span><span class="sxs-lookup"><span data-stu-id="abcc3-260">commit and push to Azure.</span></span>
4. <span data-ttu-id="abcc3-261">Verify that the change is now reflected in the beta slot by navigating to http://todoapp*&lt;your_suffix>*-beta.azurewebsites.net/.</span><span class="sxs-lookup"><span data-stu-id="abcc3-261">Verify that the change is now reflected in the beta slot by navigating to http://todoapp*&lt;your_suffix>*-beta.azurewebsites.net/.</span></span> <span data-ttu-id="abcc3-262">If you don't see the change yet, refresh your browser to get the new javascript code.</span><span class="sxs-lookup"><span data-stu-id="abcc3-262">If you don't see the change yet, refresh your browser to get the new javascript code.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-test-in-production-controlled-test-flight/08-verify-change-in-beta-site.png)

<span data-ttu-id="abcc3-263">Now that you have your change running in the beta slot, you are ready to perform a flighting deployment.</span><span class="sxs-lookup"><span data-stu-id="abcc3-263">Now that you have your change running in the beta slot, you are ready to perform a flighting deployment.</span></span>

## <a name="validate-route-traffic-to-the-beta-app"></a><span data-ttu-id="abcc3-264">Validate: Route traffic to the beta app</span><span class="sxs-lookup"><span data-stu-id="abcc3-264">Validate: Route traffic to the beta app</span></span>
<span data-ttu-id="abcc3-265">In this section, you will route traffic to the beta app.</span><span class="sxs-lookup"><span data-stu-id="abcc3-265">In this section, you will route traffic to the beta app.</span></span> <span data-ttu-id="abcc3-266">For sake of clarity of demonstration, you're going to route a significant portion of the user traffic to it.</span><span class="sxs-lookup"><span data-stu-id="abcc3-266">For sake of clarity of demonstration, you're going to route a significant portion of the user traffic to it.</span></span> <span data-ttu-id="abcc3-267">In reality, the amount of traffic you want to route will depend on your specific situation.</span><span class="sxs-lookup"><span data-stu-id="abcc3-267">In reality, the amount of traffic you want to route will depend on your specific situation.</span></span> <span data-ttu-id="abcc3-268">For example, if your site is at the scale of microsoft.com, then you may need less than one percent of your total traffic in order to gain useful data.</span><span class="sxs-lookup"><span data-stu-id="abcc3-268">For example, if your site is at the scale of microsoft.com, then you may need less than one percent of your total traffic in order to gain useful data.</span></span>

1. <span data-ttu-id="abcc3-269">In your Git Shell session, run the following commands to route half of the production traffic to the beta slot:</span><span class="sxs-lookup"><span data-stu-id="abcc3-269">In your Git Shell session, run the following commands to route half of the production traffic to the beta slot:</span></span>

        $siteName = "ToDoApp<your suffix>"
        $rule = New-Object Microsoft.WindowsAzure.Commands.Utilities.Websites.Services.WebEntities.RampUpRule
        $rule.ActionHostName = "$siteName-beta.azurewebsites.net"
        $rule.ReroutePercentage = 50
        $rule.Name = "beta"
        Set-AzureWebsite $siteName -Slot Production -RoutingRules $rule

   <span data-ttu-id="abcc3-270">The `ReroutePercentage=50` property specifies that 50% of the production traffic will be routed to the beta app's URL (specified by the `ActionHostName` property).</span><span class="sxs-lookup"><span data-stu-id="abcc3-270">The `ReroutePercentage=50` property specifies that 50% of the production traffic will be routed to the beta app's URL (specified by the `ActionHostName` property).</span></span>
2. <span data-ttu-id="abcc3-271">Now navigate to http://ToDoApp*&lt;your_suffix>*.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="abcc3-271">Now navigate to http://ToDoApp*&lt;your_suffix>*.azurewebsites.net.</span></span> <span data-ttu-id="abcc3-272">50% of the traffic should now be redirected to the beta slot.</span><span class="sxs-lookup"><span data-stu-id="abcc3-272">50% of the traffic should now be redirected to the beta slot.</span></span>
3. <span data-ttu-id="abcc3-273">In your Application Insights resource, filter the metrics by environment="beta".</span><span class="sxs-lookup"><span data-stu-id="abcc3-273">In your Application Insights resource, filter the metrics by environment="beta".</span></span>

   > [!NOTE]
   > <span data-ttu-id="abcc3-274">If you save this filtered view as another favorite, then you can easily flip the metric explorer views between production and beta views.</span><span class="sxs-lookup"><span data-stu-id="abcc3-274">If you save this filtered view as another favorite, then you can easily flip the metric explorer views between production and beta views.</span></span>
   >
   >

<span data-ttu-id="abcc3-275">Suppose in Application Insights you see something similar to the following:</span><span class="sxs-lookup"><span data-stu-id="abcc3-275">Suppose in Application Insights you see something similar to the following:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-test-in-production-controlled-test-flight/09-test-beta-site-in-production.png)

<span data-ttu-id="abcc3-276">Not only is this showing that there are many more clicks on the `<li>` tags, but there seems to be a surge of clicks on `<li>` tags.</span><span class="sxs-lookup"><span data-stu-id="abcc3-276">Not only is this showing that there are many more clicks on the `<li>` tags, but there seems to be a surge of clicks on `<li>` tags.</span></span> <span data-ttu-id="abcc3-277">You can then conclude that people have discovered the new `<li>` tags are clickable and are now clearing all their previously-completed tasks in the app.</span><span class="sxs-lookup"><span data-stu-id="abcc3-277">You can then conclude that people have discovered the new `<li>` tags are clickable and are now clearing all their previously-completed tasks in the app.</span></span>

<span data-ttu-id="abcc3-278">Based on the data of your flighting deployment, you decide that your new UI is ready for production.</span><span class="sxs-lookup"><span data-stu-id="abcc3-278">Based on the data of your flighting deployment, you decide that your new UI is ready for production.</span></span>

## <a name="go-live-move-your-new-code-into-production"></a><span data-ttu-id="abcc3-279">Go live: Move your new code into production</span><span class="sxs-lookup"><span data-stu-id="abcc3-279">Go live: Move your new code into production</span></span>
<span data-ttu-id="abcc3-280">You're now ready to move your update to production.</span><span class="sxs-lookup"><span data-stu-id="abcc3-280">You're now ready to move your update to production.</span></span> <span data-ttu-id="abcc3-281">What's great is that now you know that your update has already been validated *before* it is pushed to production.</span><span class="sxs-lookup"><span data-stu-id="abcc3-281">What's great is that now you know that your update has already been validated *before* it is pushed to production.</span></span> <span data-ttu-id="abcc3-282">So now you can confidently deploy it.</span><span class="sxs-lookup"><span data-stu-id="abcc3-282">So now you can confidently deploy it.</span></span> <span data-ttu-id="abcc3-283">Since you made an update to the AngularJS client app, you only validated the client-side code.</span><span class="sxs-lookup"><span data-stu-id="abcc3-283">Since you made an update to the AngularJS client app, you only validated the client-side code.</span></span> <span data-ttu-id="abcc3-284">If you were to make changes to the back-end Web API app, you could validate your changes similarly and easily.</span><span class="sxs-lookup"><span data-stu-id="abcc3-284">If you were to make changes to the back-end Web API app, you could validate your changes similarly and easily.</span></span>

1. <span data-ttu-id="abcc3-285">In Git Shell, remove the traffic routing rule by running the following command:</span><span class="sxs-lookup"><span data-stu-id="abcc3-285">In Git Shell, remove the traffic routing rule by running the following command:</span></span>

        Set-AzureWebsite $siteName -Slot Production -RoutingRules @()
2. <span data-ttu-id="abcc3-286">Run the Git commands:</span><span class="sxs-lookup"><span data-stu-id="abcc3-286">Run the Git commands:</span></span>

        git checkout master
        git pull origin master
        git merge beta
        git push origin master
3. <span data-ttu-id="abcc3-287">Wait for a few minutes for the new code to be deployed to the staging slot, then launch http://ToDoApp*&lt;your_suffix>*-staging.azurewebsites.net to verify that the new update is warmed up in the staging slot.</span><span class="sxs-lookup"><span data-stu-id="abcc3-287">Wait for a few minutes for the new code to be deployed to the staging slot, then launch http://ToDoApp*&lt;your_suffix>*-staging.azurewebsites.net to verify that the new update is warmed up in the staging slot.</span></span> <span data-ttu-id="abcc3-288">Remember that the your fork's master branch is linked to the staging slot of your app.</span><span class="sxs-lookup"><span data-stu-id="abcc3-288">Remember that the your fork's master branch is linked to the staging slot of your app.</span></span>
4. <span data-ttu-id="abcc3-289">Now, swap the staging slot into production</span><span class="sxs-lookup"><span data-stu-id="abcc3-289">Now, swap the staging slot into production</span></span>

        cd <ROOT>\ToDoApp\ARMTemplates
        .\swap.ps1 -Name todoapp<your_suffix>

## <a name="summary"></a><span data-ttu-id="abcc3-290">Summary</span><span class="sxs-lookup"><span data-stu-id="abcc3-290">Summary</span></span>
<span data-ttu-id="abcc3-291">Azure App Service makes it easy for small- to medium-sized businesses to test their customer-facing apps in production, something that has been traditionally done in big enterprises.</span><span class="sxs-lookup"><span data-stu-id="abcc3-291">Azure App Service makes it easy for small- to medium-sized businesses to test their customer-facing apps in production, something that has been traditionally done in big enterprises.</span></span> <span data-ttu-id="abcc3-292">Hopefully, this tutorial has given you the knowledge you need to bring together App Service and Application Insights to make possible flighting deployment, and even other test-in-production scenarios, in your DevOps world.</span><span class="sxs-lookup"><span data-stu-id="abcc3-292">Hopefully, this tutorial has given you the knowledge you need to bring together App Service and Application Insights to make possible flighting deployment, and even other test-in-production scenarios, in your DevOps world.</span></span>

## <a name="more-resources"></a><span data-ttu-id="abcc3-293">More resources</span><span class="sxs-lookup"><span data-stu-id="abcc3-293">More resources</span></span>
* [<span data-ttu-id="abcc3-294">Agile software development with Azure App Service</span><span class="sxs-lookup"><span data-stu-id="abcc3-294">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)
* [<span data-ttu-id="abcc3-295">Set up staging environments for web apps in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="abcc3-295">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)
* [<span data-ttu-id="abcc3-296">Deploy a complex application predictably in Azure</span><span class="sxs-lookup"><span data-stu-id="abcc3-296">Deploy a complex application predictably in Azure</span></span>](app-service-deploy-complex-application-predictably.md)
* [<span data-ttu-id="abcc3-297">Authoring Azure Resource Manager Templates</span><span class="sxs-lookup"><span data-stu-id="abcc3-297">Authoring Azure Resource Manager Templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="abcc3-298">JSONLint - The JSON Validator</span><span class="sxs-lookup"><span data-stu-id="abcc3-298">JSONLint - The JSON Validator</span></span>](http://jsonlint.com/)
* [<span data-ttu-id="abcc3-299">Git Branching – Basic Branching and Merging</span><span class="sxs-lookup"><span data-stu-id="abcc3-299">Git Branching – Basic Branching and Merging</span></span>](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [<span data-ttu-id="abcc3-300">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="abcc3-300">Azure PowerShell</span></span>](/powershell/azureps-cmdlets-docs)
* [<span data-ttu-id="abcc3-301">Project Kudu Wiki</span><span class="sxs-lookup"><span data-stu-id="abcc3-301">Project Kudu Wiki</span></span>](https://github.com/projectkudu/kudu/wiki)













