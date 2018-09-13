---
title: Continuous deployment for Azure Functions | Microsoft Docs
description: Use continuous deployment facilities of Azure App Service to publish your Azure Functions.
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: ''
tags: ''
ms.assetid: 361daf37-598c-4703-8d78-c77dbef91643
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/25/2016
ms.author: glenga
ms.openlocfilehash: f385bffcb7567a7dd57821a4b32403b1005e745d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551139"
---
# <a name="continuous-deployment-for-azure-functions"></a><span data-ttu-id="32f6e-103">Continuous deployment for Azure Functions</span><span class="sxs-lookup"><span data-stu-id="32f6e-103">Continuous deployment for Azure Functions</span></span>
<span data-ttu-id="32f6e-104">Azure Functions makes it easy to configure continuous deployment for your function app.</span><span class="sxs-lookup"><span data-stu-id="32f6e-104">Azure Functions makes it easy to configure continuous deployment for your function app.</span></span> <span data-ttu-id="32f6e-105">Functions uses Azure App Service integration with BitBucket, Dropbox, GitHub, and Visual Studio Team Services (VSTS) to enable a continuous deployment workflow where Azure pulls updates to your functions code when they are published to one of these services.</span><span class="sxs-lookup"><span data-stu-id="32f6e-105">Functions uses Azure App Service integration with BitBucket, Dropbox, GitHub, and Visual Studio Team Services (VSTS) to enable a continuous deployment workflow where Azure pulls updates to your functions code when they are published to one of these services.</span></span> <span data-ttu-id="32f6e-106">If you are new to Azure Functions, start with [Azure Functions Overview](functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="32f6e-106">If you are new to Azure Functions, start with [Azure Functions Overview](functions-overview.md).</span></span>

<span data-ttu-id="32f6e-107">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span><span class="sxs-lookup"><span data-stu-id="32f6e-107">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span> <span data-ttu-id="32f6e-108">It also lets you maintain source control on your functions code.</span><span class="sxs-lookup"><span data-stu-id="32f6e-108">It also lets you maintain source control on your functions code.</span></span> <span data-ttu-id="32f6e-109">The following deployment sources are currently supported:</span><span class="sxs-lookup"><span data-stu-id="32f6e-109">The following deployment sources are currently supported:</span></span>

* [<span data-ttu-id="32f6e-110">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="32f6e-110">Bitbucket</span></span>](https://bitbucket.org/)
* [<span data-ttu-id="32f6e-111">Dropbox</span><span class="sxs-lookup"><span data-stu-id="32f6e-111">Dropbox</span></span>](https://www.dropbox.com/)
* [<span data-ttu-id="32f6e-112">Git local repo</span><span class="sxs-lookup"><span data-stu-id="32f6e-112">Git local repo</span></span>](../app-service-web/app-service-deploy-local-git.md)
* <span data-ttu-id="32f6e-113">Git external repo</span><span class="sxs-lookup"><span data-stu-id="32f6e-113">Git external repo</span></span>
* <span data-ttu-id="32f6e-114">[GitHub]</span><span class="sxs-lookup"><span data-stu-id="32f6e-114">[GitHub]</span></span>
* <span data-ttu-id="32f6e-115">Mercurial external repo</span><span class="sxs-lookup"><span data-stu-id="32f6e-115">Mercurial external repo</span></span>
* [<span data-ttu-id="32f6e-116">OneDrive</span><span class="sxs-lookup"><span data-stu-id="32f6e-116">OneDrive</span></span>](https://onedrive.live.com/)
* [<span data-ttu-id="32f6e-117">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="32f6e-117">Visual Studio Team Services</span></span>](https://www.visualstudio.com/team-services/)

<span data-ttu-id="32f6e-118">Deployments are configured on a per-function-app basis.</span><span class="sxs-lookup"><span data-stu-id="32f6e-118">Deployments are configured on a per-function-app basis.</span></span> <span data-ttu-id="32f6e-119">After continuous deployment is enabled, access to function code in the portal is set to *read-only*.</span><span class="sxs-lookup"><span data-stu-id="32f6e-119">After continuous deployment is enabled, access to function code in the portal is set to *read-only*.</span></span>

## <a name="continuous-deployment-requirements"></a><span data-ttu-id="32f6e-120">Continuous deployment requirements</span><span class="sxs-lookup"><span data-stu-id="32f6e-120">Continuous deployment requirements</span></span>

<span data-ttu-id="32f6e-121">You must have your deployment source configured and your functions code in the deployment source before you set-up continuous deployment.</span><span class="sxs-lookup"><span data-stu-id="32f6e-121">You must have your deployment source configured and your functions code in the deployment source before you set-up continuous deployment.</span></span> <span data-ttu-id="32f6e-122">In a given function app deployment, each function lives in a named subdirectory, where the directory name is the name of the function.</span><span class="sxs-lookup"><span data-stu-id="32f6e-122">In a given function app deployment, each function lives in a named subdirectory, where the directory name is the name of the function.</span></span> <span data-ttu-id="32f6e-123">This folder structure is essentially your site code.</span><span class="sxs-lookup"><span data-stu-id="32f6e-123">This folder structure is essentially your site code.</span></span> 

[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

## <a name="set-up-continuous-deployment"></a><span data-ttu-id="32f6e-124">Set up continuous deployment</span><span class="sxs-lookup"><span data-stu-id="32f6e-124">Set up continuous deployment</span></span>
<span data-ttu-id="32f6e-125">Use the following procedure to configure continuous deployment for an existing function app:</span><span class="sxs-lookup"><span data-stu-id="32f6e-125">Use the following procedure to configure continuous deployment for an existing function app:</span></span>

1. <span data-ttu-id="32f6e-126">In your function app in the [Azure Functions portal](https://functions.azure.com/signin), click **Function app settings** > **Configure continuous integration** > **Setup**.</span><span class="sxs-lookup"><span data-stu-id="32f6e-126">In your function app in the [Azure Functions portal](https://functions.azure.com/signin), click **Function app settings** > **Configure continuous integration** > **Setup**.</span></span>
   
    ![Setup continuous deployment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-continuous-deployment/setup-deployment.png)
   
    ![Setup continuous deployment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-continuous-deployment/setup-deployment-1.png)
   
    <span data-ttu-id="32f6e-129">You can also get to the Deployments blade from the Functions quickstart by clicking **Start from source control**.</span><span class="sxs-lookup"><span data-stu-id="32f6e-129">You can also get to the Deployments blade from the Functions quickstart by clicking **Start from source control**.</span></span>
2. <span data-ttu-id="32f6e-130">In the **Deployment source** blade, click **Choose source**, then fill-in the information for your chosen deployment source and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="32f6e-130">In the **Deployment source** blade, click **Choose source**, then fill-in the information for your chosen deployment source and click **OK**.</span></span>
   
    ![Choose deployment source](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-continuous-deployment/choose-deployment-source.png)

<span data-ttu-id="32f6e-132">After continuous deployment is configured, all changes files in your deployment source are copied to the function app and a full site deployment is triggered.</span><span class="sxs-lookup"><span data-stu-id="32f6e-132">After continuous deployment is configured, all changes files in your deployment source are copied to the function app and a full site deployment is triggered.</span></span> <span data-ttu-id="32f6e-133">The site is redeployed when files in the source are updated.</span><span class="sxs-lookup"><span data-stu-id="32f6e-133">The site is redeployed when files in the source are updated.</span></span>

## <a name="deployment-options"></a><span data-ttu-id="32f6e-134">Deployment options</span><span class="sxs-lookup"><span data-stu-id="32f6e-134">Deployment options</span></span>

<span data-ttu-id="32f6e-135">The following are some typical deployment scenarios:</span><span class="sxs-lookup"><span data-stu-id="32f6e-135">The following are some typical deployment scenarios:</span></span>

- [<span data-ttu-id="32f6e-136">Create a staging deployment</span><span class="sxs-lookup"><span data-stu-id="32f6e-136">Create a staging deployment</span></span>](#staging)
- [<span data-ttu-id="32f6e-137">Move existing functions to continuous deployment</span><span class="sxs-lookup"><span data-stu-id="32f6e-137">Move existing functions to continuous deployment</span></span>](#existing)

<a name="staging"></a>
### <a name="create-a-staging-deployment"></a><span data-ttu-id="32f6e-138">Create a staging deployment</span><span class="sxs-lookup"><span data-stu-id="32f6e-138">Create a staging deployment</span></span>

<span data-ttu-id="32f6e-139">Function Apps doesn't yet support deployment slots.</span><span class="sxs-lookup"><span data-stu-id="32f6e-139">Function Apps doesn't yet support deployment slots.</span></span> <span data-ttu-id="32f6e-140">However, you can still manage separate staging and production deployments by using continuous integration.</span><span class="sxs-lookup"><span data-stu-id="32f6e-140">However, you can still manage separate staging and production deployments by using continuous integration.</span></span>

<span data-ttu-id="32f6e-141">The process to configure and work with a staging deployment looks generally like this:</span><span class="sxs-lookup"><span data-stu-id="32f6e-141">The process to configure and work with a staging deployment looks generally like this:</span></span>

1. <span data-ttu-id="32f6e-142">Create two function apps in your subscription, one for the production code and one for staging.</span><span class="sxs-lookup"><span data-stu-id="32f6e-142">Create two function apps in your subscription, one for the production code and one for staging.</span></span> 

2. <span data-ttu-id="32f6e-143">Create a deployment source, if you don't already have one.</span><span class="sxs-lookup"><span data-stu-id="32f6e-143">Create a deployment source, if you don't already have one.</span></span> <span data-ttu-id="32f6e-144">This example uses [GitHub].</span><span class="sxs-lookup"><span data-stu-id="32f6e-144">This example uses [GitHub].</span></span>

3. <span data-ttu-id="32f6e-145">For your production function app, complete the above steps in **Set up continuous deployment** and set the deployment branch to the master branch of your GitHub repo.</span><span class="sxs-lookup"><span data-stu-id="32f6e-145">For your production function app, complete the above steps in **Set up continuous deployment** and set the deployment branch to the master branch of your GitHub repo.</span></span>
   
    ![Choose deployment branch](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-continuous-deployment/choose-deployment-branch.png)

4. <span data-ttu-id="32f6e-147">Repeat this step for the staging function app, but choose the staging branch instead in your GitHub repo.</span><span class="sxs-lookup"><span data-stu-id="32f6e-147">Repeat this step for the staging function app, but choose the staging branch instead in your GitHub repo.</span></span> <span data-ttu-id="32f6e-148">If your deployment source doesn't support branching, use a different folder.</span><span class="sxs-lookup"><span data-stu-id="32f6e-148">If your deployment source doesn't support branching, use a different folder.</span></span>

5. <span data-ttu-id="32f6e-149">Make updates to your code in the staging branch or folder, then verify that those changes are reflected in the staging deployment.</span><span class="sxs-lookup"><span data-stu-id="32f6e-149">Make updates to your code in the staging branch or folder, then verify that those changes are reflected in the staging deployment.</span></span>

6. <span data-ttu-id="32f6e-150">After testing, merge changes from the staging branch into the master branch.</span><span class="sxs-lookup"><span data-stu-id="32f6e-150">After testing, merge changes from the staging branch into the master branch.</span></span> <span data-ttu-id="32f6e-151">This will trigger deployment to the production function app.</span><span class="sxs-lookup"><span data-stu-id="32f6e-151">This will trigger deployment to the production function app.</span></span> <span data-ttu-id="32f6e-152">If your deployment source doesn't support branches, overwrite the files in the production folder with the files from the staging folder.</span><span class="sxs-lookup"><span data-stu-id="32f6e-152">If your deployment source doesn't support branches, overwrite the files in the production folder with the files from the staging folder.</span></span>

<a name="existing"></a>
### <a name="move-existing-functions-to-continuous-deployment"></a><span data-ttu-id="32f6e-153">Move existing functions to continuous deployment</span><span class="sxs-lookup"><span data-stu-id="32f6e-153">Move existing functions to continuous deployment</span></span>
<span data-ttu-id="32f6e-154">When you have existing functions that you have created and maintained in the portal, you need to download your existing function code files using FTP or the local Git repository before you can set up continuous deployment as described above.</span><span class="sxs-lookup"><span data-stu-id="32f6e-154">When you have existing functions that you have created and maintained in the portal, you need to download your existing function code files using FTP or the local Git repository before you can set up continuous deployment as described above.</span></span> <span data-ttu-id="32f6e-155">You can do this in the App Service settings for your function app.</span><span class="sxs-lookup"><span data-stu-id="32f6e-155">You can do this in the App Service settings for your function app.</span></span> <span data-ttu-id="32f6e-156">After your files are downloaded, you can upload them to your chosen continuous deployment source.</span><span class="sxs-lookup"><span data-stu-id="32f6e-156">After your files are downloaded, you can upload them to your chosen continuous deployment source.</span></span>

> [!NOTE]
> <span data-ttu-id="32f6e-157">After you configure continuous integration, you will no longer be able to edit your source files in the Functions portal.</span><span class="sxs-lookup"><span data-stu-id="32f6e-157">After you configure continuous integration, you will no longer be able to edit your source files in the Functions portal.</span></span>

- [<span data-ttu-id="32f6e-158">How to: Configure deployment credentials</span><span class="sxs-lookup"><span data-stu-id="32f6e-158">How to: Configure deployment credentials</span></span>](#credentials)
- [<span data-ttu-id="32f6e-159">How to: Download files using FTP</span><span class="sxs-lookup"><span data-stu-id="32f6e-159">How to: Download files using FTP</span></span>](#downftp)
- [<span data-ttu-id="32f6e-160">How to: download files using the local Git repository</span><span class="sxs-lookup"><span data-stu-id="32f6e-160">How to: download files using the local Git repository</span></span>](#downgit)

<a name="credentials"></a>
#### <a name="how-to-configure-deployment-credentials"></a><span data-ttu-id="32f6e-161">How to: Configure deployment credentials</span><span class="sxs-lookup"><span data-stu-id="32f6e-161">How to: Configure deployment credentials</span></span>
<span data-ttu-id="32f6e-162">Before you can download files from your function app with FTP or local Git repository, you must configure your credentials to access the site, which you can do from the portal.</span><span class="sxs-lookup"><span data-stu-id="32f6e-162">Before you can download files from your function app with FTP or local Git repository, you must configure your credentials to access the site, which you can do from the portal.</span></span> <span data-ttu-id="32f6e-163">Credentials are set at the Function app level.</span><span class="sxs-lookup"><span data-stu-id="32f6e-163">Credentials are set at the Function app level.</span></span>

1. <span data-ttu-id="32f6e-164">In your function app in the [Azure Functions portal](https://functions.azure.com/signin), click **Function app settings** > **Go to App Service settings** > **Deployment credentials**.</span><span class="sxs-lookup"><span data-stu-id="32f6e-164">In your function app in the [Azure Functions portal](https://functions.azure.com/signin), click **Function app settings** > **Go to App Service settings** > **Deployment credentials**.</span></span>
   
    ![Set local deployment credentials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-continuous-deployment/setup-deployment-credentials.png)

2. <span data-ttu-id="32f6e-166">Type in a username and password, then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="32f6e-166">Type in a username and password, then click **Save**.</span></span> <span data-ttu-id="32f6e-167">You can now use these credentials to access your function app from FTP or the built-in Git repo.</span><span class="sxs-lookup"><span data-stu-id="32f6e-167">You can now use these credentials to access your function app from FTP or the built-in Git repo.</span></span>

<a name="downftp"></a>
#### <a name="how-to-download-files-using-ftp"></a><span data-ttu-id="32f6e-168">How to: Download files using FTP</span><span class="sxs-lookup"><span data-stu-id="32f6e-168">How to: Download files using FTP</span></span>

1. <span data-ttu-id="32f6e-169">In your function app in the [Azure Functions portal](https://functions.azure.com/signin), click **Function app settings** > **Go to App Service settings** > **Properties** and copy the values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span><span class="sxs-lookup"><span data-stu-id="32f6e-169">In your function app in the [Azure Functions portal](https://functions.azure.com/signin), click **Function app settings** > **Go to App Service settings** > **Properties** and copy the values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span>  

    <span data-ttu-id="32f6e-170">**FTP/Deployment User** must be entered as displayed in the portal, including the app name, in order to provide proper context for the FTP server.</span><span class="sxs-lookup"><span data-stu-id="32f6e-170">**FTP/Deployment User** must be entered as displayed in the portal, including the app name, in order to provide proper context for the FTP server.</span></span>
   
    ![Get your deployment information](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-continuous-deployment/get-deployment-credentials.png)

2. <span data-ttu-id="32f6e-172">From your FTP client, use the connection information you gathered to connect to your app and download the source files for your functions.</span><span class="sxs-lookup"><span data-stu-id="32f6e-172">From your FTP client, use the connection information you gathered to connect to your app and download the source files for your functions.</span></span>

<a name="downgit"></a>
#### <a name="how-to-download-files-using-the-local-git-repository"></a><span data-ttu-id="32f6e-173">How to: download files using the local Git repository</span><span class="sxs-lookup"><span data-stu-id="32f6e-173">How to: download files using the local Git repository</span></span>

1. <span data-ttu-id="32f6e-174">In your function app in the [Azure Functions portal](https://functions.azure.com/signin), click **Function app settings** > **Configure continuous integration** > **Setup**.</span><span class="sxs-lookup"><span data-stu-id="32f6e-174">In your function app in the [Azure Functions portal](https://functions.azure.com/signin), click **Function app settings** > **Configure continuous integration** > **Setup**.</span></span>

2. <span data-ttu-id="32f6e-175">In the Deployments blade, click **Choose source**, **Local Git repository**, then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="32f6e-175">In the Deployments blade, click **Choose source**, **Local Git repository**, then click **OK**.</span></span>

3. <span data-ttu-id="32f6e-176">Click **Go to App Service settings** > **Properties** and note the value of Git URL.</span><span class="sxs-lookup"><span data-stu-id="32f6e-176">Click **Go to App Service settings** > **Properties** and note the value of Git URL.</span></span> 
   
    ![Setup continuous deployment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-continuous-deployment/get-local-git-deployment-url.png)

4. <span data-ttu-id="32f6e-178">Clone the repo on your local machine using a Git-aware command line or your favorite Git tool.</span><span class="sxs-lookup"><span data-stu-id="32f6e-178">Clone the repo on your local machine using a Git-aware command line or your favorite Git tool.</span></span> <span data-ttu-id="32f6e-179">The Git clone command looks like the following:</span><span class="sxs-lookup"><span data-stu-id="32f6e-179">The Git clone command looks like the following:</span></span>
   
        git clone https://username@my-function-app.scm.azurewebsites.net:443/my-function-app.git

5. <span data-ttu-id="32f6e-180">Fetch files from your function app to the clone on your local computer, as in the following example:</span><span class="sxs-lookup"><span data-stu-id="32f6e-180">Fetch files from your function app to the clone on your local computer, as in the following example:</span></span>
   
        git pull origin master
   
    <span data-ttu-id="32f6e-181">If requested, supply the username and password for your function app deployment.</span><span class="sxs-lookup"><span data-stu-id="32f6e-181">If requested, supply the username and password for your function app deployment.</span></span>  

[GitHub]: https://github.com/







