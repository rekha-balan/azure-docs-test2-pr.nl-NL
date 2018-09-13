---
title: Create a function on Linux using a custom image (preview) | Microsoft Docs
description: Learn how to create Azure Functions running on a custom Linux image.
services: functions
keywords: ''
author: ggailey777
ms.author: glenga
ms.date: 11/15/2017
ms.topic: tutorial
ms.service: azure-functions
ms.custom: mvc
ms.devlang: azure-cli
manager: jeconnoc
ms.openlocfilehash: 1fe4e850165f89582683a6b155e64ae5cc63dc87
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867332"
---
# <a name="create-a-function-on-linux-using-a-custom-image-preview"></a><span data-ttu-id="4567d-103">Create a function on Linux using a custom image (preview)</span><span class="sxs-lookup"><span data-stu-id="4567d-103">Create a function on Linux using a custom image (preview)</span></span>

<span data-ttu-id="4567d-104">Azure Functions lets you host your functions on Linux in your own custom container.</span><span class="sxs-lookup"><span data-stu-id="4567d-104">Azure Functions lets you host your functions on Linux in your own custom container.</span></span> <span data-ttu-id="4567d-105">You can also [host on a default Azure App Service container](functions-create-first-azure-function-azure-cli-linux.md).</span><span class="sxs-lookup"><span data-stu-id="4567d-105">You can also [host on a default Azure App Service container](functions-create-first-azure-function-azure-cli-linux.md).</span></span> <span data-ttu-id="4567d-106">This functionality is currently in preview and requires [the Functions 2.0 runtime](functions-versions.md), which is also in preview.</span><span class="sxs-lookup"><span data-stu-id="4567d-106">This functionality is currently in preview and requires [the Functions 2.0 runtime](functions-versions.md), which is also in preview.</span></span>

<span data-ttu-id="4567d-107">In this tutorial, you learn how to deploy a function app as a custom Docker image.</span><span class="sxs-lookup"><span data-stu-id="4567d-107">In this tutorial, you learn how to deploy a function app as a custom Docker image.</span></span> <span data-ttu-id="4567d-108">This pattern is useful when you need to customize the built-in App Service container image.</span><span class="sxs-lookup"><span data-stu-id="4567d-108">This pattern is useful when you need to customize the built-in App Service container image.</span></span> <span data-ttu-id="4567d-109">You may want to use a custom image when your functions need a specific language version or require a specific dependency or configuration that isn't provided within the built-in image.</span><span class="sxs-lookup"><span data-stu-id="4567d-109">You may want to use a custom image when your functions need a specific language version or require a specific dependency or configuration that isn't provided within the built-in image.</span></span>

<span data-ttu-id="4567d-110">This tutorial walks you through how to use Azure Functions to create and push a custom image to Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="4567d-110">This tutorial walks you through how to use Azure Functions to create and push a custom image to Docker Hub.</span></span> <span data-ttu-id="4567d-111">You then use this image as the deployment source for a function app that runs on Linux.</span><span class="sxs-lookup"><span data-stu-id="4567d-111">You then use this image as the deployment source for a function app that runs on Linux.</span></span> <span data-ttu-id="4567d-112">You use Docker to build and push the image.</span><span class="sxs-lookup"><span data-stu-id="4567d-112">You use Docker to build and push the image.</span></span> <span data-ttu-id="4567d-113">You use the Azure CLI to create a function app and deploy the image from Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="4567d-113">You use the Azure CLI to create a function app and deploy the image from Docker Hub.</span></span> 

<span data-ttu-id="4567d-114">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="4567d-114">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4567d-115">Build a custom image using Docker.</span><span class="sxs-lookup"><span data-stu-id="4567d-115">Build a custom image using Docker.</span></span>
> * <span data-ttu-id="4567d-116">Publish a custom image to a container registry.</span><span class="sxs-lookup"><span data-stu-id="4567d-116">Publish a custom image to a container registry.</span></span> 
> * <span data-ttu-id="4567d-117">Create an Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="4567d-117">Create an Azure Storage account.</span></span> 
> * <span data-ttu-id="4567d-118">Create a Linux App Service plan.</span><span class="sxs-lookup"><span data-stu-id="4567d-118">Create a Linux App Service plan.</span></span> 
> * <span data-ttu-id="4567d-119">Deploy a function app from Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="4567d-119">Deploy a function app from Docker Hub.</span></span>
> * <span data-ttu-id="4567d-120">Add application settings to the function app.</span><span class="sxs-lookup"><span data-stu-id="4567d-120">Add application settings to the function app.</span></span> 

<span data-ttu-id="4567d-121">The following steps are supported on a Mac, Windows, or Linux computer.</span><span class="sxs-lookup"><span data-stu-id="4567d-121">The following steps are supported on a Mac, Windows, or Linux computer.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="4567d-122">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4567d-122">Prerequisites</span></span>

<span data-ttu-id="4567d-123">To complete this tutorial, you need:</span><span class="sxs-lookup"><span data-stu-id="4567d-123">To complete this tutorial, you need:</span></span>

* [<span data-ttu-id="4567d-124">Git</span><span class="sxs-lookup"><span data-stu-id="4567d-124">Git</span></span>](https://git-scm.com/downloads)
* <span data-ttu-id="4567d-125">An active [Azure subscription](https://azure.microsoft.com/pricing/free-trial/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio)</span><span class="sxs-lookup"><span data-stu-id="4567d-125">An active [Azure subscription](https://azure.microsoft.com/pricing/free-trial/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio)</span></span>
* [<span data-ttu-id="4567d-126">Docker</span><span class="sxs-lookup"><span data-stu-id="4567d-126">Docker</span></span>](https://docs.docker.com/install/)
* <span data-ttu-id="4567d-127">A [Docker Hub account](https://docs.docker.com/docker-id/)</span><span class="sxs-lookup"><span data-stu-id="4567d-127">A [Docker Hub account](https://docs.docker.com/docker-id/)</span></span>

[!INCLUDE [Free trial note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-the-sample"></a><span data-ttu-id="4567d-128">Download the sample</span><span class="sxs-lookup"><span data-stu-id="4567d-128">Download the sample</span></span>

<span data-ttu-id="4567d-129">In a terminal window, run the following command to clone the sample app repository to your local machine, then change to the directory that contains the sample code.</span><span class="sxs-lookup"><span data-stu-id="4567d-129">In a terminal window, run the following command to clone the sample app repository to your local machine, then change to the directory that contains the sample code.</span></span>

```bash
git clone https://github.com/Azure-Samples/functions-linux-custom-image.git --config core.autocrlf=input
cd functions-linux-custom-image
```

## <a name="build-the-image-from-the-docker-file"></a><span data-ttu-id="4567d-130">Build the image from the Docker file</span><span class="sxs-lookup"><span data-stu-id="4567d-130">Build the image from the Docker file</span></span>

<span data-ttu-id="4567d-131">In this Git repository, take a look at the _Dockerfile_.</span><span class="sxs-lookup"><span data-stu-id="4567d-131">In this Git repository, take a look at the _Dockerfile_.</span></span> <span data-ttu-id="4567d-132">This file describes the environment that is required to run the function app on Linux.</span><span class="sxs-lookup"><span data-stu-id="4567d-132">This file describes the environment that is required to run the function app on Linux.</span></span> 

```docker
# Base the image on the built-in Azure Functions Linux image.
FROM microsoft/azure-functions-runtime:2.0.0-jessie
ENV AzureWebJobsScriptRoot=/home/site/wwwroot

# Add files from this repo to the root site folder.
COPY . /home/site/wwwroot 
```
>[!NOTE]
> <span data-ttu-id="4567d-133">When hosting an image in a private container registry, you should add the connection settings to the function app by using **ENV** variables in the Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="4567d-133">When hosting an image in a private container registry, you should add the connection settings to the function app by using **ENV** variables in the Dockerfile.</span></span> <span data-ttu-id="4567d-134">Because this tutorial cannot guarantee that you use a private registry, the connection settings are [added after the deployment by using the Azure CLI](#configure-the-function-app) as a security best practice.</span><span class="sxs-lookup"><span data-stu-id="4567d-134">Because this tutorial cannot guarantee that you use a private registry, the connection settings are [added after the deployment by using the Azure CLI](#configure-the-function-app) as a security best practice.</span></span>   

### <a name="run-the-build-command"></a><span data-ttu-id="4567d-135">Run the Build command</span><span class="sxs-lookup"><span data-stu-id="4567d-135">Run the Build command</span></span>
<span data-ttu-id="4567d-136">To build the Docker image, run the `docker build` command, and provide a name, `mydockerimage`, and tag, `v1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="4567d-136">To build the Docker image, run the `docker build` command, and provide a name, `mydockerimage`, and tag, `v1.0.0`.</span></span> <span data-ttu-id="4567d-137">Replace `<docker-id>` with your Docker Hub account ID.</span><span class="sxs-lookup"><span data-stu-id="4567d-137">Replace `<docker-id>` with your Docker Hub account ID.</span></span>

```bash
docker build --tag <docker-id>/mydockerimage:v1.0.0 .
```

<span data-ttu-id="4567d-138">The command produces output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="4567d-138">The command produces output similar to the following:</span></span>

```bash
Sending build context to Docker daemon  169.5kB
Step 1/3 : FROM microsoft/azure-functions-runtime:v2.0.0-jessie
v2.0.0-jessie: Pulling from microsoft/azure-functions-runtime
b178b12f7913: Pull complete
2d9ce077a781: Pull complete
4775d4ba55c8: Pull complete
Digest: sha256:073f45fc167b3b5c6642ef4b3c99064430d6b17507095...
Status: Downloaded newer image for microsoft/azure-functions-runtime:v2.0.0-jessie
 ---> 217799efa500
Step 2/3 : ENV AzureWebJobsScriptRoot /home/site/wwwroot
 ---> Running in 528fa2077d17
 ---> 7cc6323b8ae0
Removing intermediate container 528fa2077d17
Step 3/3 : COPY . /home/site/wwwroot
 ---> 5bdac9878423
Successfully built 5bdac9878423
Successfully tagged ggailey777/mydockerimage:v1.0.0
```

### <a name="test-the-image-locally"></a><span data-ttu-id="4567d-139">Test the image locally</span><span class="sxs-lookup"><span data-stu-id="4567d-139">Test the image locally</span></span>
<span data-ttu-id="4567d-140">Verify that the built image works by running the Docker image in a local container.</span><span class="sxs-lookup"><span data-stu-id="4567d-140">Verify that the built image works by running the Docker image in a local container.</span></span> <span data-ttu-id="4567d-141">Issue the [docker run](https://docs.docker.com/engine/reference/commandline/run/) command and pass the name and tag of the image to it.</span><span class="sxs-lookup"><span data-stu-id="4567d-141">Issue the [docker run](https://docs.docker.com/engine/reference/commandline/run/) command and pass the name and tag of the image to it.</span></span> <span data-ttu-id="4567d-142">Be sure to specify the port using the `-p` argument.</span><span class="sxs-lookup"><span data-stu-id="4567d-142">Be sure to specify the port using the `-p` argument.</span></span>

```bash
docker run -p 8080:80 -it <docker-ID>/mydockerimage:v1.0.0
```

<span data-ttu-id="4567d-143">With the custom image running in a local Docker container, verify the function app and container are functioning correctly by browsing to <http://localhost:8080>.</span><span class="sxs-lookup"><span data-stu-id="4567d-143">With the custom image running in a local Docker container, verify the function app and container are functioning correctly by browsing to <http://localhost:8080>.</span></span>

![Test the function app locally.](./media/functions-create-function-linux-custom-image/run-image-local-success.png)

<span data-ttu-id="4567d-145">After you have verified the function app in the container, stop the execution.</span><span class="sxs-lookup"><span data-stu-id="4567d-145">After you have verified the function app in the container, stop the execution.</span></span> <span data-ttu-id="4567d-146">Now, you can push the custom image to your Docker Hub account.</span><span class="sxs-lookup"><span data-stu-id="4567d-146">Now, you can push the custom image to your Docker Hub account.</span></span>

## <a name="push-the-custom-image-to-docker-hub"></a><span data-ttu-id="4567d-147">Push the custom image to Docker Hub</span><span class="sxs-lookup"><span data-stu-id="4567d-147">Push the custom image to Docker Hub</span></span>

<span data-ttu-id="4567d-148">A registry is an application that hosts images and provides services image and container services.</span><span class="sxs-lookup"><span data-stu-id="4567d-148">A registry is an application that hosts images and provides services image and container services.</span></span> <span data-ttu-id="4567d-149">In order to share your image, you must push it to a registry.</span><span class="sxs-lookup"><span data-stu-id="4567d-149">In order to share your image, you must push it to a registry.</span></span> <span data-ttu-id="4567d-150">Docker Hub is a registry for Docker images that allows you to host your own repositories, either public or private.</span><span class="sxs-lookup"><span data-stu-id="4567d-150">Docker Hub is a registry for Docker images that allows you to host your own repositories, either public or private.</span></span> 

<span data-ttu-id="4567d-151">Before you can push an image, you must sign in to Docker Hub using the [docker login](https://docs.docker.com/engine/reference/commandline/login/) command.</span><span class="sxs-lookup"><span data-stu-id="4567d-151">Before you can push an image, you must sign in to Docker Hub using the [docker login](https://docs.docker.com/engine/reference/commandline/login/) command.</span></span> <span data-ttu-id="4567d-152">Replace `<docker-id>` with your account name and type in your password into the console at the prompt.</span><span class="sxs-lookup"><span data-stu-id="4567d-152">Replace `<docker-id>` with your account name and type in your password into the console at the prompt.</span></span> <span data-ttu-id="4567d-153">For other Docker Hub password options, see the [docker login command documentation](https://docs.docker.com/engine/reference/commandline/login/).</span><span class="sxs-lookup"><span data-stu-id="4567d-153">For other Docker Hub password options, see the [docker login command documentation](https://docs.docker.com/engine/reference/commandline/login/).</span></span>

```bash
docker login --username <docker-id> 
```

<span data-ttu-id="4567d-154">A "login succeeded" message confirms that you are logged in.</span><span class="sxs-lookup"><span data-stu-id="4567d-154">A "login succeeded" message confirms that you are logged in.</span></span> <span data-ttu-id="4567d-155">After you have signed in, you push the image to Docker Hub by using the [docker push](https://docs.docker.com/engine/reference/commandline/push/) command.</span><span class="sxs-lookup"><span data-stu-id="4567d-155">After you have signed in, you push the image to Docker Hub by using the [docker push](https://docs.docker.com/engine/reference/commandline/push/) command.</span></span>

```bash
docker push <docker-id>/mydockerimage:v1.0.0
```

<span data-ttu-id="4567d-156">Verify that the push succeeded by examining the command's output.</span><span class="sxs-lookup"><span data-stu-id="4567d-156">Verify that the push succeeded by examining the command's output.</span></span>

```bash
The push refers to a repository [docker.io/<docker-id>/mydockerimage:v1.0.0]
24d81eb139bf: Pushed
fd9e998161c9: Mounted from microsoft/azure-functions-runtime
e7796c35add2: Mounted from microsoft/azure-functions-runtime
ae9a05b85848: Mounted from microsoft/azure-functions-runtime
45c86e20670d: Mounted from microsoft/azure-functions-runtime
v1.0.0: digest: sha256:be080d80770df71234eb893fbe4d... size: 2422
```
<span data-ttu-id="4567d-157">Now, you can use this image as the deployment source for a new function app in Azure.</span><span class="sxs-lookup"><span data-stu-id="4567d-157">Now, you can use this image as the deployment source for a new function app in Azure.</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4567d-158">If you choose to install and use the CLI locally, this topic requires the Azure CLI version 2.0.21 or later.</span><span class="sxs-lookup"><span data-stu-id="4567d-158">If you choose to install and use the CLI locally, this topic requires the Azure CLI version 2.0.21 or later.</span></span> <span data-ttu-id="4567d-159">Run `az --version` to find the version you have.</span><span class="sxs-lookup"><span data-stu-id="4567d-159">Run `az --version` to find the version you have.</span></span> <span data-ttu-id="4567d-160">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4567d-160">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [functions-create-resource-group](../../includes/functions-create-resource-group.md)]

[!INCLUDE [functions-create-storage-account](../../includes/functions-create-storage-account.md)]

## <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="4567d-161">Create a Linux App Service plan</span><span class="sxs-lookup"><span data-stu-id="4567d-161">Create a Linux App Service plan</span></span>

<span data-ttu-id="4567d-162">Linux hosting for Functions is currently not supported on consumption plans.</span><span class="sxs-lookup"><span data-stu-id="4567d-162">Linux hosting for Functions is currently not supported on consumption plans.</span></span> <span data-ttu-id="4567d-163">You must run on a Linux App Service plan.</span><span class="sxs-lookup"><span data-stu-id="4567d-163">You must run on a Linux App Service plan.</span></span> <span data-ttu-id="4567d-164">To learn more about hosting, see [Azure Functions hosting plans comparison](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="4567d-164">To learn more about hosting, see [Azure Functions hosting plans comparison](functions-scale.md).</span></span> 

[!INCLUDE [app-service-plan-no-h](../../includes/app-service-web-create-app-service-plan-linux-no-h.md)]


## <a name="create-and-deploy-the-custom-image"></a><span data-ttu-id="4567d-165">Create and deploy the custom image</span><span class="sxs-lookup"><span data-stu-id="4567d-165">Create and deploy the custom image</span></span>

<span data-ttu-id="4567d-166">The function app hosts the execution of your functions.</span><span class="sxs-lookup"><span data-stu-id="4567d-166">The function app hosts the execution of your functions.</span></span> <span data-ttu-id="4567d-167">Create a function app from a Docker Hub image by using the [az functionapp create](/cli/azure/functionapp#az-functionapp-create) command.</span><span class="sxs-lookup"><span data-stu-id="4567d-167">Create a function app from a Docker Hub image by using the [az functionapp create](/cli/azure/functionapp#az-functionapp-create) command.</span></span> 

<span data-ttu-id="4567d-168">In the following command, substitute a unique function app name where you see the `<app_name>` placeholder and the storage account name for  `<storage_name>`.</span><span class="sxs-lookup"><span data-stu-id="4567d-168">In the following command, substitute a unique function app name where you see the `<app_name>` placeholder and the storage account name for  `<storage_name>`.</span></span> <span data-ttu-id="4567d-169">The `<app_name>` is used as the default DNS domain for the function app, and so the name needs to be unique across all apps in Azure.</span><span class="sxs-lookup"><span data-stu-id="4567d-169">The `<app_name>` is used as the default DNS domain for the function app, and so the name needs to be unique across all apps in Azure.</span></span> <span data-ttu-id="4567d-170">As before, `<docker-id>` is your Docker account name.</span><span class="sxs-lookup"><span data-stu-id="4567d-170">As before, `<docker-id>` is your Docker account name.</span></span>

```azurecli-interactive
az functionapp create --name <app_name> --storage-account  <storage_name>  --resource-group myResourceGroup \
--plan myAppServicePlan --deployment-container-image-name <docker-id>/mydockerimage:v1.0.0 
```
<span data-ttu-id="4567d-171">After the function app has been created, the Azure CLI shows information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="4567d-171">After the function app has been created, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "containerSize": 1536,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "quickstart.azurewebsites.net",
  "enabled": true,
  "enabledHostNames": [
    "quickstart.azurewebsites.net",
    "quickstart.scm.azurewebsites.net"
  ],
   ....
    // Remaining output has been truncated for readability.
}
```

<span data-ttu-id="4567d-172">The _deployment-container-image-name_ parameter indicates the image hosted on Docker Hub to use to create the function app.</span><span class="sxs-lookup"><span data-stu-id="4567d-172">The _deployment-container-image-name_ parameter indicates the image hosted on Docker Hub to use to create the function app.</span></span> 


## <a name="configure-the-function-app"></a><span data-ttu-id="4567d-173">Configure the function app</span><span class="sxs-lookup"><span data-stu-id="4567d-173">Configure the function app</span></span>

<span data-ttu-id="4567d-174">The function needs the connection string to connect to the default storage account.</span><span class="sxs-lookup"><span data-stu-id="4567d-174">The function needs the connection string to connect to the default storage account.</span></span> <span data-ttu-id="4567d-175">When you are publishing your custom image to a private container account, you should instead set these application settings as environment variables in the Dockerfile using the [ENV instruction](https://docs.docker.com/engine/reference/builder/#env), or equivalent.</span><span class="sxs-lookup"><span data-stu-id="4567d-175">When you are publishing your custom image to a private container account, you should instead set these application settings as environment variables in the Dockerfile using the [ENV instruction](https://docs.docker.com/engine/reference/builder/#env), or equivalent.</span></span> 

<span data-ttu-id="4567d-176">In this case, `<storage_account>` is the name of the storage account you created.</span><span class="sxs-lookup"><span data-stu-id="4567d-176">In this case, `<storage_account>` is the name of the storage account you created.</span></span> <span data-ttu-id="4567d-177">Get the connection string with the [az storage account show-connection-string](/cli/azure/storage/account#show-connection-string) command.</span><span class="sxs-lookup"><span data-stu-id="4567d-177">Get the connection string with the [az storage account show-connection-string](/cli/azure/storage/account#show-connection-string) command.</span></span> <span data-ttu-id="4567d-178">Add these application settings in the function app with the [az functionapp config appsettings set](/cli/azure/functionapp/config/appsettings#az-functionapp-config-appsettings-set) command.</span><span class="sxs-lookup"><span data-stu-id="4567d-178">Add these application settings in the function app with the [az functionapp config appsettings set](/cli/azure/functionapp/config/appsettings#az-functionapp-config-appsettings-set) command.</span></span>

```azurecli-interactive
storageConnectionString=$(az storage account show-connection-string \
--resource-group myResourceGroup --name <storage_account> \
--query connectionString --output tsv)

az functionapp config appsettings set --name <function_app> \
--resource-group myResourceGroup \
--settings AzureWebJobsDashboard=$storageConnectionString \
AzureWebJobsStorage=$storageConnectionString
```

<span data-ttu-id="4567d-179">You can now test your functions running on Linux in Azure.</span><span class="sxs-lookup"><span data-stu-id="4567d-179">You can now test your functions running on Linux in Azure.</span></span>

[!INCLUDE [functions-test-function-code](../../includes/functions-test-function-code.md)]

[!INCLUDE [functions-cleanup-resources](../../includes/functions-cleanup-resources.md)]

## <a name="next-steps"></a><span data-ttu-id="4567d-180">Next steps</span><span class="sxs-lookup"><span data-stu-id="4567d-180">Next steps</span></span>

<span data-ttu-id="4567d-181">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="4567d-181">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4567d-182">Build a custom image using Docker.</span><span class="sxs-lookup"><span data-stu-id="4567d-182">Build a custom image using Docker.</span></span>
> * <span data-ttu-id="4567d-183">Publish a custom image to a container registry.</span><span class="sxs-lookup"><span data-stu-id="4567d-183">Publish a custom image to a container registry.</span></span> 
> * <span data-ttu-id="4567d-184">Create an Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="4567d-184">Create an Azure Storage account.</span></span> 
> * <span data-ttu-id="4567d-185">Create a Linux App Service plan.</span><span class="sxs-lookup"><span data-stu-id="4567d-185">Create a Linux App Service plan.</span></span> 
> * <span data-ttu-id="4567d-186">Deploy a function app from Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="4567d-186">Deploy a function app from Docker Hub.</span></span>
> * <span data-ttu-id="4567d-187">Add application settings to the function app.</span><span class="sxs-lookup"><span data-stu-id="4567d-187">Add application settings to the function app.</span></span>

<span data-ttu-id="4567d-188">Learn how to enable continuous integration functionality built into the core App Service platform.</span><span class="sxs-lookup"><span data-stu-id="4567d-188">Learn how to enable continuous integration functionality built into the core App Service platform.</span></span> <span data-ttu-id="4567d-189">You can configure your function app so that the container is redeployed when you update your image in Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="4567d-189">You can configure your function app so that the container is redeployed when you update your image in Docker Hub.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="4567d-190">Continuous deployment with Web App for Containers</span><span class="sxs-lookup"><span data-stu-id="4567d-190">Continuous deployment with Web App for Containers</span></span>](../app-service/containers/app-service-linux-ci-cd.md)
