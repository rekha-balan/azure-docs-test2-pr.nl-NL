---
title: Quickstart - Create your first Azure Container Instances container
description: In this quickstart, you use the Azure CLI to deploy a container in Azure Container Instances
services: container-instances
author: mmacy
manager: jeconnoc
ms.service: container-instances
ms.topic: quickstart
ms.date: 05/11/2018
ms.author: marsma
ms.custom: mvc
ms.openlocfilehash: 07632e85719e2d0d446b8f718dbc64d2e9d77617
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866048"
---
# <a name="quickstart-create-your-first-container-in-azure-container-instances"></a><span data-ttu-id="05244-103">Quickstart: Create your first container in Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="05244-103">Quickstart: Create your first container in Azure Container Instances</span></span>

<span data-ttu-id="05244-104">Azure Container Instances makes it easy to create and manage Docker containers in Azure, without having to provision virtual machines or adopt a higher-level service.</span><span class="sxs-lookup"><span data-stu-id="05244-104">Azure Container Instances makes it easy to create and manage Docker containers in Azure, without having to provision virtual machines or adopt a higher-level service.</span></span> <span data-ttu-id="05244-105">In this quickstart, you create a container in Azure and expose it to the internet with a fully qualified domain name (FQDN).</span><span class="sxs-lookup"><span data-stu-id="05244-105">In this quickstart, you create a container in Azure and expose it to the internet with a fully qualified domain name (FQDN).</span></span> <span data-ttu-id="05244-106">This operation is completed in a single command.</span><span class="sxs-lookup"><span data-stu-id="05244-106">This operation is completed in a single command.</span></span> <span data-ttu-id="05244-107">Within just a few seconds, you'll see this in your browser:</span><span class="sxs-lookup"><span data-stu-id="05244-107">Within just a few seconds, you'll see this in your browser:</span></span>

![App deployed using Azure Container Instances viewed in browser][aci-app-browser]

<span data-ttu-id="05244-109">If you don't have an Azure subscription, create a [free account][azure-account] before you begin.</span><span class="sxs-lookup"><span data-stu-id="05244-109">If you don't have an Azure subscription, create a [free account][azure-account] before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="05244-110">You can use the Azure Cloud Shell or a local installation of the Azure CLI to complete this quickstart.</span><span class="sxs-lookup"><span data-stu-id="05244-110">You can use the Azure Cloud Shell or a local installation of the Azure CLI to complete this quickstart.</span></span> <span data-ttu-id="05244-111">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.27 or later.</span><span class="sxs-lookup"><span data-stu-id="05244-111">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.27 or later.</span></span> <span data-ttu-id="05244-112">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="05244-112">Run `az --version` to find the version.</span></span> <span data-ttu-id="05244-113">If you need to install or upgrade, see [Install Azure CLI][azure-cli-install].</span><span class="sxs-lookup"><span data-stu-id="05244-113">If you need to install or upgrade, see [Install Azure CLI][azure-cli-install].</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="05244-114">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="05244-114">Create a resource group</span></span>

<span data-ttu-id="05244-115">Azure container instances, like all Azure resources, must be placed in a resource group, a logical collection into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="05244-115">Azure container instances, like all Azure resources, must be placed in a resource group, a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="05244-116">Create a resource group with the [az group create][az-group-create] command.</span><span class="sxs-lookup"><span data-stu-id="05244-116">Create a resource group with the [az group create][az-group-create] command.</span></span>

<span data-ttu-id="05244-117">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span><span class="sxs-lookup"><span data-stu-id="05244-117">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-container"></a><span data-ttu-id="05244-118">Create a container</span><span class="sxs-lookup"><span data-stu-id="05244-118">Create a container</span></span>

<span data-ttu-id="05244-119">You can create a container by providing a name, a Docker image, and an Azure resource group to the [az container create][az-container-create] command.</span><span class="sxs-lookup"><span data-stu-id="05244-119">You can create a container by providing a name, a Docker image, and an Azure resource group to the [az container create][az-container-create] command.</span></span> <span data-ttu-id="05244-120">You can optionally expose the container to the internet by specifying a DNS name label.</span><span class="sxs-lookup"><span data-stu-id="05244-120">You can optionally expose the container to the internet by specifying a DNS name label.</span></span> <span data-ttu-id="05244-121">In this quickstart, you deploy a container that hosts a small web app written in [Node.js][node-js].</span><span class="sxs-lookup"><span data-stu-id="05244-121">In this quickstart, you deploy a container that hosts a small web app written in [Node.js][node-js].</span></span>

<span data-ttu-id="05244-122">Execute the following command to start a container instance.</span><span class="sxs-lookup"><span data-stu-id="05244-122">Execute the following command to start a container instance.</span></span> <span data-ttu-id="05244-123">The `--dns-name-label` value must be unique within the Azure region you create the instance, so you might need to modify this value to ensure uniqueness.</span><span class="sxs-lookup"><span data-stu-id="05244-123">The `--dns-name-label` value must be unique within the Azure region you create the instance, so you might need to modify this value to ensure uniqueness.</span></span>

```azurecli-interactive
az container create --resource-group myResourceGroup --name mycontainer --image microsoft/aci-helloworld --dns-name-label aci-demo --ports 80
```

<span data-ttu-id="05244-124">Within a few seconds, you should get a response to your request.</span><span class="sxs-lookup"><span data-stu-id="05244-124">Within a few seconds, you should get a response to your request.</span></span> <span data-ttu-id="05244-125">Initially, the container is in the **Creating** state, but it should start within a few seconds.</span><span class="sxs-lookup"><span data-stu-id="05244-125">Initially, the container is in the **Creating** state, but it should start within a few seconds.</span></span> <span data-ttu-id="05244-126">You can check the status using the [az container show][az-container-show] command:</span><span class="sxs-lookup"><span data-stu-id="05244-126">You can check the status using the [az container show][az-container-show] command:</span></span>

```azurecli-interactive
az container show --resource-group myResourceGroup --name mycontainer --query "{FQDN:ipAddress.fqdn,ProvisioningState:provisioningState}" --out table
```

<span data-ttu-id="05244-127">When you run the command, the container's fully qualified domain name (FQDN) and its provisioning state are displayed:</span><span class="sxs-lookup"><span data-stu-id="05244-127">When you run the command, the container's fully qualified domain name (FQDN) and its provisioning state are displayed:</span></span>

```console
$ az container show --resource-group myResourceGroup --name mycontainer --query "{FQDN:ipAddress.fqdn,ProvisioningState:provisioningState}" --out table
FQDN                               ProvisioningState
---------------------------------  -------------------
aci-demo.eastus.azurecontainer.io  Succeeded
```

<span data-ttu-id="05244-128">Once the container moves to the **Succeeded** state, navigate to its FQDN in your browser:</span><span class="sxs-lookup"><span data-stu-id="05244-128">Once the container moves to the **Succeeded** state, navigate to its FQDN in your browser:</span></span>

![Browser screenshot showing application running in an Azure container instance][aci-app-browser]

## <a name="pull-the-container-logs"></a><span data-ttu-id="05244-130">Pull the container logs</span><span class="sxs-lookup"><span data-stu-id="05244-130">Pull the container logs</span></span>

<span data-ttu-id="05244-131">Viewing the logs for a container instance is helpful when troubleshooting issues with your container or the application it runs.</span><span class="sxs-lookup"><span data-stu-id="05244-131">Viewing the logs for a container instance is helpful when troubleshooting issues with your container or the application it runs.</span></span>

<span data-ttu-id="05244-132">Pull the container's logs with the [az container logs][az-container-logs] command:</span><span class="sxs-lookup"><span data-stu-id="05244-132">Pull the container's logs with the [az container logs][az-container-logs] command:</span></span>

```azurecli-interactive
az container logs --resource-group myResourceGroup --name mycontainer
```

<span data-ttu-id="05244-133">The output displays the logs for the container, and should show the HTTP GET requests generated when you viewed the application in your browser.</span><span class="sxs-lookup"><span data-stu-id="05244-133">The output displays the logs for the container, and should show the HTTP GET requests generated when you viewed the application in your browser.</span></span>

```console
$ az container logs --resource-group myResourceGroup -n mycontainer
listening on port 80
::ffff:10.240.255.105 - - [15/Mar/2018:21:18:26 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/65.0.3325.146 Safari/537.36"
::ffff:10.240.255.105 - - [15/Mar/2018:21:18:26 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://aci-demo.eastus.azurecontainer.io/" "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/65.0.3325.146 Safari/537.36"
```

## <a name="attach-output-streams"></a><span data-ttu-id="05244-134">Attach output streams</span><span class="sxs-lookup"><span data-stu-id="05244-134">Attach output streams</span></span>

<span data-ttu-id="05244-135">In addition to tailing the logs, you can attach your local standard out and standard error streams to that of the container.</span><span class="sxs-lookup"><span data-stu-id="05244-135">In addition to tailing the logs, you can attach your local standard out and standard error streams to that of the container.</span></span>

<span data-ttu-id="05244-136">First, execute the [az container attach][az-container-attach] command to attach your local console the container's output streams:</span><span class="sxs-lookup"><span data-stu-id="05244-136">First, execute the [az container attach][az-container-attach] command to attach your local console the container's output streams:</span></span>

```azurecli-interactive
az container attach --resource-group myResourceGroup -n mycontainer
```

<span data-ttu-id="05244-137">Once attached, refresh your browser a few times to generate some additional output.</span><span class="sxs-lookup"><span data-stu-id="05244-137">Once attached, refresh your browser a few times to generate some additional output.</span></span> <span data-ttu-id="05244-138">Finally, detach your console with `Control+C`.</span><span class="sxs-lookup"><span data-stu-id="05244-138">Finally, detach your console with `Control+C`.</span></span> <span data-ttu-id="05244-139">You should see output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="05244-139">You should see output similar to the following:</span></span>

```console
$ az container attach --resource-group myResourceGroup -n mycontainer
Container 'mycontainer' is in state 'Running'...
(count: 1) (last timestamp: 2018-03-15 21:17:59+00:00) pulling image "microsoft/aci-helloworld"
(count: 1) (last timestamp: 2018-03-15 21:18:05+00:00) Successfully pulled image "microsoft/aci-helloworld"
(count: 1) (last timestamp: 2018-03-15 21:18:05+00:00) Created container with id 3534a1e2ee392d6f47b2c158ce8c1808d1686fc54f17de3a953d356cf5f26a45
(count: 1) (last timestamp: 2018-03-15 21:18:06+00:00) Started container with id 3534a1e2ee392d6f47b2c158ce8c1808d1686fc54f17de3a953d356cf5f26a45

Start streaming logs:
listening on port 80
::ffff:10.240.255.105 - - [15/Mar/2018:21:18:26 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/65.0.3325.146 Safari/537.36"
::ffff:10.240.255.105 - - [15/Mar/2018:21:18:26 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://aci-demo.eastus.azurecontainer.io/" "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/65.0.3325.146 Safari/537.36"
::ffff:10.240.255.107 - - [15/Mar/2018:21:18:44 +0000] "GET / HTTP/1.1" 304 - "-" "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/65.0.3325.146 Safari/537.36"
::ffff:10.240.255.107 - - [15/Mar/2018:21:18:47 +0000] "GET / HTTP/1.1" 304 - "-" "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/65.0.3325.146 Safari/537.36"
```

## <a name="clean-up-resources"></a><span data-ttu-id="05244-140">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="05244-140">Clean up resources</span></span>

<span data-ttu-id="05244-141">When you're done with the container, remove it using the [az container delete][az-container-delete] command:</span><span class="sxs-lookup"><span data-stu-id="05244-141">When you're done with the container, remove it using the [az container delete][az-container-delete] command:</span></span>

```azurecli-interactive
az container delete --resource-group myResourceGroup --name mycontainer
```

<span data-ttu-id="05244-142">To verify that the container has been deleted, execute the [az container list](/cli/azure/container#az-container-list) command:</span><span class="sxs-lookup"><span data-stu-id="05244-142">To verify that the container has been deleted, execute the [az container list](/cli/azure/container#az-container-list) command:</span></span>

```azurecli-interactive
az container list --resource-group myResourceGroup --output table
```

<span data-ttu-id="05244-143">The **mycontainer** container should not appear in the command's output.</span><span class="sxs-lookup"><span data-stu-id="05244-143">The **mycontainer** container should not appear in the command's output.</span></span> <span data-ttu-id="05244-144">If you have no other containers in the resource group, no output is displayed.</span><span class="sxs-lookup"><span data-stu-id="05244-144">If you have no other containers in the resource group, no output is displayed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05244-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="05244-145">Next steps</span></span>

<span data-ttu-id="05244-146">In this quickstart, you created an Azure container instance from an image in the public Docker Hub registry.</span><span class="sxs-lookup"><span data-stu-id="05244-146">In this quickstart, you created an Azure container instance from an image in the public Docker Hub registry.</span></span> <span data-ttu-id="05244-147">If you'd like to build a container image yourself and deploy it to Azure Container Instances from a private Azure container registry, continue to the Azure Container Instances tutorial.</span><span class="sxs-lookup"><span data-stu-id="05244-147">If you'd like to build a container image yourself and deploy it to Azure Container Instances from a private Azure container registry, continue to the Azure Container Instances tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="05244-148">Azure Container Instances tutorial</span><span class="sxs-lookup"><span data-stu-id="05244-148">Azure Container Instances tutorial</span></span>](./container-instances-tutorial-prepare-app.md)

<span data-ttu-id="05244-149">To try out options for running containers in an orchestration system on Azure, see the [Service Fabric][service-fabric] or [Azure Kubernetes Service (AKS)][container-service] quickstarts.</span><span class="sxs-lookup"><span data-stu-id="05244-149">To try out options for running containers in an orchestration system on Azure, see the [Service Fabric][service-fabric] or [Azure Kubernetes Service (AKS)][container-service] quickstarts.</span></span>

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png

<!-- LINKS - External -->
[app-github-repo]: https://github.com/Azure-Samples/aci-helloworld.git
[azure-account]: https://azure.microsoft.com/free/
[node-js]: http://nodejs.org

<!-- LINKS - Internal -->
[az-container-attach]: /cli/azure/container#az-container-attach
[az-container-create]: /cli/azure/container#az-container-create
[az-container-delete]: /cli/azure/container#az-container-delete
[az-container-list]: /cli/azure/container#az-container-list
[az-container-logs]: /cli/azure/container#az-container-logs
[az-container-show]: /cli/azure/container#az-container-show
[az-group-create]: /cli/azure/group#az-group-create
[azure-cli-install]: /cli/azure/install-azure-cli
[container-service]: ../aks/kubernetes-walkthrough.md
[service-fabric]: ../service-fabric/service-fabric-quickstart-containers.md
