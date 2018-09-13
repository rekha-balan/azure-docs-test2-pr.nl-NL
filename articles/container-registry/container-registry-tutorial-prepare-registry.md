---
title: Azure Container Registry tutorial - Prepare a geo-replicated Azure container registry
description: Create an Azure container registry, configure geo-replication, prepare a Docker image, and deploy it to the registry. Part one of a three-part series.
services: container-registry
author: mmacy
manager: jeconnoc
ms.service: container-registry
ms.topic: tutorial
ms.date: 04/30/2017
ms.author: marsma
ms.custom: mvc
ms.openlocfilehash: 379878e261007eca13a4e455ef2b97237c81eeba
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867458"
---
# <a name="tutorial-prepare-a-geo-replicated-azure-container-registry"></a><span data-ttu-id="ecf3b-104">Tutorial: Prepare a geo-replicated Azure container registry</span><span class="sxs-lookup"><span data-stu-id="ecf3b-104">Tutorial: Prepare a geo-replicated Azure container registry</span></span>

<span data-ttu-id="ecf3b-105">An Azure container registry is a private Docker registry deployed in Azure that you can keep network-close to your deployments.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-105">An Azure container registry is a private Docker registry deployed in Azure that you can keep network-close to your deployments.</span></span> <span data-ttu-id="ecf3b-106">In this set of three tutorial articles, you learn how to use geo-replication to deploy an ASP.NET Core web application running in a Linux container to two [Web Apps for Containers](../app-service/containers/index.yml) instances.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-106">In this set of three tutorial articles, you learn how to use geo-replication to deploy an ASP.NET Core web application running in a Linux container to two [Web Apps for Containers](../app-service/containers/index.yml) instances.</span></span> <span data-ttu-id="ecf3b-107">You'll see how Azure automatically deploys the image to each Web App instance from the closest geo-replicated repository.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-107">You'll see how Azure automatically deploys the image to each Web App instance from the closest geo-replicated repository.</span></span>

<span data-ttu-id="ecf3b-108">In this tutorial, part one in a three-part series:</span><span class="sxs-lookup"><span data-stu-id="ecf3b-108">In this tutorial, part one in a three-part series:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ecf3b-109">Create a geo-replicated Azure container registry</span><span class="sxs-lookup"><span data-stu-id="ecf3b-109">Create a geo-replicated Azure container registry</span></span>
> * <span data-ttu-id="ecf3b-110">Clone application source code from GitHub</span><span class="sxs-lookup"><span data-stu-id="ecf3b-110">Clone application source code from GitHub</span></span>
> * <span data-ttu-id="ecf3b-111">Build a Docker container image from application source</span><span class="sxs-lookup"><span data-stu-id="ecf3b-111">Build a Docker container image from application source</span></span>
> * <span data-ttu-id="ecf3b-112">Push the container image to your registry</span><span class="sxs-lookup"><span data-stu-id="ecf3b-112">Push the container image to your registry</span></span>

<span data-ttu-id="ecf3b-113">In subsequent tutorials, you deploy the container from your private registry to a web app running in two Azure regions.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-113">In subsequent tutorials, you deploy the container from your private registry to a web app running in two Azure regions.</span></span> <span data-ttu-id="ecf3b-114">You then update the code in the application, and update both Web App instances with a single `docker push` to your registry.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-114">You then update the code in the application, and update both Web App instances with a single `docker push` to your registry.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ecf3b-115">Before you begin</span><span class="sxs-lookup"><span data-stu-id="ecf3b-115">Before you begin</span></span>

<span data-ttu-id="ecf3b-116">This tutorial requires a local installation of the Azure CLI (version 2.0.31 or later).</span><span class="sxs-lookup"><span data-stu-id="ecf3b-116">This tutorial requires a local installation of the Azure CLI (version 2.0.31 or later).</span></span> <span data-ttu-id="ecf3b-117">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-117">Run `az --version` to find the version.</span></span> <span data-ttu-id="ecf3b-118">If you need to install or upgrade, see [Install Azure CLI]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ecf3b-118">If you need to install or upgrade, see [Install Azure CLI]( /cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="ecf3b-119">You should be familiar with core Docker concepts such as containers, container images, and basic Docker CLI commands.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-119">You should be familiar with core Docker concepts such as containers, container images, and basic Docker CLI commands.</span></span> <span data-ttu-id="ecf3b-120">For a primer on container basics, see [Get started with Docker]( https://docs.docker.com/get-started/).</span><span class="sxs-lookup"><span data-stu-id="ecf3b-120">For a primer on container basics, see [Get started with Docker]( https://docs.docker.com/get-started/).</span></span>

<span data-ttu-id="ecf3b-121">To complete this tutorial, you need a local Docker installation.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-121">To complete this tutorial, you need a local Docker installation.</span></span> <span data-ttu-id="ecf3b-122">Docker provides installation instructions for [macOS](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/), and [Linux](https://docs.docker.com/engine/installation/#supported-platforms) systems.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-122">Docker provides installation instructions for [macOS](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/), and [Linux](https://docs.docker.com/engine/installation/#supported-platforms) systems.</span></span>

<span data-ttu-id="ecf3b-123">Azure Cloud Shell does not include the Docker components required to complete every step this tutorial.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-123">Azure Cloud Shell does not include the Docker components required to complete every step this tutorial.</span></span> <span data-ttu-id="ecf3b-124">Therefore, we recommend a local installation of the Azure CLI and Docker development environment.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-124">Therefore, we recommend a local installation of the Azure CLI and Docker development environment.</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="ecf3b-125">Create a container registry</span><span class="sxs-lookup"><span data-stu-id="ecf3b-125">Create a container registry</span></span>

<span data-ttu-id="ecf3b-126">Sign in to the [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ecf3b-126">Sign in to the [Azure portal](http://portal.azure.com).</span></span>

<span data-ttu-id="ecf3b-127">Select **Create a resource** > **Containers** > **Azure Container Registry**.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-127">Select **Create a resource** > **Containers** > **Azure Container Registry**.</span></span>

![Creating a container registry in the Azure portal][tut-portal-01]

<span data-ttu-id="ecf3b-129">Configure your new registry with the following settings:</span><span class="sxs-lookup"><span data-stu-id="ecf3b-129">Configure your new registry with the following settings:</span></span>

* <span data-ttu-id="ecf3b-130">**Registry name**: Create a registry name that's globally unique within Azure, and contains 5-50 alphanumeric characters</span><span class="sxs-lookup"><span data-stu-id="ecf3b-130">**Registry name**: Create a registry name that's globally unique within Azure, and contains 5-50 alphanumeric characters</span></span>
* <span data-ttu-id="ecf3b-131">**Resource Group**: **Create new** > `myResourceGroup`</span><span class="sxs-lookup"><span data-stu-id="ecf3b-131">**Resource Group**: **Create new** > `myResourceGroup`</span></span>
* <span data-ttu-id="ecf3b-132">**Location**: `West US`</span><span class="sxs-lookup"><span data-stu-id="ecf3b-132">**Location**: `West US`</span></span>
* <span data-ttu-id="ecf3b-133">**Admin user**: `Enable` (required for Web App for Containers to pull images)</span><span class="sxs-lookup"><span data-stu-id="ecf3b-133">**Admin user**: `Enable` (required for Web App for Containers to pull images)</span></span>
* <span data-ttu-id="ecf3b-134">**SKU**: `Premium` (required for geo-replication)</span><span class="sxs-lookup"><span data-stu-id="ecf3b-134">**SKU**: `Premium` (required for geo-replication)</span></span>

<span data-ttu-id="ecf3b-135">Select **Create** to deploy the ACR instance.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-135">Select **Create** to deploy the ACR instance.</span></span>

![Creating a container registry in the Azure portal][tut-portal-02]

<span data-ttu-id="ecf3b-137">Throughout the rest of this tutorial, we use `<acrName>` as a placeholder for the container **Registry name** that you chose.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-137">Throughout the rest of this tutorial, we use `<acrName>` as a placeholder for the container **Registry name** that you chose.</span></span>

> [!TIP]
> <span data-ttu-id="ecf3b-138">Because Azure container registries are typically long-lived resources that are used across multiple container hosts, we recommend that you create your registry in its own resource group.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-138">Because Azure container registries are typically long-lived resources that are used across multiple container hosts, we recommend that you create your registry in its own resource group.</span></span> <span data-ttu-id="ecf3b-139">As you configure geo-replicated registries and webhooks, these additional resources are placed in the same resource group.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-139">As you configure geo-replicated registries and webhooks, these additional resources are placed in the same resource group.</span></span>
>

## <a name="configure-geo-replication"></a><span data-ttu-id="ecf3b-140">Configure geo-replication</span><span class="sxs-lookup"><span data-stu-id="ecf3b-140">Configure geo-replication</span></span>

<span data-ttu-id="ecf3b-141">Now that you have a Premium registry, you can configure geo-replication.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-141">Now that you have a Premium registry, you can configure geo-replication.</span></span> <span data-ttu-id="ecf3b-142">Your web app, which you configure in the next tutorial to run in two regions, can then pull its container images from the nearest registry.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-142">Your web app, which you configure in the next tutorial to run in two regions, can then pull its container images from the nearest registry.</span></span>

<span data-ttu-id="ecf3b-143">Navigate to your new container registry in the Azure portal and select **Replications** under **SERVICES**:</span><span class="sxs-lookup"><span data-stu-id="ecf3b-143">Navigate to your new container registry in the Azure portal and select **Replications** under **SERVICES**:</span></span>

![Replications in the Azure portal container registry UI][tut-portal-03]

<span data-ttu-id="ecf3b-145">A map is displayed showing green hexagons representing Azure regions available for geo-replication:</span><span class="sxs-lookup"><span data-stu-id="ecf3b-145">A map is displayed showing green hexagons representing Azure regions available for geo-replication:</span></span>

 ![Region map in the Azure portal][tut-map-01]

<span data-ttu-id="ecf3b-147">Replicate your registry to the East US region by selecting its green hexagon, then select **Create** under **Create replication**:</span><span class="sxs-lookup"><span data-stu-id="ecf3b-147">Replicate your registry to the East US region by selecting its green hexagon, then select **Create** under **Create replication**:</span></span>

 ![Create replication UI in the Azure portal][tut-portal-04]

<span data-ttu-id="ecf3b-149">When the replication is complete, the portal reflects *Ready* for both regions.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-149">When the replication is complete, the portal reflects *Ready* for both regions.</span></span> <span data-ttu-id="ecf3b-150">Use the **Refresh** button to refresh the status of the replication; it can take a minute or so for the replicas to be created and synchronized.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-150">Use the **Refresh** button to refresh the status of the replication; it can take a minute or so for the replicas to be created and synchronized.</span></span>

![Replication status UI in the Azure portal][tut-portal-05]

## <a name="container-registry-login"></a><span data-ttu-id="ecf3b-152">Container registry login</span><span class="sxs-lookup"><span data-stu-id="ecf3b-152">Container registry login</span></span>

<span data-ttu-id="ecf3b-153">Now that you've configured geo-replication, build a container image and push it to your registry.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-153">Now that you've configured geo-replication, build a container image and push it to your registry.</span></span> <span data-ttu-id="ecf3b-154">You must first log in to your ACR instance before pushing images to it.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-154">You must first log in to your ACR instance before pushing images to it.</span></span>

<span data-ttu-id="ecf3b-155">Use the [az acr login](https://docs.microsoft.com/cli/azure/acr#az-acr-login) command to authenticate and cache the credentials for your registry.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-155">Use the [az acr login](https://docs.microsoft.com/cli/azure/acr#az-acr-login) command to authenticate and cache the credentials for your registry.</span></span> <span data-ttu-id="ecf3b-156">Replace `<acrName>` with the name of the registry you created earlier.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-156">Replace `<acrName>` with the name of the registry you created earlier.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="ecf3b-157">The command returns `Login Succeeded` when complete.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-157">The command returns `Login Succeeded` when complete.</span></span>

## <a name="get-application-code"></a><span data-ttu-id="ecf3b-158">Get application code</span><span class="sxs-lookup"><span data-stu-id="ecf3b-158">Get application code</span></span>

<span data-ttu-id="ecf3b-159">The sample in this tutorial includes a small web application built with [ASP.NET Core][aspnet-core].</span><span class="sxs-lookup"><span data-stu-id="ecf3b-159">The sample in this tutorial includes a small web application built with [ASP.NET Core][aspnet-core].</span></span> <span data-ttu-id="ecf3b-160">The app serves an HTML page that displays the region from which the image was deployed by Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-160">The app serves an HTML page that displays the region from which the image was deployed by Azure Container Registry.</span></span>

![Tutorial app shown in browser][tut-app-01]

<span data-ttu-id="ecf3b-162">Use git to download the sample into a local directory, and `cd` into the directory:</span><span class="sxs-lookup"><span data-stu-id="ecf3b-162">Use git to download the sample into a local directory, and `cd` into the directory:</span></span>

```bash
git clone https://github.com/Azure-Samples/acr-helloworld.git
cd acr-helloworld
```

<span data-ttu-id="ecf3b-163">If you don't have `git` installed, you can [download the ZIP archive][acr-helloworld-zip] directly from GitHub.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-163">If you don't have `git` installed, you can [download the ZIP archive][acr-helloworld-zip] directly from GitHub.</span></span>

## <a name="update-dockerfile"></a><span data-ttu-id="ecf3b-164">Update Dockerfile</span><span class="sxs-lookup"><span data-stu-id="ecf3b-164">Update Dockerfile</span></span>

<span data-ttu-id="ecf3b-165">The Dockerfile included in the sample shows how the container is built.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-165">The Dockerfile included in the sample shows how the container is built.</span></span> <span data-ttu-id="ecf3b-166">It starts from an official [aspnetcore][dockerhub-aspnetcore] image, copies the application files into the container, installs dependencies, compiles the output using the official [aspnetcore-build][dockerhub-aspnetcore-build] image, and finally, builds an optimized aspnetcore image.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-166">It starts from an official [aspnetcore][dockerhub-aspnetcore] image, copies the application files into the container, installs dependencies, compiles the output using the official [aspnetcore-build][dockerhub-aspnetcore-build] image, and finally, builds an optimized aspnetcore image.</span></span>

<span data-ttu-id="ecf3b-167">The [Dockerfile][dockerfile] is located at `./AcrHelloworld/Dockerfile` in the cloned source.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-167">The [Dockerfile][dockerfile] is located at `./AcrHelloworld/Dockerfile` in the cloned source.</span></span>

```dockerfile
FROM microsoft/aspnetcore:2.0 AS base
# Update <acrName> with the name of your registry
# Example: uniqueregistryname.azurecr.io
ENV DOCKER_REGISTRY <acrName>.azurecr.io
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY *.sln ./
COPY AcrHelloworld/AcrHelloworld.csproj AcrHelloworld/
RUN dotnet restore
COPY . .
WORKDIR /src/AcrHelloworld
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM base AS production
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "AcrHelloworld.dll"]
```

<span data-ttu-id="ecf3b-168">The application in the *acr-helloworld* image tries to determine the region from which its container was deployed by querying DNS for information about the registry's login server.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-168">The application in the *acr-helloworld* image tries to determine the region from which its container was deployed by querying DNS for information about the registry's login server.</span></span> <span data-ttu-id="ecf3b-169">You must specify your registry login server's fully qualified domain name (FQDN) in the `DOCKER_REGISTRY` environment variable in the Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-169">You must specify your registry login server's fully qualified domain name (FQDN) in the `DOCKER_REGISTRY` environment variable in the Dockerfile.</span></span>

<span data-ttu-id="ecf3b-170">First, get the registry's login server with the `az acr show` command.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-170">First, get the registry's login server with the `az acr show` command.</span></span> <span data-ttu-id="ecf3b-171">Replace `<acrName>` with the name of the registry you created in previous steps.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-171">Replace `<acrName>` with the name of the registry you created in previous steps.</span></span>

```azurecli
az acr show --name <acrName> --query "{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="ecf3b-172">Output:</span><span class="sxs-lookup"><span data-stu-id="ecf3b-172">Output:</span></span>

```bash
AcrLoginServer
-----------------------------
uniqueregistryname.azurecr.io
```

<span data-ttu-id="ecf3b-173">Next, update the `ENV DOCKER_REGISTRY` line with the FQDN of your registry's login server.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-173">Next, update the `ENV DOCKER_REGISTRY` line with the FQDN of your registry's login server.</span></span> <span data-ttu-id="ecf3b-174">This example reflects the example registry name, *uniqueregistryname*:</span><span class="sxs-lookup"><span data-stu-id="ecf3b-174">This example reflects the example registry name, *uniqueregistryname*:</span></span>

```dockerfile
ENV DOCKER_REGISTRY uniqueregistryname.azurecr.io
```

## <a name="build-container-image"></a><span data-ttu-id="ecf3b-175">Build container image</span><span class="sxs-lookup"><span data-stu-id="ecf3b-175">Build container image</span></span>

<span data-ttu-id="ecf3b-176">Now that you've updated the Dockerfile with the FQDN of your registry login server, you can use `docker build` to create the container image.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-176">Now that you've updated the Dockerfile with the FQDN of your registry login server, you can use `docker build` to create the container image.</span></span> <span data-ttu-id="ecf3b-177">Run the following command to build the image and tag it with the URL of your private registry, again replacing `<acrName>` with the name of your registry:</span><span class="sxs-lookup"><span data-stu-id="ecf3b-177">Run the following command to build the image and tag it with the URL of your private registry, again replacing `<acrName>` with the name of your registry:</span></span>

```bash
docker build . -f ./AcrHelloworld/Dockerfile -t <acrName>.azurecr.io/acr-helloworld:v1
```

<span data-ttu-id="ecf3b-178">Several lines of output are displayed as the Docker image is built (shown here truncated):</span><span class="sxs-lookup"><span data-stu-id="ecf3b-178">Several lines of output are displayed as the Docker image is built (shown here truncated):</span></span>

```bash
Sending build context to Docker daemon  523.8kB
Step 1/18 : FROM microsoft/aspnetcore:2.0 AS base
2.0: Pulling from microsoft/aspnetcore
3e17c6eae66c: Pulling fs layer

[...]

Step 18/18 : ENTRYPOINT dotnet AcrHelloworld.dll
 ---> Running in 6906d98c47a1
 ---> c9ca1763cfb1
Removing intermediate container 6906d98c47a1
Successfully built c9ca1763cfb1
Successfully tagged uniqueregistryname.azurecr.io/acr-helloworld:v1
```

<span data-ttu-id="ecf3b-179">Use `docker images` to see the built and tagged image:</span><span class="sxs-lookup"><span data-stu-id="ecf3b-179">Use `docker images` to see the built and tagged image:</span></span>

```console
$ docker images
REPOSITORY                                      TAG    IMAGE ID        CREATED               SIZE
uniqueregistryname.azurecr.io/acr-helloworld    v1     01ac48d5c8cf    About a minute ago    284MB
[...]
```

## <a name="push-image-to-azure-container-registry"></a><span data-ttu-id="ecf3b-180">Push image to Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="ecf3b-180">Push image to Azure Container Registry</span></span>

<span data-ttu-id="ecf3b-181">Next, use the `docker push` command to push the *acr-helloworld* image to your registry.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-181">Next, use the `docker push` command to push the *acr-helloworld* image to your registry.</span></span> <span data-ttu-id="ecf3b-182">Replace `<acrName>` with the name of your registry.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-182">Replace `<acrName>` with the name of your registry.</span></span>

```bash
docker push <acrName>.azurecr.io/acr-helloworld:v1
```

<span data-ttu-id="ecf3b-183">Because you've configured your registry for geo-replication, your image is automatically replicated to both the *West US* and *East US* regions with this single `docker push` command.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-183">Because you've configured your registry for geo-replication, your image is automatically replicated to both the *West US* and *East US* regions with this single `docker push` command.</span></span>

```console
$ docker push uniqueregistryname.azurecr.io/acr-helloworld:v1
The push refers to a repository [uniqueregistryname.azurecr.io/acr-helloworld]
cd54739c444b: Pushed
d6803756744a: Pushed
b7b1f3a15779: Pushed
a89567dff12d: Pushed
59c7b561ff56: Pushed
9a2f9413d9e4: Pushed
a75caa09eb1f: Pushed
v1: digest: sha256:0799014f91384bda5b87591170b1242bcd719f07a03d1f9a1ddbae72b3543970 size: 1792
```

## <a name="next-steps"></a><span data-ttu-id="ecf3b-184">Next steps</span><span class="sxs-lookup"><span data-stu-id="ecf3b-184">Next steps</span></span>

<span data-ttu-id="ecf3b-185">In this tutorial, you created a private, geo-replicated container registry, built a container image, and then pushed that image to your registry.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-185">In this tutorial, you created a private, geo-replicated container registry, built a container image, and then pushed that image to your registry.</span></span>

<span data-ttu-id="ecf3b-186">Advance to the next tutorial to deploy your container to multiple Web Apps for Containers instances, using geo-replication to serve the images locally.</span><span class="sxs-lookup"><span data-stu-id="ecf3b-186">Advance to the next tutorial to deploy your container to multiple Web Apps for Containers instances, using geo-replication to serve the images locally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ecf3b-187">Deploy web app from Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="ecf3b-187">Deploy web app from Azure Container Registry</span></span>](container-registry-tutorial-deploy-app.md)

<!-- IMAGES -->
[tut-portal-01]: ./media/container-registry-tutorial-prepare-registry/tut-portal-01.png
[tut-portal-02]: ./media/container-registry-tutorial-prepare-registry/tut-portal-02.png
[tut-portal-03]: ./media/container-registry-tutorial-prepare-registry/tut-portal-03.png
[tut-portal-04]: ./media/container-registry-tutorial-prepare-registry/tut-portal-04.png
[tut-portal-05]: ./media/container-registry-tutorial-prepare-registry/tut-portal-05.png
[tut-app-01]: ./media/container-registry-tutorial-prepare-registry/tut-app-01.png
[tut-map-01]: ./media/container-registry-tutorial-prepare-registry/tut-map-01.png

<!-- LINKS - External -->
[acr-helloworld-zip]: https://github.com/Azure-Samples/acr-helloworld/archive/master.zip
[aspnet-core]: http://dot.net
[dockerhub-aspnetcore]: https://hub.docker.com/r/microsoft/aspnetcore/
[dockerhub-aspnetcore-build]: https://store.docker.com/community/images/microsoft/aspnetcore-build
[dockerfile]: https://github.com/Azure-Samples/acr-helloworld/blob/master/AcrHelloworld/Dockerfile