---
title: Continuous Deployment to Azure App Service | Microsoft Docs
description: Learn how to enable continuous deployment to Azure App Service.
services: app-service
documentationcenter: ''
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 6adb5c84-6cf3-424e-a336-c554f23b4000
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/28/2016
ms.author: dariagrigoriu
ms.openlocfilehash: c70bbb3d371203b795724052239b13a5d8d1db09
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554652"
---
# <a name="continuous-deployment-to-azure-app-service"></a><span data-ttu-id="32249-103">Continuous Deployment to Azure App Service</span><span class="sxs-lookup"><span data-stu-id="32249-103">Continuous Deployment to Azure App Service</span></span>
<span data-ttu-id="32249-104">This tutorial shows you how to configure a continuous deployment workflow for your [Azure App Service] app.</span><span class="sxs-lookup"><span data-stu-id="32249-104">This tutorial shows you how to configure a continuous deployment workflow for your [Azure App Service] app.</span></span> <span data-ttu-id="32249-105">App Service integration with BitBucket, GitHub, and [Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/) enables a continuous deployment workflow where Azure pulls in the most recent updates from your project published to one of these services.</span><span class="sxs-lookup"><span data-stu-id="32249-105">App Service integration with BitBucket, GitHub, and [Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/) enables a continuous deployment workflow where Azure pulls in the most recent updates from your project published to one of these services.</span></span> <span data-ttu-id="32249-106">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span><span class="sxs-lookup"><span data-stu-id="32249-106">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span>

<span data-ttu-id="32249-107">To find out how to configure continuous deployment manually from a cloud repository not listed by the Azure Portal (such as [GitLab](https://gitlab.com/)), see [Setting up continuous deployment using manual steps](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).</span><span class="sxs-lookup"><span data-stu-id="32249-107">To find out how to configure continuous deployment manually from a cloud repository not listed by the Azure Portal (such as [GitLab](https://gitlab.com/)), see [Setting up continuous deployment using manual steps](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).</span></span>

## <a name="overview"></a><span data-ttu-id="32249-108">Enable continuous deployment</span><span class="sxs-lookup"><span data-stu-id="32249-108">Enable continuous deployment</span></span>
<span data-ttu-id="32249-109">To enable continuous deployment,</span><span class="sxs-lookup"><span data-stu-id="32249-109">To enable continuous deployment,</span></span>

1. <span data-ttu-id="32249-110">Publish your app content to the repository that will be used for continuous deployment.</span><span class="sxs-lookup"><span data-stu-id="32249-110">Publish your app content to the repository that will be used for continuous deployment.</span></span>  
    <span data-ttu-id="32249-111">For more information on publishing your project to these services, see [Create a repo (GitHub)], [Create a repo (BitBucket)], and [Get started with VSTS].</span><span class="sxs-lookup"><span data-stu-id="32249-111">For more information on publishing your project to these services, see [Create a repo (GitHub)], [Create a repo (BitBucket)], and [Get started with VSTS].</span></span>
2. <span data-ttu-id="32249-112">In your app's menu blade in the [Azure portal], click **APP DEPLOYMENT > Deployment options**.</span><span class="sxs-lookup"><span data-stu-id="32249-112">In your app's menu blade in the [Azure portal], click **APP DEPLOYMENT > Deployment options**.</span></span> <span data-ttu-id="32249-113">Click **Choose Source**, then select the deployment source.</span><span class="sxs-lookup"><span data-stu-id="32249-113">Click **Choose Source**, then select the deployment source.</span></span>  
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-continuous-deployment/cd_options.png)
   
   > [!NOTE]
   > <span data-ttu-id="32249-114">To configure a VSTS account for App Service deployment please see this [tutorial](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).</span><span class="sxs-lookup"><span data-stu-id="32249-114">To configure a VSTS account for App Service deployment please see this [tutorial](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).</span></span>
   > 
   > 
3. <span data-ttu-id="32249-115">Complete the authorization workflow.</span><span class="sxs-lookup"><span data-stu-id="32249-115">Complete the authorization workflow.</span></span>
4. <span data-ttu-id="32249-116">In the **Deployment source** blade, choose the project and branch to deploy from.</span><span class="sxs-lookup"><span data-stu-id="32249-116">In the **Deployment source** blade, choose the project and branch to deploy from.</span></span> <span data-ttu-id="32249-117">When you're done, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="32249-117">When you're done, click **OK**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-continuous-deployment/github_option.png)
   
   > [!NOTE]
   > <span data-ttu-id="32249-118">When enabling continuous deployment with GitHub or BitBucket, both public and private projects will be displayed.</span><span class="sxs-lookup"><span data-stu-id="32249-118">When enabling continuous deployment with GitHub or BitBucket, both public and private projects will be displayed.</span></span>
   > 
   > 
   
    <span data-ttu-id="32249-119">App Service creates an association with the selected repository, pulls in the files from the specified branch, and maintains a clone of your repository for your App Service app.</span><span class="sxs-lookup"><span data-stu-id="32249-119">App Service creates an association with the selected repository, pulls in the files from the specified branch, and maintains a clone of your repository for your App Service app.</span></span> <span data-ttu-id="32249-120">When you configure VSTS continuous deployment from the Azure portal, the integration uses the App Service [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki), which already automates build and deployment tasks with every `git push`.</span><span class="sxs-lookup"><span data-stu-id="32249-120">When you configure VSTS continuous deployment from the Azure portal, the integration uses the App Service [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki), which already automates build and deployment tasks with every `git push`.</span></span> <span data-ttu-id="32249-121">You do not need to separately set up continuous deployment in VSTS.</span><span class="sxs-lookup"><span data-stu-id="32249-121">You do not need to separately set up continuous deployment in VSTS.</span></span> <span data-ttu-id="32249-122">After this process completes, the **Deployment options** app blade will show an active deployment that indicates deployment has succeeded.</span><span class="sxs-lookup"><span data-stu-id="32249-122">After this process completes, the **Deployment options** app blade will show an active deployment that indicates deployment has succeeded.</span></span>
5. <span data-ttu-id="32249-123">To verify the app is successfully deployed, click the **URL** at the top of the app's blade in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="32249-123">To verify the app is successfully deployed, click the **URL** at the top of the app's blade in the Azure portal.</span></span>
6. <span data-ttu-id="32249-124">To verify that continuous deployment is occurring from the repository of your choice, push a change to the repository.</span><span class="sxs-lookup"><span data-stu-id="32249-124">To verify that continuous deployment is occurring from the repository of your choice, push a change to the repository.</span></span> <span data-ttu-id="32249-125">Your app should update to reflect the changes shortly after the push to the repository completes.</span><span class="sxs-lookup"><span data-stu-id="32249-125">Your app should update to reflect the changes shortly after the push to the repository completes.</span></span> <span data-ttu-id="32249-126">You can verify that it has pulled in the update in the **Deployment options** blade of your app.</span><span class="sxs-lookup"><span data-stu-id="32249-126">You can verify that it has pulled in the update in the **Deployment options** blade of your app.</span></span>

## <a name="VSsolution"></a><span data-ttu-id="32249-127">Continuous deployment of a Visual Studio solution</span><span class="sxs-lookup"><span data-stu-id="32249-127">Continuous deployment of a Visual Studio solution</span></span>
<span data-ttu-id="32249-128">Pushing a Visual Studio solution to Azure App Service is just as easy as pushing a simple index.html file.</span><span class="sxs-lookup"><span data-stu-id="32249-128">Pushing a Visual Studio solution to Azure App Service is just as easy as pushing a simple index.html file.</span></span> <span data-ttu-id="32249-129">The App Service deployment process streamlines all the details, including restoring NuGet dependencies and building the application binaries.</span><span class="sxs-lookup"><span data-stu-id="32249-129">The App Service deployment process streamlines all the details, including restoring NuGet dependencies and building the application binaries.</span></span> <span data-ttu-id="32249-130">You can follow the source control best practices of maintaining code only in your Git repository, and let App Service deployment take care of the rest.</span><span class="sxs-lookup"><span data-stu-id="32249-130">You can follow the source control best practices of maintaining code only in your Git repository, and let App Service deployment take care of the rest.</span></span>

<span data-ttu-id="32249-131">The steps for pushing your Visual Studio solution to App Service are the same as in the [previous section](#overview), provided that you configure your solution and repository as follows:</span><span class="sxs-lookup"><span data-stu-id="32249-131">The steps for pushing your Visual Studio solution to App Service are the same as in the [previous section](#overview), provided that you configure your solution and repository as follows:</span></span>

* <span data-ttu-id="32249-132">Use the Visual Studio source control option to generate a `.gitignore` file such as the image below or manually add a `.gitignore` file in your repository root with content similar to this [.gitignore sample](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span><span class="sxs-lookup"><span data-stu-id="32249-132">Use the Visual Studio source control option to generate a `.gitignore` file such as the image below or manually add a `.gitignore` file in your repository root with content similar to this [.gitignore sample](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>
  
  ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-continuous-deployment/VS_source_control.png)
* <span data-ttu-id="32249-133">Add the entire solution's directory tree to your repository, with the .sln file in the repository root.</span><span class="sxs-lookup"><span data-stu-id="32249-133">Add the entire solution's directory tree to your repository, with the .sln file in the repository root.</span></span>

<span data-ttu-id="32249-134">Once you have set up your repository as described, and configured your app in Azure for continuous publishing from one of the online Git repositories, you can develop your ASP.NET application locally in Visual Studio and continuously deploy your code simply by pushing your changes to your online Git repository.</span><span class="sxs-lookup"><span data-stu-id="32249-134">Once you have set up your repository as described, and configured your app in Azure for continuous publishing from one of the online Git repositories, you can develop your ASP.NET application locally in Visual Studio and continuously deploy your code simply by pushing your changes to your online Git repository.</span></span>

## <a name="disableCD"></a><span data-ttu-id="32249-135">Disable continuous deployment</span><span class="sxs-lookup"><span data-stu-id="32249-135">Disable continuous deployment</span></span>
<span data-ttu-id="32249-136">To disable continuous deployment,</span><span class="sxs-lookup"><span data-stu-id="32249-136">To disable continuous deployment,</span></span>

1. <span data-ttu-id="32249-137">In your app's menu blade in the [Azure portal], click **APP DEPLOYMENT > Deployment options**.</span><span class="sxs-lookup"><span data-stu-id="32249-137">In your app's menu blade in the [Azure portal], click **APP DEPLOYMENT > Deployment options**.</span></span> <span data-ttu-id="32249-138">Then click **Disconnect** in the **Deployment options** blade.</span><span class="sxs-lookup"><span data-stu-id="32249-138">Then click **Disconnect** in the **Deployment options** blade.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-continuous-deployment/cd_disconnect.png)
2. <span data-ttu-id="32249-139">After answering **Yes** to the confirmation message, you can return to your app's blade and click **APP DEPLOYMENT > Deployment options** if you would like to set up publishing from another source.</span><span class="sxs-lookup"><span data-stu-id="32249-139">After answering **Yes** to the confirmation message, you can return to your app's blade and click **APP DEPLOYMENT > Deployment options** if you would like to set up publishing from another source.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="32249-140">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="32249-140">Additional Resources</span></span>
* [<span data-ttu-id="32249-141">How to investigate common issues with continuous deployment</span><span class="sxs-lookup"><span data-stu-id="32249-141">How to investigate common issues with continuous deployment</span></span>](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment)
* <span data-ttu-id="32249-142">[How to use PowerShell for Azure]</span><span class="sxs-lookup"><span data-stu-id="32249-142">[How to use PowerShell for Azure]</span></span>
* <span data-ttu-id="32249-143">[How to use the Azure Command-Line Tools for Mac and Linux]</span><span class="sxs-lookup"><span data-stu-id="32249-143">[How to use the Azure Command-Line Tools for Mac and Linux]</span></span>
* <span data-ttu-id="32249-144">[Git documentation]</span><span class="sxs-lookup"><span data-stu-id="32249-144">[Git documentation]</span></span>
* [<span data-ttu-id="32249-145">Project Kudu</span><span class="sxs-lookup"><span data-stu-id="32249-145">Project Kudu</span></span>](https://github.com/projectkudu/kudu/wiki)
* [<span data-ttu-id="32249-146">Use Azure to automatically generate a CI/CD pipeline to deploy an ASP.NET 4 app</span><span class="sxs-lookup"><span data-stu-id="32249-146">Use Azure to automatically generate a CI/CD pipeline to deploy an ASP.NET 4 app</span></span>](https://www.visualstudio.com/docs/build/get-started/aspnet-4-ci-cd-azure-automatic)

> [!NOTE]
> <span data-ttu-id="32249-147">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="32249-147">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="32249-148">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="32249-148">No credit cards required; no commitments.</span></span>
> 
> 

[Azure App Service]: https://azure.microsoft.com/en-us/documentation/articles/app-service-changes-existing-services/
[Azure portal]: https://portal.azure.com
[VSTS Portal]: https://www.visualstudio.com/en-us/products/visual-studio-team-services-vs.aspx
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[How to use PowerShell for Azure]: /powershell/azureps-cmdlets-docs
[How to use the Azure Command-Line Tools for Mac and Linux]:../cli-install-nodejs.md
[Git Documentation]: http://git-scm.com/documentation

[Create a repo (GitHub)]: https://help.github.com/articles/create-a-repo
[Create a repo (BitBucket)]: https://confluence.atlassian.com/display/BITBUCKET/Create+an+Account+and+a+Git+Repo
[Get started with VSTS]: https://www.visualstudio.com/docs/vsts-tfs-overview
[Continuous delivery to Azure using Visual Studio Team Services]: ../articles/cloud-services/cloud-services-continuous-delivery-use-vso.md




