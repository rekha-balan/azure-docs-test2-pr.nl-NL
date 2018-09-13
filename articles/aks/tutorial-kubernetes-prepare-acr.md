---
title: Kubernetes on Azure tutorial - Create a container registry
description: In this Azure Kubernetes Service (AKS) tutorial, you create an Azure Container Registry instance and upload a sample application container image.
services: container-service
author: iainfoulds
manager: jeconnoc
ms.service: container-service
ms.topic: tutorial
ms.date: 08/14/2018
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 4f240d346457717c66a6ed189cfd8610c7a764da
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864431"
---
# <a name="tutorial-deploy-and-use-azure-container-registry"></a><span data-ttu-id="67b95-103">Tutorial: Deploy and use Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="67b95-103">Tutorial: Deploy and use Azure Container Registry</span></span>

<span data-ttu-id="67b95-104">Azure Container Registry (ACR) is an Azure-based private registry for Docker container images.</span><span class="sxs-lookup"><span data-stu-id="67b95-104">Azure Container Registry (ACR) is an Azure-based private registry for Docker container images.</span></span> <span data-ttu-id="67b95-105">A private container registry lets you securely build and deploy your applications and custom code.</span><span class="sxs-lookup"><span data-stu-id="67b95-105">A private container registry lets you securely build and deploy your applications and custom code.</span></span> <span data-ttu-id="67b95-106">In this tutorial, part two of seven, you deploy an ACR instance and push a container image to it.</span><span class="sxs-lookup"><span data-stu-id="67b95-106">In this tutorial, part two of seven, you deploy an ACR instance and push a container image to it.</span></span> <span data-ttu-id="67b95-107">You learn how to:</span><span class="sxs-lookup"><span data-stu-id="67b95-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="67b95-108">Create an Azure Container Registry (ACR) instance</span><span class="sxs-lookup"><span data-stu-id="67b95-108">Create an Azure Container Registry (ACR) instance</span></span>
> * <span data-ttu-id="67b95-109">Tag a container image for ACR</span><span class="sxs-lookup"><span data-stu-id="67b95-109">Tag a container image for ACR</span></span>
> * <span data-ttu-id="67b95-110">Upload the image to ACR</span><span class="sxs-lookup"><span data-stu-id="67b95-110">Upload the image to ACR</span></span>
> * <span data-ttu-id="67b95-111">View images in your registry</span><span class="sxs-lookup"><span data-stu-id="67b95-111">View images in your registry</span></span>

<span data-ttu-id="67b95-112">In subsequent tutorials, this ACR instance is integrated with a Kubernetes cluster in AKS, and an application is deployed from the image.</span><span class="sxs-lookup"><span data-stu-id="67b95-112">In subsequent tutorials, this ACR instance is integrated with a Kubernetes cluster in AKS, and an application is deployed from the image.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="67b95-113">Before you begin</span><span class="sxs-lookup"><span data-stu-id="67b95-113">Before you begin</span></span>

<span data-ttu-id="67b95-114">In the [previous tutorial][aks-tutorial-prepare-app], a container image was created for a simple Azure Voting application.</span><span class="sxs-lookup"><span data-stu-id="67b95-114">In the [previous tutorial][aks-tutorial-prepare-app], a container image was created for a simple Azure Voting application.</span></span> <span data-ttu-id="67b95-115">If you have not created the Azure Voting app image, return to [Tutorial 1 – Create container images][aks-tutorial-prepare-app].</span><span class="sxs-lookup"><span data-stu-id="67b95-115">If you have not created the Azure Voting app image, return to [Tutorial 1 – Create container images][aks-tutorial-prepare-app].</span></span>

<span data-ttu-id="67b95-116">This tutorial requires that you are running the Azure CLI version 2.0.44 or later.</span><span class="sxs-lookup"><span data-stu-id="67b95-116">This tutorial requires that you are running the Azure CLI version 2.0.44 or later.</span></span> <span data-ttu-id="67b95-117">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="67b95-117">Run `az --version` to find the version.</span></span> <span data-ttu-id="67b95-118">If you need to install or upgrade, see [Install Azure CLI][azure-cli-install].</span><span class="sxs-lookup"><span data-stu-id="67b95-118">If you need to install or upgrade, see [Install Azure CLI][azure-cli-install].</span></span>

## <a name="create-an-azure-container-registry"></a><span data-ttu-id="67b95-119">Create an Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="67b95-119">Create an Azure Container Registry</span></span>

<span data-ttu-id="67b95-120">To create an Azure Container Registry, you first need a resource group.</span><span class="sxs-lookup"><span data-stu-id="67b95-120">To create an Azure Container Registry, you first need a resource group.</span></span> <span data-ttu-id="67b95-121">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="67b95-121">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="67b95-122">Create a resource group with the [az group create][az-group-create] command.</span><span class="sxs-lookup"><span data-stu-id="67b95-122">Create a resource group with the [az group create][az-group-create] command.</span></span> <span data-ttu-id="67b95-123">In the following example, a resource group named *myResourceGroup* is created in the *eastus* region:</span><span class="sxs-lookup"><span data-stu-id="67b95-123">In the following example, a resource group named *myResourceGroup* is created in the *eastus* region:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="67b95-124">Create an Azure Container Registry instance with the [az acr create][az-acr-create] command and provide your own registry name.</span><span class="sxs-lookup"><span data-stu-id="67b95-124">Create an Azure Container Registry instance with the [az acr create][az-acr-create] command and provide your own registry name.</span></span> <span data-ttu-id="67b95-125">The registry name must be unique within Azure, and contain 5-50 alphanumeric characters.</span><span class="sxs-lookup"><span data-stu-id="67b95-125">The registry name must be unique within Azure, and contain 5-50 alphanumeric characters.</span></span> <span data-ttu-id="67b95-126">In the rest of this tutorial, `<acrName>` is used as a placeholder for the container registry name.</span><span class="sxs-lookup"><span data-stu-id="67b95-126">In the rest of this tutorial, `<acrName>` is used as a placeholder for the container registry name.</span></span> <span data-ttu-id="67b95-127">The *Basic* SKU is a cost-optimized entry point for development purposes that provides a balance of storage and throughput.</span><span class="sxs-lookup"><span data-stu-id="67b95-127">The *Basic* SKU is a cost-optimized entry point for development purposes that provides a balance of storage and throughput.</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name <acrName> --sku Basic
```

## <a name="log-in-to-the-container-registry"></a><span data-ttu-id="67b95-128">Log in to the container registry</span><span class="sxs-lookup"><span data-stu-id="67b95-128">Log in to the container registry</span></span>

<span data-ttu-id="67b95-129">To use the ACR instance, you must first log in.</span><span class="sxs-lookup"><span data-stu-id="67b95-129">To use the ACR instance, you must first log in.</span></span> <span data-ttu-id="67b95-130">Use the [az acr login][az-acr-login] command and provide the unique name given to the container registry in the previous step.</span><span class="sxs-lookup"><span data-stu-id="67b95-130">Use the [az acr login][az-acr-login] command and provide the unique name given to the container registry in the previous step.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="67b95-131">The command returns a *Login Succeeded* message once completed.</span><span class="sxs-lookup"><span data-stu-id="67b95-131">The command returns a *Login Succeeded* message once completed.</span></span>

## <a name="tag-a-container-image"></a><span data-ttu-id="67b95-132">Tag a container image</span><span class="sxs-lookup"><span data-stu-id="67b95-132">Tag a container image</span></span>

<span data-ttu-id="67b95-133">To see a list of your current local images, use the [docker images][docker-images] command:</span><span class="sxs-lookup"><span data-stu-id="67b95-133">To see a list of your current local images, use the [docker images][docker-images] command:</span></span>

```
$ docker images

REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front             latest              4675398c9172        13 minutes ago      694MB
redis                        latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask               788ca94b2313        9 months ago        694MB
```

<span data-ttu-id="67b95-134">To use the *azure-vote-front* container image with ACR, the image needs to be tagged with the login server address of your registry.</span><span class="sxs-lookup"><span data-stu-id="67b95-134">To use the *azure-vote-front* container image with ACR, the image needs to be tagged with the login server address of your registry.</span></span> <span data-ttu-id="67b95-135">This tag is used for routing when pushing container images to an image registry.</span><span class="sxs-lookup"><span data-stu-id="67b95-135">This tag is used for routing when pushing container images to an image registry.</span></span>

<span data-ttu-id="67b95-136">To get the login server address, use the [az acr list][az-acr-list] command and query for the *loginServer* as follows:</span><span class="sxs-lookup"><span data-stu-id="67b95-136">To get the login server address, use the [az acr list][az-acr-list] command and query for the *loginServer* as follows:</span></span>

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="67b95-137">Now, tag your local *azure-vote-front* image with the *acrloginServer* address of the container registry.</span><span class="sxs-lookup"><span data-stu-id="67b95-137">Now, tag your local *azure-vote-front* image with the *acrloginServer* address of the container registry.</span></span> <span data-ttu-id="67b95-138">To indicate the image version, add *:v1* to the end of the image name:</span><span class="sxs-lookup"><span data-stu-id="67b95-138">To indicate the image version, add *:v1* to the end of the image name:</span></span>

```console
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:v1
```

<span data-ttu-id="67b95-139">To verify the tags are applied, run [docker images][docker-images] again.</span><span class="sxs-lookup"><span data-stu-id="67b95-139">To verify the tags are applied, run [docker images][docker-images] again.</span></span> <span data-ttu-id="67b95-140">An image is tagged with the ACR instance address and a version number.</span><span class="sxs-lookup"><span data-stu-id="67b95-140">An image is tagged with the ACR instance address and a version number.</span></span>

```
$ docker images

REPOSITORY                                           TAG           IMAGE ID            CREATED             SIZE
azure-vote-front                                     latest        eaf2b9c57e5e        8 minutes ago       716 MB
mycontainerregistry.azurecr.io/azure-vote-front      v1            eaf2b9c57e5e        8 minutes ago       716 MB
redis                                                latest        a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask                           flask         788ca94b2313        8 months ago        694 MB
```

## <a name="push-images-to-registry"></a><span data-ttu-id="67b95-141">Push images to registry</span><span class="sxs-lookup"><span data-stu-id="67b95-141">Push images to registry</span></span>

<span data-ttu-id="67b95-142">You can now push the *azure-vote-front* image to your ACR instance.</span><span class="sxs-lookup"><span data-stu-id="67b95-142">You can now push the *azure-vote-front* image to your ACR instance.</span></span> <span data-ttu-id="67b95-143">Use [docker push][docker-push] and provide your own *acrLoginServer* address for the image name as follows:</span><span class="sxs-lookup"><span data-stu-id="67b95-143">Use [docker push][docker-push] and provide your own *acrLoginServer* address for the image name as follows:</span></span>

```console
docker push <acrLoginServer>/azure-vote-front:v1
```

<span data-ttu-id="67b95-144">It may take a few minutes to complete the image push to ACR.</span><span class="sxs-lookup"><span data-stu-id="67b95-144">It may take a few minutes to complete the image push to ACR.</span></span>

## <a name="list-images-in-registry"></a><span data-ttu-id="67b95-145">List images in registry</span><span class="sxs-lookup"><span data-stu-id="67b95-145">List images in registry</span></span>

<span data-ttu-id="67b95-146">To return a list of images that have been pushed to your ACR instance, use the [az acr repository list][az-acr-repository-list] command.</span><span class="sxs-lookup"><span data-stu-id="67b95-146">To return a list of images that have been pushed to your ACR instance, use the [az acr repository list][az-acr-repository-list] command.</span></span> <span data-ttu-id="67b95-147">Provide your own `<acrName>` as follows:</span><span class="sxs-lookup"><span data-stu-id="67b95-147">Provide your own `<acrName>` as follows:</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="67b95-148">The following example output lists the *azure-vote-front* image as available in the registry:</span><span class="sxs-lookup"><span data-stu-id="67b95-148">The following example output lists the *azure-vote-front* image as available in the registry:</span></span>

```
Result
----------------
azure-vote-front
```

<span data-ttu-id="67b95-149">To see the tags for a specific image, use the [az acr repository show-tags][az-acr-repository-show-tags] command as follows:</span><span class="sxs-lookup"><span data-stu-id="67b95-149">To see the tags for a specific image, use the [az acr repository show-tags][az-acr-repository-show-tags] command as follows:</span></span>

```azurecli
az acr repository show-tags --name <acrName> --repository azure-vote-front --output table
```

<span data-ttu-id="67b95-150">The following example output shows the *v1* image tagged in a previous step:</span><span class="sxs-lookup"><span data-stu-id="67b95-150">The following example output shows the *v1* image tagged in a previous step:</span></span>

```
Result
--------
v1
```

<span data-ttu-id="67b95-151">You now have a container image that is stored in a private Azure Container Registry instance.</span><span class="sxs-lookup"><span data-stu-id="67b95-151">You now have a container image that is stored in a private Azure Container Registry instance.</span></span> <span data-ttu-id="67b95-152">This image is deployed from ACR to a Kubernetes cluster in the next tutorial.</span><span class="sxs-lookup"><span data-stu-id="67b95-152">This image is deployed from ACR to a Kubernetes cluster in the next tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67b95-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="67b95-153">Next steps</span></span>

<span data-ttu-id="67b95-154">In this tutorial, you created an Azure Container Registry and pushed an image for use in an AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="67b95-154">In this tutorial, you created an Azure Container Registry and pushed an image for use in an AKS cluster.</span></span> <span data-ttu-id="67b95-155">You learned how to:</span><span class="sxs-lookup"><span data-stu-id="67b95-155">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="67b95-156">Create an Azure Container Registry (ACR) instance</span><span class="sxs-lookup"><span data-stu-id="67b95-156">Create an Azure Container Registry (ACR) instance</span></span>
> * <span data-ttu-id="67b95-157">Tag a container image for ACR</span><span class="sxs-lookup"><span data-stu-id="67b95-157">Tag a container image for ACR</span></span>
> * <span data-ttu-id="67b95-158">Upload the image to ACR</span><span class="sxs-lookup"><span data-stu-id="67b95-158">Upload the image to ACR</span></span>
> * <span data-ttu-id="67b95-159">View images in your registry</span><span class="sxs-lookup"><span data-stu-id="67b95-159">View images in your registry</span></span>

<span data-ttu-id="67b95-160">Advance to the next tutorial to learn how to deploy a Kubernetes cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="67b95-160">Advance to the next tutorial to learn how to deploy a Kubernetes cluster in Azure.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="67b95-161">[Deploy Kubernetes cluster][aks-tutorial-deploy-cluster]</span><span class="sxs-lookup"><span data-stu-id="67b95-161">[Deploy Kubernetes cluster][aks-tutorial-deploy-cluster]</span></span>

<!-- LINKS - external -->
[docker-images]: https://docs.docker.com/engine/reference/commandline/images/
[docker-push]: https://docs.docker.com/engine/reference/commandline/push/

<!-- LINKS - internal -->
[az-acr-create]: /cli/azure/acr#create
[az-acr-list]: /cli/azure/acr#list
[az-acr-login]: https://docs.microsoft.com/cli/azure/acr#az-acr-login
[az-acr-list]: https://docs.microsoft.com/cli/azure/acr#az-acr-list
[az-acr-repository-list]: /cli/azure/acr/repository#list
[az-acr-repository-show-tags]: /cli/azure/acr/repository#show-tags
[az-group-create]: /cli/azure/group#az-group-create
[azure-cli-install]: /cli/azure/install-azure-cli
[aks-tutorial-deploy-cluster]: ./tutorial-kubernetes-deploy-cluster.md
[aks-tutorial-prepare-app]: ./tutorial-kubernetes-prepare-app.md
