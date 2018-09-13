---
title: Azure App Service on Linux FAQ | Microsoft Docs
description: Azure App Service on Linux FAQ.
keywords: azure app service, web app, faq, linux, oss, web app for containers, multi-container, multicontainer
services: app-service
documentationCenter: ''
author: yili
manager: apurvajo
editor: ''
ms.assetid: ''
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2018
ms.author: yili
ms.openlocfilehash: aba6a1f7028ac09cad8acf587fd56dcc2c16919b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869783"
---
# <a name="azure-app-service-on-linux-faq"></a><span data-ttu-id="7f51a-104">Azure App Service on Linux FAQ</span><span class="sxs-lookup"><span data-stu-id="7f51a-104">Azure App Service on Linux FAQ</span></span>

<span data-ttu-id="7f51a-105">With the release of App Service on Linux, we're working on adding features and making improvements to our platform.</span><span class="sxs-lookup"><span data-stu-id="7f51a-105">With the release of App Service on Linux, we're working on adding features and making improvements to our platform.</span></span> <span data-ttu-id="7f51a-106">This article provides answers to questions that our customers have been asking us recently.</span><span class="sxs-lookup"><span data-stu-id="7f51a-106">This article provides answers to questions that our customers have been asking us recently.</span></span>

<span data-ttu-id="7f51a-107">If you have a question, comment on this article.</span><span class="sxs-lookup"><span data-stu-id="7f51a-107">If you have a question, comment on this article.</span></span>

## <a name="built-in-images"></a><span data-ttu-id="7f51a-108">Built-in images</span><span class="sxs-lookup"><span data-stu-id="7f51a-108">Built-in images</span></span>

<span data-ttu-id="7f51a-109">**I want to fork the built-in Docker containers that the platform provides. Where can I find those files?**</span><span class="sxs-lookup"><span data-stu-id="7f51a-109">**I want to fork the built-in Docker containers that the platform provides. Where can I find those files?**</span></span>

<span data-ttu-id="7f51a-110">You can find all Docker files on [GitHub](https://github.com/azure-app-service).</span><span class="sxs-lookup"><span data-stu-id="7f51a-110">You can find all Docker files on [GitHub](https://github.com/azure-app-service).</span></span> <span data-ttu-id="7f51a-111">You can find all Docker containers on [Docker Hub](https://hub.docker.com/u/appsvc/).</span><span class="sxs-lookup"><span data-stu-id="7f51a-111">You can find all Docker containers on [Docker Hub](https://hub.docker.com/u/appsvc/).</span></span>

<span data-ttu-id="7f51a-112">**What are the expected values for the Startup File section when I configure the runtime stack?**</span><span class="sxs-lookup"><span data-stu-id="7f51a-112">**What are the expected values for the Startup File section when I configure the runtime stack?**</span></span>

<span data-ttu-id="7f51a-113">For Node.js, you specify the PM2 configuration file or your script file.</span><span class="sxs-lookup"><span data-stu-id="7f51a-113">For Node.js, you specify the PM2 configuration file or your script file.</span></span> <span data-ttu-id="7f51a-114">For .NET Core, specify your compiled DLL name as `dotnet <myapp>.dll`.</span><span class="sxs-lookup"><span data-stu-id="7f51a-114">For .NET Core, specify your compiled DLL name as `dotnet <myapp>.dll`.</span></span> <span data-ttu-id="7f51a-115">For Ruby, you can specify the Ruby script that you want to initialize your app with.</span><span class="sxs-lookup"><span data-stu-id="7f51a-115">For Ruby, you can specify the Ruby script that you want to initialize your app with.</span></span>

## <a name="management"></a><span data-ttu-id="7f51a-116">Management</span><span class="sxs-lookup"><span data-stu-id="7f51a-116">Management</span></span>

<span data-ttu-id="7f51a-117">**What happens when I press the restart button in the Azure portal?**</span><span class="sxs-lookup"><span data-stu-id="7f51a-117">**What happens when I press the restart button in the Azure portal?**</span></span>

<span data-ttu-id="7f51a-118">This action is the same as a Docker restart.</span><span class="sxs-lookup"><span data-stu-id="7f51a-118">This action is the same as a Docker restart.</span></span>

<span data-ttu-id="7f51a-119">**Can I use Secure Shell (SSH) to connect to the app container virtual machine (VM)?**</span><span class="sxs-lookup"><span data-stu-id="7f51a-119">**Can I use Secure Shell (SSH) to connect to the app container virtual machine (VM)?**</span></span>

<span data-ttu-id="7f51a-120">Yes, you can do that through the source control management (SCM) site.</span><span class="sxs-lookup"><span data-stu-id="7f51a-120">Yes, you can do that through the source control management (SCM) site.</span></span>

> [!NOTE]
> <span data-ttu-id="7f51a-121">You can also connect to the app container directly from your local development machine using SSH, SFTP, or Visual Studio Code (for live debugging Node.js apps).</span><span class="sxs-lookup"><span data-stu-id="7f51a-121">You can also connect to the app container directly from your local development machine using SSH, SFTP, or Visual Studio Code (for live debugging Node.js apps).</span></span> <span data-ttu-id="7f51a-122">For more information, see [Remote debugging and SSH in App Service on Linux](https://aka.ms/linux-debug).</span><span class="sxs-lookup"><span data-stu-id="7f51a-122">For more information, see [Remote debugging and SSH in App Service on Linux](https://aka.ms/linux-debug).</span></span>
>

<span data-ttu-id="7f51a-123">**How can I create a Linux App Service plan through an SDK or an Azure Resource Manager template?**</span><span class="sxs-lookup"><span data-stu-id="7f51a-123">**How can I create a Linux App Service plan through an SDK or an Azure Resource Manager template?**</span></span>

<span data-ttu-id="7f51a-124">You should set the **reserved** field of the app service to *true*.</span><span class="sxs-lookup"><span data-stu-id="7f51a-124">You should set the **reserved** field of the app service to *true*.</span></span>

## <a name="continuous-integration-and-deployment"></a><span data-ttu-id="7f51a-125">Continuous integration and deployment</span><span class="sxs-lookup"><span data-stu-id="7f51a-125">Continuous integration and deployment</span></span>

<span data-ttu-id="7f51a-126">**My web app still uses an old Docker container image after I've updated the image on Docker Hub. Do you support continuous integration and deployment of custom containers?**</span><span class="sxs-lookup"><span data-stu-id="7f51a-126">**My web app still uses an old Docker container image after I've updated the image on Docker Hub. Do you support continuous integration and deployment of custom containers?**</span></span>

<span data-ttu-id="7f51a-127">Yes, to set up continuous integration/deployment for Azure Container Registry or DockerHub, by following [Continuous Deployment with Web App for Containers](./app-service-linux-ci-cd.md).</span><span class="sxs-lookup"><span data-stu-id="7f51a-127">Yes, to set up continuous integration/deployment for Azure Container Registry or DockerHub, by following [Continuous Deployment with Web App for Containers](./app-service-linux-ci-cd.md).</span></span> <span data-ttu-id="7f51a-128">For private registries, you can refresh the container by stopping and then starting your web app.</span><span class="sxs-lookup"><span data-stu-id="7f51a-128">For private registries, you can refresh the container by stopping and then starting your web app.</span></span> <span data-ttu-id="7f51a-129">Or you can change or add a dummy application setting to force a refresh of your container.</span><span class="sxs-lookup"><span data-stu-id="7f51a-129">Or you can change or add a dummy application setting to force a refresh of your container.</span></span>

<span data-ttu-id="7f51a-130">**Do you support staging environments?**</span><span class="sxs-lookup"><span data-stu-id="7f51a-130">**Do you support staging environments?**</span></span>

<span data-ttu-id="7f51a-131">Yes.</span><span class="sxs-lookup"><span data-stu-id="7f51a-131">Yes.</span></span>

<span data-ttu-id="7f51a-132">**Can I use *WebDeploy/MSDeploy* to deploy my web app?**</span><span class="sxs-lookup"><span data-stu-id="7f51a-132">**Can I use *WebDeploy/MSDeploy* to deploy my web app?**</span></span>

<span data-ttu-id="7f51a-133">Yes, you need to set an app setting called `WEBSITE_WEBDEPLOY_USE_SCM` to *false*.</span><span class="sxs-lookup"><span data-stu-id="7f51a-133">Yes, you need to set an app setting called `WEBSITE_WEBDEPLOY_USE_SCM` to *false*.</span></span>

<span data-ttu-id="7f51a-134">**Git deployment of my application fails when using Linux web app. How can I work around the issue?**</span><span class="sxs-lookup"><span data-stu-id="7f51a-134">**Git deployment of my application fails when using Linux web app. How can I work around the issue?**</span></span>

<span data-ttu-id="7f51a-135">If Git deployment fails to your Linux web app, choose one of the following options to deploy your application code:</span><span class="sxs-lookup"><span data-stu-id="7f51a-135">If Git deployment fails to your Linux web app, choose one of the following options to deploy your application code:</span></span>

- <span data-ttu-id="7f51a-136">Use the Continuous Delivery (Preview) feature: You can store your app’s source code in a Azure DevOps Git repo or GitHub repo to use Azure Continuous Delivery.</span><span class="sxs-lookup"><span data-stu-id="7f51a-136">Use the Continuous Delivery (Preview) feature: You can store your app’s source code in a Azure DevOps Git repo or GitHub repo to use Azure Continuous Delivery.</span></span> <span data-ttu-id="7f51a-137">For more information, see [How to configure Continuous Delivery for Linux web app](https://blogs.msdn.microsoft.com/devops/2017/05/10/use-azure-portal-to-setup-continuous-delivery-for-web-app-on-linux/).</span><span class="sxs-lookup"><span data-stu-id="7f51a-137">For more information, see [How to configure Continuous Delivery for Linux web app](https://blogs.msdn.microsoft.com/devops/2017/05/10/use-azure-portal-to-setup-continuous-delivery-for-web-app-on-linux/).</span></span>

- <span data-ttu-id="7f51a-138">Use the [ZIP deploy API](https://github.com/projectkudu/kudu/wiki/Deploying-from-a-zip-file): To use this API, [SSH into your web app](https://docs.microsoft.com/azure/app-service/containers/app-service-linux-ssh-support#making-a-client-connection) and go to the folder where you want to deploy your code.</span><span class="sxs-lookup"><span data-stu-id="7f51a-138">Use the [ZIP deploy API](https://github.com/projectkudu/kudu/wiki/Deploying-from-a-zip-file): To use this API, [SSH into your web app](https://docs.microsoft.com/azure/app-service/containers/app-service-linux-ssh-support#making-a-client-connection) and go to the folder where you want to deploy your code.</span></span> <span data-ttu-id="7f51a-139">Run the following code:</span><span class="sxs-lookup"><span data-stu-id="7f51a-139">Run the following code:</span></span>

   ```bash
   curl -X POST -u <user> --data-binary @<zipfile> https://{your-sitename}.scm.azurewebsites.net/api/zipdeploy
   ```

   <span data-ttu-id="7f51a-140">If you get an error that the `curl` command is not found, make sure you install curl by using `apt-get install curl` before you run the previous `curl` command.</span><span class="sxs-lookup"><span data-stu-id="7f51a-140">If you get an error that the `curl` command is not found, make sure you install curl by using `apt-get install curl` before you run the previous `curl` command.</span></span>

## <a name="language-support"></a><span data-ttu-id="7f51a-141">Language support</span><span class="sxs-lookup"><span data-stu-id="7f51a-141">Language support</span></span>

<span data-ttu-id="7f51a-142">**I want to use web sockets in my Node.js application, any special settings, or configurations to set?**</span><span class="sxs-lookup"><span data-stu-id="7f51a-142">**I want to use web sockets in my Node.js application, any special settings, or configurations to set?**</span></span>

<span data-ttu-id="7f51a-143">Yes, disable `perMessageDeflate` in your server-side Node.js code.</span><span class="sxs-lookup"><span data-stu-id="7f51a-143">Yes, disable `perMessageDeflate` in your server-side Node.js code.</span></span> <span data-ttu-id="7f51a-144">For example, if you are using socket.io, use the following code:</span><span class="sxs-lookup"><span data-stu-id="7f51a-144">For example, if you are using socket.io, use the following code:</span></span>

```nodejs
var io = require('socket.io')(server,{
  perMessageDeflate :false
});
```

<span data-ttu-id="7f51a-145">**Do you support uncompiled .NET Core apps?**</span><span class="sxs-lookup"><span data-stu-id="7f51a-145">**Do you support uncompiled .NET Core apps?**</span></span>

<span data-ttu-id="7f51a-146">Yes.</span><span class="sxs-lookup"><span data-stu-id="7f51a-146">Yes.</span></span>

<span data-ttu-id="7f51a-147">**Do you support Composer as a dependency manager for PHP apps?**</span><span class="sxs-lookup"><span data-stu-id="7f51a-147">**Do you support Composer as a dependency manager for PHP apps?**</span></span>

<span data-ttu-id="7f51a-148">Yes, during a Git deployment, Kudu should detect that you're deploying a PHP application (thanks to the presence of a composer.lock file), and Kudu will then trigger a composer install.</span><span class="sxs-lookup"><span data-stu-id="7f51a-148">Yes, during a Git deployment, Kudu should detect that you're deploying a PHP application (thanks to the presence of a composer.lock file), and Kudu will then trigger a composer install.</span></span>

## <a name="custom-containers"></a><span data-ttu-id="7f51a-149">Custom containers</span><span class="sxs-lookup"><span data-stu-id="7f51a-149">Custom containers</span></span>

<span data-ttu-id="7f51a-150">**I'm using my own custom container. I want the platform to mount an SMB share to the `/home/` directory.**</span><span class="sxs-lookup"><span data-stu-id="7f51a-150">**I'm using my own custom container. I want the platform to mount an SMB share to the `/home/` directory.**</span></span>

<span data-ttu-id="7f51a-151">You can do that by setting the `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app setting to *true*.</span><span class="sxs-lookup"><span data-stu-id="7f51a-151">You can do that by setting the `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app setting to *true*.</span></span> <span data-ttu-id="7f51a-152">Keep in mind that this will cause container restarts when the platform storage goes through a change.</span><span class="sxs-lookup"><span data-stu-id="7f51a-152">Keep in mind that this will cause container restarts when the platform storage goes through a change.</span></span>

>[!NOTE]
><span data-ttu-id="7f51a-153">If the `WEBSITES_ENABLE_APP_SERVICE_STORAGE` setting is unspecified or set to *false*, the `/home/` directory will not be shared across scale instances, and files that are written there will not be persisted across restarts.</span><span class="sxs-lookup"><span data-stu-id="7f51a-153">If the `WEBSITES_ENABLE_APP_SERVICE_STORAGE` setting is unspecified or set to *false*, the `/home/` directory will not be shared across scale instances, and files that are written there will not be persisted across restarts.</span></span>

<span data-ttu-id="7f51a-154">**My custom container takes a long time to start, and the platform restarts the container before it finishes starting up.**</span><span class="sxs-lookup"><span data-stu-id="7f51a-154">**My custom container takes a long time to start, and the platform restarts the container before it finishes starting up.**</span></span>

<span data-ttu-id="7f51a-155">You can configure the amount of time the platform will wait before it restarts your container.</span><span class="sxs-lookup"><span data-stu-id="7f51a-155">You can configure the amount of time the platform will wait before it restarts your container.</span></span> <span data-ttu-id="7f51a-156">To do so, set the `WEBSITES_CONTAINER_START_TIME_LIMIT` app setting to the value you want.</span><span class="sxs-lookup"><span data-stu-id="7f51a-156">To do so, set the `WEBSITES_CONTAINER_START_TIME_LIMIT` app setting to the value you want.</span></span> <span data-ttu-id="7f51a-157">The default value is 230 seconds, and the maximum value is 1800 seconds.</span><span class="sxs-lookup"><span data-stu-id="7f51a-157">The default value is 230 seconds, and the maximum value is 1800 seconds.</span></span>

<span data-ttu-id="7f51a-158">**What is the format for the private registry server URL?**</span><span class="sxs-lookup"><span data-stu-id="7f51a-158">**What is the format for the private registry server URL?**</span></span>

<span data-ttu-id="7f51a-159">Provide the full registry URL, including `http://` or `https://`.</span><span class="sxs-lookup"><span data-stu-id="7f51a-159">Provide the full registry URL, including `http://` or `https://`.</span></span>

<span data-ttu-id="7f51a-160">**What is the format for the image name in the private registry option?**</span><span class="sxs-lookup"><span data-stu-id="7f51a-160">**What is the format for the image name in the private registry option?**</span></span>

<span data-ttu-id="7f51a-161">Add the full image name, including the private registry URL (for example, myacr.azurecr.io/dotnet:latest).</span><span class="sxs-lookup"><span data-stu-id="7f51a-161">Add the full image name, including the private registry URL (for example, myacr.azurecr.io/dotnet:latest).</span></span> <span data-ttu-id="7f51a-162">Image names that use a custom port [cannot be entered through the portal](https://feedback.azure.com/forums/169385-web-apps/suggestions/31304650).</span><span class="sxs-lookup"><span data-stu-id="7f51a-162">Image names that use a custom port [cannot be entered through the portal](https://feedback.azure.com/forums/169385-web-apps/suggestions/31304650).</span></span> <span data-ttu-id="7f51a-163">To set `docker-custom-image-name`, use the [`az` command-line tool](https://docs.microsoft.com/cli/azure/webapp/config/container?view=azure-cli-latest#az-webapp-config-container-set).</span><span class="sxs-lookup"><span data-stu-id="7f51a-163">To set `docker-custom-image-name`, use the [`az` command-line tool](https://docs.microsoft.com/cli/azure/webapp/config/container?view=azure-cli-latest#az-webapp-config-container-set).</span></span>

<span data-ttu-id="7f51a-164">**Can I expose more than one port on my custom container image?**</span><span class="sxs-lookup"><span data-stu-id="7f51a-164">**Can I expose more than one port on my custom container image?**</span></span>

<span data-ttu-id="7f51a-165">We do not currently support exposing more than one port.</span><span class="sxs-lookup"><span data-stu-id="7f51a-165">We do not currently support exposing more than one port.</span></span>

<span data-ttu-id="7f51a-166">**Can I bring my own storage?**</span><span class="sxs-lookup"><span data-stu-id="7f51a-166">**Can I bring my own storage?**</span></span>

<span data-ttu-id="7f51a-167">We do not currently support bringing your own storage.</span><span class="sxs-lookup"><span data-stu-id="7f51a-167">We do not currently support bringing your own storage.</span></span>

<span data-ttu-id="7f51a-168">**Why can't I browse my custom container's file system or running processes from the SCM site?**</span><span class="sxs-lookup"><span data-stu-id="7f51a-168">**Why can't I browse my custom container's file system or running processes from the SCM site?**</span></span>

<span data-ttu-id="7f51a-169">The SCM site runs in a separate container.</span><span class="sxs-lookup"><span data-stu-id="7f51a-169">The SCM site runs in a separate container.</span></span> <span data-ttu-id="7f51a-170">You can't check the file system or running processes of the app container.</span><span class="sxs-lookup"><span data-stu-id="7f51a-170">You can't check the file system or running processes of the app container.</span></span>

<span data-ttu-id="7f51a-171">**My custom container listens to a port other than port 80. How can I configure my app to route requests to that port?**</span><span class="sxs-lookup"><span data-stu-id="7f51a-171">**My custom container listens to a port other than port 80. How can I configure my app to route requests to that port?**</span></span>

<span data-ttu-id="7f51a-172">We have automatic port detection.</span><span class="sxs-lookup"><span data-stu-id="7f51a-172">We have automatic port detection.</span></span> <span data-ttu-id="7f51a-173">You can also specify an app setting called *WEBSITES_PORT* and give it the value of the expected port number.</span><span class="sxs-lookup"><span data-stu-id="7f51a-173">You can also specify an app setting called *WEBSITES_PORT* and give it the value of the expected port number.</span></span> <span data-ttu-id="7f51a-174">Previously, the platform used the *PORT* app setting.</span><span class="sxs-lookup"><span data-stu-id="7f51a-174">Previously, the platform used the *PORT* app setting.</span></span> <span data-ttu-id="7f51a-175">We are planning to deprecate this app setting and to use *WEBSITES_PORT* exclusively.</span><span class="sxs-lookup"><span data-stu-id="7f51a-175">We are planning to deprecate this app setting and to use *WEBSITES_PORT* exclusively.</span></span>

<span data-ttu-id="7f51a-176">**Do I need to implement HTTPS in my custom container?**</span><span class="sxs-lookup"><span data-stu-id="7f51a-176">**Do I need to implement HTTPS in my custom container?**</span></span>

<span data-ttu-id="7f51a-177">No, the platform handles HTTPS termination at the shared front ends.</span><span class="sxs-lookup"><span data-stu-id="7f51a-177">No, the platform handles HTTPS termination at the shared front ends.</span></span>

## <a name="multi-container-with-docker-compose-and-kubernetes"></a><span data-ttu-id="7f51a-178">Multi-container with Docker Compose and Kubernetes</span><span class="sxs-lookup"><span data-stu-id="7f51a-178">Multi-container with Docker Compose and Kubernetes</span></span>

<span data-ttu-id="7f51a-179">**How do I configure Azure Container Registry (ACR) to use with multi-container?**</span><span class="sxs-lookup"><span data-stu-id="7f51a-179">**How do I configure Azure Container Registry (ACR) to use with multi-container?**</span></span>

<span data-ttu-id="7f51a-180">In order to use ACR with multi-container, **all container images** need to be hosted on the same ACR registry server.</span><span class="sxs-lookup"><span data-stu-id="7f51a-180">In order to use ACR with multi-container, **all container images** need to be hosted on the same ACR registry server.</span></span> <span data-ttu-id="7f51a-181">Once they are on the same registry server, you will need to create application settings and then update the Docker Compose or Kubernetes configuration file to include the ACR image name.</span><span class="sxs-lookup"><span data-stu-id="7f51a-181">Once they are on the same registry server, you will need to create application settings and then update the Docker Compose or Kubernetes configuration file to include the ACR image name.</span></span>

<span data-ttu-id="7f51a-182">Create the following application settings:</span><span class="sxs-lookup"><span data-stu-id="7f51a-182">Create the following application settings:</span></span>

- <span data-ttu-id="7f51a-183">DOCKER_REGISTRY_SERVER_USERNAME</span><span class="sxs-lookup"><span data-stu-id="7f51a-183">DOCKER_REGISTRY_SERVER_USERNAME</span></span>
- <span data-ttu-id="7f51a-184">DOCKER_REGISTRY_SERVER_URL (full URL, ex: https://<server-name>.azurecr.io)</span><span class="sxs-lookup"><span data-stu-id="7f51a-184">DOCKER_REGISTRY_SERVER_URL (full URL, ex: https://<server-name>.azurecr.io)</span></span>
- <span data-ttu-id="7f51a-185">DOCKER_REGISTRY_SERVER_PASSWORD (enable admin access in ACR settings)</span><span class="sxs-lookup"><span data-stu-id="7f51a-185">DOCKER_REGISTRY_SERVER_PASSWORD (enable admin access in ACR settings)</span></span>

<span data-ttu-id="7f51a-186">Within the configuration file, reference your ACR image like the following example:</span><span class="sxs-lookup"><span data-stu-id="7f51a-186">Within the configuration file, reference your ACR image like the following example:</span></span>

```yaml
image: <server-name>.azurecr.io/<image-name>:<tag>
```

<span data-ttu-id="7f51a-187">**How do I know which container is internet accessible?**</span><span class="sxs-lookup"><span data-stu-id="7f51a-187">**How do I know which container is internet accessible?**</span></span>

- <span data-ttu-id="7f51a-188">Only one container can be open for access</span><span class="sxs-lookup"><span data-stu-id="7f51a-188">Only one container can be open for access</span></span>
- <span data-ttu-id="7f51a-189">Only port 80 and 8080 is accessible (exposed ports)</span><span class="sxs-lookup"><span data-stu-id="7f51a-189">Only port 80 and 8080 is accessible (exposed ports)</span></span>

<span data-ttu-id="7f51a-190">Here are the rules for determining which container is accessible - in the order of precedence:</span><span class="sxs-lookup"><span data-stu-id="7f51a-190">Here are the rules for determining which container is accessible - in the order of precedence:</span></span>

- <span data-ttu-id="7f51a-191">Application setting `WEBSITES_WEB_CONTAINER_NAME` set to the container name</span><span class="sxs-lookup"><span data-stu-id="7f51a-191">Application setting `WEBSITES_WEB_CONTAINER_NAME` set to the container name</span></span>
- <span data-ttu-id="7f51a-192">The first container to define port 80 or 8080</span><span class="sxs-lookup"><span data-stu-id="7f51a-192">The first container to define port 80 or 8080</span></span>
- <span data-ttu-id="7f51a-193">If neither of the above is true, the first container defined in the file will be accessible (exposed)</span><span class="sxs-lookup"><span data-stu-id="7f51a-193">If neither of the above is true, the first container defined in the file will be accessible (exposed)</span></span>

## <a name="pricing-and-sla"></a><span data-ttu-id="7f51a-194">Pricing and SLA</span><span class="sxs-lookup"><span data-stu-id="7f51a-194">Pricing and SLA</span></span>

<span data-ttu-id="7f51a-195">**What is the pricing, now that the service is generally available?**</span><span class="sxs-lookup"><span data-stu-id="7f51a-195">**What is the pricing, now that the service is generally available?**</span></span>

<span data-ttu-id="7f51a-196">You are charged the normal Azure App Service pricing for the number of hours that your app runs.</span><span class="sxs-lookup"><span data-stu-id="7f51a-196">You are charged the normal Azure App Service pricing for the number of hours that your app runs.</span></span>

## <a name="other-questions"></a><span data-ttu-id="7f51a-197">Other questions</span><span class="sxs-lookup"><span data-stu-id="7f51a-197">Other questions</span></span>

<span data-ttu-id="7f51a-198">**What are the supported characters in application settings names?**</span><span class="sxs-lookup"><span data-stu-id="7f51a-198">**What are the supported characters in application settings names?**</span></span>

<span data-ttu-id="7f51a-199">You can use only letters (A-Z, a-z), numbers (0-9), and the underscore character (_) for application settings.</span><span class="sxs-lookup"><span data-stu-id="7f51a-199">You can use only letters (A-Z, a-z), numbers (0-9), and the underscore character (_) for application settings.</span></span>

<span data-ttu-id="7f51a-200">**Where can I request new features?**</span><span class="sxs-lookup"><span data-stu-id="7f51a-200">**Where can I request new features?**</span></span>

<span data-ttu-id="7f51a-201">You can submit your idea at the [Web Apps feedback forum](https://aka.ms/webapps-uservoice).</span><span class="sxs-lookup"><span data-stu-id="7f51a-201">You can submit your idea at the [Web Apps feedback forum](https://aka.ms/webapps-uservoice).</span></span> <span data-ttu-id="7f51a-202">Add "[Linux]" to the title of your idea.</span><span class="sxs-lookup"><span data-stu-id="7f51a-202">Add "[Linux]" to the title of your idea.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f51a-203">Next steps</span><span class="sxs-lookup"><span data-stu-id="7f51a-203">Next steps</span></span>

- [<span data-ttu-id="7f51a-204">What is Azure App Service on Linux?</span><span class="sxs-lookup"><span data-stu-id="7f51a-204">What is Azure App Service on Linux?</span></span>](app-service-linux-intro.md)
- [<span data-ttu-id="7f51a-205">Set up staging environments in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="7f51a-205">Set up staging environments in Azure App Service</span></span>](../../app-service/web-sites-staged-publishing.md?toc=%2fazure%2fapp-service%2fcontainers%2ftoc.json)
- [<span data-ttu-id="7f51a-206">Continuous Deployment with Web App for Containers</span><span class="sxs-lookup"><span data-stu-id="7f51a-206">Continuous Deployment with Web App for Containers</span></span>](./app-service-linux-ci-cd.md)
