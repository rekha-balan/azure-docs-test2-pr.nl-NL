---
title: Use a custom Docker image for Web App for Containers - Azure | Microsoft Docs
description: How to use a custom Docker image for Web App for Containers.
keywords: azure app service, web app, linux, docker, container
services: app-service
documentationcenter: ''
author: SyntaxC4
manager: SyntaxC4
editor: ''
ms.assetid: b97bd4e6-dff0-4976-ac20-d5c109a559a8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 10/24/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 161207b96deb2f7bd605d845a9207393f9f59c23
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867113"
---
# <a name="use-a-custom-docker-image-for-web-app-for-containers"></a><span data-ttu-id="59083-104">Use a custom Docker image for Web App for Containers</span><span class="sxs-lookup"><span data-stu-id="59083-104">Use a custom Docker image for Web App for Containers</span></span>

<span data-ttu-id="59083-105">[Web App for Containers](app-service-linux-intro.md) provides built-in Docker images on Linux with support for specific versions, such as PHP 7.0 and Node.js 4.5.</span><span class="sxs-lookup"><span data-stu-id="59083-105">[Web App for Containers](app-service-linux-intro.md) provides built-in Docker images on Linux with support for specific versions, such as PHP 7.0 and Node.js 4.5.</span></span> <span data-ttu-id="59083-106">Web App for Containers uses the Docker container technology to host both built-in images and custom images as a platform as a service.</span><span class="sxs-lookup"><span data-stu-id="59083-106">Web App for Containers uses the Docker container technology to host both built-in images and custom images as a platform as a service.</span></span> <span data-ttu-id="59083-107">In this tutorial, you learn how to build a custom Docker image and deploy it to Web App for Containers.</span><span class="sxs-lookup"><span data-stu-id="59083-107">In this tutorial, you learn how to build a custom Docker image and deploy it to Web App for Containers.</span></span> <span data-ttu-id="59083-108">This pattern is useful when the built-in images don't include your language of choice, or when your application requires a specific configuration that isn't provided within the built-in images.</span><span class="sxs-lookup"><span data-stu-id="59083-108">This pattern is useful when the built-in images don't include your language of choice, or when your application requires a specific configuration that isn't provided within the built-in images.</span></span>

<span data-ttu-id="59083-109">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="59083-109">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="59083-110">Deploy a custom Docker image to Azure</span><span class="sxs-lookup"><span data-stu-id="59083-110">Deploy a custom Docker image to Azure</span></span>
> * <span data-ttu-id="59083-111">Configure environment variables to run the container</span><span class="sxs-lookup"><span data-stu-id="59083-111">Configure environment variables to run the container</span></span>
> * <span data-ttu-id="59083-112">Update the Docker image and redeploy it</span><span class="sxs-lookup"><span data-stu-id="59083-112">Update the Docker image and redeploy it</span></span>
> * <span data-ttu-id="59083-113">Connect to the container using SSH</span><span class="sxs-lookup"><span data-stu-id="59083-113">Connect to the container using SSH</span></span>
> * <span data-ttu-id="59083-114">Deploy a private Docker image to Azure</span><span class="sxs-lookup"><span data-stu-id="59083-114">Deploy a private Docker image to Azure</span></span>

[!INCLUDE [Free trial note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="59083-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="59083-115">Prerequisites</span></span>

<span data-ttu-id="59083-116">To complete this tutorial, you need:</span><span class="sxs-lookup"><span data-stu-id="59083-116">To complete this tutorial, you need:</span></span>

* [<span data-ttu-id="59083-117">Git</span><span class="sxs-lookup"><span data-stu-id="59083-117">Git</span></span>](https://git-scm.com/downloads)
* [<span data-ttu-id="59083-118">Docker</span><span class="sxs-lookup"><span data-stu-id="59083-118">Docker</span></span>](https://docs.docker.com/get-started/#setup)
* <span data-ttu-id="59083-119">A [Docker Hub account](https://docs.docker.com/docker-id/)</span><span class="sxs-lookup"><span data-stu-id="59083-119">A [Docker Hub account](https://docs.docker.com/docker-id/)</span></span>

## <a name="download-the-sample"></a><span data-ttu-id="59083-120">Download the sample</span><span class="sxs-lookup"><span data-stu-id="59083-120">Download the sample</span></span>

<span data-ttu-id="59083-121">In a terminal window, run the following command to clone the sample app repository to your local machine, then change to the directory that contains the sample code.</span><span class="sxs-lookup"><span data-stu-id="59083-121">In a terminal window, run the following command to clone the sample app repository to your local machine, then change to the directory that contains the sample code.</span></span>

```bash
git clone https://github.com/Azure-Samples/docker-django-webapp-linux.git --config core.autocrlf=input
cd docker-django-webapp-linux
```

## <a name="build-the-image-from-the-docker-file"></a><span data-ttu-id="59083-122">Build the image from the Docker file</span><span class="sxs-lookup"><span data-stu-id="59083-122">Build the image from the Docker file</span></span>

<span data-ttu-id="59083-123">In the Git repository, take a look at _Dockerfile_.</span><span class="sxs-lookup"><span data-stu-id="59083-123">In the Git repository, take a look at _Dockerfile_.</span></span> <span data-ttu-id="59083-124">This file describes the Python environment that is required to run your application.</span><span class="sxs-lookup"><span data-stu-id="59083-124">This file describes the Python environment that is required to run your application.</span></span> <span data-ttu-id="59083-125">Additionally, the image sets up an [SSH](https://www.ssh.com/ssh/protocol/) server for secure communication between the container and the host.</span><span class="sxs-lookup"><span data-stu-id="59083-125">Additionally, the image sets up an [SSH](https://www.ssh.com/ssh/protocol/) server for secure communication between the container and the host.</span></span>

```docker
FROM python:3.4

RUN mkdir /code
WORKDIR /code
ADD requirements.txt /code/
RUN pip install -r requirements.txt
ADD . /code/

# ssh
ENV SSH_PASSWD "root:Docker!"
RUN apt-get update \
        && apt-get install -y --no-install-recommends dialog \
        && apt-get update \
    && apt-get install -y --no-install-recommends openssh-server \
    && echo "$SSH_PASSWD" | chpasswd 

COPY sshd_config /etc/ssh/
COPY init.sh /usr/local/bin/
    
RUN chmod u+x /usr/local/bin/init.sh
EXPOSE 8000 2222
#CMD ["python", "/code/manage.py", "runserver", "0.0.0.0:8000"]
ENTRYPOINT ["init.sh"]
```

<span data-ttu-id="59083-126">To build the Docker image, run the `docker build` command, and provide a name, _mydockerimage_, and tag, _v1.0.0_.</span><span class="sxs-lookup"><span data-stu-id="59083-126">To build the Docker image, run the `docker build` command, and provide a name, _mydockerimage_, and tag, _v1.0.0_.</span></span> <span data-ttu-id="59083-127">Replace _\<docker-id>_ with your Docker Hub account ID.</span><span class="sxs-lookup"><span data-stu-id="59083-127">Replace _\<docker-id>_ with your Docker Hub account ID.</span></span>

```bash
docker build --tag <docker-id>/mydockerimage:v1.0.0 .
```

<span data-ttu-id="59083-128">The command produces output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="59083-128">The command produces output similar to the following:</span></span>

```
# The output from the commands in this article has been shortened for brevity.

Sending build context to Docker daemon  5.558MB
Step 1/13 : FROM python:3.4
 ---> 9ff45ddb54e9
Step 2/13 : RUN mkdir /code
 ---> Using cache
 ---> f3f3ac01db0a
Step 3/13 : WORKDIR /code
 ---> Using cache
 ---> 38b32f15b442
.
.
.
Step 13/13 : ENTRYPOINT init.sh
 ---> Running in 5904e4c70043
 ---> e7cf08275692
Removing intermediate container 5904e4c70043
Successfully built e7cf08275692
Successfully tagged cephalin/mydockerimage:v1.0.0
```

<span data-ttu-id="59083-129">Test that the build works by running the Docker container.</span><span class="sxs-lookup"><span data-stu-id="59083-129">Test that the build works by running the Docker container.</span></span> <span data-ttu-id="59083-130">Issue the [`docker run`](https://docs.docker.com/engine/reference/commandline/run/) command and pass the name and tag of the image to it.</span><span class="sxs-lookup"><span data-stu-id="59083-130">Issue the [`docker run`](https://docs.docker.com/engine/reference/commandline/run/) command and pass the name and tag of the image to it.</span></span> <span data-ttu-id="59083-131">Be sure to specify the port using the `-p` argument.</span><span class="sxs-lookup"><span data-stu-id="59083-131">Be sure to specify the port using the `-p` argument.</span></span>

```bash
docker run -p 2222:8000 <docker-ID>/mydockerimage:v1.0.0
```

<span data-ttu-id="59083-132">Verify the web app and container are functioning correctly by browsing to `http://localhost:2222`.</span><span class="sxs-lookup"><span data-stu-id="59083-132">Verify the web app and container are functioning correctly by browsing to `http://localhost:2222`.</span></span>

![Test web app locally](./media/app-service-linux-using-custom-docker-image/app-service-linux-browse-local.png)

> [!NOTE] 
> <span data-ttu-id="59083-134">You can also connect to the app container directly from your local development machine using SSH, SFTP, or Visual Studio Code (for live debugging Node.js apps).</span><span class="sxs-lookup"><span data-stu-id="59083-134">You can also connect to the app container directly from your local development machine using SSH, SFTP, or Visual Studio Code (for live debugging Node.js apps).</span></span> <span data-ttu-id="59083-135">For more information, see [Remote debugging and SSH in App Service on Linux](https://aka.ms/linux-debug).</span><span class="sxs-lookup"><span data-stu-id="59083-135">For more information, see [Remote debugging and SSH in App Service on Linux](https://aka.ms/linux-debug).</span></span>
>

## <a name="push-the-docker-image-to-docker-hub"></a><span data-ttu-id="59083-136">Push the Docker image to Docker Hub</span><span class="sxs-lookup"><span data-stu-id="59083-136">Push the Docker image to Docker Hub</span></span>

<span data-ttu-id="59083-137">A registry is an application that hosts images and provides services image and container services.</span><span class="sxs-lookup"><span data-stu-id="59083-137">A registry is an application that hosts images and provides services image and container services.</span></span> <span data-ttu-id="59083-138">In order to share your image, you must push it to a registry.</span><span class="sxs-lookup"><span data-stu-id="59083-138">In order to share your image, you must push it to a registry.</span></span> 

<!-- Depending on your requirements, you may have your docker images in a Public Docker Registry, such as Docker Hub, or a Private Docker Registry such as Azure Container Registry. Select the appropriate tab for your scenario below (your selection will switch multiple tabs on this page). -->

> [!NOTE]
> <span data-ttu-id="59083-139">Pushing to a Private Docker Registry?</span><span class="sxs-lookup"><span data-stu-id="59083-139">Pushing to a Private Docker Registry?</span></span> <span data-ttu-id="59083-140">See the optional instructions to [Use a Docker image from any private registry](#use-a-docker-image-from-any-private-registry-optional).</span><span class="sxs-lookup"><span data-stu-id="59083-140">See the optional instructions to [Use a Docker image from any private registry](#use-a-docker-image-from-any-private-registry-optional).</span></span>

<!--## [Docker Hub](#tab/docker-hub)-->

<span data-ttu-id="59083-141">Docker Hub is a registry for Docker images that allows you to host your own repositories, either public or private.</span><span class="sxs-lookup"><span data-stu-id="59083-141">Docker Hub is a registry for Docker images that allows you to host your own repositories, either public or private.</span></span> <span data-ttu-id="59083-142">To push a custom Docker image to the public Docker Hub, use the [`docker push`](https://docs.docker.com/engine/reference/commandline/push/) command and provide a full image name and tag.</span><span class="sxs-lookup"><span data-stu-id="59083-142">To push a custom Docker image to the public Docker Hub, use the [`docker push`](https://docs.docker.com/engine/reference/commandline/push/) command and provide a full image name and tag.</span></span> <span data-ttu-id="59083-143">A full image name and tag looks like the following sample:</span><span class="sxs-lookup"><span data-stu-id="59083-143">A full image name and tag looks like the following sample:</span></span>

```
<docker-id>/image-name:tag
```

<span data-ttu-id="59083-144">Before you can push an image, you must sign in to Docker Hub using the [`docker login`](https://docs.docker.com/engine/reference/commandline/login/) command.</span><span class="sxs-lookup"><span data-stu-id="59083-144">Before you can push an image, you must sign in to Docker Hub using the [`docker login`](https://docs.docker.com/engine/reference/commandline/login/) command.</span></span> <span data-ttu-id="59083-145">Replace _\<docker-id>_ with your account name and type in your password into the console at the prompt.</span><span class="sxs-lookup"><span data-stu-id="59083-145">Replace _\<docker-id>_ with your account name and type in your password into the console at the prompt.</span></span>

```bash
docker login --username <docker-id>
```

<span data-ttu-id="59083-146">A "login succeeded" message confirms that you are logged in.</span><span class="sxs-lookup"><span data-stu-id="59083-146">A "login succeeded" message confirms that you are logged in.</span></span> <span data-ttu-id="59083-147">Once logged in, you can push the image to Docker Hub using the [`docker push`](https://docs.docker.com/engine/reference/commandline/push/) command.</span><span class="sxs-lookup"><span data-stu-id="59083-147">Once logged in, you can push the image to Docker Hub using the [`docker push`](https://docs.docker.com/engine/reference/commandline/push/) command.</span></span>

```bash
docker push <docker-id>/mydockerimage:v1.0.0
```

<span data-ttu-id="59083-148">Verify that the push succeeded by examining the command's output.</span><span class="sxs-lookup"><span data-stu-id="59083-148">Verify that the push succeeded by examining the command's output.</span></span>

```
The push refers to a repository [docker.io/<docker-id>/mydockerimage:v1.0.0]
c33197c3f6d4: Pushed
ccd2c850ee43: Pushed
02dff2853466: Pushed
6ce78153632a: Pushed
efef3f03cc58: Pushed
3439624d77fb: Pushed
3a07adfb35c5: Pushed
2fcec228e1b7: Mounted from library/python
97d2d3bae505: Mounted from library/python
95aadeabf504: Mounted from library/python
b456afdc9996: Mounted from library/python
d752a0310ee4: Mounted from library/python
db64edce4b5b: Mounted from library/python
d5d60fc34309: Mounted from library/python
c01c63c6823d: Mounted from library/python
v1.0.0: digest: sha256:21f2798b20555f4143f2ca0591a43b4f6c8138406041f2d32ec908974feced66 size: 3676
```

<!--
# [Private Registry](#tab/private-registry)

// Move Private Registry instructions here when Tabbed Conceptual bug is fixed

---
-->

[!INCLUDE [Try Cloud Shell](../../../includes/cloud-shell-try-it.md)]

## <a name="deploy-app-to-azure"></a><span data-ttu-id="59083-149">Deploy app to Azure</span><span class="sxs-lookup"><span data-stu-id="59083-149">Deploy app to Azure</span></span>

<span data-ttu-id="59083-150">You can host native Linux applications in the cloud by using Azure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="59083-150">You can host native Linux applications in the cloud by using Azure Web Apps.</span></span> <span data-ttu-id="59083-151">To create a Web App for Containers, you must run Azure CLI commands that create a group, then a service plan, and finally the web app itself.</span><span class="sxs-lookup"><span data-stu-id="59083-151">To create a Web App for Containers, you must run Azure CLI commands that create a group, then a service plan, and finally the web app itself.</span></span> 

### <a name="create-a-resource-group"></a><span data-ttu-id="59083-152">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="59083-152">Create a resource group</span></span>

[!INCLUDE [Create resource group](../../../includes/app-service-web-create-resource-group-linux-no-h.md)] 

### <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="59083-153">Create a Linux App Service plan</span><span class="sxs-lookup"><span data-stu-id="59083-153">Create a Linux App Service plan</span></span>

[!INCLUDE [Create app service plan](../../../includes/app-service-web-create-app-service-plan-linux-no-h.md)] 

### <a name="create-a-web-app"></a><span data-ttu-id="59083-154">Create a web app</span><span class="sxs-lookup"><span data-stu-id="59083-154">Create a web app</span></span>

<span data-ttu-id="59083-155">In the Cloud Shell, create a [web app](app-service-linux-intro.md) in the `myAppServicePlan` App Service plan with the [`az webapp create`](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) command.</span><span class="sxs-lookup"><span data-stu-id="59083-155">In the Cloud Shell, create a [web app](app-service-linux-intro.md) in the `myAppServicePlan` App Service plan with the [`az webapp create`](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) command.</span></span> <span data-ttu-id="59083-156">Don't forget to replace _<appname>_ with a unique app name, and _\<docker-ID>_ with your Docker ID.</span><span class="sxs-lookup"><span data-stu-id="59083-156">Don't forget to replace _<appname>_ with a unique app name, and _\<docker-ID>_ with your Docker ID.</span></span>

```azurecli-interactive
az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app_name> --deployment-container-image-name <docker-ID>/mydockerimage:v1.0.0
```

<span data-ttu-id="59083-157">When the web app has been created, the Azure CLI shows output similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="59083-157">When the web app has been created, the Azure CLI shows output similar to the following example:</span></span>

```json
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

### <a name="configure-environment-variables"></a><span data-ttu-id="59083-158">Configure environment variables</span><span class="sxs-lookup"><span data-stu-id="59083-158">Configure environment variables</span></span>

<span data-ttu-id="59083-159">Most Docker images have environment variables that need to be configured.</span><span class="sxs-lookup"><span data-stu-id="59083-159">Most Docker images have environment variables that need to be configured.</span></span> <span data-ttu-id="59083-160">If you are using an existing Docker image built by someone else, the image may use a port other than 80.</span><span class="sxs-lookup"><span data-stu-id="59083-160">If you are using an existing Docker image built by someone else, the image may use a port other than 80.</span></span> <span data-ttu-id="59083-161">You tell Azure about the port that your image uses by using the `WEBSITES_PORT` app setting.</span><span class="sxs-lookup"><span data-stu-id="59083-161">You tell Azure about the port that your image uses by using the `WEBSITES_PORT` app setting.</span></span> <span data-ttu-id="59083-162">The GitHub page for the [Python sample in this tutorial](https://github.com/Azure-Samples/docker-django-webapp-linux) shows that you need to set `WEBSITES_PORT` to _8000_.</span><span class="sxs-lookup"><span data-stu-id="59083-162">The GitHub page for the [Python sample in this tutorial](https://github.com/Azure-Samples/docker-django-webapp-linux) shows that you need to set `WEBSITES_PORT` to _8000_.</span></span>

<span data-ttu-id="59083-163">To set app settings, use the [`az webapp config appsettings set`](/cli/azure/webapp/config/appsettings?view=azure-cli-latest#az-webapp-config-appsettings-set) command in the Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="59083-163">To set app settings, use the [`az webapp config appsettings set`](/cli/azure/webapp/config/appsettings?view=azure-cli-latest#az-webapp-config-appsettings-set) command in the Cloud Shell.</span></span> <span data-ttu-id="59083-164">App settings are case-sensitive and space-separated.</span><span class="sxs-lookup"><span data-stu-id="59083-164">App settings are case-sensitive and space-separated.</span></span>

```azurecli-interactive
az webapp config appsettings set --resource-group myResourceGroup --name <app_name> --settings WEBSITES_PORT=8000
```

<!-- Depending on your requirements, you may have your docker images in a Public Docker Registry, such as Docker Hub, or a Private Docker Registry, such as Azure Container Registry. Select the appropriate tab for your scenario below: -->

> [!NOTE]
> <span data-ttu-id="59083-165">Deploying from a Private Docker Registry?</span><span class="sxs-lookup"><span data-stu-id="59083-165">Deploying from a Private Docker Registry?</span></span> <span data-ttu-id="59083-166">See the optional instructions to [Use a Docker image from any private registry](#use-a-docker-image-from-any-private-registry-optional).</span><span class="sxs-lookup"><span data-stu-id="59083-166">See the optional instructions to [Use a Docker image from any private registry](#use-a-docker-image-from-any-private-registry-optional).</span></span>

<!-- # [Docker Hub](#tab/docker-hub)-->

<!-- # [Private Registry](#tab/private-registry)

// Place Private Registry text back here once Tabbed Conceptual bug is fixed

---
-->

### <a name="test-the-web-app"></a><span data-ttu-id="59083-167">Test the web app</span><span class="sxs-lookup"><span data-stu-id="59083-167">Test the web app</span></span>

<span data-ttu-id="59083-168">Verify that the web app works by browsing to it (`http://<app_name>azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="59083-168">Verify that the web app works by browsing to it (`http://<app_name>azurewebsites.net`).</span></span> 

![Test web app port configuration](./media/app-service-linux-using-custom-docker-image/app-service-linux-browse-azure.png)

## <a name="change-web-app-and-redeploy"></a><span data-ttu-id="59083-170">Change web app and redeploy</span><span class="sxs-lookup"><span data-stu-id="59083-170">Change web app and redeploy</span></span>

<span data-ttu-id="59083-171">In your local Git repository, open app/templates/app/index.html.</span><span class="sxs-lookup"><span data-stu-id="59083-171">In your local Git repository, open app/templates/app/index.html.</span></span> <span data-ttu-id="59083-172">Locate the first HTML element and change it to.</span><span class="sxs-lookup"><span data-stu-id="59083-172">Locate the first HTML element and change it to.</span></span>

```python
<nav class="navbar navbar-inverse navbar-fixed-top">
    <div class="container">
      <div class="navbar-header">         
        <a class="navbar-brand" href="#">Azure App Service - Updated Here!</a>       
      </div>            
    </div>
  </nav> 
```

<span data-ttu-id="59083-173">Once you've modified the Python file and saved it, you must rebuild and push the new Docker image.</span><span class="sxs-lookup"><span data-stu-id="59083-173">Once you've modified the Python file and saved it, you must rebuild and push the new Docker image.</span></span> <span data-ttu-id="59083-174">Then restart the web app for the changes to take effect.</span><span class="sxs-lookup"><span data-stu-id="59083-174">Then restart the web app for the changes to take effect.</span></span> <span data-ttu-id="59083-175">Use the same commands that you have previously used in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="59083-175">Use the same commands that you have previously used in this tutorial.</span></span> <span data-ttu-id="59083-176">You can refer to [Build the image from the Docker file](#build-the-image-from-the-docker-file) and [Push the Docker image to Docker Hub](#push-the-docker-image-to-docker-hub).</span><span class="sxs-lookup"><span data-stu-id="59083-176">You can refer to [Build the image from the Docker file](#build-the-image-from-the-docker-file) and [Push the Docker image to Docker Hub](#push-the-docker-image-to-docker-hub).</span></span> <span data-ttu-id="59083-177">Test the web app by following the instructions in [Test the web app](#test-the-web-app).</span><span class="sxs-lookup"><span data-stu-id="59083-177">Test the web app by following the instructions in [Test the web app](#test-the-web-app).</span></span>

## <a name="connect-to-web-app-for-containers-using-ssh"></a><span data-ttu-id="59083-178">Connect to Web App for Containers using SSH</span><span class="sxs-lookup"><span data-stu-id="59083-178">Connect to Web App for Containers using SSH</span></span>

<span data-ttu-id="59083-179">SSH enables secure communication between a container and a client.</span><span class="sxs-lookup"><span data-stu-id="59083-179">SSH enables secure communication between a container and a client.</span></span> <span data-ttu-id="59083-180">In order for a custom Docker image to support SSH, you must build it into a Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="59083-180">In order for a custom Docker image to support SSH, you must build it into a Dockerfile.</span></span> <span data-ttu-id="59083-181">You enable SSH in the Docker file itself.</span><span class="sxs-lookup"><span data-stu-id="59083-181">You enable SSH in the Docker file itself.</span></span> <span data-ttu-id="59083-182">The SSH instructions have already been added to the sample dockerfile, so you can follow these instructions with your own custom image:</span><span class="sxs-lookup"><span data-stu-id="59083-182">The SSH instructions have already been added to the sample dockerfile, so you can follow these instructions with your own custom image:</span></span>

* <span data-ttu-id="59083-183">A [RUN](https://docs.docker.com/engine/reference/builder/#run) instruction that calls `apt-get`, then sets the password for the root account to `"Docker!"`.</span><span class="sxs-lookup"><span data-stu-id="59083-183">A [RUN](https://docs.docker.com/engine/reference/builder/#run) instruction that calls `apt-get`, then sets the password for the root account to `"Docker!"`.</span></span>

    ```docker
    ENV SSH_PASSWD "root:Docker!"
    RUN apt-get update \
            && apt-get install -y --no-install-recommends dialog \
            && apt-get update \
      && apt-get install -y --no-install-recommends openssh-server \
      && echo "$SSH_PASSWD" | chpasswd 
    ```

    > [!NOTE]
    > <span data-ttu-id="59083-184">This configuration does not allow external connections to the container.</span><span class="sxs-lookup"><span data-stu-id="59083-184">This configuration does not allow external connections to the container.</span></span> <span data-ttu-id="59083-185">SSH is available only through the Kudu/SCM Site.</span><span class="sxs-lookup"><span data-stu-id="59083-185">SSH is available only through the Kudu/SCM Site.</span></span> <span data-ttu-id="59083-186">The Kudu/SCM site is authenticated with the publishing credentials.</span><span class="sxs-lookup"><span data-stu-id="59083-186">The Kudu/SCM site is authenticated with the publishing credentials.</span></span>

* <span data-ttu-id="59083-187">A [COPY](https://docs.docker.com/engine/reference/builder/#copy) instruction that instructs the Docker engine to copy the [sshd_config](http://man.openbsd.org/sshd_config) file to the */etc/ssh/* directory.</span><span class="sxs-lookup"><span data-stu-id="59083-187">A [COPY](https://docs.docker.com/engine/reference/builder/#copy) instruction that instructs the Docker engine to copy the [sshd_config](http://man.openbsd.org/sshd_config) file to the */etc/ssh/* directory.</span></span> <span data-ttu-id="59083-188">Your configuration file should be based on [this sshd_config file](https://github.com/Azure-App-Service/node/blob/master/6.11.1/sshd_config).</span><span class="sxs-lookup"><span data-stu-id="59083-188">Your configuration file should be based on [this sshd_config file](https://github.com/Azure-App-Service/node/blob/master/6.11.1/sshd_config).</span></span>

    ```docker
    COPY sshd_config /etc/ssh/
    ```

    > [!NOTE]
    > <span data-ttu-id="59083-189">The *sshd_config* file must include the following items:</span><span class="sxs-lookup"><span data-stu-id="59083-189">The *sshd_config* file must include the following items:</span></span> 
    > * <span data-ttu-id="59083-190">`Ciphers` must include at least one item in this list: `aes128-cbc,3des-cbc,aes256-cbc`.</span><span class="sxs-lookup"><span data-stu-id="59083-190">`Ciphers` must include at least one item in this list: `aes128-cbc,3des-cbc,aes256-cbc`.</span></span>
    > * <span data-ttu-id="59083-191">`MACs` must include at least one item in this list: `hmac-sha1,hmac-sha1-96`.</span><span class="sxs-lookup"><span data-stu-id="59083-191">`MACs` must include at least one item in this list: `hmac-sha1,hmac-sha1-96`.</span></span>

* <span data-ttu-id="59083-192">An [EXPOSE](https://docs.docker.com/engine/reference/builder/#expose) instruction that exposes port 2222 in the container.</span><span class="sxs-lookup"><span data-stu-id="59083-192">An [EXPOSE](https://docs.docker.com/engine/reference/builder/#expose) instruction that exposes port 2222 in the container.</span></span> <span data-ttu-id="59083-193">Although the root password is known, port 2222 cannot be accessed from the internet.</span><span class="sxs-lookup"><span data-stu-id="59083-193">Although the root password is known, port 2222 cannot be accessed from the internet.</span></span> <span data-ttu-id="59083-194">It is an internal port accessible only by containers within the bridge network of a private virtual network.</span><span class="sxs-lookup"><span data-stu-id="59083-194">It is an internal port accessible only by containers within the bridge network of a private virtual network.</span></span> <span data-ttu-id="59083-195">After that, commands copy SSH configuration details and start the `ssh` service.</span><span class="sxs-lookup"><span data-stu-id="59083-195">After that, commands copy SSH configuration details and start the `ssh` service.</span></span>

    ```docker
    EXPOSE 8000 2222
    ```

* <span data-ttu-id="59083-196">Make sure to [start the ssh service](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) by using a shell script in the /bin directory.</span><span class="sxs-lookup"><span data-stu-id="59083-196">Make sure to [start the ssh service](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) by using a shell script in the /bin directory.</span></span>
 
    ```bash
    #!/bin/bash
    service ssh start
    ```
     
### <a name="open-ssh-connection-to-container"></a><span data-ttu-id="59083-197">Open SSH connection to container</span><span class="sxs-lookup"><span data-stu-id="59083-197">Open SSH connection to container</span></span>

<span data-ttu-id="59083-198">Web App for Containers does not allow external connections to the container.</span><span class="sxs-lookup"><span data-stu-id="59083-198">Web App for Containers does not allow external connections to the container.</span></span> <span data-ttu-id="59083-199">SSH is available only through the Kudu site, which is accessible at `https://<app_name>.scm.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="59083-199">SSH is available only through the Kudu site, which is accessible at `https://<app_name>.scm.azurewebsites.net`.</span></span>

<span data-ttu-id="59083-200">To connect, browse to `https://<app_name>.scm.azurewebsites.net/webssh/host` and sign in with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="59083-200">To connect, browse to `https://<app_name>.scm.azurewebsites.net/webssh/host` and sign in with your Azure account.</span></span>

<span data-ttu-id="59083-201">You are then redirected to a page displaying an interactive console.</span><span class="sxs-lookup"><span data-stu-id="59083-201">You are then redirected to a page displaying an interactive console.</span></span> 

<span data-ttu-id="59083-202">You may wish to verify that certain applications are running in the container.</span><span class="sxs-lookup"><span data-stu-id="59083-202">You may wish to verify that certain applications are running in the container.</span></span> <span data-ttu-id="59083-203">To inspect the container and verify running processes, issue the `top` command at the prompt.</span><span class="sxs-lookup"><span data-stu-id="59083-203">To inspect the container and verify running processes, issue the `top` command at the prompt.</span></span>

```bash
top
```

<span data-ttu-id="59083-204">The `top` command exposes all running processes in a container.</span><span class="sxs-lookup"><span data-stu-id="59083-204">The `top` command exposes all running processes in a container.</span></span>

```
PID USER      PR  NI    VIRT    RES    SHR S %CPU %MEM     TIME+ COMMAND
 1 root      20   0  945616  35372  15348 S  0.0  2.1   0:04.63 node
20 root      20   0   55180   2776   2516 S  0.0  0.2   0:00.00 sshd
42 root      20   0  944596  33340  15352 S  0.0  1.9   0:05.80 node /opt/s+
56 root      20   0   59812   5244   4512 S  0.0  0.3   0:00.93 sshd
58 root      20   0   20228   3128   2664 S  0.0  0.2   0:00.00 bash
62 root      20   0   21916   2272   1944 S  0.0  0.1   0:03.15 top
63 root      20   0   59812   5344   4612 S  0.0  0.3   0:00.03 sshd
65 root      20   0   20228   3140   2672 S  0.0  0.2   0:00.00 bash
71 root      20   0   59812   5380   4648 S  0.0  0.3   0:00.02 sshd
73 root      20   0   20228   3160   2696 S  0.0  0.2   0:00.00 bash
77 root      20   0   21920   2304   1972 R  0.0  0.1   0:00.00 top
```

<span data-ttu-id="59083-205">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="59083-205">Congratulations!</span></span> <span data-ttu-id="59083-206">You've configured a custom Docker image for a Web App for Containers.</span><span class="sxs-lookup"><span data-stu-id="59083-206">You've configured a custom Docker image for a Web App for Containers.</span></span>

## <a name="use-a-private-image-from-docker-hub-optional"></a><span data-ttu-id="59083-207">Use a private image from Docker Hub (optional)</span><span class="sxs-lookup"><span data-stu-id="59083-207">Use a private image from Docker Hub (optional)</span></span>

<span data-ttu-id="59083-208">In [Create a web app](#create-a-web-app), you specified an image on Docker Hub in the `az webapp create` command.</span><span class="sxs-lookup"><span data-stu-id="59083-208">In [Create a web app](#create-a-web-app), you specified an image on Docker Hub in the `az webapp create` command.</span></span> <span data-ttu-id="59083-209">This is good enough for a public image.</span><span class="sxs-lookup"><span data-stu-id="59083-209">This is good enough for a public image.</span></span> <span data-ttu-id="59083-210">To use a private image, you need to configure your Docker account ID and password in your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="59083-210">To use a private image, you need to configure your Docker account ID and password in your Azure web app.</span></span>

<span data-ttu-id="59083-211">In the Cloud Shell, follow the `az webapp create` command with [`az webapp config container set`](/cli/azure/webapp/config/container?view=azure-cli-latest#az-webapp-config-container-set).</span><span class="sxs-lookup"><span data-stu-id="59083-211">In the Cloud Shell, follow the `az webapp create` command with [`az webapp config container set`](/cli/azure/webapp/config/container?view=azure-cli-latest#az-webapp-config-container-set).</span></span> <span data-ttu-id="59083-212">Replace *\<app_name>*, and also _\<docker-id>_ and _\<password>_ with your Docker ID and password.</span><span class="sxs-lookup"><span data-stu-id="59083-212">Replace *\<app_name>*, and also _\<docker-id>_ and _\<password>_ with your Docker ID and password.</span></span>

```azurecli-interactive
az webapp config container set --name <app_name> --resource-group myResourceGroup --docker-registry-server-user <docker-id> --docker-registry-server-password <password>
```

<span data-ttu-id="59083-213">The command reveals output similar to the following JSON string, showing that the configuration change succeeded:</span><span class="sxs-lookup"><span data-stu-id="59083-213">The command reveals output similar to the following JSON string, showing that the configuration change succeeded:</span></span>

```json
[
  {
    "name": "WEBSITES_ENABLE_APP_SERVICE_STORAGE",
    "slotSetting": false,
    "value": "false"
  },
  {
    "name": "DOCKER_REGISTRY_SERVER_USERNAME",
    "slotSetting": false,
    "value": "<docker-id>"
  },
  {
    "name": "DOCKER_REGISTRY_SERVER_PASSWORD",
    "slotSetting": false,
    "value": null
  },
  {
    "name": "DOCKER_CUSTOM_IMAGE_NAME",
    "value": "DOCKER|<image-name-and-tag>"
  }
]
```

## <a name="use-a-docker-image-from-any-private-registry-optional"></a><span data-ttu-id="59083-214">Use a Docker image from any private registry (optional)</span><span class="sxs-lookup"><span data-stu-id="59083-214">Use a Docker image from any private registry (optional)</span></span>

<span data-ttu-id="59083-215">In this section, you learn how to use a Docker image from a private registry in Web App for Containers, and it uses Azure Container Registry as an example.</span><span class="sxs-lookup"><span data-stu-id="59083-215">In this section, you learn how to use a Docker image from a private registry in Web App for Containers, and it uses Azure Container Registry as an example.</span></span> <span data-ttu-id="59083-216">The steps for using other private registries are similar.</span><span class="sxs-lookup"><span data-stu-id="59083-216">The steps for using other private registries are similar.</span></span> 

<span data-ttu-id="59083-217">Azure Container Registry is a managed Docker service from Azure for hosting private images.</span><span class="sxs-lookup"><span data-stu-id="59083-217">Azure Container Registry is a managed Docker service from Azure for hosting private images.</span></span> <span data-ttu-id="59083-218">The deployments may be any type, including [Docker Swarm](https://docs.docker.com/engine/swarm/), [Kubernetes](https://kubernetes.io/), and Web App for Containers.</span><span class="sxs-lookup"><span data-stu-id="59083-218">The deployments may be any type, including [Docker Swarm](https://docs.docker.com/engine/swarm/), [Kubernetes](https://kubernetes.io/), and Web App for Containers.</span></span> 

### <a name="create-an-azure-container-registry"></a><span data-ttu-id="59083-219">Create an Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="59083-219">Create an Azure Container Registry</span></span>

<span data-ttu-id="59083-220">In the Cloud Shell, use the [`az acr create`](/cli/azure/acr?view=azure-cli-latest#az-acr-create) command to create an Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="59083-220">In the Cloud Shell, use the [`az acr create`](/cli/azure/acr?view=azure-cli-latest#az-acr-create) command to create an Azure Container Registry.</span></span> <span data-ttu-id="59083-221">Pass in the name, resource group, and `Basic` for the SKU.</span><span class="sxs-lookup"><span data-stu-id="59083-221">Pass in the name, resource group, and `Basic` for the SKU.</span></span> <span data-ttu-id="59083-222">Available SKUs are `Classic`, `Basic`, `Standard`, and `Premium`.</span><span class="sxs-lookup"><span data-stu-id="59083-222">Available SKUs are `Classic`, `Basic`, `Standard`, and `Premium`.</span></span>

```azurecli-interactive
az acr create --name <azure-container-registry-name> --resource-group myResourceGroup --sku Basic --admin-enabled true
```

<span data-ttu-id="59083-223">Creating a container produces the following output:</span><span class="sxs-lookup"><span data-stu-id="59083-223">Creating a container produces the following output:</span></span>

```
 - Finished ..
Create a new service principal and assign access:
  az ad sp create-for-rbac --scopes /subscriptions/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/<azure-container-registry-name> --role Owner --password <password>

Use an existing service principal and assign access:
  az role assignment create --scope /subscriptions/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/<azure-container-registry-name> --role Owner --assignee <app-id>
{
  "adminUserEnabled": false,
  "creationDate": "2017-08-09T04:21:09.654153+00:00",
  "id": "/subscriptions/<subscriptionId>/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/<azure-container-registry-name>",
  "location": "westeurope",
  "loginServer": "<azure-container-registry-name>.azurecr.io",
  "name": "<azure-container-registry-name>",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "myazurecontainerre042025"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

### <a name="log-in-to-azure-container-registry"></a><span data-ttu-id="59083-224">Log in to Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="59083-224">Log in to Azure Container Registry</span></span>

<span data-ttu-id="59083-225">In order to push an image to the registry, you need to supply credentials so the registry accepts the push.</span><span class="sxs-lookup"><span data-stu-id="59083-225">In order to push an image to the registry, you need to supply credentials so the registry accepts the push.</span></span> <span data-ttu-id="59083-226">You can retrieve these credentials by using the [`az acr show`](/cli/azure/acr?view=azure-cli-latest#az-acr-show) command in the Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="59083-226">You can retrieve these credentials by using the [`az acr show`](/cli/azure/acr?view=azure-cli-latest#az-acr-show) command in the Cloud Shell.</span></span> 

```azurecli-interactive
az acr credential show --name <azure-container-registry-name>
```

<span data-ttu-id="59083-227">The command reveals two passwords that can be used with the user name.</span><span class="sxs-lookup"><span data-stu-id="59083-227">The command reveals two passwords that can be used with the user name.</span></span>

```json
<
  "passwords": [
    {
      "name": "password",
      "value": "{password}"
    },
    {
      "name": "password2",
      "value": "{password}"
    }
  ],
  "username": "<registry-username>"
}
```

<span data-ttu-id="59083-228">From your local terminal window, log in to the Azure Container Registry using the `docker login` command.</span><span class="sxs-lookup"><span data-stu-id="59083-228">From your local terminal window, log in to the Azure Container Registry using the `docker login` command.</span></span> <span data-ttu-id="59083-229">The server name is required to log in.</span><span class="sxs-lookup"><span data-stu-id="59083-229">The server name is required to log in.</span></span> <span data-ttu-id="59083-230">Use the format `{azure-container-registry-name>.azurecr.io`.</span><span class="sxs-lookup"><span data-stu-id="59083-230">Use the format `{azure-container-registry-name>.azurecr.io`.</span></span> <span data-ttu-id="59083-231">Type in your password into the console at the prompt.</span><span class="sxs-lookup"><span data-stu-id="59083-231">Type in your password into the console at the prompt.</span></span>

```bash
docker login <azure-container-registry-name>.azurecr.io --username <registry-username>
```

<span data-ttu-id="59083-232">Confirm that the login succeeded.</span><span class="sxs-lookup"><span data-stu-id="59083-232">Confirm that the login succeeded.</span></span> 

### <a name="push-an-image-to-azure-container-registry"></a><span data-ttu-id="59083-233">Push an image to Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="59083-233">Push an image to Azure Container Registry</span></span>

> [!NOTE]
> <span data-ttu-id="59083-234">If you're using your own image, tag the image as follows:</span><span class="sxs-lookup"><span data-stu-id="59083-234">If you're using your own image, tag the image as follows:</span></span>
> ```bash
> docker tag <azure-container-registry-name>.azurecr.io/mydockerimage
> ```

<span data-ttu-id="59083-235">Push the image by using the `docker push` command.</span><span class="sxs-lookup"><span data-stu-id="59083-235">Push the image by using the `docker push` command.</span></span> <span data-ttu-id="59083-236">Tag the image with the name of the registry, followed by your image name and tag.</span><span class="sxs-lookup"><span data-stu-id="59083-236">Tag the image with the name of the registry, followed by your image name and tag.</span></span>

```bash
docker push <azure-container-registry-name>.azurecr.io/mydockerimage:v1.0.0
```

<span data-ttu-id="59083-237">Verify that the push successfully added a container to the registry by listing the ACR repositories.</span><span class="sxs-lookup"><span data-stu-id="59083-237">Verify that the push successfully added a container to the registry by listing the ACR repositories.</span></span> 

```azurecli-interactive
az acr repository list -n <azure-container-registry-name>
```

<span data-ttu-id="59083-238">Listing the images in the registry confirms that `mydockerimage` is in the registry.</span><span class="sxs-lookup"><span data-stu-id="59083-238">Listing the images in the registry confirms that `mydockerimage` is in the registry.</span></span>

```json
[
  "mydockerimage"
]
```

### <a name="configure-web-app-to-use-the-image-from-azure-container-registry-or-any-private-registry"></a><span data-ttu-id="59083-239">Configure Web App to use the image from Azure Container Registry (or any private registry)</span><span class="sxs-lookup"><span data-stu-id="59083-239">Configure Web App to use the image from Azure Container Registry (or any private registry)</span></span>

<span data-ttu-id="59083-240">You can configure Web App for Containers so that it runs a container stored in the Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="59083-240">You can configure Web App for Containers so that it runs a container stored in the Azure Container Registry.</span></span> <span data-ttu-id="59083-241">Using the Azure Container Registry is just like using any private registry, so if you need to use your own private registry, the steps to complete this task are similar.</span><span class="sxs-lookup"><span data-stu-id="59083-241">Using the Azure Container Registry is just like using any private registry, so if you need to use your own private registry, the steps to complete this task are similar.</span></span>

<span data-ttu-id="59083-242">In the Cloud Shell, run [`az acr credential show`](/cli/azure/acr/credential?view=azure-cli-latest#az-acr-credential-show) to display the username and password for the Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="59083-242">In the Cloud Shell, run [`az acr credential show`](/cli/azure/acr/credential?view=azure-cli-latest#az-acr-credential-show) to display the username and password for the Azure Container Registry.</span></span> <span data-ttu-id="59083-243">Copy the username and one of the passwords so you can use it to configure the web app in the next step.</span><span class="sxs-lookup"><span data-stu-id="59083-243">Copy the username and one of the passwords so you can use it to configure the web app in the next step.</span></span>

```bash
az acr credential show --name <azure-container-registry-name>
```

```json
{
  "passwords": [
    {
      "name": "password",
      "value": "password"
    },
    {
      "name": "password2",
      "value": "password2"
    }
  ],
  "username": "<registry-username>"
}
```

<span data-ttu-id="59083-244">In the Cloud Shell, run the [`az webapp config container set`](/cli/azure/webapp/config/container?view=azure-cli-latest#az-webapp-config-container-set) command to assign the custom Docker image to the web app.</span><span class="sxs-lookup"><span data-stu-id="59083-244">In the Cloud Shell, run the [`az webapp config container set`](/cli/azure/webapp/config/container?view=azure-cli-latest#az-webapp-config-container-set) command to assign the custom Docker image to the web app.</span></span> <span data-ttu-id="59083-245">Replace *\<app_name>*, *\<docker-registry-server-url>*, _\<registry-username>_, and _\<password>_.</span><span class="sxs-lookup"><span data-stu-id="59083-245">Replace *\<app_name>*, *\<docker-registry-server-url>*, _\<registry-username>_, and _\<password>_.</span></span> <span data-ttu-id="59083-246">For Azure Container Registry, *\<docker-registry-server-url>* is in the format `https://<azure-container-registry-name>.azurecr.io`.</span><span class="sxs-lookup"><span data-stu-id="59083-246">For Azure Container Registry, *\<docker-registry-server-url>* is in the format `https://<azure-container-registry-name>.azurecr.io`.</span></span> <span data-ttu-id="59083-247">If you are using any registry besides Docker Hub, the image name needs to begin with the fully-qualified domain name (FQDN) of your registry.</span><span class="sxs-lookup"><span data-stu-id="59083-247">If you are using any registry besides Docker Hub, the image name needs to begin with the fully-qualified domain name (FQDN) of your registry.</span></span> <span data-ttu-id="59083-248">For Azure Container Registry, this will look like `<azure-container-registry>.azurecr.io/mydockerimage`.</span><span class="sxs-lookup"><span data-stu-id="59083-248">For Azure Container Registry, this will look like `<azure-container-registry>.azurecr.io/mydockerimage`.</span></span> 

```azurecli-interactive
az webapp config container set --name <app_name> --resource-group myResourceGroup --docker-custom-image-name <azure-container-registry-name>.azurecr.io/mydockerimage --docker-registry-server-url https://<azure-container-registry-name>.azurecr.io --docker-registry-server-user <registry-username> --docker-registry-server-password <password>
```

> [!NOTE]
> <span data-ttu-id="59083-249">`https://` is required in *\<docker-registry-server-url>*.</span><span class="sxs-lookup"><span data-stu-id="59083-249">`https://` is required in *\<docker-registry-server-url>*.</span></span>
>

<span data-ttu-id="59083-250">The command reveals output similar to the following JSON string, showing that the configuration change succeeded:</span><span class="sxs-lookup"><span data-stu-id="59083-250">The command reveals output similar to the following JSON string, showing that the configuration change succeeded:</span></span>

```json
[
  {
    "name": "DOCKER_CUSTOM_IMAGE_NAME",
    "slotSetting": false,
    "value": "mydockerimage"
  },
  {
    "name": "DOCKER_REGISTRY_SERVER_URL",
    "slotSetting": false,
    "value": "<azure-container-registry-name>.azurecr.io"
  },
  {
    "name": "DOCKER_REGISTRY_SERVER_USERNAME",
    "slotSetting": false,
    "value": "<registry-username>"
  },
  {
    "name": "DOCKER_REGISTRY_SERVER_PASSWORD",
    "slotSetting": false,
    "value": null
  }
]
```

[!INCLUDE [Clean-up section](../../../includes/cli-script-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="59083-251">Next steps</span><span class="sxs-lookup"><span data-stu-id="59083-251">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="59083-252">Build a Docker Python and PostgreSQL web app in Azure</span><span class="sxs-lookup"><span data-stu-id="59083-252">Build a Docker Python and PostgreSQL web app in Azure</span></span>](tutorial-docker-python-postgresql-app.md)
