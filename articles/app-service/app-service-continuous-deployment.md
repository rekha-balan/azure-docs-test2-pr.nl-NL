---
title: Continuous deployment to Azure App Service | Microsoft Docs
description: Learn how to enable continuous deployment to Azure App Service.
services: app-service
documentationcenter: ''
author: cephalin
manager: cfowler
ms.assetid: 6adb5c84-6cf3-424e-a336-c554f23b4000
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2018
ms.author: cephalin;dariagrigoriu
ms.openlocfilehash: bd440e0ef017e2bf116e80ad049883e2338efddb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870482"
---
# <a name="continuous-deployment-to-azure-app-service"></a><span data-ttu-id="b88ef-103">Continuous deployment to Azure App Service</span><span class="sxs-lookup"><span data-stu-id="b88ef-103">Continuous deployment to Azure App Service</span></span>
<span data-ttu-id="b88ef-104">This article shows you how to configure continuous deployment for [Azure App Service](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b88ef-104">This article shows you how to configure continuous deployment for [Azure App Service](app-service-web-overview.md).</span></span> <span data-ttu-id="b88ef-105">App Service enables continuous deployment from BitBucket, GitHub, and [Azure DevOps Services](https://www.visualstudio.com/team-services/) by pulling in the most recent updates from your existing repository in one of these services.</span><span class="sxs-lookup"><span data-stu-id="b88ef-105">App Service enables continuous deployment from BitBucket, GitHub, and [Azure DevOps Services](https://www.visualstudio.com/team-services/) by pulling in the most recent updates from your existing repository in one of these services.</span></span>

<span data-ttu-id="b88ef-106">To find out how to configure continuous deployment manually from a cloud repository not listed by the Azure portal (such as [GitLab](https://gitlab.com/)), see [Setting up continuous deployment using manual steps](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).</span><span class="sxs-lookup"><span data-stu-id="b88ef-106">To find out how to configure continuous deployment manually from a cloud repository not listed by the Azure portal (such as [GitLab](https://gitlab.com/)), see [Setting up continuous deployment using manual steps](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).</span></span>

[!INCLUDE [Prepare repository](../../includes/app-service-deploy-prepare-repo.md)]

<span data-ttu-id="b88ef-107">Publish your prepared repository to one of the supported services.</span><span class="sxs-lookup"><span data-stu-id="b88ef-107">Publish your prepared repository to one of the supported services.</span></span> <span data-ttu-id="b88ef-108">For more information on publishing your project to these services, see [Create a repo (GitHub)], [Create a repo (BitBucket)], and [Get started with Azure DevOps Services].</span><span class="sxs-lookup"><span data-stu-id="b88ef-108">For more information on publishing your project to these services, see [Create a repo (GitHub)], [Create a repo (BitBucket)], and [Get started with Azure DevOps Services].</span></span>

## <a name="deploy-continuously-from-github"></a><span data-ttu-id="b88ef-109">Deploy continuously from GitHub</span><span class="sxs-lookup"><span data-stu-id="b88ef-109">Deploy continuously from GitHub</span></span>

<span data-ttu-id="b88ef-110">To enable continuous deployment with GitHub, navigate to your App Service app page in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b88ef-110">To enable continuous deployment with GitHub, navigate to your App Service app page in the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="b88ef-111">In the left menu, click **Deployment Center** > **GitHub** > **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="b88ef-111">In the left menu, click **Deployment Center** > **GitHub** > **Authorize**.</span></span> <span data-ttu-id="b88ef-112">Follow the authorization prompts.</span><span class="sxs-lookup"><span data-stu-id="b88ef-112">Follow the authorization prompts.</span></span> 

![](media/app-service-continuous-deployment/github-choose-source.png)

<span data-ttu-id="b88ef-113">You only need to authorize with GitHub once.</span><span class="sxs-lookup"><span data-stu-id="b88ef-113">You only need to authorize with GitHub once.</span></span> <span data-ttu-id="b88ef-114">If you're already authorized, just click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="b88ef-114">If you're already authorized, just click **Continue**.</span></span> <span data-ttu-id="b88ef-115">You can change the authorized GitHub account by clicking **Change account**.</span><span class="sxs-lookup"><span data-stu-id="b88ef-115">You can change the authorized GitHub account by clicking **Change account**.</span></span>

![](media/app-service-continuous-deployment/github-continue.png)

<span data-ttu-id="b88ef-116">In the **Build provider** page, choose the build provider and click > **Continue**.</span><span class="sxs-lookup"><span data-stu-id="b88ef-116">In the **Build provider** page, choose the build provider and click > **Continue**.</span></span>

### <a name="option-1-use-app-service-kudu-build-server"></a><span data-ttu-id="b88ef-117">Option 1: use App Service Kudu build server</span><span class="sxs-lookup"><span data-stu-id="b88ef-117">Option 1: use App Service Kudu build server</span></span>

<span data-ttu-id="b88ef-118">In the **Configure** page, select the organization, repository, and branch from which you want to deploy continuously.</span><span class="sxs-lookup"><span data-stu-id="b88ef-118">In the **Configure** page, select the organization, repository, and branch from which you want to deploy continuously.</span></span> <span data-ttu-id="b88ef-119">When finished, click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="b88ef-119">When finished, click **Continue**.</span></span>

### <a name="option-2-use-azure-devops-services-continuous-delivery"></a><span data-ttu-id="b88ef-120">Option 2: use Azure DevOps Services continuous delivery</span><span class="sxs-lookup"><span data-stu-id="b88ef-120">Option 2: use Azure DevOps Services continuous delivery</span></span>

> [!NOTE]
> <span data-ttu-id="b88ef-121">For App Service to create the necessary Azure Pipelines in your Azure DevOps Services organization, your Azure account must have the role of **Owner** in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="b88ef-121">For App Service to create the necessary Azure Pipelines in your Azure DevOps Services organization, your Azure account must have the role of **Owner** in your Azure subscription.</span></span>
>

<span data-ttu-id="b88ef-122">In the **Configure** page, in the **Code** section, select the organization, repository, and branch from which you want to deploy continuously.</span><span class="sxs-lookup"><span data-stu-id="b88ef-122">In the **Configure** page, in the **Code** section, select the organization, repository, and branch from which you want to deploy continuously.</span></span> <span data-ttu-id="b88ef-123">When finished, click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="b88ef-123">When finished, click **Continue**.</span></span>

<span data-ttu-id="b88ef-124">In the **Configure** page, in the **Build** section, configure a new Azure DevOps Services organization or specify an existing organization.</span><span class="sxs-lookup"><span data-stu-id="b88ef-124">In the **Configure** page, in the **Build** section, configure a new Azure DevOps Services organization or specify an existing organization.</span></span> <span data-ttu-id="b88ef-125">When finished, click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="b88ef-125">When finished, click **Continue**.</span></span>

> [!NOTE]
> <span data-ttu-id="b88ef-126">If you want to use an existing Azure DevOps Services organization that is not listed, you need to [link the Azure DevOps Services organization to your Azure subscription](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).</span><span class="sxs-lookup"><span data-stu-id="b88ef-126">If you want to use an existing Azure DevOps Services organization that is not listed, you need to [link the Azure DevOps Services organization to your Azure subscription](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).</span></span>

<span data-ttu-id="b88ef-127">In the **Test** page, choose whether to enable load tests, then click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="b88ef-127">In the **Test** page, choose whether to enable load tests, then click **Continue**.</span></span>

<span data-ttu-id="b88ef-128">Depending on the [pricing tier](https://azure.microsoft.com/pricing/details/app-service/plans/) of your App Service plan, you may also see a **Deploy to staging** page.</span><span class="sxs-lookup"><span data-stu-id="b88ef-128">Depending on the [pricing tier](https://azure.microsoft.com/pricing/details/app-service/plans/) of your App Service plan, you may also see a **Deploy to staging** page.</span></span> <span data-ttu-id="b88ef-129">Choose whether to [enable deployment slots](web-sites-staged-publishing.md), then click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="b88ef-129">Choose whether to [enable deployment slots](web-sites-staged-publishing.md), then click **Continue**.</span></span>

### <a name="finish-configuration"></a><span data-ttu-id="b88ef-130">Finish configuration</span><span class="sxs-lookup"><span data-stu-id="b88ef-130">Finish configuration</span></span>

<span data-ttu-id="b88ef-131">In the **Summary** page, verify your options and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="b88ef-131">In the **Summary** page, verify your options and click **Finish**.</span></span>

<span data-ttu-id="b88ef-132">When configuration completes, new commits in the selected repository are deployed continuously into your App Service app.</span><span class="sxs-lookup"><span data-stu-id="b88ef-132">When configuration completes, new commits in the selected repository are deployed continuously into your App Service app.</span></span>

![](media/app-service-continuous-deployment/github-finished.png)

## <a name="deploy-continuously-from-bitbucket"></a><span data-ttu-id="b88ef-133">Deploy continuously from BitBucket</span><span class="sxs-lookup"><span data-stu-id="b88ef-133">Deploy continuously from BitBucket</span></span>

<span data-ttu-id="b88ef-134">To enable continuous deployment with BitBucket, navigate to your App Service app page in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b88ef-134">To enable continuous deployment with BitBucket, navigate to your App Service app page in the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="b88ef-135">In the left menu, click **Deployment Center** > **BitBucket** > **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="b88ef-135">In the left menu, click **Deployment Center** > **BitBucket** > **Authorize**.</span></span> <span data-ttu-id="b88ef-136">Follow the authorization prompts.</span><span class="sxs-lookup"><span data-stu-id="b88ef-136">Follow the authorization prompts.</span></span> 

![](media/app-service-continuous-deployment/bitbucket-choose-source.png)

<span data-ttu-id="b88ef-137">You only need to authorize with BitBucket once.</span><span class="sxs-lookup"><span data-stu-id="b88ef-137">You only need to authorize with BitBucket once.</span></span> <span data-ttu-id="b88ef-138">If you're already authorized, just click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="b88ef-138">If you're already authorized, just click **Continue**.</span></span> <span data-ttu-id="b88ef-139">You can change the authorized BitBucket account by clicking **Change account**.</span><span class="sxs-lookup"><span data-stu-id="b88ef-139">You can change the authorized BitBucket account by clicking **Change account**.</span></span>

![](media/app-service-continuous-deployment/bitbucket-continue.png)

<span data-ttu-id="b88ef-140">In the **Configure** page, select the repository and branch from which you want to deploy continuously.</span><span class="sxs-lookup"><span data-stu-id="b88ef-140">In the **Configure** page, select the repository and branch from which you want to deploy continuously.</span></span> <span data-ttu-id="b88ef-141">When finished, click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="b88ef-141">When finished, click **Continue**.</span></span>

<span data-ttu-id="b88ef-142">In the **Summary** page, verify your options and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="b88ef-142">In the **Summary** page, verify your options and click **Finish**.</span></span>

<span data-ttu-id="b88ef-143">When configuration completes, new commits in the selected repository are deployed continuously into your App Service app.</span><span class="sxs-lookup"><span data-stu-id="b88ef-143">When configuration completes, new commits in the selected repository are deployed continuously into your App Service app.</span></span>

## <a name="deploy-continuously-from-azure-devops-services"></a><span data-ttu-id="b88ef-144">Deploy continuously from Azure DevOps Services</span><span class="sxs-lookup"><span data-stu-id="b88ef-144">Deploy continuously from Azure DevOps Services</span></span>

<span data-ttu-id="b88ef-145">To enable continuous deployment with Azure DevOps Services, navigate to your App Service app page in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b88ef-145">To enable continuous deployment with Azure DevOps Services, navigate to your App Service app page in the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="b88ef-146">In the left menu, click **Deployment Center** > **Azure DevOps Services** > **Continue**.</span><span class="sxs-lookup"><span data-stu-id="b88ef-146">In the left menu, click **Deployment Center** > **Azure DevOps Services** > **Continue**.</span></span> 

![](media/app-service-continuous-deployment/vsts-choose-source.png)

<span data-ttu-id="b88ef-147">In the **Build provider** page, choose the build provider and click > **Continue**.</span><span class="sxs-lookup"><span data-stu-id="b88ef-147">In the **Build provider** page, choose the build provider and click > **Continue**.</span></span>

### <a name="option-1-use-app-service-kudu-build-server"></a><span data-ttu-id="b88ef-148">Option 1: use App Service Kudu build server</span><span class="sxs-lookup"><span data-stu-id="b88ef-148">Option 1: use App Service Kudu build server</span></span>

<span data-ttu-id="b88ef-149">In the **Configure** page, select the Azure DevOps Services organization, project, repository, and branch from which you want to deploy continuously.</span><span class="sxs-lookup"><span data-stu-id="b88ef-149">In the **Configure** page, select the Azure DevOps Services organization, project, repository, and branch from which you want to deploy continuously.</span></span> <span data-ttu-id="b88ef-150">When finished, click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="b88ef-150">When finished, click **Continue**.</span></span>

### <a name="option-2-use-azure-devops-services-continuous-delivery"></a><span data-ttu-id="b88ef-151">Option 2: use Azure DevOps Services continuous delivery</span><span class="sxs-lookup"><span data-stu-id="b88ef-151">Option 2: use Azure DevOps Services continuous delivery</span></span>

> [!NOTE]
> <span data-ttu-id="b88ef-152">For App Service to create the necessary Azure Pipelines in your Azure DevOps Services organization, your Azure account must have the role of **Owner** in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="b88ef-152">For App Service to create the necessary Azure Pipelines in your Azure DevOps Services organization, your Azure account must have the role of **Owner** in your Azure subscription.</span></span>
>

<span data-ttu-id="b88ef-153">In the **Configure** page, in the **Code** section, select the Azure DevOps Services organization, project, repository, and branch from which you want to deploy continuously.</span><span class="sxs-lookup"><span data-stu-id="b88ef-153">In the **Configure** page, in the **Code** section, select the Azure DevOps Services organization, project, repository, and branch from which you want to deploy continuously.</span></span> <span data-ttu-id="b88ef-154">When finished, click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="b88ef-154">When finished, click **Continue**.</span></span>

> [!NOTE]
> <span data-ttu-id="b88ef-155">If you want to use an existing Azure DevOps Services organization that is not listed, you need to [link the Azure DevOps Services organization to your Azure subscription](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).</span><span class="sxs-lookup"><span data-stu-id="b88ef-155">If you want to use an existing Azure DevOps Services organization that is not listed, you need to [link the Azure DevOps Services organization to your Azure subscription](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).</span></span>

<span data-ttu-id="b88ef-156">In the **Configure** page, in the **Build** section, specify the language framework that Azure DevOps Services should use to run the build tasks for your selected repository.</span><span class="sxs-lookup"><span data-stu-id="b88ef-156">In the **Configure** page, in the **Build** section, specify the language framework that Azure DevOps Services should use to run the build tasks for your selected repository.</span></span> <span data-ttu-id="b88ef-157">When finished, click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="b88ef-157">When finished, click **Continue**.</span></span>

<span data-ttu-id="b88ef-158">In the **Test** page, choose whether to enable load tests, then click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="b88ef-158">In the **Test** page, choose whether to enable load tests, then click **Continue**.</span></span>

<span data-ttu-id="b88ef-159">Depending on the [pricing tier](https://azure.microsoft.com/pricing/details/app-service/plans/) of your App Service plan, you may also see a **Deploy to staging** page.</span><span class="sxs-lookup"><span data-stu-id="b88ef-159">Depending on the [pricing tier](https://azure.microsoft.com/pricing/details/app-service/plans/) of your App Service plan, you may also see a **Deploy to staging** page.</span></span> <span data-ttu-id="b88ef-160">Choose whether to [enable deployment slots](web-sites-staged-publishing.md), then click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="b88ef-160">Choose whether to [enable deployment slots](web-sites-staged-publishing.md), then click **Continue**.</span></span> 

### <a name="finish-configuration"></a><span data-ttu-id="b88ef-161">Finish configuration</span><span class="sxs-lookup"><span data-stu-id="b88ef-161">Finish configuration</span></span>

<span data-ttu-id="b88ef-162">In the **Summary** page, verify your options and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="b88ef-162">In the **Summary** page, verify your options and click **Finish**.</span></span>

<span data-ttu-id="b88ef-163">When configuration completes, new commits in the selected repository are deployed continuously into your App Service app.</span><span class="sxs-lookup"><span data-stu-id="b88ef-163">When configuration completes, new commits in the selected repository are deployed continuously into your App Service app.</span></span>

## <a name="disable-continuous-deployment"></a><span data-ttu-id="b88ef-164">Disable continuous deployment</span><span class="sxs-lookup"><span data-stu-id="b88ef-164">Disable continuous deployment</span></span>

<span data-ttu-id="b88ef-165">To disable continuous deployment, navigate to your App Service app page in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b88ef-165">To disable continuous deployment, navigate to your App Service app page in the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="b88ef-166">In the left menu, click **Deployment Center** > **GitHub** or **Azure DevOps Services** or **BitBucket** > **Disconnect**.</span><span class="sxs-lookup"><span data-stu-id="b88ef-166">In the left menu, click **Deployment Center** > **GitHub** or **Azure DevOps Services** or **BitBucket** > **Disconnect**.</span></span>

![](media/app-service-continuous-deployment/disable.png)

[!INCLUDE [What happens to my app during deployment?](../../includes/app-service-deploy-atomicity.md)]

## <a name="additional-resources"></a><span data-ttu-id="b88ef-167">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="b88ef-167">Additional Resources</span></span>

* [<span data-ttu-id="b88ef-168">How to investigate common issues with continuous deployment</span><span class="sxs-lookup"><span data-stu-id="b88ef-168">How to investigate common issues with continuous deployment</span></span>](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment)
* <span data-ttu-id="b88ef-169">[How to use PowerShell for Azure]</span><span class="sxs-lookup"><span data-stu-id="b88ef-169">[How to use PowerShell for Azure]</span></span>
* <span data-ttu-id="b88ef-170">[Git documentation]</span><span class="sxs-lookup"><span data-stu-id="b88ef-170">[Git documentation]</span></span>
* [<span data-ttu-id="b88ef-171">Project Kudu</span><span class="sxs-lookup"><span data-stu-id="b88ef-171">Project Kudu</span></span>](https://github.com/projectkudu/kudu/wiki)
* [<span data-ttu-id="b88ef-172">Use Azure to automatically generate a CI/CD pipeline to deploy an ASP.NET 4 app</span><span class="sxs-lookup"><span data-stu-id="b88ef-172">Use Azure to automatically generate a CI/CD pipeline to deploy an ASP.NET 4 app</span></span>](https://www.visualstudio.com/docs/build/get-started/aspnet-4-ci-cd-azure-automatic)

[Azure portal]: https://portal.azure.com
[VSTS Portal]: https://www.visualstudio.com/en-us/products/visual-studio-team-services-vs.aspx
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[How to use PowerShell for Azure]: /powershell/azureps-cmdlets-docs
[Git Documentation]: http://git-scm.com/documentation

[Create a repo (GitHub)]: https://help.github.com/articles/create-a-repo
[Create a repo (BitBucket)]: https://confluence.atlassian.com/display/BITBUCKET/Create+an+Account+and+a+Git+Repo
[Get started with Azure DevOps Services]: https://www.visualstudio.com/docs/vsts-tfs-overview
