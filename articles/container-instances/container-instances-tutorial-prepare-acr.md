---
title: Azure Container Instances tutorial - Prepare Azure Container Registry
description: Azure Container Instances tutorial part 2 of 3 - Prepare Azure Container Registry
services: container-instances
author: mmacy
manager: jeconnoc
ms.service: container-instances
ms.topic: tutorial
ms.date: 03/21/2018
ms.author: marsma
ms.custom: mvc
ms.openlocfilehash: e01c736896043ac7639a374c4f75390c4a0e2e52
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870044"
---
# <a name="tutorial-deploy-and-use-azure-container-registry"></a><span data-ttu-id="d8319-103">Tutorial: Deploy and use Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="d8319-103">Tutorial: Deploy and use Azure Container Registry</span></span>

<span data-ttu-id="d8319-104">This is part two of a three-part tutorial.</span><span class="sxs-lookup"><span data-stu-id="d8319-104">This is part two of a three-part tutorial.</span></span> <span data-ttu-id="d8319-105">[Part one](container-instances-tutorial-prepare-app.md) of the tutorial created a Docker container image for a Node.js web application.</span><span class="sxs-lookup"><span data-stu-id="d8319-105">[Part one](container-instances-tutorial-prepare-app.md) of the tutorial created a Docker container image for a Node.js web application.</span></span> <span data-ttu-id="d8319-106">In this tutorial, you push the image to Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="d8319-106">In this tutorial, you push the image to Azure Container Registry.</span></span> <span data-ttu-id="d8319-107">If you haven't yet created the container image, return to [Tutorial 1 – Create container image](container-instances-tutorial-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="d8319-107">If you haven't yet created the container image, return to [Tutorial 1 – Create container image](container-instances-tutorial-prepare-app.md).</span></span>

<span data-ttu-id="d8319-108">Azure Container Registry is your private Docker registry in Azure.</span><span class="sxs-lookup"><span data-stu-id="d8319-108">Azure Container Registry is your private Docker registry in Azure.</span></span> <span data-ttu-id="d8319-109">In this tutorial, you create an Azure Container Registry instance in your subscription, then push the previously created container image to it.</span><span class="sxs-lookup"><span data-stu-id="d8319-109">In this tutorial, you create an Azure Container Registry instance in your subscription, then push the previously created container image to it.</span></span> <span data-ttu-id="d8319-110">In this article, part two of the series, you:</span><span class="sxs-lookup"><span data-stu-id="d8319-110">In this article, part two of the series, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d8319-111">Create an Azure Container Registry instance</span><span class="sxs-lookup"><span data-stu-id="d8319-111">Create an Azure Container Registry instance</span></span>
> * <span data-ttu-id="d8319-112">Tag a container image for your Azure container registry</span><span class="sxs-lookup"><span data-stu-id="d8319-112">Tag a container image for your Azure container registry</span></span>
> * <span data-ttu-id="d8319-113">Upload  the image to your registry</span><span class="sxs-lookup"><span data-stu-id="d8319-113">Upload  the image to your registry</span></span>

<span data-ttu-id="d8319-114">In the next article, the last in the series, you deploy the container from your private registry to Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="d8319-114">In the next article, the last in the series, you deploy the container from your private registry to Azure Container Instances.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d8319-115">Before you begin</span><span class="sxs-lookup"><span data-stu-id="d8319-115">Before you begin</span></span>

[!INCLUDE [container-instances-tutorial-prerequisites](../../includes/container-instances-tutorial-prerequisites.md)]

## <a name="create-azure-container-registry"></a><span data-ttu-id="d8319-116">Create Azure container registry</span><span class="sxs-lookup"><span data-stu-id="d8319-116">Create Azure container registry</span></span>

<span data-ttu-id="d8319-117">Before you create your container registry, you need a *resource group* to deploy it to.</span><span class="sxs-lookup"><span data-stu-id="d8319-117">Before you create your container registry, you need a *resource group* to deploy it to.</span></span> <span data-ttu-id="d8319-118">A resource group is a logical collection into which all Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="d8319-118">A resource group is a logical collection into which all Azure resources are deployed and managed.</span></span>

<span data-ttu-id="d8319-119">Create a resource group with the [az group create][az-group-create] command.</span><span class="sxs-lookup"><span data-stu-id="d8319-119">Create a resource group with the [az group create][az-group-create] command.</span></span> <span data-ttu-id="d8319-120">In the following example, a resource group named *myResourceGroup* is created in the *eastus* region:</span><span class="sxs-lookup"><span data-stu-id="d8319-120">In the following example, a resource group named *myResourceGroup* is created in the *eastus* region:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="d8319-121">Once you've created the resource group, create an Azure container registry with the [az acr create][az-acr-create] command.</span><span class="sxs-lookup"><span data-stu-id="d8319-121">Once you've created the resource group, create an Azure container registry with the [az acr create][az-acr-create] command.</span></span> <span data-ttu-id="d8319-122">The container registry name must be unique within Azure, and contain 5-50 alphanumeric characters.</span><span class="sxs-lookup"><span data-stu-id="d8319-122">The container registry name must be unique within Azure, and contain 5-50 alphanumeric characters.</span></span> <span data-ttu-id="d8319-123">Replace `<acrName>` with a unique name for your registry:</span><span class="sxs-lookup"><span data-stu-id="d8319-123">Replace `<acrName>` with a unique name for your registry:</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name <acrName> --sku Basic --admin-enabled true
```

<span data-ttu-id="d8319-124">Here's example output for a new Azure container registry named *mycontainerregistry082* (shown here truncated):</span><span class="sxs-lookup"><span data-stu-id="d8319-124">Here's example output for a new Azure container registry named *mycontainerregistry082* (shown here truncated):</span></span>

```console
$ az acr create --resource-group myResourceGroup --name mycontainerregistry082 --sku Basic --admin-enabled true
...
{
  "adminUserEnabled": true,
  "creationDate": "2018-03-16T21:54:47.297875+00:00",
  "id": "/subscriptions/<Subscription ID>/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/mycontainerregistry082",
  "location": "eastus",
  "loginServer": "mycontainerregistry082.azurecr.io",
  "name": "mycontainerregistry082",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "status": null,
  "storageAccount": null,
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

<span data-ttu-id="d8319-125">The rest of the tutorial refers to `<acrName>` as a placeholder for the container registry name that you chose in this step.</span><span class="sxs-lookup"><span data-stu-id="d8319-125">The rest of the tutorial refers to `<acrName>` as a placeholder for the container registry name that you chose in this step.</span></span>

## <a name="log-in-to-container-registry"></a><span data-ttu-id="d8319-126">Log in to container registry</span><span class="sxs-lookup"><span data-stu-id="d8319-126">Log in to container registry</span></span>

<span data-ttu-id="d8319-127">You must log in to your Azure Container Registry instance before pushing images to it.</span><span class="sxs-lookup"><span data-stu-id="d8319-127">You must log in to your Azure Container Registry instance before pushing images to it.</span></span> <span data-ttu-id="d8319-128">Use the [az acr login][az-acr-login] command to complete the operation.</span><span class="sxs-lookup"><span data-stu-id="d8319-128">Use the [az acr login][az-acr-login] command to complete the operation.</span></span> <span data-ttu-id="d8319-129">You must provide the unique name you chose for the container registry when you created it.</span><span class="sxs-lookup"><span data-stu-id="d8319-129">You must provide the unique name you chose for the container registry when you created it.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="d8319-130">The command returns `Login Succeeded` once completed:</span><span class="sxs-lookup"><span data-stu-id="d8319-130">The command returns `Login Succeeded` once completed:</span></span>

```console
$ az acr login --name mycontainerregistry082
Login Succeeded
```

## <a name="tag-container-image"></a><span data-ttu-id="d8319-131">Tag container image</span><span class="sxs-lookup"><span data-stu-id="d8319-131">Tag container image</span></span>

<span data-ttu-id="d8319-132">To push a container image to a private registry like Azure Container Registry, you must first tag the image with the full name of the registry's login server.</span><span class="sxs-lookup"><span data-stu-id="d8319-132">To push a container image to a private registry like Azure Container Registry, you must first tag the image with the full name of the registry's login server.</span></span>

<span data-ttu-id="d8319-133">First, get the full login server name for your Azure container registry.</span><span class="sxs-lookup"><span data-stu-id="d8319-133">First, get the full login server name for your Azure container registry.</span></span> <span data-ttu-id="d8319-134">Run the following [az acr show][az-acr-show] command, and replace `<acrName>` with the name of registry you just created:</span><span class="sxs-lookup"><span data-stu-id="d8319-134">Run the following [az acr show][az-acr-show] command, and replace `<acrName>` with the name of registry you just created:</span></span>

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

<span data-ttu-id="d8319-135">For example, if your registry is named *mycontainerregistry082*:</span><span class="sxs-lookup"><span data-stu-id="d8319-135">For example, if your registry is named *mycontainerregistry082*:</span></span>

```console
$ az acr show --name mycontainerregistry082 --query loginServer --output table
Result
------------------------
mycontainerregistry082.azurecr.io
```

<span data-ttu-id="d8319-136">Now, display the list of your local images with the [docker images][docker-images] command:</span><span class="sxs-lookup"><span data-stu-id="d8319-136">Now, display the list of your local images with the [docker images][docker-images] command:</span></span>

```bash
docker images
```

<span data-ttu-id="d8319-137">Along with any other images you have on your machine, you should see the *aci-tutorial-app* image you built in the [previous tutorial](container-instances-tutorial-prepare-app.md):</span><span class="sxs-lookup"><span data-stu-id="d8319-137">Along with any other images you have on your machine, you should see the *aci-tutorial-app* image you built in the [previous tutorial](container-instances-tutorial-prepare-app.md):</span></span>

```console
$ docker images
REPOSITORY          TAG       IMAGE ID        CREATED           SIZE
aci-tutorial-app    latest    5c745774dfa9    39 minutes ago    68.1 MB
```

<span data-ttu-id="d8319-138">Tag the *aci-tutorial-app* image with the loginServer of your container registry.</span><span class="sxs-lookup"><span data-stu-id="d8319-138">Tag the *aci-tutorial-app* image with the loginServer of your container registry.</span></span> <span data-ttu-id="d8319-139">Also, add the `:v1` tag to the end of the image name to indicate the image version number.</span><span class="sxs-lookup"><span data-stu-id="d8319-139">Also, add the `:v1` tag to the end of the image name to indicate the image version number.</span></span> <span data-ttu-id="d8319-140">Replace `<acrLoginServer>` with the result of the [az acr show][az-acr-show] command you executed earlier.</span><span class="sxs-lookup"><span data-stu-id="d8319-140">Replace `<acrLoginServer>` with the result of the [az acr show][az-acr-show] command you executed earlier.</span></span>

```bash
docker tag aci-tutorial-app <acrLoginServer>/aci-tutorial-app:v1
```

<span data-ttu-id="d8319-141">Run `docker images` again to verify the tagging operation:</span><span class="sxs-lookup"><span data-stu-id="d8319-141">Run `docker images` again to verify the tagging operation:</span></span>

```console
$ docker images
REPOSITORY                                            TAG       IMAGE ID        CREATED           SIZE
aci-tutorial-app                                      latest    5c745774dfa9    39 minutes ago    68.1 MB
mycontainerregistry082.azurecr.io/aci-tutorial-app    v1        5c745774dfa9    7 minutes ago     68.1 MB
```

## <a name="push-image-to-azure-container-registry"></a><span data-ttu-id="d8319-142">Push image to Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="d8319-142">Push image to Azure Container Registry</span></span>

<span data-ttu-id="d8319-143">Now that you've tagged the *aci-tutorial-app* image with the full login server name of your private registry, you can push it to the registry with the [docker push][docker-push] command.</span><span class="sxs-lookup"><span data-stu-id="d8319-143">Now that you've tagged the *aci-tutorial-app* image with the full login server name of your private registry, you can push it to the registry with the [docker push][docker-push] command.</span></span> <span data-ttu-id="d8319-144">Replace `<acrLoginServer>` with the full login server name you obtained in the earlier step.</span><span class="sxs-lookup"><span data-stu-id="d8319-144">Replace `<acrLoginServer>` with the full login server name you obtained in the earlier step.</span></span>

```bash
docker push <acrLoginServer>/aci-tutorial-app:v1
```

<span data-ttu-id="d8319-145">The `push` operation should take a few seconds to a few minutes depending on your internet connection, and output is similar to the following:</span><span class="sxs-lookup"><span data-stu-id="d8319-145">The `push` operation should take a few seconds to a few minutes depending on your internet connection, and output is similar to the following:</span></span>

```console
$ docker push mycontainerregistry082.azurecr.io/aci-tutorial-app:v1
The push refers to a repository [mycontainerregistry082.azurecr.io/aci-tutorial-app]
3db9cac20d49: Pushed
13f653351004: Pushed
4cd158165f4d: Pushed
d8fbd47558a8: Pushed
44ab46125c35: Pushed
5bef08742407: Pushed
v1: digest: sha256:ed67fff971da47175856505585dcd92d1270c3b37543e8afd46014d328f05715 size: 1576
```

## <a name="list-images-in-azure-container-registry"></a><span data-ttu-id="d8319-146">List images in Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="d8319-146">List images in Azure Container Registry</span></span>

<span data-ttu-id="d8319-147">To verify that the image you just pushed is indeed in your Azure container registry, list the images in your registry with the [az acr repository list][az-acr-repository-list] command.</span><span class="sxs-lookup"><span data-stu-id="d8319-147">To verify that the image you just pushed is indeed in your Azure container registry, list the images in your registry with the [az acr repository list][az-acr-repository-list] command.</span></span> <span data-ttu-id="d8319-148">Replace `<acrName>` with the name of your container registry.</span><span class="sxs-lookup"><span data-stu-id="d8319-148">Replace `<acrName>` with the name of your container registry.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="d8319-149">For example:</span><span class="sxs-lookup"><span data-stu-id="d8319-149">For example:</span></span>

```console
$ az acr repository list --name mycontainerregistry082 --output table
Result
----------------
aci-tutorial-app
```

<span data-ttu-id="d8319-150">To see the *tags* for a specific image, use the [az acr repository show-tags][az-acr-repository-show-tags] command.</span><span class="sxs-lookup"><span data-stu-id="d8319-150">To see the *tags* for a specific image, use the [az acr repository show-tags][az-acr-repository-show-tags] command.</span></span>

```azurecli
az acr repository show-tags --name <acrName> --repository aci-tutorial-app --output table
```

<span data-ttu-id="d8319-151">You should see output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="d8319-151">You should see output similar to the following:</span></span>

```console
$ az acr repository show-tags --name mycontainerregistry082 --repository aci-tutorial-app --output table
Result
--------
v1
```

## <a name="next-steps"></a><span data-ttu-id="d8319-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="d8319-152">Next steps</span></span>

<span data-ttu-id="d8319-153">In this tutorial, you prepared an Azure container registry for use with Azure Container Instances, and pushed a container image to the registry.</span><span class="sxs-lookup"><span data-stu-id="d8319-153">In this tutorial, you prepared an Azure container registry for use with Azure Container Instances, and pushed a container image to the registry.</span></span> <span data-ttu-id="d8319-154">The following steps were completed:</span><span class="sxs-lookup"><span data-stu-id="d8319-154">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d8319-155">Deployed an Azure Container Registry instance</span><span class="sxs-lookup"><span data-stu-id="d8319-155">Deployed an Azure Container Registry instance</span></span>
> * <span data-ttu-id="d8319-156">Tagged a container image for Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="d8319-156">Tagged a container image for Azure Container Registry</span></span>
> * <span data-ttu-id="d8319-157">Uploaded an image to Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="d8319-157">Uploaded an image to Azure Container Registry</span></span>

<span data-ttu-id="d8319-158">Advance to the next tutorial to learn how to deploy the container to Azure using Azure Container Instances:</span><span class="sxs-lookup"><span data-stu-id="d8319-158">Advance to the next tutorial to learn how to deploy the container to Azure using Azure Container Instances:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d8319-159">Deploy container to Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="d8319-159">Deploy container to Azure Container Instances</span></span>](container-instances-tutorial-deploy-app.md)

<!-- LINKS - External -->
[docker-build]: https://docs.docker.com/engine/reference/commandline/build/
[docker-get-started]: https://docs.docker.com/get-started/
[docker-hub-nodeimage]: https://store.docker.com/images/node
[docker-images]: https://docs.docker.com/engine/reference/commandline/images/
[docker-linux]: https://docs.docker.com/engine/installation/#supported-platforms
[docker-login]: https://docs.docker.com/engine/reference/commandline/login/
[docker-mac]: https://docs.docker.com/docker-for-mac/
[docker-push]: https://docs.docker.com/engine/reference/commandline/push/
[docker-tag]: https://docs.docker.com/engine/reference/commandline/tag/
[docker-windows]: https://docs.docker.com/docker-for-windows/
[nodejs]: http://nodejs.org

<!-- LINKS - Internal -->
[az-acr-create]: /cli/azure/acr#az-acr-create
[az-acr-login]: /cli/azure/acr#az-acr-login
[az-acr-repository-list]: /cli/azure/acr/repository#az-acr-list
[az-acr-repository-show-tags]: /cli/azure/acr/repository#az-acr-repository-show-tags
[az-acr-show]: /cli/azure/acr#az-acr-show
[az-group-create]: /cli/azure/group#az-group-create
[azure-cli-install]: /cli/azure/install-azure-cli
