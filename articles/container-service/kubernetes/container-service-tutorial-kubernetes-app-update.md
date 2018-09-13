---
title: Azure Container Service tutorial - Update application
description: Azure Container Service tutorial - Update Application
services: container-service
author: neilpeterson
manager: jeconnoc
ms.service: container-service
ms.topic: tutorial
ms.date: 02/26/2018
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 9cb5769d7f54a1036bf14199c87961c95ed2e7ce
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867528"
---
# <a name="update-an-application-in-kubernetes"></a><span data-ttu-id="c34e5-103">Update an application in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="c34e5-103">Update an application in Kubernetes</span></span>

[!INCLUDE [aks-preview-redirect.md](../../../includes/aks-preview-redirect.md)]

<span data-ttu-id="c34e5-104">After an application has been deployed in Kubernetes, it can be updated by specifying a new container image or image version.</span><span class="sxs-lookup"><span data-stu-id="c34e5-104">After an application has been deployed in Kubernetes, it can be updated by specifying a new container image or image version.</span></span> <span data-ttu-id="c34e5-105">When doing so, the update is staged so that only a portion of the deployment is concurrently updated.</span><span class="sxs-lookup"><span data-stu-id="c34e5-105">When doing so, the update is staged so that only a portion of the deployment is concurrently updated.</span></span> <span data-ttu-id="c34e5-106">This staged update enables the application to keep running during the update.</span><span class="sxs-lookup"><span data-stu-id="c34e5-106">This staged update enables the application to keep running during the update.</span></span> <span data-ttu-id="c34e5-107">It also provides a rollback mechanism if a deployment failure occurs.</span><span class="sxs-lookup"><span data-stu-id="c34e5-107">It also provides a rollback mechanism if a deployment failure occurs.</span></span> 

<span data-ttu-id="c34e5-108">In this tutorial, part six of seven, the sample Azure Vote app is updated.</span><span class="sxs-lookup"><span data-stu-id="c34e5-108">In this tutorial, part six of seven, the sample Azure Vote app is updated.</span></span> <span data-ttu-id="c34e5-109">Tasks that you complete include:</span><span class="sxs-lookup"><span data-stu-id="c34e5-109">Tasks that you complete include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c34e5-110">Updating the front-end application code</span><span class="sxs-lookup"><span data-stu-id="c34e5-110">Updating the front-end application code</span></span>
> * <span data-ttu-id="c34e5-111">Creating an updated container image</span><span class="sxs-lookup"><span data-stu-id="c34e5-111">Creating an updated container image</span></span>
> * <span data-ttu-id="c34e5-112">Pushing the container image to Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="c34e5-112">Pushing the container image to Azure Container Registry</span></span>
> * <span data-ttu-id="c34e5-113">Deploying the updated container image</span><span class="sxs-lookup"><span data-stu-id="c34e5-113">Deploying the updated container image</span></span>

<span data-ttu-id="c34e5-114">In subsequent tutorials, Log Analytics is configured to monitor the Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="c34e5-114">In subsequent tutorials, Log Analytics is configured to monitor the Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c34e5-115">Before you begin</span><span class="sxs-lookup"><span data-stu-id="c34e5-115">Before you begin</span></span>

<span data-ttu-id="c34e5-116">In previous tutorials, an application was packaged into a container image, the image uploaded to Azure Container Registry, and a Kubernetes cluster created.</span><span class="sxs-lookup"><span data-stu-id="c34e5-116">In previous tutorials, an application was packaged into a container image, the image uploaded to Azure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="c34e5-117">The application was then run on the Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="c34e5-117">The application was then run on the Kubernetes cluster.</span></span> 

<span data-ttu-id="c34e5-118">An application repository was also cloned which includes the application source code, and a pre-created Docker Compose file used in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="c34e5-118">An application repository was also cloned which includes the application source code, and a pre-created Docker Compose file used in this tutorial.</span></span> <span data-ttu-id="c34e5-119">Verify that you have created a clone of the repo, and that you have changed directories into the cloned directory.</span><span class="sxs-lookup"><span data-stu-id="c34e5-119">Verify that you have created a clone of the repo, and that you have changed directories into the cloned directory.</span></span> <span data-ttu-id="c34e5-120">Inside is a directory named `azure-vote` and a file named `docker-compose.yml`.</span><span class="sxs-lookup"><span data-stu-id="c34e5-120">Inside is a directory named `azure-vote` and a file named `docker-compose.yml`.</span></span>

<span data-ttu-id="c34e5-121">If you haven't completed these steps, and want to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="c34e5-121">If you haven't completed these steps, and want to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

## <a name="update-application"></a><span data-ttu-id="c34e5-122">Update application</span><span class="sxs-lookup"><span data-stu-id="c34e5-122">Update application</span></span>

<span data-ttu-id="c34e5-123">For this tutorial, a change is made to the application, and the updated application deployed to the Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="c34e5-123">For this tutorial, a change is made to the application, and the updated application deployed to the Kubernetes cluster.</span></span> 

<span data-ttu-id="c34e5-124">The application source code can be found inside of the `azure-vote` directory.</span><span class="sxs-lookup"><span data-stu-id="c34e5-124">The application source code can be found inside of the `azure-vote` directory.</span></span> <span data-ttu-id="c34e5-125">Open the `config_file.cfg` file with any code or text editor.</span><span class="sxs-lookup"><span data-stu-id="c34e5-125">Open the `config_file.cfg` file with any code or text editor.</span></span> <span data-ttu-id="c34e5-126">In this example `vi` is used.</span><span class="sxs-lookup"><span data-stu-id="c34e5-126">In this example `vi` is used.</span></span>

```bash
vi azure-vote/azure-vote/config_file.cfg
```

<span data-ttu-id="c34e5-127">Change the values for `VOTE1VALUE` and `VOTE2VALUE`, and then save the file.</span><span class="sxs-lookup"><span data-stu-id="c34e5-127">Change the values for `VOTE1VALUE` and `VOTE2VALUE`, and then save the file.</span></span>

```bash
# UI Configurations
TITLE = 'Azure Voting App'
VOTE1VALUE = 'Blue'
VOTE2VALUE = 'Purple'
SHOWHOST = 'false'
```

<span data-ttu-id="c34e5-128">Save and close the file.</span><span class="sxs-lookup"><span data-stu-id="c34e5-128">Save and close the file.</span></span>

## <a name="update-container-image"></a><span data-ttu-id="c34e5-129">Update container image</span><span class="sxs-lookup"><span data-stu-id="c34e5-129">Update container image</span></span>

<span data-ttu-id="c34e5-130">Use [docker-compose](https://docs.docker.com/compose/) to re-create the front-end image and run the updated application.</span><span class="sxs-lookup"><span data-stu-id="c34e5-130">Use [docker-compose](https://docs.docker.com/compose/) to re-create the front-end image and run the updated application.</span></span> <span data-ttu-id="c34e5-131">The `--build` argument is used to instruct Docker Compose to re-create the application image.</span><span class="sxs-lookup"><span data-stu-id="c34e5-131">The `--build` argument is used to instruct Docker Compose to re-create the application image.</span></span>

```bash
docker-compose up --build -d
```

## <a name="test-application-locally"></a><span data-ttu-id="c34e5-132">Test application locally</span><span class="sxs-lookup"><span data-stu-id="c34e5-132">Test application locally</span></span>

<span data-ttu-id="c34e5-133">Browse to http://localhost:8080 to see the updated application.</span><span class="sxs-lookup"><span data-stu-id="c34e5-133">Browse to http://localhost:8080 to see the updated application.</span></span>

![Image of Kubernetes cluster on Azure](media/container-service-kubernetes-tutorials/vote-app-updated.png)

## <a name="tag-and-push-images"></a><span data-ttu-id="c34e5-135">Tag and push images</span><span class="sxs-lookup"><span data-stu-id="c34e5-135">Tag and push images</span></span>

<span data-ttu-id="c34e5-136">Tag the `azure-vote-front` image with the loginServer of the container registry.</span><span class="sxs-lookup"><span data-stu-id="c34e5-136">Tag the `azure-vote-front` image with the loginServer of the container registry.</span></span> 

<span data-ttu-id="c34e5-137">Get the login server name with the [az acr list](/cli/azure/acr#az-acr-list) command.</span><span class="sxs-lookup"><span data-stu-id="c34e5-137">Get the login server name with the [az acr list](/cli/azure/acr#az-acr-list) command.</span></span>

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="c34e5-138">Use [docker tag](https://docs.docker.com/engine/reference/commandline/tag/) to tag the image.</span><span class="sxs-lookup"><span data-stu-id="c34e5-138">Use [docker tag](https://docs.docker.com/engine/reference/commandline/tag/) to tag the image.</span></span> <span data-ttu-id="c34e5-139">Replace `<acrLoginServer>` with your Azure Container Registry login server name or public registry hostname.</span><span class="sxs-lookup"><span data-stu-id="c34e5-139">Replace `<acrLoginServer>` with your Azure Container Registry login server name or public registry hostname.</span></span> <span data-ttu-id="c34e5-140">Also notice that the image version is updated to `redis-v2`.</span><span class="sxs-lookup"><span data-stu-id="c34e5-140">Also notice that the image version is updated to `redis-v2`.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="c34e5-141">Use [docker push](https://docs.docker.com/engine/reference/commandline/push/) to upload the image to your registry.</span><span class="sxs-lookup"><span data-stu-id="c34e5-141">Use [docker push](https://docs.docker.com/engine/reference/commandline/push/) to upload the image to your registry.</span></span> <span data-ttu-id="c34e5-142">Replace `<acrLoginServer>` with your Azure Container Registry login server name.</span><span class="sxs-lookup"><span data-stu-id="c34e5-142">Replace `<acrLoginServer>` with your Azure Container Registry login server name.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v2
```

## <a name="deploy-update-application"></a><span data-ttu-id="c34e5-143">Deploy update application</span><span class="sxs-lookup"><span data-stu-id="c34e5-143">Deploy update application</span></span>

<span data-ttu-id="c34e5-144">To ensure maximum uptime, multiple instances of the application pod must be running.</span><span class="sxs-lookup"><span data-stu-id="c34e5-144">To ensure maximum uptime, multiple instances of the application pod must be running.</span></span> <span data-ttu-id="c34e5-145">Verify this configuration with the [kubectl get pod](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command.</span><span class="sxs-lookup"><span data-stu-id="c34e5-145">Verify this configuration with the [kubectl get pod](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command.</span></span>

```bash
kubectl get pod
```

<span data-ttu-id="c34e5-146">Output:</span><span class="sxs-lookup"><span data-stu-id="c34e5-146">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-217588096-5w632    1/1       Running   0          10m
azure-vote-front-233282510-b5pkz   1/1       Running   0          10m
azure-vote-front-233282510-dhrtr   1/1       Running   0          10m
azure-vote-front-233282510-pqbfk   1/1       Running   0          10m
```

<span data-ttu-id="c34e5-147">If you do not have multiple pods running the azure-vote-front image, scale the `azure-vote-front` deployment.</span><span class="sxs-lookup"><span data-stu-id="c34e5-147">If you do not have multiple pods running the azure-vote-front image, scale the `azure-vote-front` deployment.</span></span>


```azurecli-interactive
kubectl scale --replicas=3 deployment/azure-vote-front
```

<span data-ttu-id="c34e5-148">To update the application, use the [kubectl set](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#set) command.</span><span class="sxs-lookup"><span data-stu-id="c34e5-148">To update the application, use the [kubectl set](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#set) command.</span></span> <span data-ttu-id="c34e5-149">Update `<acrLoginServer>` with the login server or host name of your container registry.</span><span class="sxs-lookup"><span data-stu-id="c34e5-149">Update `<acrLoginServer>` with the login server or host name of your container registry.</span></span>

```azurecli-interactive
kubectl set image deployment azure-vote-front azure-vote-front=<acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="c34e5-150">To monitor the deployment, use the [kubectl get pod](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command.</span><span class="sxs-lookup"><span data-stu-id="c34e5-150">To monitor the deployment, use the [kubectl get pod](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command.</span></span> <span data-ttu-id="c34e5-151">As the updated application is deployed, your pods are terminated and re-created with the new container image.</span><span class="sxs-lookup"><span data-stu-id="c34e5-151">As the updated application is deployed, your pods are terminated and re-created with the new container image.</span></span>

```azurecli-interactive
kubectl get pod
```

<span data-ttu-id="c34e5-152">Output:</span><span class="sxs-lookup"><span data-stu-id="c34e5-152">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2978095810-gq9g0   1/1       Running   0          5m
azure-vote-front-1297194256-tpjlg   1/1       Running   0         1m
azure-vote-front-1297194256-tptnx   1/1       Running   0         5m
azure-vote-front-1297194256-zktw9   1/1       Terminating   0         1m
```

## <a name="test-updated-application"></a><span data-ttu-id="c34e5-153">Test updated application</span><span class="sxs-lookup"><span data-stu-id="c34e5-153">Test updated application</span></span>

<span data-ttu-id="c34e5-154">Get the external IP address of the `azure-vote-front` service.</span><span class="sxs-lookup"><span data-stu-id="c34e5-154">Get the external IP address of the `azure-vote-front` service.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front
```

<span data-ttu-id="c34e5-155">Browse to the IP address to see the updated application.</span><span class="sxs-lookup"><span data-stu-id="c34e5-155">Browse to the IP address to see the updated application.</span></span>

![Image of Kubernetes cluster on Azure](media/container-service-kubernetes-tutorials/vote-app-updated-external.png)

## <a name="next-steps"></a><span data-ttu-id="c34e5-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="c34e5-157">Next steps</span></span>

<span data-ttu-id="c34e5-158">In this tutorial, you updated an application and rolled out this update to a Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="c34e5-158">In this tutorial, you updated an application and rolled out this update to a Kubernetes cluster.</span></span> <span data-ttu-id="c34e5-159">The following tasks were completed:</span><span class="sxs-lookup"><span data-stu-id="c34e5-159">The following tasks were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c34e5-160">Updated the front-end application code</span><span class="sxs-lookup"><span data-stu-id="c34e5-160">Updated the front-end application code</span></span>
> * <span data-ttu-id="c34e5-161">Created an updated container image</span><span class="sxs-lookup"><span data-stu-id="c34e5-161">Created an updated container image</span></span>
> * <span data-ttu-id="c34e5-162">Pushed the container image to Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="c34e5-162">Pushed the container image to Azure Container Registry</span></span>
> * <span data-ttu-id="c34e5-163">Deployed the updated application</span><span class="sxs-lookup"><span data-stu-id="c34e5-163">Deployed the updated application</span></span>

<span data-ttu-id="c34e5-164">Advance to the next tutorial to learn about how to monitor Kubernetes with Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="c34e5-164">Advance to the next tutorial to learn about how to monitor Kubernetes with Log Analytics.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c34e5-165">Monitor Kubernetes with Log Analytics</span><span class="sxs-lookup"><span data-stu-id="c34e5-165">Monitor Kubernetes with Log Analytics</span></span>](./container-service-tutorial-kubernetes-monitor.md)