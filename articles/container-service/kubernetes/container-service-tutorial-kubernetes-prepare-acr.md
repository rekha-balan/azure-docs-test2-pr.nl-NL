---
title: Azure Container Service tutorial - Prepare ACR
description: Azure Container Service tutorial - Prepare ACR
services: container-service
author: neilpeterson
manager: jeconnoc
ms.service: container-service
ms.topic: tutorial
ms.date: 02/26/2018
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 8f14a7aabbdf815992e0777eaf5335a69570ce2e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869281"
---
# <a name="deploy-and-use-azure-container-registry"></a><span data-ttu-id="729c8-103">Deploy and use Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="729c8-103">Deploy and use Azure Container Registry</span></span>

[!INCLUDE [aks-preview-redirect.md](../../../includes/aks-preview-redirect.md)]

<span data-ttu-id="729c8-104">Azure Container Registry (ACR) is an Azure-based, private registry, for Docker container images.</span><span class="sxs-lookup"><span data-stu-id="729c8-104">Azure Container Registry (ACR) is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="729c8-105">This tutorial, part two of seven, walks through deploying an Azure Container Registry instance, and pushing a container image to it.</span><span class="sxs-lookup"><span data-stu-id="729c8-105">This tutorial, part two of seven, walks through deploying an Azure Container Registry instance, and pushing a container image to it.</span></span> <span data-ttu-id="729c8-106">Steps completed include:</span><span class="sxs-lookup"><span data-stu-id="729c8-106">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="729c8-107">Deploying an Azure Container Registry (ACR) instance</span><span class="sxs-lookup"><span data-stu-id="729c8-107">Deploying an Azure Container Registry (ACR) instance</span></span>
> * <span data-ttu-id="729c8-108">Tagging a container image for ACR</span><span class="sxs-lookup"><span data-stu-id="729c8-108">Tagging a container image for ACR</span></span>
> * <span data-ttu-id="729c8-109">Uploading the image to ACR</span><span class="sxs-lookup"><span data-stu-id="729c8-109">Uploading the image to ACR</span></span>

<span data-ttu-id="729c8-110">In subsequent tutorials, this ACR instance is integrated with an Azure Container Service Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="729c8-110">In subsequent tutorials, this ACR instance is integrated with an Azure Container Service Kubernetes cluster.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="729c8-111">Before you begin</span><span class="sxs-lookup"><span data-stu-id="729c8-111">Before you begin</span></span>

<span data-ttu-id="729c8-112">In the [previous tutorial](./container-service-tutorial-kubernetes-prepare-app.md), a container image was created for a simple Azure Voting application.</span><span class="sxs-lookup"><span data-stu-id="729c8-112">In the [previous tutorial](./container-service-tutorial-kubernetes-prepare-app.md), a container image was created for a simple Azure Voting application.</span></span> <span data-ttu-id="729c8-113">If you have not created the Azure Voting app image, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="729c8-113">If you have not created the Azure Voting app image, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span>

<span data-ttu-id="729c8-114">This tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span><span class="sxs-lookup"><span data-stu-id="729c8-114">This tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="729c8-115">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="729c8-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="729c8-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="729c8-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="729c8-117">Deploy Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="729c8-117">Deploy Azure Container Registry</span></span>

<span data-ttu-id="729c8-118">When deploying an Azure Container Registry, you first need a resource group.</span><span class="sxs-lookup"><span data-stu-id="729c8-118">When deploying an Azure Container Registry, you first need a resource group.</span></span> <span data-ttu-id="729c8-119">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="729c8-119">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="729c8-120">Create a resource group with the [az group create](/cli/azure/group#az-group-create) command.</span><span class="sxs-lookup"><span data-stu-id="729c8-120">Create a resource group with the [az group create](/cli/azure/group#az-group-create) command.</span></span> <span data-ttu-id="729c8-121">In this example, a resource group named `myResourceGroup` is created in the `westeurope` region.</span><span class="sxs-lookup"><span data-stu-id="729c8-121">In this example, a resource group named `myResourceGroup` is created in the `westeurope` region.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="729c8-122">Create an Azure Container registry with the [az acr create](/cli/azure/acr#az-acr-create) command.</span><span class="sxs-lookup"><span data-stu-id="729c8-122">Create an Azure Container registry with the [az acr create](/cli/azure/acr#az-acr-create) command.</span></span> <span data-ttu-id="729c8-123">The name of a Container Registry **must be unique**.</span><span class="sxs-lookup"><span data-stu-id="729c8-123">The name of a Container Registry **must be unique**.</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name <acrName> --sku Basic
```

<span data-ttu-id="729c8-124">Throughout the rest of this tutorial, we use `<acrname>` as a placeholder for the container registry name.</span><span class="sxs-lookup"><span data-stu-id="729c8-124">Throughout the rest of this tutorial, we use `<acrname>` as a placeholder for the container registry name.</span></span>

## <a name="container-registry-login"></a><span data-ttu-id="729c8-125">Container registry login</span><span class="sxs-lookup"><span data-stu-id="729c8-125">Container registry login</span></span>

<span data-ttu-id="729c8-126">Use the [az acr login](https://docs.microsoft.com/cli/azure/acr#az-acr-login) command to log in to the ACR instance.</span><span class="sxs-lookup"><span data-stu-id="729c8-126">Use the [az acr login](https://docs.microsoft.com/cli/azure/acr#az-acr-login) command to log in to the ACR instance.</span></span> <span data-ttu-id="729c8-127">You need to provide the unique name given to the container registry when it was created.</span><span class="sxs-lookup"><span data-stu-id="729c8-127">You need to provide the unique name given to the container registry when it was created.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="729c8-128">The command returns a 'Login Succeeded’ message once completed.</span><span class="sxs-lookup"><span data-stu-id="729c8-128">The command returns a 'Login Succeeded’ message once completed.</span></span>

## <a name="tag-container-images"></a><span data-ttu-id="729c8-129">Tag container images</span><span class="sxs-lookup"><span data-stu-id="729c8-129">Tag container images</span></span>

<span data-ttu-id="729c8-130">To see a list of current images, use the [docker images](https://docs.docker.com/engine/reference/commandline/images/) command.</span><span class="sxs-lookup"><span data-stu-id="729c8-130">To see a list of current images, use the [docker images](https://docs.docker.com/engine/reference/commandline/images/) command.</span></span>

```bash
docker images
```

<span data-ttu-id="729c8-131">Output:</span><span class="sxs-lookup"><span data-stu-id="729c8-131">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front             latest              4675398c9172        13 minutes ago      694MB
redis                        latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask               788ca94b2313        9 months ago        694MB
```

<span data-ttu-id="729c8-132">Each container image needs to be tagged with the loginServer name of the registry.</span><span class="sxs-lookup"><span data-stu-id="729c8-132">Each container image needs to be tagged with the loginServer name of the registry.</span></span> <span data-ttu-id="729c8-133">This tag is used for routing when pushing container images to an image registry.</span><span class="sxs-lookup"><span data-stu-id="729c8-133">This tag is used for routing when pushing container images to an image registry.</span></span>

<span data-ttu-id="729c8-134">To get the loginServer name, run the following command.</span><span class="sxs-lookup"><span data-stu-id="729c8-134">To get the loginServer name, run the following command.</span></span>

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="729c8-135">Now, tag the `azure-vote-front` image with the loginServer of the container registry.</span><span class="sxs-lookup"><span data-stu-id="729c8-135">Now, tag the `azure-vote-front` image with the loginServer of the container registry.</span></span> <span data-ttu-id="729c8-136">Also, add `:v1` to the end of the image name.</span><span class="sxs-lookup"><span data-stu-id="729c8-136">Also, add `:v1` to the end of the image name.</span></span> <span data-ttu-id="729c8-137">This tag indicates the image version.</span><span class="sxs-lookup"><span data-stu-id="729c8-137">This tag indicates the image version.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:v1
```

<span data-ttu-id="729c8-138">Once tagged, run [docker images] (https://docs.docker.com/engine/reference/commandline/images/) to verify the operation.</span><span class="sxs-lookup"><span data-stu-id="729c8-138">Once tagged, run [docker images] (https://docs.docker.com/engine/reference/commandline/images/) to verify the operation.</span></span>

```bash
docker images
```

<span data-ttu-id="729c8-139">Output:</span><span class="sxs-lookup"><span data-stu-id="729c8-139">Output:</span></span>

```bash
REPOSITORY                                           TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front                                     latest              eaf2b9c57e5e        8 minutes ago       716 MB
mycontainerregistry082.azurecr.io/azure-vote-front   v1            eaf2b9c57e5e        8 minutes ago       716 MB
redis                                                latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask                           flask               788ca94b2313        8 months ago        694 MB
```

## <a name="push-images-to-registry"></a><span data-ttu-id="729c8-140">Push images to registry</span><span class="sxs-lookup"><span data-stu-id="729c8-140">Push images to registry</span></span>

<span data-ttu-id="729c8-141">Push the `azure-vote-front` image to the registry.</span><span class="sxs-lookup"><span data-stu-id="729c8-141">Push the `azure-vote-front` image to the registry.</span></span> 

<span data-ttu-id="729c8-142">Using the following example, replace the ACR loginServer name with the loginServer from your environment.</span><span class="sxs-lookup"><span data-stu-id="729c8-142">Using the following example, replace the ACR loginServer name with the loginServer from your environment.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:v1
```

<span data-ttu-id="729c8-143">This takes a couple of minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="729c8-143">This takes a couple of minutes to complete.</span></span>

## <a name="list-images-in-registry"></a><span data-ttu-id="729c8-144">List images in registry</span><span class="sxs-lookup"><span data-stu-id="729c8-144">List images in registry</span></span>

<span data-ttu-id="729c8-145">To return a list of images that have been pushed to your Azure Container registry, user the [az acr repository list](/cli/azure/acr/repository#az-acr-repository-list) command.</span><span class="sxs-lookup"><span data-stu-id="729c8-145">To return a list of images that have been pushed to your Azure Container registry, user the [az acr repository list](/cli/azure/acr/repository#az-acr-repository-list) command.</span></span> <span data-ttu-id="729c8-146">Update the command with the ACR instance name.</span><span class="sxs-lookup"><span data-stu-id="729c8-146">Update the command with the ACR instance name.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="729c8-147">Output:</span><span class="sxs-lookup"><span data-stu-id="729c8-147">Output:</span></span>

```azurecli
Result
----------------
azure-vote-front
```

<span data-ttu-id="729c8-148">And then to see the tags for a specific image, use the [az acr repository show-tags](/cli/azure/acr/repository#show-tags) command.</span><span class="sxs-lookup"><span data-stu-id="729c8-148">And then to see the tags for a specific image, use the [az acr repository show-tags](/cli/azure/acr/repository#show-tags) command.</span></span>

```azurecli
az acr repository show-tags --name <acrName> --repository azure-vote-front --output table
```

<span data-ttu-id="729c8-149">Output:</span><span class="sxs-lookup"><span data-stu-id="729c8-149">Output:</span></span>

```azurecli
Result
--------
v1
```

<span data-ttu-id="729c8-150">At tutorial completion, the container image has been stored in a private Azure Container Registry instance.</span><span class="sxs-lookup"><span data-stu-id="729c8-150">At tutorial completion, the container image has been stored in a private Azure Container Registry instance.</span></span> <span data-ttu-id="729c8-151">This image is deployed from ACR to a Kubernetes cluster in subsequent tutorials.</span><span class="sxs-lookup"><span data-stu-id="729c8-151">This image is deployed from ACR to a Kubernetes cluster in subsequent tutorials.</span></span>

## <a name="next-steps"></a><span data-ttu-id="729c8-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="729c8-152">Next steps</span></span>

<span data-ttu-id="729c8-153">In this tutorial, an Azure Container Registry was prepared for use in an ACS Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="729c8-153">In this tutorial, an Azure Container Registry was prepared for use in an ACS Kubernetes cluster.</span></span> <span data-ttu-id="729c8-154">The following steps were completed:</span><span class="sxs-lookup"><span data-stu-id="729c8-154">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="729c8-155">Deployed an Azure Container Registry instance</span><span class="sxs-lookup"><span data-stu-id="729c8-155">Deployed an Azure Container Registry instance</span></span>
> * <span data-ttu-id="729c8-156">Tagged a container image for ACR</span><span class="sxs-lookup"><span data-stu-id="729c8-156">Tagged a container image for ACR</span></span>
> * <span data-ttu-id="729c8-157">Uploaded the image to ACR</span><span class="sxs-lookup"><span data-stu-id="729c8-157">Uploaded the image to ACR</span></span>

<span data-ttu-id="729c8-158">Advance to the next tutorial to learn about deploying a Kubernetes cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="729c8-158">Advance to the next tutorial to learn about deploying a Kubernetes cluster in Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="729c8-159">Deploy Kubernetes cluster</span><span class="sxs-lookup"><span data-stu-id="729c8-159">Deploy Kubernetes cluster</span></span>](./container-service-tutorial-kubernetes-deploy-cluster.md)