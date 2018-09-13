---
title: Local Git Deployment to Azure App Service
description: Learn how to enable local Git deployment to Azure App Service.
services: app-service
documentationcenter: ''
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: ac50a623-c4b8-4dfd-96b2-a09420770063
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 53b430205d56bae6bbd1b569946b6d76b98bfbbe
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553760"
---
# <a name="local-git-deployment-to-azure-app-service"></a><span data-ttu-id="aaaf8-103">Local Git Deployment to Azure App Service</span><span class="sxs-lookup"><span data-stu-id="aaaf8-103">Local Git Deployment to Azure App Service</span></span>
<span data-ttu-id="aaaf8-104">This tutorial shows you how to deploy your app to [Azure App Service] from a Git repository on your local computer.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-104">This tutorial shows you how to deploy your app to [Azure App Service] from a Git repository on your local computer.</span></span> <span data-ttu-id="aaaf8-105">App Service supports this approach with the **Local Git** deployment option in the [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="aaaf8-105">App Service supports this approach with the **Local Git** deployment option in the [Azure Portal].</span></span>  
<span data-ttu-id="aaaf8-106">Many of the Git commands described in this article are performed automatically when creating an App Service app using the [Azure Command-Line Interface] as described [here](app-service-web-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="aaaf8-106">Many of the Git commands described in this article are performed automatically when creating an App Service app using the [Azure Command-Line Interface] as described [here](app-service-web-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aaaf8-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="aaaf8-107">Prerequisites</span></span>
<span data-ttu-id="aaaf8-108">To complete this tutorial, you need:</span><span class="sxs-lookup"><span data-stu-id="aaaf8-108">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="aaaf8-109">Git.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-109">Git.</span></span> <span data-ttu-id="aaaf8-110">You can download the installation binary [here](http://www.git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="aaaf8-110">You can download the installation binary [here](http://www.git-scm.com/downloads).</span></span>  
* <span data-ttu-id="aaaf8-111">Basic knowledge of Git.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-111">Basic knowledge of Git.</span></span>
* <span data-ttu-id="aaaf8-112">A Microsoft Azure account.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-112">A Microsoft Azure account.</span></span> <span data-ttu-id="aaaf8-113">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).</span><span class="sxs-lookup"><span data-stu-id="aaaf8-113">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).</span></span>

> [!NOTE]
> <span data-ttu-id="aaaf8-114">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter app in App Service.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-114">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter app in App Service.</span></span> <span data-ttu-id="aaaf8-115">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-115">No credit cards required; no commitments.</span></span>  
> 
> 

## <a name="Step1"></a><span data-ttu-id="aaaf8-116">Step 1: Create a local repository</span><span class="sxs-lookup"><span data-stu-id="aaaf8-116">Step 1: Create a local repository</span></span>
<span data-ttu-id="aaaf8-117">Perform the following tasks to create a new Git repository.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-117">Perform the following tasks to create a new Git repository.</span></span>

1. <span data-ttu-id="aaaf8-118">Start a command-line tool, such as **GitBash** (Windows) or **Bash** (Unix Shell).</span><span class="sxs-lookup"><span data-stu-id="aaaf8-118">Start a command-line tool, such as **GitBash** (Windows) or **Bash** (Unix Shell).</span></span> <span data-ttu-id="aaaf8-119">On OS X systems you can access the command-line through the **Terminal** application.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-119">On OS X systems you can access the command-line through the **Terminal** application.</span></span>
2. <span data-ttu-id="aaaf8-120">Navigate to the directory where the content to deploy would be located.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-120">Navigate to the directory where the content to deploy would be located.</span></span>
3. <span data-ttu-id="aaaf8-121">Use the following command to initialize a new Git repository:</span><span class="sxs-lookup"><span data-stu-id="aaaf8-121">Use the following command to initialize a new Git repository:</span></span>
   
        git init

## <a name="Step2"></a><span data-ttu-id="aaaf8-122">Step 2: Commit your content</span><span class="sxs-lookup"><span data-stu-id="aaaf8-122">Step 2: Commit your content</span></span>
<span data-ttu-id="aaaf8-123">App Service supports applications created in a variety of programming languages.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-123">App Service supports applications created in a variety of programming languages.</span></span> 

1. <span data-ttu-id="aaaf8-124">If your repository already includes content skip this point and move to point 2 below.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-124">If your repository already includes content skip this point and move to point 2 below.</span></span> <span data-ttu-id="aaaf8-125">If your repository does not already include content simply populate with a static .html file as follows:</span><span class="sxs-lookup"><span data-stu-id="aaaf8-125">If your repository does not already include content simply populate with a static .html file as follows:</span></span> 
   
   * <span data-ttu-id="aaaf8-126">Using a text editor, create a new file named **index.html** at the root of the Git repository</span><span class="sxs-lookup"><span data-stu-id="aaaf8-126">Using a text editor, create a new file named **index.html** at the root of the Git repository</span></span>
   * <span data-ttu-id="aaaf8-127">Add the following text as the contents for the index.html file and save it: *Hello Git!*</span><span class="sxs-lookup"><span data-stu-id="aaaf8-127">Add the following text as the contents for the index.html file and save it: *Hello Git!*</span></span>
2. <span data-ttu-id="aaaf8-128">From the command-line, verify that you are under the root of your Git repository.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-128">From the command-line, verify that you are under the root of your Git repository.</span></span> <span data-ttu-id="aaaf8-129">Then use the following command to add files to your repository:</span><span class="sxs-lookup"><span data-stu-id="aaaf8-129">Then use the following command to add files to your repository:</span></span>
   
        git add -A 
3. <span data-ttu-id="aaaf8-130">Next, commit the changes to the repository by using the following command:</span><span class="sxs-lookup"><span data-stu-id="aaaf8-130">Next, commit the changes to the repository by using the following command:</span></span>
   
        git commit -m "Hello Azure App Service"

## <a name="Step3"></a><span data-ttu-id="aaaf8-131">Step 3: Enable the App Service app repository</span><span class="sxs-lookup"><span data-stu-id="aaaf8-131">Step 3: Enable the App Service app repository</span></span>
<span data-ttu-id="aaaf8-132">Perform the following steps to enable a Git repository for your App Service app.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-132">Perform the following steps to enable a Git repository for your App Service app.</span></span>

1. <span data-ttu-id="aaaf8-133">Log in to the [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="aaaf8-133">Log in to the [Azure Portal].</span></span>
2. <span data-ttu-id="aaaf8-134">In your App Service app's blade, click **Settings > Deployment source**.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-134">In your App Service app's blade, click **Settings > Deployment source**.</span></span> <span data-ttu-id="aaaf8-135">Click **Choose source**, then click **Local Git Repository**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-135">Click **Choose source**, then click **Local Git Repository**, and then click **OK**.</span></span>  
   
    ![Local Git Repository](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-deploy-local-git/local_git_selection.png)
3. <span data-ttu-id="aaaf8-137">If this is your first time setting up a repository in Azure, you need to create login credentials for it.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-137">If this is your first time setting up a repository in Azure, you need to create login credentials for it.</span></span> <span data-ttu-id="aaaf8-138">You will use them to log into the Azure repository and push changes from your local Git repository.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-138">You will use them to log into the Azure repository and push changes from your local Git repository.</span></span> <span data-ttu-id="aaaf8-139">From your app's blade, click **Settings > Deployment credentials**, then configure your deployment username and password.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-139">From your app's blade, click **Settings > Deployment credentials**, then configure your deployment username and password.</span></span> <span data-ttu-id="aaaf8-140">When you're done, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-140">When you're done, click **Save**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-deploy-local-git/deployment_credentials.png)

## <a name="Step4"></a><span data-ttu-id="aaaf8-141">Step 4: Deploy your project</span><span class="sxs-lookup"><span data-stu-id="aaaf8-141">Step 4: Deploy your project</span></span>
<span data-ttu-id="aaaf8-142">Use the following steps to publish your app to App Service using Local Git.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-142">Use the following steps to publish your app to App Service using Local Git.</span></span>

1. <span data-ttu-id="aaaf8-143">In your app's blade in the Azure Portal, click **Settings > Properties** for the **Git URL**.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-143">In your app's blade in the Azure Portal, click **Settings > Properties** for the **Git URL**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-deploy-local-git/git_url.png)
   
    <span data-ttu-id="aaaf8-144">**Git URL** is the remote reference to deploy to from your local repository.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-144">**Git URL** is the remote reference to deploy to from your local repository.</span></span> <span data-ttu-id="aaaf8-145">You'll use this URL in the following steps.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-145">You'll use this URL in the following steps.</span></span>
2. <span data-ttu-id="aaaf8-146">Using the command-line, verify that you are in the root of your local Git repository.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-146">Using the command-line, verify that you are in the root of your local Git repository.</span></span>
3. <span data-ttu-id="aaaf8-147">Use `git remote` to add the remote reference listed in **Git URL** from step 1.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-147">Use `git remote` to add the remote reference listed in **Git URL** from step 1.</span></span> <span data-ttu-id="aaaf8-148">Your command will look similar to the following:</span><span class="sxs-lookup"><span data-stu-id="aaaf8-148">Your command will look similar to the following:</span></span>
   
        git remote add azure https://<username>@localgitdeployment.scm.azurewebsites.net:443/localgitdeployment.git         
   > [!NOTE]
   > <span data-ttu-id="aaaf8-149">The **remote** command adds a named reference to a remote repository.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-149">The **remote** command adds a named reference to a remote repository.</span></span> <span data-ttu-id="aaaf8-150">In this example, it creates a reference named 'azure' for your web app's repository.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-150">In this example, it creates a reference named 'azure' for your web app's repository.</span></span>
   > 
   > 
4. <span data-ttu-id="aaaf8-151">Push your content to App Service using the new **azure** remote you just created.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-151">Push your content to App Service using the new **azure** remote you just created.</span></span>
   
        git push azure master
   
    <span data-ttu-id="aaaf8-152">You will be prompted for the password you created earlier when you reset your deployment credentials in the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-152">You will be prompted for the password you created earlier when you reset your deployment credentials in the Azure Portal.</span></span> <span data-ttu-id="aaaf8-153">Enter the password (note that Gitbash does not echo asterisks to the console as you type your password).</span><span class="sxs-lookup"><span data-stu-id="aaaf8-153">Enter the password (note that Gitbash does not echo asterisks to the console as you type your password).</span></span> 
5. <span data-ttu-id="aaaf8-154">Go back to your app in the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-154">Go back to your app in the Azure Portal.</span></span> <span data-ttu-id="aaaf8-155">A log entry of your most recent push should be displayed in the **Deployments** blade.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-155">A log entry of your most recent push should be displayed in the **Deployments** blade.</span></span> 
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-deploy-local-git/deployment_history.png)
6. <span data-ttu-id="aaaf8-156">Click the **Browse** button at the top of the app's blade to verify the content has been deployed.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-156">Click the **Browse** button at the top of the app's blade to verify the content has been deployed.</span></span> 

## <a name="Step5"></a><span data-ttu-id="aaaf8-157">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="aaaf8-157">Troubleshooting</span></span>
<span data-ttu-id="aaaf8-158">The following are errors or problems commonly encountered when using Git to publish to an App Service app in Azure:</span><span class="sxs-lookup"><span data-stu-id="aaaf8-158">The following are errors or problems commonly encountered when using Git to publish to an App Service app in Azure:</span></span>

- - -
<span data-ttu-id="aaaf8-159">**Symptom**: Unable to access '[siteURL]': Failed to connect to [scmAddress]</span><span class="sxs-lookup"><span data-stu-id="aaaf8-159">**Symptom**: Unable to access '[siteURL]': Failed to connect to [scmAddress]</span></span>

<span data-ttu-id="aaaf8-160">**Cause**: This error can occur if the app is not up and running.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-160">**Cause**: This error can occur if the app is not up and running.</span></span>

<span data-ttu-id="aaaf8-161">**Resolution**: Start the app in the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-161">**Resolution**: Start the app in the Azure Portal.</span></span> <span data-ttu-id="aaaf8-162">Git deployment will not work unless the app is running.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-162">Git deployment will not work unless the app is running.</span></span> 

- - -
<span data-ttu-id="aaaf8-163">**Symptom**: Couldn't resolve host 'hostname'</span><span class="sxs-lookup"><span data-stu-id="aaaf8-163">**Symptom**: Couldn't resolve host 'hostname'</span></span>

<span data-ttu-id="aaaf8-164">**Cause**: This error can occur if the address information entered when creating the 'azure' remote was incorrect.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-164">**Cause**: This error can occur if the address information entered when creating the 'azure' remote was incorrect.</span></span>

<span data-ttu-id="aaaf8-165">**Resolution**: Use the `git remote -v` command to list all remotes, along with the associated URL.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-165">**Resolution**: Use the `git remote -v` command to list all remotes, along with the associated URL.</span></span> <span data-ttu-id="aaaf8-166">Verify that the URL for the 'azure' remote is correct.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-166">Verify that the URL for the 'azure' remote is correct.</span></span> <span data-ttu-id="aaaf8-167">If needed, remove and recreate this remote using the correct URL.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-167">If needed, remove and recreate this remote using the correct URL.</span></span>

- - -
<span data-ttu-id="aaaf8-168">**Symptom**: No refs in common and none specified; doing nothing.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-168">**Symptom**: No refs in common and none specified; doing nothing.</span></span> <span data-ttu-id="aaaf8-169">Perhaps you should specify a branch such as 'master'.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-169">Perhaps you should specify a branch such as 'master'.</span></span>

<span data-ttu-id="aaaf8-170">**Cause**: This error can occur if you do not specify a branch when performing a git push operation, and have not set the push.default value used by Git.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-170">**Cause**: This error can occur if you do not specify a branch when performing a git push operation, and have not set the push.default value used by Git.</span></span>

<span data-ttu-id="aaaf8-171">**Resolution**: Perform the push operation again, specifying the master branch.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-171">**Resolution**: Perform the push operation again, specifying the master branch.</span></span> <span data-ttu-id="aaaf8-172">For example:</span><span class="sxs-lookup"><span data-stu-id="aaaf8-172">For example:</span></span>

    git push azure master

- - -
<span data-ttu-id="aaaf8-173">**Symptom**: src refspec [branchname] does not match any.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-173">**Symptom**: src refspec [branchname] does not match any.</span></span>

<span data-ttu-id="aaaf8-174">**Cause**: This error can occur if you attempt to push to a branch other than master on the 'azure' remote.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-174">**Cause**: This error can occur if you attempt to push to a branch other than master on the 'azure' remote.</span></span>

<span data-ttu-id="aaaf8-175">**Resolution**: Perform the push operation again, specifying the master branch.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-175">**Resolution**: Perform the push operation again, specifying the master branch.</span></span> <span data-ttu-id="aaaf8-176">For example:</span><span class="sxs-lookup"><span data-stu-id="aaaf8-176">For example:</span></span>

    git push azure master

- - -
<span data-ttu-id="aaaf8-177">**Symptom**: RPC failed; result=22, HTTP code = 502.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-177">**Symptom**: RPC failed; result=22, HTTP code = 502.</span></span>

<span data-ttu-id="aaaf8-178">**Cause**: This error can occur if you attempt to push a large git repository over HTTPS.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-178">**Cause**: This error can occur if you attempt to push a large git repository over HTTPS.</span></span>

<span data-ttu-id="aaaf8-179">**Resolution**: Change the git configuration on the local machine to make the postBuffer bigger</span><span class="sxs-lookup"><span data-stu-id="aaaf8-179">**Resolution**: Change the git configuration on the local machine to make the postBuffer bigger</span></span>

    git config --global http.postBuffer 524288000

- - -
<span data-ttu-id="aaaf8-180">**Symptom**: Error - Changes committed to remote repository but your web app not updated.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-180">**Symptom**: Error - Changes committed to remote repository but your web app not updated.</span></span>

<span data-ttu-id="aaaf8-181">**Cause**: This error can occur if you are deploying a Node.js app containing a package.json file that specifies additional required modules.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-181">**Cause**: This error can occur if you are deploying a Node.js app containing a package.json file that specifies additional required modules.</span></span>

<span data-ttu-id="aaaf8-182">**Resolution**: Additional messages containing 'npm ERR!'</span><span class="sxs-lookup"><span data-stu-id="aaaf8-182">**Resolution**: Additional messages containing 'npm ERR!'</span></span> <span data-ttu-id="aaaf8-183">should be logged prior to this error, and can provide additional context on the failure.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-183">should be logged prior to this error, and can provide additional context on the failure.</span></span> <span data-ttu-id="aaaf8-184">The following are known causes of this error and the corresponding 'npm ERR!'</span><span class="sxs-lookup"><span data-stu-id="aaaf8-184">The following are known causes of this error and the corresponding 'npm ERR!'</span></span> <span data-ttu-id="aaaf8-185">message:</span><span class="sxs-lookup"><span data-stu-id="aaaf8-185">message:</span></span>

* <span data-ttu-id="aaaf8-186">**Malformed package.json file**: npm ERR!</span><span class="sxs-lookup"><span data-stu-id="aaaf8-186">**Malformed package.json file**: npm ERR!</span></span> <span data-ttu-id="aaaf8-187">Couldn't read dependencies.</span><span class="sxs-lookup"><span data-stu-id="aaaf8-187">Couldn't read dependencies.</span></span>
* <span data-ttu-id="aaaf8-188">**Native module that does not have a binary distribution for Windows**:</span><span class="sxs-lookup"><span data-stu-id="aaaf8-188">**Native module that does not have a binary distribution for Windows**:</span></span>
  
  * <span data-ttu-id="aaaf8-189">npm ERR!</span><span class="sxs-lookup"><span data-stu-id="aaaf8-189">npm ERR!</span></span> <span data-ttu-id="aaaf8-190">\`cmd "/c" "node-gyp rebuild"\` failed with 1</span><span class="sxs-lookup"><span data-stu-id="aaaf8-190">\`cmd "/c" "node-gyp rebuild"\` failed with 1</span></span>
    
      <span data-ttu-id="aaaf8-191">OR</span><span class="sxs-lookup"><span data-stu-id="aaaf8-191">OR</span></span>
  * <span data-ttu-id="aaaf8-192">npm ERR!</span><span class="sxs-lookup"><span data-stu-id="aaaf8-192">npm ERR!</span></span> <span data-ttu-id="aaaf8-193">[modulename@version] preinstall: \`make || gmake\`</span><span class="sxs-lookup"><span data-stu-id="aaaf8-193">[modulename@version] preinstall: \`make || gmake\`</span></span>

## <a name="additional-resources"></a><span data-ttu-id="aaaf8-194">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="aaaf8-194">Additional Resources</span></span>
* [<span data-ttu-id="aaaf8-195">Git documentation</span><span class="sxs-lookup"><span data-stu-id="aaaf8-195">Git documentation</span></span>](http://git-scm.com/documentation)
* [<span data-ttu-id="aaaf8-196">Project Kudu documentation</span><span class="sxs-lookup"><span data-stu-id="aaaf8-196">Project Kudu documentation</span></span>](https://github.com/projectkudu/kudu/wiki)
* [<span data-ttu-id="aaaf8-197">Continous Deployment to Azure App Service</span><span class="sxs-lookup"><span data-stu-id="aaaf8-197">Continous Deployment to Azure App Service</span></span>](app-service-continuous-deployment.md)
* [<span data-ttu-id="aaaf8-198">How to use PowerShell for Azure</span><span class="sxs-lookup"><span data-stu-id="aaaf8-198">How to use PowerShell for Azure</span></span>](/powershell/azureps-cmdlets-docs)
* [<span data-ttu-id="aaaf8-199">How to use the Azure Command-Line Interface</span><span class="sxs-lookup"><span data-stu-id="aaaf8-199">How to use the Azure Command-Line Interface</span></span>](../cli-install-nodejs.md)

[Azure App Service]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/
[Azure Developer Center]: http://www.windowsazure.com/en-us/develop/overview/
[Azure Portal]: https://portal.azure.com
[Git website]: http://git-scm.com
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[Azure Command-Line Interface]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/

[Using Git with CodePlex]: http://codeplex.codeplex.com/wikipage?title=Using%20Git%20with%20CodePlex&referringTitle=Source%20control%20clients&ProjectName=codeplex
[Quick Start - Mercurial]: http://mercurial.selenic.com/wiki/QuickStart




