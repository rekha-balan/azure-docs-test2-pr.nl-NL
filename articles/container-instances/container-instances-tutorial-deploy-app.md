---
title: Azure Container Instances tutorial - Deploy app
description: Azure Container Instances tutorial part 3 of 3 - Deploy application
services: container-instances
author: mmacy
manager: jeconnoc
ms.service: container-instances
ms.topic: tutorial
ms.date: 03/21/2018
ms.author: marsma
ms.custom: mvc
ms.openlocfilehash: 5a68baa0c04dd90236e99cf010c96b1876fb4638
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865186"
---
# <a name="tutorial-deploy-a-container-to-azure-container-instances"></a><span data-ttu-id="4eef0-103">Tutorial: Deploy a container to Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="4eef0-103">Tutorial: Deploy a container to Azure Container Instances</span></span>

<span data-ttu-id="4eef0-104">This is the final tutorial in a three-part series.</span><span class="sxs-lookup"><span data-stu-id="4eef0-104">This is the final tutorial in a three-part series.</span></span> <span data-ttu-id="4eef0-105">Earlier in the series, [a container image was created](container-instances-tutorial-prepare-app.md) and [pushed to Azure Container Registry](container-instances-tutorial-prepare-acr.md).</span><span class="sxs-lookup"><span data-stu-id="4eef0-105">Earlier in the series, [a container image was created](container-instances-tutorial-prepare-app.md) and [pushed to Azure Container Registry](container-instances-tutorial-prepare-acr.md).</span></span> <span data-ttu-id="4eef0-106">This article completes the series by deploying the container to Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="4eef0-106">This article completes the series by deploying the container to Azure Container Instances.</span></span>

<span data-ttu-id="4eef0-107">In this tutorial, you:</span><span class="sxs-lookup"><span data-stu-id="4eef0-107">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4eef0-108">Deploy the container from Azure Container Registry to Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="4eef0-108">Deploy the container from Azure Container Registry to Azure Container Instances</span></span>
> * <span data-ttu-id="4eef0-109">View the running application in the browser</span><span class="sxs-lookup"><span data-stu-id="4eef0-109">View the running application in the browser</span></span>
> * <span data-ttu-id="4eef0-110">Display the container's logs</span><span class="sxs-lookup"><span data-stu-id="4eef0-110">Display the container's logs</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4eef0-111">Before you begin</span><span class="sxs-lookup"><span data-stu-id="4eef0-111">Before you begin</span></span>

[!INCLUDE [container-instances-tutorial-prerequisites](../../includes/container-instances-tutorial-prerequisites.md)]

## <a name="deploy-the-container-using-the-azure-cli"></a><span data-ttu-id="4eef0-112">Deploy the container using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4eef0-112">Deploy the container using the Azure CLI</span></span>

<span data-ttu-id="4eef0-113">In this section, you use the Azure CLI to deploy the image built in the [first tutorial](container-instances-tutorial-prepare-app.md) and pushed to Azure Container Registry in the [second tutorial](container-instances-tutorial-prepare-acr.md).</span><span class="sxs-lookup"><span data-stu-id="4eef0-113">In this section, you use the Azure CLI to deploy the image built in the [first tutorial](container-instances-tutorial-prepare-app.md) and pushed to Azure Container Registry in the [second tutorial](container-instances-tutorial-prepare-acr.md).</span></span> <span data-ttu-id="4eef0-114">Be sure you've completed those tutorials before proceeding.</span><span class="sxs-lookup"><span data-stu-id="4eef0-114">Be sure you've completed those tutorials before proceeding.</span></span>

### <a name="get-registry-credentials"></a><span data-ttu-id="4eef0-115">Get registry credentials</span><span class="sxs-lookup"><span data-stu-id="4eef0-115">Get registry credentials</span></span>

<span data-ttu-id="4eef0-116">When you deploy an image that's hosted in a private container registry like the one created in the [second tutorial](container-instances-tutorial-prepare-acr.md), you must supply the registry's credentials.</span><span class="sxs-lookup"><span data-stu-id="4eef0-116">When you deploy an image that's hosted in a private container registry like the one created in the [second tutorial](container-instances-tutorial-prepare-acr.md), you must supply the registry's credentials.</span></span>

<span data-ttu-id="4eef0-117">First, get the full name of the container registry login server (replace `<acrName>` with the name of your registry):</span><span class="sxs-lookup"><span data-stu-id="4eef0-117">First, get the full name of the container registry login server (replace `<acrName>` with the name of your registry):</span></span>

```azurecli
az acr show --name <acrName> --query loginServer
```

<span data-ttu-id="4eef0-118">Next, get the container registry password:</span><span class="sxs-lookup"><span data-stu-id="4eef0-118">Next, get the container registry password:</span></span>

```azurecli
az acr credential show --name <acrName> --query "passwords[0].value"
```

### <a name="deploy-container"></a><span data-ttu-id="4eef0-119">Deploy container</span><span class="sxs-lookup"><span data-stu-id="4eef0-119">Deploy container</span></span>

<span data-ttu-id="4eef0-120">Now, use the [az container create][az-container-create] command to deploy the container.</span><span class="sxs-lookup"><span data-stu-id="4eef0-120">Now, use the [az container create][az-container-create] command to deploy the container.</span></span> <span data-ttu-id="4eef0-121">Replace `<acrLoginServer>` and `<acrPassword>` with the values you obtained from the previous two commands.</span><span class="sxs-lookup"><span data-stu-id="4eef0-121">Replace `<acrLoginServer>` and `<acrPassword>` with the values you obtained from the previous two commands.</span></span> <span data-ttu-id="4eef0-122">Replace `<acrName>` with the name of your container registry.</span><span class="sxs-lookup"><span data-stu-id="4eef0-122">Replace `<acrName>` with the name of your container registry.</span></span>

```azurecli
az container create --resource-group myResourceGroup --name aci-tutorial-app --image <acrLoginServer>/aci-tutorial-app:v1 --cpu 1 --memory 1 --registry-login-server <acrLoginServer> --registry-username <acrName> --registry-password <acrPassword> --dns-name-label aci-demo --ports 80
```

<span data-ttu-id="4eef0-123">Within a few seconds, you should receive an initial response from Azure.</span><span class="sxs-lookup"><span data-stu-id="4eef0-123">Within a few seconds, you should receive an initial response from Azure.</span></span> <span data-ttu-id="4eef0-124">The `--dns-name-label` value must be unique within the Azure region you create the container instance.</span><span class="sxs-lookup"><span data-stu-id="4eef0-124">The `--dns-name-label` value must be unique within the Azure region you create the container instance.</span></span> <span data-ttu-id="4eef0-125">Modify the value in the preceding command if you receive a **DNS name label** error message when you execute the command.</span><span class="sxs-lookup"><span data-stu-id="4eef0-125">Modify the value in the preceding command if you receive a **DNS name label** error message when you execute the command.</span></span>

### <a name="verify-deployment-progress"></a><span data-ttu-id="4eef0-126">Verify deployment progress</span><span class="sxs-lookup"><span data-stu-id="4eef0-126">Verify deployment progress</span></span>

<span data-ttu-id="4eef0-127">To view the state of the deployment, use [az container show][az-container-show]:</span><span class="sxs-lookup"><span data-stu-id="4eef0-127">To view the state of the deployment, use [az container show][az-container-show]:</span></span>

```azurecli
az container show --resource-group myResourceGroup --name aci-tutorial-app --query instanceView.state
```

<span data-ttu-id="4eef0-128">Repeat the [az container show][az-container-show] command until the state changes from *Pending* to *Running*, which should take under a minute.</span><span class="sxs-lookup"><span data-stu-id="4eef0-128">Repeat the [az container show][az-container-show] command until the state changes from *Pending* to *Running*, which should take under a minute.</span></span> <span data-ttu-id="4eef0-129">When the container is *Running*, proceed to the next step.</span><span class="sxs-lookup"><span data-stu-id="4eef0-129">When the container is *Running*, proceed to the next step.</span></span>

## <a name="view-the-application-and-container-logs"></a><span data-ttu-id="4eef0-130">View the application and container logs</span><span class="sxs-lookup"><span data-stu-id="4eef0-130">View the application and container logs</span></span>

<span data-ttu-id="4eef0-131">Once the deployment succeeds, display the container's fully qualified domain name (FQDN) with the [az container show][az-container-show] command:</span><span class="sxs-lookup"><span data-stu-id="4eef0-131">Once the deployment succeeds, display the container's fully qualified domain name (FQDN) with the [az container show][az-container-show] command:</span></span>

```bash
az container show --resource-group myResourceGroup --name aci-tutorial-app --query ipAddress.fqdn
```

<span data-ttu-id="4eef0-132">For example:</span><span class="sxs-lookup"><span data-stu-id="4eef0-132">For example:</span></span>
```console
$ az container show --resource-group myResourceGroup --name aci-tutorial-app --query ipAddress.fqdn
"aci-demo.eastus.azurecontainer.io"
```

<span data-ttu-id="4eef0-133">To see the running application, navigate to the displayed DNS name in your favorite browser:</span><span class="sxs-lookup"><span data-stu-id="4eef0-133">To see the running application, navigate to the displayed DNS name in your favorite browser:</span></span>

![Hello world app in the browser][aci-app-browser]

<span data-ttu-id="4eef0-135">You can also view the log output of the container:</span><span class="sxs-lookup"><span data-stu-id="4eef0-135">You can also view the log output of the container:</span></span>

```azurecli
az container logs --resource-group myResourceGroup --name aci-tutorial-app
```

<span data-ttu-id="4eef0-136">Example output:</span><span class="sxs-lookup"><span data-stu-id="4eef0-136">Example output:</span></span>

```bash
$ az container logs --resource-group myResourceGroup --name aci-tutorial-app
listening on port 80
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://aci-demo.eastus.azurecontainer.io/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="clean-up-resources"></a><span data-ttu-id="4eef0-137">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="4eef0-137">Clean up resources</span></span>

<span data-ttu-id="4eef0-138">If you no longer need any of the resources you created in this tutorial series, you can execute the [az group delete][az-group-delete] command to remove the resource group and all resources it contains.</span><span class="sxs-lookup"><span data-stu-id="4eef0-138">If you no longer need any of the resources you created in this tutorial series, you can execute the [az group delete][az-group-delete] command to remove the resource group and all resources it contains.</span></span> <span data-ttu-id="4eef0-139">This command deletes the container registry you created, as well as the running container, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="4eef0-139">This command deletes the container registry you created, as well as the running container, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="4eef0-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="4eef0-140">Next steps</span></span>

<span data-ttu-id="4eef0-141">In this tutorial, you completed the process of deploying your container to Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="4eef0-141">In this tutorial, you completed the process of deploying your container to Azure Container Instances.</span></span> <span data-ttu-id="4eef0-142">The following steps were completed:</span><span class="sxs-lookup"><span data-stu-id="4eef0-142">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4eef0-143">Deployed the container from Azure Container Registry using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4eef0-143">Deployed the container from Azure Container Registry using the Azure CLI</span></span>
> * <span data-ttu-id="4eef0-144">Viewed the application in the browser</span><span class="sxs-lookup"><span data-stu-id="4eef0-144">Viewed the application in the browser</span></span>
> * <span data-ttu-id="4eef0-145">Viewed the container logs</span><span class="sxs-lookup"><span data-stu-id="4eef0-145">Viewed the container logs</span></span>

<span data-ttu-id="4eef0-146">Now that you have the basics down, move on to learning more about Azure Container Instances, such as how container groups work:</span><span class="sxs-lookup"><span data-stu-id="4eef0-146">Now that you have the basics down, move on to learning more about Azure Container Instances, such as how container groups work:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4eef0-147">Container groups in Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="4eef0-147">Container groups in Azure Container Instances</span></span>](container-instances-container-groups.md)

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png

<!-- LINKS - external -->
[docker-linux]: https://docs.docker.com/engine/installation/#supported-platforms
[docker-login]: https://docs.docker.com/engine/reference/commandline/login/
[docker-mac]: https://docs.docker.com/docker-for-mac/
[docker-push]: https://docs.docker.com/engine/reference/commandline/push/
[docker-tag]: https://docs.docker.com/engine/reference/commandline/tag/
[docker-windows]: https://docs.docker.com/docker-for-windows/

<!-- LINKS - internal -->
[az-container-create]: /cli/azure/container#az-container-create
[az-container-show]: /cli/azure/container#az-container-show
[az-group-delete]: /cli/azure/group#az-group-delete
[azure-cli-install]: /cli/azure/install-azure-cli
[prepare-app]: ./container-instances-tutorial-prepare-app.md
