---
title: Using ACR with an Azure DC/OS cluster
description: Use an Azure Container Registry with a DC/OS cluster in Azure Container Service
services: container-service
author: julienstroheker
manager: dcaro
ms.service: container-service
ms.topic: tutorial
ms.date: 03/23/2017
ms.author: juliens
ms.custom: mvc
ms.openlocfilehash: 15bd452ad2b80334c3f6168e6dee89bdd7c5efc4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865005"
---
# <a name="use-acr-with-a-dcos-cluster-to-deploy-your-application"></a><span data-ttu-id="ea83a-103">Use ACR with a DC/OS cluster to deploy your application</span><span class="sxs-lookup"><span data-stu-id="ea83a-103">Use ACR with a DC/OS cluster to deploy your application</span></span>

<span data-ttu-id="ea83a-104">In this article, we explore how to use Azure Container Registry with a DC/OS cluster.</span><span class="sxs-lookup"><span data-stu-id="ea83a-104">In this article, we explore how to use Azure Container Registry with a DC/OS cluster.</span></span> <span data-ttu-id="ea83a-105">Using ACR allows you to privately store and manage container images.</span><span class="sxs-lookup"><span data-stu-id="ea83a-105">Using ACR allows you to privately store and manage container images.</span></span> <span data-ttu-id="ea83a-106">This tutorial covers the following tasks:</span><span class="sxs-lookup"><span data-stu-id="ea83a-106">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ea83a-107">Deploy Azure Container Registry (if needed)</span><span class="sxs-lookup"><span data-stu-id="ea83a-107">Deploy Azure Container Registry (if needed)</span></span>
> * <span data-ttu-id="ea83a-108">Configure ACR authentication on a DC/OS cluster</span><span class="sxs-lookup"><span data-stu-id="ea83a-108">Configure ACR authentication on a DC/OS cluster</span></span>
> * <span data-ttu-id="ea83a-109">Uploaded an image to the Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="ea83a-109">Uploaded an image to the Azure Container Registry</span></span>
> * <span data-ttu-id="ea83a-110">Run a container image from the Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="ea83a-110">Run a container image from the Azure Container Registry</span></span>

<span data-ttu-id="ea83a-111">You need an ACS DC/OS cluster to complete the steps in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="ea83a-111">You need an ACS DC/OS cluster to complete the steps in this tutorial.</span></span> <span data-ttu-id="ea83a-112">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span><span class="sxs-lookup"><span data-stu-id="ea83a-112">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="ea83a-113">This tutorial requires the Azure CLI version 2.0.4 or later.</span><span class="sxs-lookup"><span data-stu-id="ea83a-113">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="ea83a-114">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="ea83a-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="ea83a-115">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ea83a-115">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="ea83a-116">Deploy Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="ea83a-116">Deploy Azure Container Registry</span></span>

<span data-ttu-id="ea83a-117">If needed, create an Azure Container registry with the [az acr create](/cli/azure/acr#az-acr-create) command.</span><span class="sxs-lookup"><span data-stu-id="ea83a-117">If needed, create an Azure Container registry with the [az acr create](/cli/azure/acr#az-acr-create) command.</span></span> 

<span data-ttu-id="ea83a-118">The following example creates a registry with a randomly generate name.</span><span class="sxs-lookup"><span data-stu-id="ea83a-118">The following example creates a registry with a randomly generate name.</span></span> <span data-ttu-id="ea83a-119">The registry is also configured with an admin account using the `--admin-enabled` argument.</span><span class="sxs-lookup"><span data-stu-id="ea83a-119">The registry is also configured with an admin account using the `--admin-enabled` argument.</span></span>

```azurecli-interactive
az acr create --resource-group myResourceGroup --name myContainerRegistry$RANDOM --sku Basic
```

<span data-ttu-id="ea83a-120">Once the registry has been created, the Azure CLI outputs data similar to the following.</span><span class="sxs-lookup"><span data-stu-id="ea83a-120">Once the registry has been created, the Azure CLI outputs data similar to the following.</span></span> <span data-ttu-id="ea83a-121">Take note of the `name` and `loginServer`, these are used in later steps.</span><span class="sxs-lookup"><span data-stu-id="ea83a-121">Take note of the `name` and `loginServer`, these are used in later steps.</span></span>

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T03:40:56.511597+00:00",
  "id": "/subscriptions/f2799821-a08a-434e-9128-454ec4348b10/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry23489",
  "location": "eastus",
  "loginServer": "mycontainerregistry23489.azurecr.io",
  "name": "myContainerRegistry23489",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "mycontainerregistr034017"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

<span data-ttu-id="ea83a-122">Get the container registry credentials using the [az acr credential show](/cli/azure/acr/credential) command.</span><span class="sxs-lookup"><span data-stu-id="ea83a-122">Get the container registry credentials using the [az acr credential show](/cli/azure/acr/credential) command.</span></span> <span data-ttu-id="ea83a-123">Substitute the `--name` with the one noted in the last step.</span><span class="sxs-lookup"><span data-stu-id="ea83a-123">Substitute the `--name` with the one noted in the last step.</span></span> <span data-ttu-id="ea83a-124">Take note of one password, it is needed in a later step.</span><span class="sxs-lookup"><span data-stu-id="ea83a-124">Take note of one password, it is needed in a later step.</span></span>

```azurecli-interactive
az acr credential show --name myContainerRegistry23489
```

<span data-ttu-id="ea83a-125">For more information on Azure Container Registry, see [Introduction to private Docker container registries](../../container-registry/container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="ea83a-125">For more information on Azure Container Registry, see [Introduction to private Docker container registries](../../container-registry/container-registry-intro.md).</span></span> 

## <a name="manage-acr-authentication"></a><span data-ttu-id="ea83a-126">Manage ACR authentication</span><span class="sxs-lookup"><span data-stu-id="ea83a-126">Manage ACR authentication</span></span>

<span data-ttu-id="ea83a-127">The conventional way to push and pull image from a private registry is to first authenticate with the registry.</span><span class="sxs-lookup"><span data-stu-id="ea83a-127">The conventional way to push and pull image from a private registry is to first authenticate with the registry.</span></span> <span data-ttu-id="ea83a-128">To do so, you would use the `docker login` command on any client that needs to access the private registry.</span><span class="sxs-lookup"><span data-stu-id="ea83a-128">To do so, you would use the `docker login` command on any client that needs to access the private registry.</span></span> <span data-ttu-id="ea83a-129">Because a DC/OS cluster can contain many nodes, all of which need to be authenticated with the ACR, it is helpful to automate this process across each node.</span><span class="sxs-lookup"><span data-stu-id="ea83a-129">Because a DC/OS cluster can contain many nodes, all of which need to be authenticated with the ACR, it is helpful to automate this process across each node.</span></span> 

### <a name="create-shared-storage"></a><span data-ttu-id="ea83a-130">Create shared storage</span><span class="sxs-lookup"><span data-stu-id="ea83a-130">Create shared storage</span></span>

<span data-ttu-id="ea83a-131">This process uses an Azure file share that has been mounted on each node in the cluster.</span><span class="sxs-lookup"><span data-stu-id="ea83a-131">This process uses an Azure file share that has been mounted on each node in the cluster.</span></span> <span data-ttu-id="ea83a-132">If you have not already set up shared storage, see [Setup a file share inside a DC/OS cluster](container-service-dcos-fileshare.md).</span><span class="sxs-lookup"><span data-stu-id="ea83a-132">If you have not already set up shared storage, see [Setup a file share inside a DC/OS cluster](container-service-dcos-fileshare.md).</span></span>

### <a name="configure-acr-authentication"></a><span data-ttu-id="ea83a-133">Configure ACR authentication</span><span class="sxs-lookup"><span data-stu-id="ea83a-133">Configure ACR authentication</span></span>

<span data-ttu-id="ea83a-134">First, get the FQDN of the DC/OS master and store it in a variable.</span><span class="sxs-lookup"><span data-stu-id="ea83a-134">First, get the FQDN of the DC/OS master and store it in a variable.</span></span>

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

<span data-ttu-id="ea83a-135">Create an SSH connection with the master (or the first master) of your DC/OS-based cluster.</span><span class="sxs-lookup"><span data-stu-id="ea83a-135">Create an SSH connection with the master (or the first master) of your DC/OS-based cluster.</span></span> <span data-ttu-id="ea83a-136">Update the user name if a non-default value was used when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="ea83a-136">Update the user name if a non-default value was used when creating the cluster.</span></span>

```azurecli-interactive
ssh azureuser@$FQDN
```

<span data-ttu-id="ea83a-137">Run the following command to login to the Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="ea83a-137">Run the following command to login to the Azure Container Registry.</span></span> <span data-ttu-id="ea83a-138">Replace the `--username` with the name of the container registry, and the `--password` with one of the provided passwords.</span><span class="sxs-lookup"><span data-stu-id="ea83a-138">Replace the `--username` with the name of the container registry, and the `--password` with one of the provided passwords.</span></span> <span data-ttu-id="ea83a-139">Replace the last argument *mycontainerregistry.azurecr.io* in the example with the loginServer name of the container registry.</span><span class="sxs-lookup"><span data-stu-id="ea83a-139">Replace the last argument *mycontainerregistry.azurecr.io* in the example with the loginServer name of the container registry.</span></span> 

<span data-ttu-id="ea83a-140">This command stores the authentication values locally under the `~/.docker` path.</span><span class="sxs-lookup"><span data-stu-id="ea83a-140">This command stores the authentication values locally under the `~/.docker` path.</span></span>

```azurecli-interactive
docker -H tcp://localhost:2375 login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry.azurecr.io
```

<span data-ttu-id="ea83a-141">Create a compressed file that contains the container registry authentication values.</span><span class="sxs-lookup"><span data-stu-id="ea83a-141">Create a compressed file that contains the container registry authentication values.</span></span>

```azurecli-interactive
tar czf docker.tar.gz .docker
```

<span data-ttu-id="ea83a-142">Copy this file to the cluster shared storage.</span><span class="sxs-lookup"><span data-stu-id="ea83a-142">Copy this file to the cluster shared storage.</span></span> <span data-ttu-id="ea83a-143">This step makes the file available on all nodes of the DC/OS cluster.</span><span class="sxs-lookup"><span data-stu-id="ea83a-143">This step makes the file available on all nodes of the DC/OS cluster.</span></span>

```azurecli-interactive
cp docker.tar.gz /mnt/share/dcosshare
```

## <a name="upload-image-to-acr"></a><span data-ttu-id="ea83a-144">Upload image to ACR</span><span class="sxs-lookup"><span data-stu-id="ea83a-144">Upload image to ACR</span></span>

<span data-ttu-id="ea83a-145">Now from a development machine, or any other system with Docker installed, create an image and upload it to the Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="ea83a-145">Now from a development machine, or any other system with Docker installed, create an image and upload it to the Azure Container Registry.</span></span>

<span data-ttu-id="ea83a-146">Create a container from the Ubuntu image.</span><span class="sxs-lookup"><span data-stu-id="ea83a-146">Create a container from the Ubuntu image.</span></span>

```azurecli-interactive
docker run ubuntu --name base-image
```

<span data-ttu-id="ea83a-147">Now capture the container into a new image.</span><span class="sxs-lookup"><span data-stu-id="ea83a-147">Now capture the container into a new image.</span></span> <span data-ttu-id="ea83a-148">The image name needs to include the `loginServer` name of the container registrywith a format of `loginServer/imageName`.</span><span class="sxs-lookup"><span data-stu-id="ea83a-148">The image name needs to include the `loginServer` name of the container registrywith a format of `loginServer/imageName`.</span></span>

```azurecli-interactive
docker -H tcp://localhost:2375 commit base-image mycontainerregistry30678.azurecr.io/dcos-demo
````

<span data-ttu-id="ea83a-149">Login into the Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="ea83a-149">Login into the Azure Container Registry.</span></span> <span data-ttu-id="ea83a-150">Replace the name with the loginServer name, the --username with the name of the container registry, and the --password with one of the provided passwords.</span><span class="sxs-lookup"><span data-stu-id="ea83a-150">Replace the name with the loginServer name, the --username with the name of the container registry, and the --password with one of the provided passwords.</span></span>

```azurecli-interactive
docker login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry2675.azurecr.io
```

<span data-ttu-id="ea83a-151">Finally, upload the image to the ACR registry.</span><span class="sxs-lookup"><span data-stu-id="ea83a-151">Finally, upload the image to the ACR registry.</span></span> <span data-ttu-id="ea83a-152">This example uploads an image named dcos-demo.</span><span class="sxs-lookup"><span data-stu-id="ea83a-152">This example uploads an image named dcos-demo.</span></span>

```azurecli-interactive
docker push mycontainerregistry30678.azurecr.io/dcos-demo
```

## <a name="run-an-image-from-acr"></a><span data-ttu-id="ea83a-153">Run an image from ACR</span><span class="sxs-lookup"><span data-stu-id="ea83a-153">Run an image from ACR</span></span>

<span data-ttu-id="ea83a-154">To use an image from the ACR registry, create a file names *acrDemo.json* and copy the following text into it.</span><span class="sxs-lookup"><span data-stu-id="ea83a-154">To use an image from the ACR registry, create a file names *acrDemo.json* and copy the following text into it.</span></span> <span data-ttu-id="ea83a-155">Replace the image name with the container registry loginServer name and image name, for example `loginServer/imageName`.</span><span class="sxs-lookup"><span data-stu-id="ea83a-155">Replace the image name with the container registry loginServer name and image name, for example `loginServer/imageName`.</span></span> <span data-ttu-id="ea83a-156">Take note of the `uris` property.</span><span class="sxs-lookup"><span data-stu-id="ea83a-156">Take note of the `uris` property.</span></span> <span data-ttu-id="ea83a-157">This property holds the location of the container registry authentication file, which in this case is the Azure file share that is mounted on each node in the DC/OS cluster.</span><span class="sxs-lookup"><span data-stu-id="ea83a-157">This property holds the location of the container registry authentication file, which in this case is the Azure file share that is mounted on each node in the DC/OS cluster.</span></span>

```json
{
  "id": "myapp",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "mycontainerregistry30678.azurecr.io/dcos-demo",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "uris":  [
       "file:///mnt/share/dcosshare/docker.tar.gz"
   ]
}
```

<span data-ttu-id="ea83a-158">Deploy the application with the DC/OC CLI.</span><span class="sxs-lookup"><span data-stu-id="ea83a-158">Deploy the application with the DC/OC CLI.</span></span>

```azurecli-interactive
dcos marathon app add acrDemo.json
```

## <a name="next-steps"></a><span data-ttu-id="ea83a-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="ea83a-159">Next steps</span></span>

<span data-ttu-id="ea83a-160">In this tutorial you have configure DC/OS to use Azure Container Registry including the following tasks:</span><span class="sxs-lookup"><span data-stu-id="ea83a-160">In this tutorial you have configure DC/OS to use Azure Container Registry including the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ea83a-161">Deploy Azure Container Registry (if needed)</span><span class="sxs-lookup"><span data-stu-id="ea83a-161">Deploy Azure Container Registry (if needed)</span></span>
> * <span data-ttu-id="ea83a-162">Configure ACR authentication on a DC/OS cluster</span><span class="sxs-lookup"><span data-stu-id="ea83a-162">Configure ACR authentication on a DC/OS cluster</span></span>
> * <span data-ttu-id="ea83a-163">Uploaded an image to the Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="ea83a-163">Uploaded an image to the Azure Container Registry</span></span>
> * <span data-ttu-id="ea83a-164">Run a container image from the Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="ea83a-164">Run a container image from the Azure Container Registry</span></span>
