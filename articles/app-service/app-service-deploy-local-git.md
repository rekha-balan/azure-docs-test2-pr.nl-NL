---
title: Local Git Deployment to Azure App Service
description: Learn how to enable local Git deployment to Azure App Service.
services: app-service
documentationcenter: ''
author: cephalin
manager: cfowler
ms.assetid: ac50a623-c4b8-4dfd-96b2-a09420770063
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2018
ms.author: dariagrigoriu;cephalin
ms.openlocfilehash: ae8739a65efbe7662a8f72e961d772fecaf4b527
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966840"
---
# <a name="local-git-deployment-to-azure-app-service"></a><span data-ttu-id="0d772-103">Local Git Deployment to Azure App Service</span><span class="sxs-lookup"><span data-stu-id="0d772-103">Local Git Deployment to Azure App Service</span></span>

<span data-ttu-id="0d772-104">This how-to guide shows you how to deploy your code to [Azure App Service](app-service-web-overview.md) from a Git repository on your local computer.</span><span class="sxs-lookup"><span data-stu-id="0d772-104">This how-to guide shows you how to deploy your code to [Azure App Service](app-service-web-overview.md) from a Git repository on your local computer.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="0d772-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0d772-105">Prerequisites</span></span>

<span data-ttu-id="0d772-106">To follow the steps in this how-to guide:</span><span class="sxs-lookup"><span data-stu-id="0d772-106">To follow the steps in this how-to guide:</span></span>

* <span data-ttu-id="0d772-107">[Install Git](http://www.git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="0d772-107">[Install Git](http://www.git-scm.com/downloads).</span></span>
* <span data-ttu-id="0d772-108">Maintain a local Git repository with code you want to deploy.</span><span class="sxs-lookup"><span data-stu-id="0d772-108">Maintain a local Git repository with code you want to deploy.</span></span>

<span data-ttu-id="0d772-109">To use a sample repository to follow along, run the following command in your local terminal window:</span><span class="sxs-lookup"><span data-stu-id="0d772-109">To use a sample repository to follow along, run the following command in your local terminal window:</span></span>

```bash
git clone https://github.com/Azure-Samples/nodejs-docs-hello-world.git
```

[!INCLUDE [Prepare repository](../../includes/app-service-deploy-prepare-repo.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="deploy-from-local-git-with-kudu-builds"></a><span data-ttu-id="0d772-110">Deploy from local Git with Kudu builds</span><span class="sxs-lookup"><span data-stu-id="0d772-110">Deploy from local Git with Kudu builds</span></span>

<span data-ttu-id="0d772-111">The easiest way to enable local Git deployment for your app with the Kudu build server is to use the Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="0d772-111">The easiest way to enable local Git deployment for your app with the Kudu build server is to use the Cloud Shell.</span></span>

### <a name="create-a-deployment-user"></a><span data-ttu-id="0d772-112">Create a deployment user</span><span class="sxs-lookup"><span data-stu-id="0d772-112">Create a deployment user</span></span>

[!INCLUDE [Configure a deployment user](../../includes/configure-deployment-user-no-h.md)]

### <a name="enable-local-git-with-kudu"></a><span data-ttu-id="0d772-113">Enable local Git with Kudu</span><span class="sxs-lookup"><span data-stu-id="0d772-113">Enable local Git with Kudu</span></span>

<span data-ttu-id="0d772-114">To enable local Git deployment for your app with the Kudu build server, run [`az webapp deployment source config-local-git`](/cli/azure/webapp/deployment/source?view=azure-cli-latest#az-webapp-deployment-source-config-local-git) in the Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="0d772-114">To enable local Git deployment for your app with the Kudu build server, run [`az webapp deployment source config-local-git`](/cli/azure/webapp/deployment/source?view=azure-cli-latest#az-webapp-deployment-source-config-local-git) in the Cloud Shell.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group <group_name>
```

<span data-ttu-id="0d772-115">To create a Git-enabled app instead, run [`az webapp create`](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) in the Cloud Shell with the `--deployment-local-git` parameter.</span><span class="sxs-lookup"><span data-stu-id="0d772-115">To create a Git-enabled app instead, run [`az webapp create`](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) in the Cloud Shell with the `--deployment-local-git` parameter.</span></span>

```azurecli-interactive
az webapp create --name <app_name> --resource-group <group_name> --plan <plan_name> --deployment-local-git
```

<span data-ttu-id="0d772-116">The `az webapp create` command should give you something similar to the following output:</span><span class="sxs-lookup"><span data-stu-id="0d772-116">The `az webapp create` command should give you something similar to the following output:</span></span>

```json
Local git is configured with url of 'https://<username>@<app_name>.scm.azurewebsites.net/<app_name>.git'
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "deploymentLocalGitUrl": "https://<username>@<app_name>.scm.azurewebsites.net/<app_name>.git",
  "enabled": true,
  < JSON data removed for brevity. >
}
```

### <a name="deploy-your-project"></a><span data-ttu-id="0d772-117">Deploy your project</span><span class="sxs-lookup"><span data-stu-id="0d772-117">Deploy your project</span></span>

<span data-ttu-id="0d772-118">Back in the _local terminal window_, add an Azure remote to your local Git repository.</span><span class="sxs-lookup"><span data-stu-id="0d772-118">Back in the _local terminal window_, add an Azure remote to your local Git repository.</span></span> <span data-ttu-id="0d772-119">Replace _\<url>_ with the URL of the Git remote that you got from [Enable Git for your app](#enable-git-for-you-app).</span><span class="sxs-lookup"><span data-stu-id="0d772-119">Replace _\<url>_ with the URL of the Git remote that you got from [Enable Git for your app](#enable-git-for-you-app).</span></span>

```bash
git remote add azure <url>
```

<span data-ttu-id="0d772-120">Push to the Azure remote to deploy your app with the following command.</span><span class="sxs-lookup"><span data-stu-id="0d772-120">Push to the Azure remote to deploy your app with the following command.</span></span> <span data-ttu-id="0d772-121">When prompted for a password, make sure that you enter the password you created in [Configure a deployment user](#configure-a-deployment-user), not the password you use to log in to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0d772-121">When prompted for a password, make sure that you enter the password you created in [Configure a deployment user](#configure-a-deployment-user), not the password you use to log in to the Azure portal.</span></span>

```bash
git push azure master
```

<span data-ttu-id="0d772-122">You may see runtime-specific automation in the output, such as MSBuild for ASP.NET, `npm install` for Node.js, and `pip install` for Python.</span><span class="sxs-lookup"><span data-stu-id="0d772-122">You may see runtime-specific automation in the output, such as MSBuild for ASP.NET, `npm install` for Node.js, and `pip install` for Python.</span></span> 

<span data-ttu-id="0d772-123">Browse to your app to verify that the content is deployed.</span><span class="sxs-lookup"><span data-stu-id="0d772-123">Browse to your app to verify that the content is deployed.</span></span>

## <a name="deploy-from-local-git-with-azure-devops-services-builds"></a><span data-ttu-id="0d772-124">Deploy from local Git with Azure DevOps Services builds</span><span class="sxs-lookup"><span data-stu-id="0d772-124">Deploy from local Git with Azure DevOps Services builds</span></span>

> [!NOTE]
> <span data-ttu-id="0d772-125">For App Service to create the necessary Azure Pipelines in your Azure DevOps Services organization, your Azure account must have the role of **Owner** in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="0d772-125">For App Service to create the necessary Azure Pipelines in your Azure DevOps Services organization, your Azure account must have the role of **Owner** in your Azure subscription.</span></span>
>

<span data-ttu-id="0d772-126">To enable local Git deployment for your app with the Kudu build server, navigate to your app in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0d772-126">To enable local Git deployment for your app with the Kudu build server, navigate to your app in the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="0d772-127">In the left navigation of your app page, click **Deployment Center** > **Local Git** > **Continue**.</span><span class="sxs-lookup"><span data-stu-id="0d772-127">In the left navigation of your app page, click **Deployment Center** > **Local Git** > **Continue**.</span></span> 

![](media/app-service-deploy-local-git/portal-enable.png)

<span data-ttu-id="0d772-128">Click **Azure DevOps Services Continuous Delivery** > **Continue**.</span><span class="sxs-lookup"><span data-stu-id="0d772-128">Click **Azure DevOps Services Continuous Delivery** > **Continue**.</span></span>

![](media/app-service-deploy-local-git/vsts-build-server.png)

<span data-ttu-id="0d772-129">In the **Configure** page, configure a new Azure DevOps Services organization, or specify an existing organization.</span><span class="sxs-lookup"><span data-stu-id="0d772-129">In the **Configure** page, configure a new Azure DevOps Services organization, or specify an existing organization.</span></span> <span data-ttu-id="0d772-130">When finished, click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="0d772-130">When finished, click **Continue**.</span></span>

> [!NOTE]
> <span data-ttu-id="0d772-131">If you want to use an existing Azure DevOps Services organization that is not listed, you need to [link the Azure DevOps Services organization to your Azure subscription](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).</span><span class="sxs-lookup"><span data-stu-id="0d772-131">If you want to use an existing Azure DevOps Services organization that is not listed, you need to [link the Azure DevOps Services organization to your Azure subscription](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).</span></span>

<span data-ttu-id="0d772-132">In the **Test** page, choose whether to enable load tests, then click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="0d772-132">In the **Test** page, choose whether to enable load tests, then click **Continue**.</span></span>

<span data-ttu-id="0d772-133">Depending on the [pricing tier](https://azure.microsoft.com/pricing/details/app-service/plans/) of your App Service plan, you may also see a **Deploy to staging** page.</span><span class="sxs-lookup"><span data-stu-id="0d772-133">Depending on the [pricing tier](https://azure.microsoft.com/pricing/details/app-service/plans/) of your App Service plan, you may also see a **Deploy to staging** page.</span></span> <span data-ttu-id="0d772-134">Choose whether to enable deployment slots, then click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="0d772-134">Choose whether to enable deployment slots, then click **Continue**.</span></span>

<span data-ttu-id="0d772-135">In the **Summary** page, verify your options and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="0d772-135">In the **Summary** page, verify your options and click **Finish**.</span></span>

<span data-ttu-id="0d772-136">It takes a few minutes for the Azure DevOps Services organization to be ready.</span><span class="sxs-lookup"><span data-stu-id="0d772-136">It takes a few minutes for the Azure DevOps Services organization to be ready.</span></span> <span data-ttu-id="0d772-137">When it's ready, copy the Git repository URL in the deployment center.</span><span class="sxs-lookup"><span data-stu-id="0d772-137">When it's ready, copy the Git repository URL in the deployment center.</span></span>

![](media/app-service-deploy-local-git/vsts-repo-ready.png)

<span data-ttu-id="0d772-138">Back in the _local terminal window_, add an Azure remote to your local Git repository.</span><span class="sxs-lookup"><span data-stu-id="0d772-138">Back in the _local terminal window_, add an Azure remote to your local Git repository.</span></span> <span data-ttu-id="0d772-139">Replace _\<url>_ with the URL you got from the last step.</span><span class="sxs-lookup"><span data-stu-id="0d772-139">Replace _\<url>_ with the URL you got from the last step.</span></span>

```bash
git remote add vsts <url>
```

<span data-ttu-id="0d772-140">Push to the Azure remote to deploy your app with the following command.</span><span class="sxs-lookup"><span data-stu-id="0d772-140">Push to the Azure remote to deploy your app with the following command.</span></span> <span data-ttu-id="0d772-141">When prompted by Git Credential Manager, sign in with your visualstudio.com user.</span><span class="sxs-lookup"><span data-stu-id="0d772-141">When prompted by Git Credential Manager, sign in with your visualstudio.com user.</span></span> <span data-ttu-id="0d772-142">For additional authentication methods, see [Azure DevOps Services authentication overview](/vsts/git/auth-overview?view=vsts).</span><span class="sxs-lookup"><span data-stu-id="0d772-142">For additional authentication methods, see [Azure DevOps Services authentication overview](/vsts/git/auth-overview?view=vsts).</span></span>

```bash
git push vsts master
```

<span data-ttu-id="0d772-143">Once deployment is finished, you can find the build progress at `https://<vsts_account>.visualstudio.com/<project_name>/_build` and the deployment progress at `https://<vsts_account>.visualstudio.com/<project_name>/_release`.</span><span class="sxs-lookup"><span data-stu-id="0d772-143">Once deployment is finished, you can find the build progress at `https://<vsts_account>.visualstudio.com/<project_name>/_build` and the deployment progress at `https://<vsts_account>.visualstudio.com/<project_name>/_release`.</span></span>

<span data-ttu-id="0d772-144">Browse to your app to verify that the content is deployed.</span><span class="sxs-lookup"><span data-stu-id="0d772-144">Browse to your app to verify that the content is deployed.</span></span>

[!INCLUDE [What happens to my app during deployment?](../../includes/app-service-deploy-atomicity.md)]

## <a name="troubleshooting-kudu-deployment"></a><span data-ttu-id="0d772-145">Troubleshooting Kudu deployment</span><span class="sxs-lookup"><span data-stu-id="0d772-145">Troubleshooting Kudu deployment</span></span>

<span data-ttu-id="0d772-146">The following are common errors or problems when using Git to publish to an App Service app in Azure:</span><span class="sxs-lookup"><span data-stu-id="0d772-146">The following are common errors or problems when using Git to publish to an App Service app in Azure:</span></span>

---
<span data-ttu-id="0d772-147">**Symptom**: `Unable to access '[siteURL]': Failed to connect to [scmAddress]`</span><span class="sxs-lookup"><span data-stu-id="0d772-147">**Symptom**: `Unable to access '[siteURL]': Failed to connect to [scmAddress]`</span></span>

<span data-ttu-id="0d772-148">**Cause**: This error can happen if the app isn't up and running.</span><span class="sxs-lookup"><span data-stu-id="0d772-148">**Cause**: This error can happen if the app isn't up and running.</span></span>

<span data-ttu-id="0d772-149">**Resolution**: Start the app in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0d772-149">**Resolution**: Start the app in the Azure portal.</span></span> <span data-ttu-id="0d772-150">Git deployment is unavailable when the Web App is stopped.</span><span class="sxs-lookup"><span data-stu-id="0d772-150">Git deployment is unavailable when the Web App is stopped.</span></span>

---
<span data-ttu-id="0d772-151">**Symptom**: `Couldn't resolve host 'hostname'`</span><span class="sxs-lookup"><span data-stu-id="0d772-151">**Symptom**: `Couldn't resolve host 'hostname'`</span></span>

<span data-ttu-id="0d772-152">**Cause**: This error can happen if the address information entered when creating the 'azure' remote was incorrect.</span><span class="sxs-lookup"><span data-stu-id="0d772-152">**Cause**: This error can happen if the address information entered when creating the 'azure' remote was incorrect.</span></span>

<span data-ttu-id="0d772-153">**Resolution**: Use the `git remote -v` command to list all remotes, along with the associated URL.</span><span class="sxs-lookup"><span data-stu-id="0d772-153">**Resolution**: Use the `git remote -v` command to list all remotes, along with the associated URL.</span></span> <span data-ttu-id="0d772-154">Verify that the URL for the 'azure' remote is correct.</span><span class="sxs-lookup"><span data-stu-id="0d772-154">Verify that the URL for the 'azure' remote is correct.</span></span> <span data-ttu-id="0d772-155">If needed, remove and recreate this remote using the correct URL.</span><span class="sxs-lookup"><span data-stu-id="0d772-155">If needed, remove and recreate this remote using the correct URL.</span></span>

---
<span data-ttu-id="0d772-156">**Symptom**: `No refs in common and none specified; doing nothing. Perhaps you should specify a branch such as 'master'.`</span><span class="sxs-lookup"><span data-stu-id="0d772-156">**Symptom**: `No refs in common and none specified; doing nothing. Perhaps you should specify a branch such as 'master'.`</span></span>

<span data-ttu-id="0d772-157">**Cause**: This error can happen if you don't specify a branch during `git push`, or if you haven't set the `push.default` value in `.gitconfig`.</span><span class="sxs-lookup"><span data-stu-id="0d772-157">**Cause**: This error can happen if you don't specify a branch during `git push`, or if you haven't set the `push.default` value in `.gitconfig`.</span></span>

<span data-ttu-id="0d772-158">**Resolution**: Run `git push` again, specifying the master branch.</span><span class="sxs-lookup"><span data-stu-id="0d772-158">**Resolution**: Run `git push` again, specifying the master branch.</span></span> <span data-ttu-id="0d772-159">For example:</span><span class="sxs-lookup"><span data-stu-id="0d772-159">For example:</span></span>

```bash
git push azure master
```

---
<span data-ttu-id="0d772-160">**Symptom**: `src refspec [branchname] does not match any.`</span><span class="sxs-lookup"><span data-stu-id="0d772-160">**Symptom**: `src refspec [branchname] does not match any.`</span></span>

<span data-ttu-id="0d772-161">**Cause**: This error can happen if you try to push to a branch other than master on the 'azure' remote.</span><span class="sxs-lookup"><span data-stu-id="0d772-161">**Cause**: This error can happen if you try to push to a branch other than master on the 'azure' remote.</span></span>

<span data-ttu-id="0d772-162">**Resolution**: Run `git push` again, specifying the master branch.</span><span class="sxs-lookup"><span data-stu-id="0d772-162">**Resolution**: Run `git push` again, specifying the master branch.</span></span> <span data-ttu-id="0d772-163">For example:</span><span class="sxs-lookup"><span data-stu-id="0d772-163">For example:</span></span>

```bash
git push azure master
```

---
<span data-ttu-id="0d772-164">**Symptom**: `RPC failed; result=22, HTTP code = 5xx.`</span><span class="sxs-lookup"><span data-stu-id="0d772-164">**Symptom**: `RPC failed; result=22, HTTP code = 5xx.`</span></span>

<span data-ttu-id="0d772-165">**Cause**: This error can happen if you try to push a large git repository over HTTPS.</span><span class="sxs-lookup"><span data-stu-id="0d772-165">**Cause**: This error can happen if you try to push a large git repository over HTTPS.</span></span>

<span data-ttu-id="0d772-166">**Resolution**: Change the git configuration on the local machine to make the postBuffer bigger</span><span class="sxs-lookup"><span data-stu-id="0d772-166">**Resolution**: Change the git configuration on the local machine to make the postBuffer bigger</span></span>

```bash
git config --global http.postBuffer 524288000
```

---
<span data-ttu-id="0d772-167">**Symptom**: `Error - Changes committed to remote repository but your web app not updated.`</span><span class="sxs-lookup"><span data-stu-id="0d772-167">**Symptom**: `Error - Changes committed to remote repository but your web app not updated.`</span></span>

<span data-ttu-id="0d772-168">**Cause**: This error can happen if you deploy a Node.js app with a _package.json_ file that specifies additional required modules.</span><span class="sxs-lookup"><span data-stu-id="0d772-168">**Cause**: This error can happen if you deploy a Node.js app with a _package.json_ file that specifies additional required modules.</span></span>

<span data-ttu-id="0d772-169">**Resolution**: Additional messages with 'npm ERR!'</span><span class="sxs-lookup"><span data-stu-id="0d772-169">**Resolution**: Additional messages with 'npm ERR!'</span></span> <span data-ttu-id="0d772-170">should be logged before this error, and can provide additional context on the failure.</span><span class="sxs-lookup"><span data-stu-id="0d772-170">should be logged before this error, and can provide additional context on the failure.</span></span> <span data-ttu-id="0d772-171">The following are known causes of this error and the corresponding 'npm ERR!'</span><span class="sxs-lookup"><span data-stu-id="0d772-171">The following are known causes of this error and the corresponding 'npm ERR!'</span></span> <span data-ttu-id="0d772-172">message:</span><span class="sxs-lookup"><span data-stu-id="0d772-172">message:</span></span>

* <span data-ttu-id="0d772-173">**Malformed package.json file**: npm ERR!</span><span class="sxs-lookup"><span data-stu-id="0d772-173">**Malformed package.json file**: npm ERR!</span></span> <span data-ttu-id="0d772-174">Couldn't read dependencies.</span><span class="sxs-lookup"><span data-stu-id="0d772-174">Couldn't read dependencies.</span></span>
* <span data-ttu-id="0d772-175">**Native module that doesn't have a binary distribution for Windows**:</span><span class="sxs-lookup"><span data-stu-id="0d772-175">**Native module that doesn't have a binary distribution for Windows**:</span></span>

  * `npm ERR! \cmd "/c" "node-gyp rebuild"\ failed with 1`

      <span data-ttu-id="0d772-176">OR</span><span class="sxs-lookup"><span data-stu-id="0d772-176">OR</span></span>
  * `npm ERR! [modulename@version] preinstall: \make || gmake\`

## <a name="additional-resources"></a><span data-ttu-id="0d772-177">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="0d772-177">Additional Resources</span></span>

* [<span data-ttu-id="0d772-178">Project Kudu documentation</span><span class="sxs-lookup"><span data-stu-id="0d772-178">Project Kudu documentation</span></span>](https://github.com/projectkudu/kudu/wiki)
* [<span data-ttu-id="0d772-179">Continuous Deployment to Azure App Service</span><span class="sxs-lookup"><span data-stu-id="0d772-179">Continuous Deployment to Azure App Service</span></span>](app-service-continuous-deployment.md)
* [<span data-ttu-id="0d772-180">Sample: Create Web App and deploy code from a local Git repository (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="0d772-180">Sample: Create Web App and deploy code from a local Git repository (Azure CLI)</span></span>](./scripts/app-service-cli-deploy-local-git.md?toc=%2fcli%2fazure%2ftoc.json)
* [<span data-ttu-id="0d772-181">Sample: Create Web App and deploy code from a local Git repository (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="0d772-181">Sample: Create Web App and deploy code from a local Git repository (PowerShell)</span></span>](./scripts/app-service-powershell-deploy-local-git.md?toc=%2fpowershell%2fmodule%2ftoc.json)
