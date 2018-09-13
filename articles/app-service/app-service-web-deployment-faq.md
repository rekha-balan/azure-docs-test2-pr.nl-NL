---
title: Deployment FAQs for Azure web apps | Microsoft Docs
description: Get answers to frequently asked questions about deployment for the Web Apps feature of Azure App Service.
services: app-service\web
documentationcenter: ''
author: genlin
manager: cshepard
editor: ''
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/11/2018
ms.author: genli
ms.openlocfilehash: ab8750e5824cf9f7635d11a6b2be332b2f9a761c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869146"
---
# <a name="deployment-faqs-for-web-apps-in-azure"></a><span data-ttu-id="784fa-103">Deployment FAQs for Web Apps in Azure</span><span class="sxs-lookup"><span data-stu-id="784fa-103">Deployment FAQs for Web Apps in Azure</span></span>

<span data-ttu-id="784fa-104">This article has answers to frequently asked questions (FAQs) about deployment issues for the [Web Apps feature of Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="784fa-104">This article has answers to frequently asked questions (FAQs) about deployment issues for the [Web Apps feature of Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="i-am-just-getting-started-with-app-service-web-apps-how-do-i-publish-my-code"></a><span data-ttu-id="784fa-105">I am just getting started with App Service web apps.</span><span class="sxs-lookup"><span data-stu-id="784fa-105">I am just getting started with App Service web apps.</span></span> <span data-ttu-id="784fa-106">How do I publish my code?</span><span class="sxs-lookup"><span data-stu-id="784fa-106">How do I publish my code?</span></span>

<span data-ttu-id="784fa-107">Here are some options for publishing your web app code:</span><span class="sxs-lookup"><span data-stu-id="784fa-107">Here are some options for publishing your web app code:</span></span>

*   <span data-ttu-id="784fa-108">Deploy by using Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="784fa-108">Deploy by using Visual Studio.</span></span> <span data-ttu-id="784fa-109">If you have the Visual Studio solution, right-click the web application project, and then select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="784fa-109">If you have the Visual Studio solution, right-click the web application project, and then select **Publish**.</span></span>
*   <span data-ttu-id="784fa-110">Deploy by using an FTP client.</span><span class="sxs-lookup"><span data-stu-id="784fa-110">Deploy by using an FTP client.</span></span> <span data-ttu-id="784fa-111">In the Azure portal, download the publish profile for the web app that you want to deploy your code to.</span><span class="sxs-lookup"><span data-stu-id="784fa-111">In the Azure portal, download the publish profile for the web app that you want to deploy your code to.</span></span> <span data-ttu-id="784fa-112">Then, upload the files to \site\wwwroot by using the same publish profile FTP credentials.</span><span class="sxs-lookup"><span data-stu-id="784fa-112">Then, upload the files to \site\wwwroot by using the same publish profile FTP credentials.</span></span>

<span data-ttu-id="784fa-113">For more information, see [Deploy your app to App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="784fa-113">For more information, see [Deploy your app to App Service](app-service-deploy-local-git.md).</span></span>

## <a name="i-see-an-error-message-when-i-try-to-deploy-from-visual-studio-how-do-i-resolve-this"></a><span data-ttu-id="784fa-114">I see an error message when I try to deploy from Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="784fa-114">I see an error message when I try to deploy from Visual Studio.</span></span> <span data-ttu-id="784fa-115">How do I resolve this?</span><span class="sxs-lookup"><span data-stu-id="784fa-115">How do I resolve this?</span></span>

<span data-ttu-id="784fa-116">If you see the following message, you might be using an older version of the SDK: “Error during deployment for resource 'YourResourceName' in resource group 'YourResourceGroup': MissingRegistrationForLocation: The subscription is not registered for the resource type 'components' in the location 'Central US'.</span><span class="sxs-lookup"><span data-stu-id="784fa-116">If you see the following message, you might be using an older version of the SDK: “Error during deployment for resource 'YourResourceName' in resource group 'YourResourceGroup': MissingRegistrationForLocation: The subscription is not registered for the resource type 'components' in the location 'Central US'.</span></span> <span data-ttu-id="784fa-117">Please re-register for this provider in order to have access to this location.”</span><span class="sxs-lookup"><span data-stu-id="784fa-117">Please re-register for this provider in order to have access to this location.”</span></span> 

<span data-ttu-id="784fa-118">To resolve this error, upgrade to the [latest SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="784fa-118">To resolve this error, upgrade to the [latest SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="784fa-119">If you see this message and you have the latest SDK, submit a support request.</span><span class="sxs-lookup"><span data-stu-id="784fa-119">If you see this message and you have the latest SDK, submit a support request.</span></span>

## <a name="how-do-i-deploy-an-aspnet-application-from-visual-studio-to-app-service"></a><span data-ttu-id="784fa-120">How do I deploy an ASP.NET application from Visual Studio to App Service?</span><span class="sxs-lookup"><span data-stu-id="784fa-120">How do I deploy an ASP.NET application from Visual Studio to App Service?</span></span>
<a id="deployasp"></a>

<span data-ttu-id="784fa-121">The tutorial [Create your first ASP.NET web app in Azure in five minutes](app-service-web-get-started-dotnet.md) shows you how to deploy an ASP.NET web application to a web app in App Service by using Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="784fa-121">The tutorial [Create your first ASP.NET web app in Azure in five minutes](app-service-web-get-started-dotnet.md) shows you how to deploy an ASP.NET web application to a web app in App Service by using Visual Studio 2017.</span></span>

## <a name="what-are-the-different-types-of-deployment-credentials"></a><span data-ttu-id="784fa-122">What are the different types of deployment credentials?</span><span class="sxs-lookup"><span data-stu-id="784fa-122">What are the different types of deployment credentials?</span></span>

<span data-ttu-id="784fa-123">App Service supports two types of credentials for local Git deployment and FTP/S deployment.</span><span class="sxs-lookup"><span data-stu-id="784fa-123">App Service supports two types of credentials for local Git deployment and FTP/S deployment.</span></span> <span data-ttu-id="784fa-124">For more information about how to configure deployment credentials, see [Configure deployment credentials for App Service](app-service-deployment-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="784fa-124">For more information about how to configure deployment credentials, see [Configure deployment credentials for App Service](app-service-deployment-credentials.md).</span></span>

## <a name="what-is-the-file-or-directory-structure-of-my-app-service-web-app"></a><span data-ttu-id="784fa-125">What is the file or directory structure of my App Service web app?</span><span class="sxs-lookup"><span data-stu-id="784fa-125">What is the file or directory structure of my App Service web app?</span></span>

<span data-ttu-id="784fa-126">For information about the file structure of your App Service app, see [File structure in Azure](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure).</span><span class="sxs-lookup"><span data-stu-id="784fa-126">For information about the file structure of your App Service app, see [File structure in Azure](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure).</span></span>

## <a name="how-do-i-resolve-ftp-error-550---there-is-not-enough-space-on-the-disk-when-i-try-to-ftp-my-files"></a><span data-ttu-id="784fa-127">How do I resolve "FTP Error 550 - There is not enough space on the disk" when I try to FTP my files?</span><span class="sxs-lookup"><span data-stu-id="784fa-127">How do I resolve "FTP Error 550 - There is not enough space on the disk" when I try to FTP my files?</span></span>

<span data-ttu-id="784fa-128">If you see this message, it's likely that you are running into a disk quota in the service plan for your web app.</span><span class="sxs-lookup"><span data-stu-id="784fa-128">If you see this message, it's likely that you are running into a disk quota in the service plan for your web app.</span></span> <span data-ttu-id="784fa-129">You might need to scale up to a higher service tier based on your disk space needs.</span><span class="sxs-lookup"><span data-stu-id="784fa-129">You might need to scale up to a higher service tier based on your disk space needs.</span></span> <span data-ttu-id="784fa-130">For more information about pricing plans and resource limits, see [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="784fa-130">For more information about pricing plans and resource limits, see [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

## <a name="how-do-i-set-up-continuous-deployment-for-my-app-service-web-app"></a><span data-ttu-id="784fa-131">How do I set up continuous deployment for my App Service web app?</span><span class="sxs-lookup"><span data-stu-id="784fa-131">How do I set up continuous deployment for my App Service web app?</span></span>

<span data-ttu-id="784fa-132">You can set up continuous deployment from several resources, including Azure DevOps, OneDrive, GitHub, Bitbucket, Dropbox, and other Git repositories.</span><span class="sxs-lookup"><span data-stu-id="784fa-132">You can set up continuous deployment from several resources, including Azure DevOps, OneDrive, GitHub, Bitbucket, Dropbox, and other Git repositories.</span></span> <span data-ttu-id="784fa-133">These options are available in the portal.</span><span class="sxs-lookup"><span data-stu-id="784fa-133">These options are available in the portal.</span></span> <span data-ttu-id="784fa-134">[Continuous deployment to App Service](app-service-continuous-deployment.md) is a helpful tutorial that explains how to set up continuous deployment.</span><span class="sxs-lookup"><span data-stu-id="784fa-134">[Continuous deployment to App Service](app-service-continuous-deployment.md) is a helpful tutorial that explains how to set up continuous deployment.</span></span>

## <a name="how-do-i-troubleshoot-issues-with-continuous-deployment-from-github-and-bitbucket"></a><span data-ttu-id="784fa-135">How do I troubleshoot issues with continuous deployment from GitHub and Bitbucket?</span><span class="sxs-lookup"><span data-stu-id="784fa-135">How do I troubleshoot issues with continuous deployment from GitHub and Bitbucket?</span></span>

<span data-ttu-id="784fa-136">For help investigating issues with continuous deployment from GitHub or Bitbucket, see [Investigating continuous deployment](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment).</span><span class="sxs-lookup"><span data-stu-id="784fa-136">For help investigating issues with continuous deployment from GitHub or Bitbucket, see [Investigating continuous deployment](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment).</span></span>

## <a name="i-cant-ftp-to-my-site-and-publish-my-code-how-do-i-resolve-this"></a><span data-ttu-id="784fa-137">I can't FTP to my site and publish my code.</span><span class="sxs-lookup"><span data-stu-id="784fa-137">I can't FTP to my site and publish my code.</span></span> <span data-ttu-id="784fa-138">How do I resolve this?</span><span class="sxs-lookup"><span data-stu-id="784fa-138">How do I resolve this?</span></span>

<span data-ttu-id="784fa-139">To resolve FTP issues:</span><span class="sxs-lookup"><span data-stu-id="784fa-139">To resolve FTP issues:</span></span>

1. <span data-ttu-id="784fa-140">Verify that you are entering the correct host name and credentials.</span><span class="sxs-lookup"><span data-stu-id="784fa-140">Verify that you are entering the correct host name and credentials.</span></span> <span data-ttu-id="784fa-141">For detailed information about different types of credentials and how to use them, see [Deployment credentials](https://github.com/projectkudu/kudu/wiki/Deployment-credentials).</span><span class="sxs-lookup"><span data-stu-id="784fa-141">For detailed information about different types of credentials and how to use them, see [Deployment credentials](https://github.com/projectkudu/kudu/wiki/Deployment-credentials).</span></span>
2. <span data-ttu-id="784fa-142">Verify that the FTP ports are not blocked by a firewall.</span><span class="sxs-lookup"><span data-stu-id="784fa-142">Verify that the FTP ports are not blocked by a firewall.</span></span> <span data-ttu-id="784fa-143">The ports should have these settings:</span><span class="sxs-lookup"><span data-stu-id="784fa-143">The ports should have these settings:</span></span>
    * <span data-ttu-id="784fa-144">FTP control connection port: 21</span><span class="sxs-lookup"><span data-stu-id="784fa-144">FTP control connection port: 21</span></span>
    * <span data-ttu-id="784fa-145">FTP data connection port: 989, 10001-10300</span><span class="sxs-lookup"><span data-stu-id="784fa-145">FTP data connection port: 989, 10001-10300</span></span>

## <a name="how-do-i-publish-my-code-to-app-service"></a><span data-ttu-id="784fa-146">How do I publish my code to App Service?</span><span class="sxs-lookup"><span data-stu-id="784fa-146">How do I publish my code to App Service?</span></span>

<span data-ttu-id="784fa-147">The Azure Quickstart is designed to help you deploy your app by using the deployment stack and method of your choice.</span><span class="sxs-lookup"><span data-stu-id="784fa-147">The Azure Quickstart is designed to help you deploy your app by using the deployment stack and method of your choice.</span></span> <span data-ttu-id="784fa-148">To use the Quickstart, in the Azure portal, go to **Settings** > **App Deployment**.</span><span class="sxs-lookup"><span data-stu-id="784fa-148">To use the Quickstart, in the Azure portal, go to **Settings** > **App Deployment**.</span></span>

## <a name="why-does-my-app-sometimes-restart-after-deployment-to-app-service"></a><span data-ttu-id="784fa-149">Why does my app sometimes restart after deployment to App Service?</span><span class="sxs-lookup"><span data-stu-id="784fa-149">Why does my app sometimes restart after deployment to App Service?</span></span>

<span data-ttu-id="784fa-150">To learn about the circumstances under which an application deployment might result in a restart, see [Deployment vs. runtime issues](https://github.com/projectkudu/kudu/wiki/Deployment-vs-runtime-issues#deployments-and-web-app-restarts").</span><span class="sxs-lookup"><span data-stu-id="784fa-150">To learn about the circumstances under which an application deployment might result in a restart, see [Deployment vs. runtime issues](https://github.com/projectkudu/kudu/wiki/Deployment-vs-runtime-issues#deployments-and-web-app-restarts").</span></span> <span data-ttu-id="784fa-151">As the article describes, App Service deploys files to the wwwroot folder.</span><span class="sxs-lookup"><span data-stu-id="784fa-151">As the article describes, App Service deploys files to the wwwroot folder.</span></span> <span data-ttu-id="784fa-152">It never directly restarts your app.</span><span class="sxs-lookup"><span data-stu-id="784fa-152">It never directly restarts your app.</span></span>

## <a name="how-do-i-integrate-azure-devops-code-with-app-service"></a><span data-ttu-id="784fa-153">How do I integrate Azure DevOps code with App Service?</span><span class="sxs-lookup"><span data-stu-id="784fa-153">How do I integrate Azure DevOps code with App Service?</span></span>

<span data-ttu-id="784fa-154">You have two options for using continuous deployment with Azure DevOps:</span><span class="sxs-lookup"><span data-stu-id="784fa-154">You have two options for using continuous deployment with Azure DevOps:</span></span>

*   <span data-ttu-id="784fa-155">Use a Git project.</span><span class="sxs-lookup"><span data-stu-id="784fa-155">Use a Git project.</span></span> <span data-ttu-id="784fa-156">Connect via App Service by using the deployment options for that repo.</span><span class="sxs-lookup"><span data-stu-id="784fa-156">Connect via App Service by using the deployment options for that repo.</span></span>
*   <span data-ttu-id="784fa-157">Use a Team Foundation Version Control (TFVC) project.</span><span class="sxs-lookup"><span data-stu-id="784fa-157">Use a Team Foundation Version Control (TFVC) project.</span></span> <span data-ttu-id="784fa-158">Deploy by using the build agent for App Service.</span><span class="sxs-lookup"><span data-stu-id="784fa-158">Deploy by using the build agent for App Service.</span></span>

<span data-ttu-id="784fa-159">Continuous code deployment for both these options depends on existing developer workflows and check-in procedures.</span><span class="sxs-lookup"><span data-stu-id="784fa-159">Continuous code deployment for both these options depends on existing developer workflows and check-in procedures.</span></span> <span data-ttu-id="784fa-160">For more information, see these articles:</span><span class="sxs-lookup"><span data-stu-id="784fa-160">For more information, see these articles:</span></span> 

*   [<span data-ttu-id="784fa-161">Implement continuous deployment of your app to an Azure website</span><span class="sxs-lookup"><span data-stu-id="784fa-161">Implement continuous deployment of your app to an Azure website</span></span>](https://www.visualstudio.com/docs/release/examples/azure/azure-web-apps-from-build-and-release-hubs)
*   [<span data-ttu-id="784fa-162">Set up an Azure DevOps organization so it can deploy to a web app</span><span class="sxs-lookup"><span data-stu-id="784fa-162">Set up an Azure DevOps organization so it can deploy to a web app</span></span>](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App)

## <a name="how-do-i-use-ftp-or-ftps-to-deploy-my-app-to-app-service"></a><span data-ttu-id="784fa-163">How do I use FTP or FTPS to deploy my app to App Service?</span><span class="sxs-lookup"><span data-stu-id="784fa-163">How do I use FTP or FTPS to deploy my app to App Service?</span></span>

<span data-ttu-id="784fa-164">For information about using FTP or FTPS to deploy your web app to App Service, see [Deploy your app to App Service by using FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="784fa-164">For information about using FTP or FTPS to deploy your web app to App Service, see [Deploy your app to App Service by using FTP/S](app-service-deploy-ftp.md).</span></span>
