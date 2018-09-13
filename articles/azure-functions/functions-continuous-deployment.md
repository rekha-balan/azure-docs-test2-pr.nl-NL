---
title: Continuous deployment for Azure Functions | Microsoft Docs
description: Use continuous deployment facilities of Azure App Service to publish your Azure Functions.
services: functions
documentationcenter: na
author: ggailey777
manager: jeconnoc
ms.assetid: 361daf37-598c-4703-8d78-c77dbef91643
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 09/25/2016
ms.author: glenga
ms.openlocfilehash: 7529d20535eedab92d164df5a0435efeda83fca2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44797698"
---
# <a name="continuous-deployment-for-azure-functions"></a><span data-ttu-id="bb819-103">Continuous deployment for Azure Functions</span><span class="sxs-lookup"><span data-stu-id="bb819-103">Continuous deployment for Azure Functions</span></span>
<span data-ttu-id="bb819-104">Azure Functions makes it easy to deploy your function app using App Service continuous integration.</span><span class="sxs-lookup"><span data-stu-id="bb819-104">Azure Functions makes it easy to deploy your function app using App Service continuous integration.</span></span> <span data-ttu-id="bb819-105">Functions integrates with BitBucket, Dropbox, GitHub, and Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="bb819-105">Functions integrates with BitBucket, Dropbox, GitHub, and Azure DevOps.</span></span> <span data-ttu-id="bb819-106">This enables a workflow where function code updates made by using one of these integrated services trigger deployment to Azure.</span><span class="sxs-lookup"><span data-stu-id="bb819-106">This enables a workflow where function code updates made by using one of these integrated services trigger deployment to Azure.</span></span> <span data-ttu-id="bb819-107">If you are new to Azure Functions, start with [Azure Functions Overview](functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bb819-107">If you are new to Azure Functions, start with [Azure Functions Overview](functions-overview.md).</span></span>

<span data-ttu-id="bb819-108">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span><span class="sxs-lookup"><span data-stu-id="bb819-108">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span> <span data-ttu-id="bb819-109">It also lets you maintain source control on your functions code.</span><span class="sxs-lookup"><span data-stu-id="bb819-109">It also lets you maintain source control on your functions code.</span></span> <span data-ttu-id="bb819-110">The following deployment sources are currently supported:</span><span class="sxs-lookup"><span data-stu-id="bb819-110">The following deployment sources are currently supported:</span></span>

* [<span data-ttu-id="bb819-111">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="bb819-111">Bitbucket</span></span>](https://bitbucket.org/)
* [<span data-ttu-id="bb819-112">Dropbox</span><span class="sxs-lookup"><span data-stu-id="bb819-112">Dropbox</span></span>](https://www.dropbox.com/)
* <span data-ttu-id="bb819-113">External repository (Git or Mercurial)</span><span class="sxs-lookup"><span data-stu-id="bb819-113">External repository (Git or Mercurial)</span></span>
* [<span data-ttu-id="bb819-114">Git local repository</span><span class="sxs-lookup"><span data-stu-id="bb819-114">Git local repository</span></span>](../app-service/app-service-deploy-local-git.md)
* [<span data-ttu-id="bb819-115">GitHub</span><span class="sxs-lookup"><span data-stu-id="bb819-115">GitHub</span></span>](https://github.com)
* [<span data-ttu-id="bb819-116">OneDrive</span><span class="sxs-lookup"><span data-stu-id="bb819-116">OneDrive</span></span>](https://onedrive.live.com/)
* [<span data-ttu-id="bb819-117">Azure DevOps Services</span><span class="sxs-lookup"><span data-stu-id="bb819-117">Azure DevOps Services</span></span>](https://www.visualstudio.com/team-services/)

<span data-ttu-id="bb819-118">Deployments are configured on a per-function app basis.</span><span class="sxs-lookup"><span data-stu-id="bb819-118">Deployments are configured on a per-function app basis.</span></span> <span data-ttu-id="bb819-119">After continuous deployment is enabled, access to function code in the portal is set to *read-only*.</span><span class="sxs-lookup"><span data-stu-id="bb819-119">After continuous deployment is enabled, access to function code in the portal is set to *read-only*.</span></span>

## <a name="continuous-deployment-requirements"></a><span data-ttu-id="bb819-120">Continuous deployment requirements</span><span class="sxs-lookup"><span data-stu-id="bb819-120">Continuous deployment requirements</span></span>

<span data-ttu-id="bb819-121">You must have your deployment source configured and your functions code in the deployment source before you set up continuous deployment.</span><span class="sxs-lookup"><span data-stu-id="bb819-121">You must have your deployment source configured and your functions code in the deployment source before you set up continuous deployment.</span></span> <span data-ttu-id="bb819-122">In a given function app deployment, each function lives in a named subdirectory, where the directory name is the name of the function.</span><span class="sxs-lookup"><span data-stu-id="bb819-122">In a given function app deployment, each function lives in a named subdirectory, where the directory name is the name of the function.</span></span>  

[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

<span data-ttu-id="bb819-123">To be able to deploy from Azure DevOps, you must first link your Azure DevOps organization with your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="bb819-123">To be able to deploy from Azure DevOps, you must first link your Azure DevOps organization with your Azure subscription.</span></span> <span data-ttu-id="bb819-124">For more information, see [Set up billing for your Azure DevOps organization](https://docs.microsoft.com/azure/devops/organizations/billing/set-up-billing-for-your-organization-vs?view=vsts#set-up-billing-via-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="bb819-124">For more information, see [Set up billing for your Azure DevOps organization](https://docs.microsoft.com/azure/devops/organizations/billing/set-up-billing-for-your-organization-vs?view=vsts#set-up-billing-via-the-azure-portal).</span></span>

## <a name="set-up-continuous-deployment"></a><span data-ttu-id="bb819-125">Set up continuous deployment</span><span class="sxs-lookup"><span data-stu-id="bb819-125">Set up continuous deployment</span></span>
<span data-ttu-id="bb819-126">Use this procedure to configure continuous deployment for an existing function app.</span><span class="sxs-lookup"><span data-stu-id="bb819-126">Use this procedure to configure continuous deployment for an existing function app.</span></span> <span data-ttu-id="bb819-127">These steps demonstrate integration with a GitHub repository, but similar steps apply for Azure DevOps or other deployment services.</span><span class="sxs-lookup"><span data-stu-id="bb819-127">These steps demonstrate integration with a GitHub repository, but similar steps apply for Azure DevOps or other deployment services.</span></span>

1. <span data-ttu-id="bb819-128">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span><span class="sxs-lookup"><span data-stu-id="bb819-128">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![Setup continuous deployment](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="bb819-130">Then in the **Deployments** blade click **Setup**.</span><span class="sxs-lookup"><span data-stu-id="bb819-130">Then in the **Deployments** blade click **Setup**.</span></span>
 
    ![Setup continuous deployment](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="bb819-132">In the **Deployment source** blade, click **Choose source**, then fill in the information for your chosen deployment source and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="bb819-132">In the **Deployment source** blade, click **Choose source**, then fill in the information for your chosen deployment source and click **OK**.</span></span>
   
    ![Choose deployment source](./media/functions-continuous-deployment/choose-deployment-source.png)

<span data-ttu-id="bb819-134">After continuous deployment is configured, all file changes in your deployment source are copied to the function app and a full site deployment is triggered.</span><span class="sxs-lookup"><span data-stu-id="bb819-134">After continuous deployment is configured, all file changes in your deployment source are copied to the function app and a full site deployment is triggered.</span></span> <span data-ttu-id="bb819-135">The site is redeployed when files in the source are updated.</span><span class="sxs-lookup"><span data-stu-id="bb819-135">The site is redeployed when files in the source are updated.</span></span>

## <a name="deployment-options"></a><span data-ttu-id="bb819-136">Deployment options</span><span class="sxs-lookup"><span data-stu-id="bb819-136">Deployment options</span></span>

<span data-ttu-id="bb819-137">The following are some typical deployment scenarios:</span><span class="sxs-lookup"><span data-stu-id="bb819-137">The following are some typical deployment scenarios:</span></span>

- [<span data-ttu-id="bb819-138">Create a staging deployment</span><span class="sxs-lookup"><span data-stu-id="bb819-138">Create a staging deployment</span></span>](#staging)
- [<span data-ttu-id="bb819-139">Move existing functions to continuous deployment</span><span class="sxs-lookup"><span data-stu-id="bb819-139">Move existing functions to continuous deployment</span></span>](#existing)

<a name="staging"></a>
### <a name="create-a-staging-deployment"></a><span data-ttu-id="bb819-140">Create a staging deployment</span><span class="sxs-lookup"><span data-stu-id="bb819-140">Create a staging deployment</span></span>

<span data-ttu-id="bb819-141">Function Apps doesn't yet support deployment slots.</span><span class="sxs-lookup"><span data-stu-id="bb819-141">Function Apps doesn't yet support deployment slots.</span></span> <span data-ttu-id="bb819-142">However, you can still manage separate staging and production deployments by using continuous integration.</span><span class="sxs-lookup"><span data-stu-id="bb819-142">However, you can still manage separate staging and production deployments by using continuous integration.</span></span>

<span data-ttu-id="bb819-143">The process to configure and work with a staging deployment looks generally like this:</span><span class="sxs-lookup"><span data-stu-id="bb819-143">The process to configure and work with a staging deployment looks generally like this:</span></span>

1. <span data-ttu-id="bb819-144">Create two function apps in your subscription, one for the production code and one for staging.</span><span class="sxs-lookup"><span data-stu-id="bb819-144">Create two function apps in your subscription, one for the production code and one for staging.</span></span> 

2. <span data-ttu-id="bb819-145">Create a deployment source, if you don't already have one.</span><span class="sxs-lookup"><span data-stu-id="bb819-145">Create a deployment source, if you don't already have one.</span></span> <span data-ttu-id="bb819-146">This example uses [GitHub].</span><span class="sxs-lookup"><span data-stu-id="bb819-146">This example uses [GitHub].</span></span>

3. <span data-ttu-id="bb819-147">For your production function app, complete the preceding steps in **Set up continuous deployment** and set the deployment branch to the master branch of your GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="bb819-147">For your production function app, complete the preceding steps in **Set up continuous deployment** and set the deployment branch to the master branch of your GitHub repository.</span></span>
   
    ![Choose deployment branch](./media/functions-continuous-deployment/choose-deployment-branch.png)

4. <span data-ttu-id="bb819-149">Repeat this step for the staging function app, but choose the staging branch instead in your GitHub repo.</span><span class="sxs-lookup"><span data-stu-id="bb819-149">Repeat this step for the staging function app, but choose the staging branch instead in your GitHub repo.</span></span> <span data-ttu-id="bb819-150">If your deployment source doesn't support branching, use a different folder.</span><span class="sxs-lookup"><span data-stu-id="bb819-150">If your deployment source doesn't support branching, use a different folder.</span></span>
    
5. <span data-ttu-id="bb819-151">Make updates to your code in the staging branch or folder, then verify that those changes are reflected in the staging deployment.</span><span class="sxs-lookup"><span data-stu-id="bb819-151">Make updates to your code in the staging branch or folder, then verify that those changes are reflected in the staging deployment.</span></span>

6. <span data-ttu-id="bb819-152">After testing, merge changes from the staging branch into the master branch.</span><span class="sxs-lookup"><span data-stu-id="bb819-152">After testing, merge changes from the staging branch into the master branch.</span></span> <span data-ttu-id="bb819-153">This merge triggers deployment to the production function app.</span><span class="sxs-lookup"><span data-stu-id="bb819-153">This merge triggers deployment to the production function app.</span></span> <span data-ttu-id="bb819-154">If your deployment source doesn't support branches, overwrite the files in the production folder with the files from the staging folder.</span><span class="sxs-lookup"><span data-stu-id="bb819-154">If your deployment source doesn't support branches, overwrite the files in the production folder with the files from the staging folder.</span></span>

<a name="existing"></a>
### <a name="move-existing-functions-to-continuous-deployment"></a><span data-ttu-id="bb819-155">Move existing functions to continuous deployment</span><span class="sxs-lookup"><span data-stu-id="bb819-155">Move existing functions to continuous deployment</span></span>
<span data-ttu-id="bb819-156">When you have existing functions that you have created and maintained in the portal, you need to download your existing function code files using FTP or the local Git repository before you can set up continuous deployment as described above.</span><span class="sxs-lookup"><span data-stu-id="bb819-156">When you have existing functions that you have created and maintained in the portal, you need to download your existing function code files using FTP or the local Git repository before you can set up continuous deployment as described above.</span></span> <span data-ttu-id="bb819-157">You can do this in the App Service settings for your function app.</span><span class="sxs-lookup"><span data-stu-id="bb819-157">You can do this in the App Service settings for your function app.</span></span> <span data-ttu-id="bb819-158">After your files are downloaded, you can upload them to your chosen continuous deployment source.</span><span class="sxs-lookup"><span data-stu-id="bb819-158">After your files are downloaded, you can upload them to your chosen continuous deployment source.</span></span>

> [!NOTE]
> <span data-ttu-id="bb819-159">After you configure continuous integration, you will no longer be able to edit your source files in the Functions portal.</span><span class="sxs-lookup"><span data-stu-id="bb819-159">After you configure continuous integration, you will no longer be able to edit your source files in the Functions portal.</span></span>

- [<span data-ttu-id="bb819-160">How to: Configure deployment credentials</span><span class="sxs-lookup"><span data-stu-id="bb819-160">How to: Configure deployment credentials</span></span>](#credentials)
- [<span data-ttu-id="bb819-161">How to: Download files using FTP</span><span class="sxs-lookup"><span data-stu-id="bb819-161">How to: Download files using FTP</span></span>](#downftp)
- [<span data-ttu-id="bb819-162">How to: Download files using the local Git repository</span><span class="sxs-lookup"><span data-stu-id="bb819-162">How to: Download files using the local Git repository</span></span>](#downgit)

<a name="credentials"></a>
#### <a name="how-to-configure-deployment-credentials"></a><span data-ttu-id="bb819-163">How to: Configure deployment credentials</span><span class="sxs-lookup"><span data-stu-id="bb819-163">How to: Configure deployment credentials</span></span>
<span data-ttu-id="bb819-164">Before you can download files from your function app with FTP or local Git repository, you must configure your credentials to access the site.</span><span class="sxs-lookup"><span data-stu-id="bb819-164">Before you can download files from your function app with FTP or local Git repository, you must configure your credentials to access the site.</span></span> <span data-ttu-id="bb819-165">Credentials are set at the Function app level.</span><span class="sxs-lookup"><span data-stu-id="bb819-165">Credentials are set at the Function app level.</span></span> <span data-ttu-id="bb819-166">Use the following steps to set deployment credentials in the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="bb819-166">Use the following steps to set deployment credentials in the Azure portal:</span></span>

1. <span data-ttu-id="bb819-167">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment credentials**.</span><span class="sxs-lookup"><span data-stu-id="bb819-167">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment credentials**.</span></span>
   
    ![Set local deployment credentials](./media/functions-continuous-deployment/setup-deployment-credentials.png)

2. <span data-ttu-id="bb819-169">Type in a username and password, then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="bb819-169">Type in a username and password, then click **Save**.</span></span> <span data-ttu-id="bb819-170">You can now use these credentials to access your function app from FTP or the built-in Git repo.</span><span class="sxs-lookup"><span data-stu-id="bb819-170">You can now use these credentials to access your function app from FTP or the built-in Git repo.</span></span>

<a name="downftp"></a>
#### <a name="how-to-download-files-using-ftp"></a><span data-ttu-id="bb819-171">How to: Download files using FTP</span><span class="sxs-lookup"><span data-stu-id="bb819-171">How to: Download files using FTP</span></span>

1. <span data-ttu-id="bb819-172">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Properties**, then copy the values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span><span class="sxs-lookup"><span data-stu-id="bb819-172">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Properties**, then copy the values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span>  

    <span data-ttu-id="bb819-173">**FTP/Deployment User** must be entered as displayed in the portal, including the app name, to provide proper context for the FTP server.</span><span class="sxs-lookup"><span data-stu-id="bb819-173">**FTP/Deployment User** must be entered as displayed in the portal, including the app name, to provide proper context for the FTP server.</span></span>
   
    ![Get your deployment information](./media/functions-continuous-deployment/get-deployment-credentials.png)

2. <span data-ttu-id="bb819-175">From your FTP client, use the connection information you gathered to connect to your app and download the source files for your functions.</span><span class="sxs-lookup"><span data-stu-id="bb819-175">From your FTP client, use the connection information you gathered to connect to your app and download the source files for your functions.</span></span>

<a name="downgit"></a>
#### <a name="how-to-download-files-using-a-local-git-repository"></a><span data-ttu-id="bb819-176">How to: Download files using a local Git repository</span><span class="sxs-lookup"><span data-stu-id="bb819-176">How to: Download files using a local Git repository</span></span>

1. <span data-ttu-id="bb819-177">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span><span class="sxs-lookup"><span data-stu-id="bb819-177">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![Setup continuous deployment](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="bb819-179">Then in the **Deployments** blade click **Setup**.</span><span class="sxs-lookup"><span data-stu-id="bb819-179">Then in the **Deployments** blade click **Setup**.</span></span>
 
    ![Setup continuous deployment](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="bb819-181">In the **Deployment source** blade, click **Local Git repository** and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="bb819-181">In the **Deployment source** blade, click **Local Git repository** and then click **OK**.</span></span>

3. <span data-ttu-id="bb819-182">In **Platform features**, click **Properties** and note the value of Git URL.</span><span class="sxs-lookup"><span data-stu-id="bb819-182">In **Platform features**, click **Properties** and note the value of Git URL.</span></span> 
   
    ![Setup continuous deployment](./media/functions-continuous-deployment/get-local-git-deployment-url.png)

4. <span data-ttu-id="bb819-184">Clone the repository on your local machine using a Git-aware command prompt or your favorite Git tool.</span><span class="sxs-lookup"><span data-stu-id="bb819-184">Clone the repository on your local machine using a Git-aware command prompt or your favorite Git tool.</span></span> <span data-ttu-id="bb819-185">The Git clone command looks like this:</span><span class="sxs-lookup"><span data-stu-id="bb819-185">The Git clone command looks like this:</span></span>
   
        git clone https://username@my-function-app.scm.azurewebsites.net:443/my-function-app.git

5. <span data-ttu-id="bb819-186">Fetch files from your function app to the clone on your local computer, as in the following example:</span><span class="sxs-lookup"><span data-stu-id="bb819-186">Fetch files from your function app to the clone on your local computer, as in the following example:</span></span>
   
        git pull origin master
   
    <span data-ttu-id="bb819-187">If requested, supply your [configured deployment credentials](#credentials).</span><span class="sxs-lookup"><span data-stu-id="bb819-187">If requested, supply your [configured deployment credentials](#credentials).</span></span>  

[GitHub]: https://github.com/

## <a name="next-steps"></a><span data-ttu-id="bb819-189">Next steps</span><span class="sxs-lookup"><span data-stu-id="bb819-189">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bb819-190">Best Practices for Azure Functions</span><span class="sxs-lookup"><span data-stu-id="bb819-190">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
