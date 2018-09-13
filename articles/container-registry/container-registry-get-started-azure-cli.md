---
title: Quickstart - Create a private Docker registry in Azure with the Azure CLI
description: Quickly learn to create a private Docker container registry with the Azure CLI.
services: container-registry
author: mmacy
manager: jeconnoc
ms.service: container-registry
ms.topic: quickstart
ms.date: 03/03/2018
ms.author: marsma
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 0c427ebc767b79227db0847c7fcda63e65ef70d3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44794851"
---
# <a name="quickstart-create-a-container-registry-using-the-azure-cli"></a><span data-ttu-id="1e231-103">Quickstart: Create a container registry using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1e231-103">Quickstart: Create a container registry using the Azure CLI</span></span>

<span data-ttu-id="1e231-104">Azure Container Registry is a managed Docker container registry service used for storing private Docker container images.</span><span class="sxs-lookup"><span data-stu-id="1e231-104">Azure Container Registry is a managed Docker container registry service used for storing private Docker container images.</span></span> <span data-ttu-id="1e231-105">This guide details creating an Azure Container Registry instance using the Azure CLI, pushing a container image into the registry and finally deploying the container from your registry into Azure Container Instances (ACI).</span><span class="sxs-lookup"><span data-stu-id="1e231-105">This guide details creating an Azure Container Registry instance using the Azure CLI, pushing a container image into the registry and finally deploying the container from your registry into Azure Container Instances (ACI).</span></span>

<span data-ttu-id="1e231-106">This quickstart requires that you are running the Azure CLI version 2.0.27 or later.</span><span class="sxs-lookup"><span data-stu-id="1e231-106">This quickstart requires that you are running the Azure CLI version 2.0.27 or later.</span></span> <span data-ttu-id="1e231-107">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="1e231-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="1e231-108">If you need to install or upgrade, see [Install Azure CLI][azure-cli].</span><span class="sxs-lookup"><span data-stu-id="1e231-108">If you need to install or upgrade, see [Install Azure CLI][azure-cli].</span></span>

<span data-ttu-id="1e231-109">You must also have Docker installed locally.</span><span class="sxs-lookup"><span data-stu-id="1e231-109">You must also have Docker installed locally.</span></span> <span data-ttu-id="1e231-110">Docker provides packages that easily configure Docker on any [macOS][docker-mac], [Windows][docker-windows], or [Linux][docker-linux] system.</span><span class="sxs-lookup"><span data-stu-id="1e231-110">Docker provides packages that easily configure Docker on any [macOS][docker-mac], [Windows][docker-windows], or [Linux][docker-linux] system.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="1e231-111">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="1e231-111">Create a resource group</span></span>

<span data-ttu-id="1e231-112">Create a resource group with the [az group create][az-group-create] command.</span><span class="sxs-lookup"><span data-stu-id="1e231-112">Create a resource group with the [az group create][az-group-create] command.</span></span> <span data-ttu-id="1e231-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="1e231-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="1e231-114">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span><span class="sxs-lookup"><span data-stu-id="1e231-114">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-container-registry"></a><span data-ttu-id="1e231-115">Create a container registry</span><span class="sxs-lookup"><span data-stu-id="1e231-115">Create a container registry</span></span>

<span data-ttu-id="1e231-116">In this quickstart you create a *Basic* registry.</span><span class="sxs-lookup"><span data-stu-id="1e231-116">In this quickstart you create a *Basic* registry.</span></span> <span data-ttu-id="1e231-117">Azure Container Registry is available in several different SKUs, described briefly in the following table.</span><span class="sxs-lookup"><span data-stu-id="1e231-117">Azure Container Registry is available in several different SKUs, described briefly in the following table.</span></span> <span data-ttu-id="1e231-118">For extended details on each, see [Container registry SKUs][container-registry-skus].</span><span class="sxs-lookup"><span data-stu-id="1e231-118">For extended details on each, see [Container registry SKUs][container-registry-skus].</span></span>

[!INCLUDE [container-registry-sku-matrix](../../includes/container-registry-sku-matrix.md)]

<span data-ttu-id="1e231-119">Create an ACR instance using the [az acr create][az-acr-create] command.</span><span class="sxs-lookup"><span data-stu-id="1e231-119">Create an ACR instance using the [az acr create][az-acr-create] command.</span></span> <span data-ttu-id="1e231-120">The registry name must be unique within Azure, and contain 5-50 alphanumeric characters.</span><span class="sxs-lookup"><span data-stu-id="1e231-120">The registry name must be unique within Azure, and contain 5-50 alphanumeric characters.</span></span> <span data-ttu-id="1e231-121">In the following example, *myContainerRegistry007* is used.</span><span class="sxs-lookup"><span data-stu-id="1e231-121">In the following example, *myContainerRegistry007* is used.</span></span> <span data-ttu-id="1e231-122">Update this to a unique value.</span><span class="sxs-lookup"><span data-stu-id="1e231-122">Update this to a unique value.</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name myContainerRegistry007 --sku Basic
```

<span data-ttu-id="1e231-123">When the registry is created, the output is similar to the following:</span><span class="sxs-lookup"><span data-stu-id="1e231-123">When the registry is created, the output is similar to the following:</span></span>

```json
{
  "adminUserEnabled": false,
  "creationDate": "2017-09-08T22:32:13.175925+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry007",
  "location": "eastus",
  "loginServer": "myContainerRegistry007.azurecr.io",
  "name": "myContainerRegistry007",
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

<span data-ttu-id="1e231-124">Throughout the rest of this quickstart `<acrName>` is a placeholder for the container registry name.</span><span class="sxs-lookup"><span data-stu-id="1e231-124">Throughout the rest of this quickstart `<acrName>` is a placeholder for the container registry name.</span></span>

## <a name="log-in-to-acr"></a><span data-ttu-id="1e231-125">Log in to ACR</span><span class="sxs-lookup"><span data-stu-id="1e231-125">Log in to ACR</span></span>

<span data-ttu-id="1e231-126">Before pushing and pulling container images, you must log in to the ACR instance.</span><span class="sxs-lookup"><span data-stu-id="1e231-126">Before pushing and pulling container images, you must log in to the ACR instance.</span></span> <span data-ttu-id="1e231-127">To do so, use the [az acr login][az-acr-login] command.</span><span class="sxs-lookup"><span data-stu-id="1e231-127">To do so, use the [az acr login][az-acr-login] command.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="1e231-128">The command returns a `Login Succeeded` message once completed.</span><span class="sxs-lookup"><span data-stu-id="1e231-128">The command returns a `Login Succeeded` message once completed.</span></span>

## <a name="push-image-to-acr"></a><span data-ttu-id="1e231-129">Push image to ACR</span><span class="sxs-lookup"><span data-stu-id="1e231-129">Push image to ACR</span></span>

<span data-ttu-id="1e231-130">To push an image to an Azure Container registry, you must first have an image.</span><span class="sxs-lookup"><span data-stu-id="1e231-130">To push an image to an Azure Container registry, you must first have an image.</span></span> <span data-ttu-id="1e231-131">If you don't yet have any local container images, run the following command to pull an existing image from Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="1e231-131">If you don't yet have any local container images, run the following command to pull an existing image from Docker Hub.</span></span>

```bash
docker pull microsoft/aci-helloworld
```

<span data-ttu-id="1e231-132">Before you can push an image to your registry, you must tag it with the fully qualified name of your ACR login server.</span><span class="sxs-lookup"><span data-stu-id="1e231-132">Before you can push an image to your registry, you must tag it with the fully qualified name of your ACR login server.</span></span> <span data-ttu-id="1e231-133">Run the following command to obtain the full login server name of the ACR instance.</span><span class="sxs-lookup"><span data-stu-id="1e231-133">Run the following command to obtain the full login server name of the ACR instance.</span></span>

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="1e231-134">Tag the image using the [docker tag][docker-tag] command.</span><span class="sxs-lookup"><span data-stu-id="1e231-134">Tag the image using the [docker tag][docker-tag] command.</span></span> <span data-ttu-id="1e231-135">Replace `<acrLoginServer>` with the login server name of your ACR instance.</span><span class="sxs-lookup"><span data-stu-id="1e231-135">Replace `<acrLoginServer>` with the login server name of your ACR instance.</span></span>

```bash
docker tag microsoft/aci-helloworld <acrLoginServer>/aci-helloworld:v1
```

<span data-ttu-id="1e231-136">Finally, use [docker push][docker-push] to push the image to the ACR instance.</span><span class="sxs-lookup"><span data-stu-id="1e231-136">Finally, use [docker push][docker-push] to push the image to the ACR instance.</span></span> <span data-ttu-id="1e231-137">Replace `<acrLoginServer>` with the login server name of your ACR instance.</span><span class="sxs-lookup"><span data-stu-id="1e231-137">Replace `<acrLoginServer>` with the login server name of your ACR instance.</span></span>

```bash
docker push <acrLoginServer>/aci-helloworld:v1
```

## <a name="list-container-images"></a><span data-ttu-id="1e231-138">List container images</span><span class="sxs-lookup"><span data-stu-id="1e231-138">List container images</span></span>

<span data-ttu-id="1e231-139">The following example lists the repositories in a registry:</span><span class="sxs-lookup"><span data-stu-id="1e231-139">The following example lists the repositories in a registry:</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="1e231-140">Output:</span><span class="sxs-lookup"><span data-stu-id="1e231-140">Output:</span></span>

```bash
Result
----------------
aci-helloworld
```

<span data-ttu-id="1e231-141">The following example lists the tags on the **aci-helloworld** repository.</span><span class="sxs-lookup"><span data-stu-id="1e231-141">The following example lists the tags on the **aci-helloworld** repository.</span></span>

```azurecli
az acr repository show-tags --name <acrName> --repository aci-helloworld --output table
```

<span data-ttu-id="1e231-142">Output:</span><span class="sxs-lookup"><span data-stu-id="1e231-142">Output:</span></span>

```bash
Result
--------
v1
```

## <a name="deploy-image-to-aci"></a><span data-ttu-id="1e231-143">Deploy image to ACI</span><span class="sxs-lookup"><span data-stu-id="1e231-143">Deploy image to ACI</span></span>

<span data-ttu-id="1e231-144">In order to deploy a container instance from the registry you created, you must provide the registry credentials when you deploy it.</span><span class="sxs-lookup"><span data-stu-id="1e231-144">In order to deploy a container instance from the registry you created, you must provide the registry credentials when you deploy it.</span></span> <span data-ttu-id="1e231-145">In production scenarios you should use a [service principal][container-registry-auth-aci] for container registry access, but to keep this quickstart brief, enable the admin user on your registry with the following command:</span><span class="sxs-lookup"><span data-stu-id="1e231-145">In production scenarios you should use a [service principal][container-registry-auth-aci] for container registry access, but to keep this quickstart brief, enable the admin user on your registry with the following command:</span></span>

```azurecli
az acr update --name <acrName> --admin-enabled true
```

<span data-ttu-id="1e231-146">Once admin is enabled the username is the same as your registry name and you can retrieve the password with this command:</span><span class="sxs-lookup"><span data-stu-id="1e231-146">Once admin is enabled the username is the same as your registry name and you can retrieve the password with this command:</span></span>

```azurecli
az acr credential show --name <acrName> --query "passwords[0].value"
```

<span data-ttu-id="1e231-147">To deploy your container image with 1 CPU core and 1 GB of memory, run the following command.</span><span class="sxs-lookup"><span data-stu-id="1e231-147">To deploy your container image with 1 CPU core and 1 GB of memory, run the following command.</span></span> <span data-ttu-id="1e231-148">Replace `<acrName>`, `<acrLoginServer>`, and `<acrPassword>` with the values you obtained from previous commands.</span><span class="sxs-lookup"><span data-stu-id="1e231-148">Replace `<acrName>`, `<acrLoginServer>`, and `<acrPassword>` with the values you obtained from previous commands.</span></span>

```azurecli
az container create --resource-group myResourceGroup --name acr-quickstart --image <acrLoginServer>/aci-helloworld:v1 --cpu 1 --memory 1 --registry-username <acrName> --registry-password <acrPassword> --dns-name-label aci-demo --ports 80
```

<span data-ttu-id="1e231-149">You should get an initial response back from Azure Resource Manager with details on your container.</span><span class="sxs-lookup"><span data-stu-id="1e231-149">You should get an initial response back from Azure Resource Manager with details on your container.</span></span> <span data-ttu-id="1e231-150">To monitor the status of your container and check and see when it is running, repeat the [az container show][az-container-show].</span><span class="sxs-lookup"><span data-stu-id="1e231-150">To monitor the status of your container and check and see when it is running, repeat the [az container show][az-container-show].</span></span> <span data-ttu-id="1e231-151">It should take less than a minute.</span><span class="sxs-lookup"><span data-stu-id="1e231-151">It should take less than a minute.</span></span>

```azurecli
az container show --resource-group myResourceGroup --name acr-quickstart --query instanceView.state
```

## <a name="view-the-application"></a><span data-ttu-id="1e231-152">View the application</span><span class="sxs-lookup"><span data-stu-id="1e231-152">View the application</span></span>

<span data-ttu-id="1e231-153">Once the deployment to ACI is successful, retrieve the container's FQDN with the [az container show][az-container-show] command:</span><span class="sxs-lookup"><span data-stu-id="1e231-153">Once the deployment to ACI is successful, retrieve the container's FQDN with the [az container show][az-container-show] command:</span></span>

```azurecli
az container show --resource-group myResourceGroup --name acr-quickstart --query ipAddress.fqdn
```

<span data-ttu-id="1e231-154">Example output: `"aci-demo.eastus.azurecontainer.io"`</span><span class="sxs-lookup"><span data-stu-id="1e231-154">Example output: `"aci-demo.eastus.azurecontainer.io"`</span></span>

<span data-ttu-id="1e231-155">To see the running application, navigate to the public IP address in your favorite browser.</span><span class="sxs-lookup"><span data-stu-id="1e231-155">To see the running application, navigate to the public IP address in your favorite browser.</span></span>

![Hello world app in the browser][aci-app-browser]

## <a name="clean-up-resources"></a><span data-ttu-id="1e231-157">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="1e231-157">Clean up resources</span></span>

<span data-ttu-id="1e231-158">When no longer needed, you can use the [az group delete][az-group-delete] command to remove the resource group, ACR instance, and all container images.</span><span class="sxs-lookup"><span data-stu-id="1e231-158">When no longer needed, you can use the [az group delete][az-group-delete] command to remove the resource group, ACR instance, and all container images.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="1e231-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="1e231-159">Next steps</span></span>

<span data-ttu-id="1e231-160">In this quickstart, you created an Azure Container Registry with the Azure CLI, pushed a container image to the registry, and launched an instance of it via Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="1e231-160">In this quickstart, you created an Azure Container Registry with the Azure CLI, pushed a container image to the registry, and launched an instance of it via Azure Container Instances.</span></span> <span data-ttu-id="1e231-161">Continue to the Azure Container Instances tutorial for a deeper look at ACI.</span><span class="sxs-lookup"><span data-stu-id="1e231-161">Continue to the Azure Container Instances tutorial for a deeper look at ACI.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="1e231-162">[Azure Container Instances tutorial][container-instances-tutorial-prepare-app]</span><span class="sxs-lookup"><span data-stu-id="1e231-162">[Azure Container Instances tutorial][container-instances-tutorial-prepare-app]</span></span>

<!-- IMAGES> -->
[aci-app-browser]: ../container-instances/media/container-instances-quickstart/aci-app-browser.png


<!-- LINKS - external -->
[docker-linux]: https://docs.docker.com/engine/installation/#supported-platforms
[docker-login]: https://docs.docker.com/engine/reference/commandline/login/
[docker-mac]: https://docs.docker.com/docker-for-mac/
[docker-push]: https://docs.docker.com/engine/reference/commandline/push/
[docker-tag]: https://docs.docker.com/engine/reference/commandline/tag/
[docker-windows]: https://docs.docker.com/docker-for-windows/

<!-- LINKS - internal -->
[az-acr-create]: /cli/azure/acr#az-acr-create
[az-acr-login]: /cli/azure/acr#az-acr-login
[az-group-create]: /cli/azure/group#az-group-create
[az-group-delete]: /cli/azure/group#az-group-delete
[azure-cli]: /cli/azure/install-azure-cli
[az-container-show]: /cli/azure/container#az-container-show
[container-instances-tutorial-prepare-app]: ../container-instances/container-instances-tutorial-prepare-app.md
[container-registry-skus]: container-registry-skus.md
[container-registry-auth-aci]: container-registry-auth-aci.md
