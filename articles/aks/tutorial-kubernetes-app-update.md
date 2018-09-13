---
title: Kubernetes on Azure tutorial - Update an application
description: In this Azure Kubernetes Service (AKS) tutorial, you learn how to update an existing application deployment to AKS with a new version of the application code.
services: container-service
author: iainfoulds
manager: jeconnoc
ms.service: container-service
ms.topic: tutorial
ms.date: 08/14/2018
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: b2dd52fec112b879e072d3ac5598dd7978e68cbc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865201"
---
# <a name="tutorial-update-an-application-in-azure-kubernetes-service-aks"></a><span data-ttu-id="602fe-103">Tutorial: Update an application in Azure Kubernetes Service (AKS)</span><span class="sxs-lookup"><span data-stu-id="602fe-103">Tutorial: Update an application in Azure Kubernetes Service (AKS)</span></span>

<span data-ttu-id="602fe-104">After an application has been deployed in Kubernetes, it can be updated by specifying a new container image or image version.</span><span class="sxs-lookup"><span data-stu-id="602fe-104">After an application has been deployed in Kubernetes, it can be updated by specifying a new container image or image version.</span></span> <span data-ttu-id="602fe-105">When doing so, the update is staged so that only a portion of the deployment is concurrently updated.</span><span class="sxs-lookup"><span data-stu-id="602fe-105">When doing so, the update is staged so that only a portion of the deployment is concurrently updated.</span></span> <span data-ttu-id="602fe-106">This staged update enables the application to keep running during the update.</span><span class="sxs-lookup"><span data-stu-id="602fe-106">This staged update enables the application to keep running during the update.</span></span> <span data-ttu-id="602fe-107">It also provides a rollback mechanism if a deployment failure occurs.</span><span class="sxs-lookup"><span data-stu-id="602fe-107">It also provides a rollback mechanism if a deployment failure occurs.</span></span>

<span data-ttu-id="602fe-108">In this tutorial, part six of seven, the sample Azure Vote app is updated.</span><span class="sxs-lookup"><span data-stu-id="602fe-108">In this tutorial, part six of seven, the sample Azure Vote app is updated.</span></span> <span data-ttu-id="602fe-109">You learn how to:</span><span class="sxs-lookup"><span data-stu-id="602fe-109">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="602fe-110">Update the front-end application code</span><span class="sxs-lookup"><span data-stu-id="602fe-110">Update the front-end application code</span></span>
> * <span data-ttu-id="602fe-111">Create an updated container image</span><span class="sxs-lookup"><span data-stu-id="602fe-111">Create an updated container image</span></span>
> * <span data-ttu-id="602fe-112">Push the container image to Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="602fe-112">Push the container image to Azure Container Registry</span></span>
> * <span data-ttu-id="602fe-113">Deploy the updated container image</span><span class="sxs-lookup"><span data-stu-id="602fe-113">Deploy the updated container image</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="602fe-114">Before you begin</span><span class="sxs-lookup"><span data-stu-id="602fe-114">Before you begin</span></span>

<span data-ttu-id="602fe-115">In previous tutorials, an application was packaged into a container image, the image uploaded to Azure Container Registry (ACR), and a Kubernetes cluster created.</span><span class="sxs-lookup"><span data-stu-id="602fe-115">In previous tutorials, an application was packaged into a container image, the image uploaded to Azure Container Registry (ACR), and a Kubernetes cluster created.</span></span> <span data-ttu-id="602fe-116">The application was then run on the Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="602fe-116">The application was then run on the Kubernetes cluster.</span></span>

<span data-ttu-id="602fe-117">An application repository was also cloned that includes the application source code, and a pre-created Docker Compose file used in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="602fe-117">An application repository was also cloned that includes the application source code, and a pre-created Docker Compose file used in this tutorial.</span></span> <span data-ttu-id="602fe-118">Verify that you have created a clone of the repo, and that you have changed directories into the cloned directory.</span><span class="sxs-lookup"><span data-stu-id="602fe-118">Verify that you have created a clone of the repo, and that you have changed directories into the cloned directory.</span></span> <span data-ttu-id="602fe-119">If you haven't completed these steps, and want to follow along, return to [Tutorial 1 – Create container images][aks-tutorial-prepare-app].</span><span class="sxs-lookup"><span data-stu-id="602fe-119">If you haven't completed these steps, and want to follow along, return to [Tutorial 1 – Create container images][aks-tutorial-prepare-app].</span></span>

<span data-ttu-id="602fe-120">This tutorial requires that you are running the Azure CLI version 2.0.44 or later.</span><span class="sxs-lookup"><span data-stu-id="602fe-120">This tutorial requires that you are running the Azure CLI version 2.0.44 or later.</span></span> <span data-ttu-id="602fe-121">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="602fe-121">Run `az --version` to find the version.</span></span> <span data-ttu-id="602fe-122">If you need to install or upgrade, see [Install Azure CLI][azure-cli-install].</span><span class="sxs-lookup"><span data-stu-id="602fe-122">If you need to install or upgrade, see [Install Azure CLI][azure-cli-install].</span></span>

## <a name="update-an-application"></a><span data-ttu-id="602fe-123">Update an application</span><span class="sxs-lookup"><span data-stu-id="602fe-123">Update an application</span></span>

<span data-ttu-id="602fe-124">Let's make a change to the sample application, then update the version already deployed to your AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="602fe-124">Let's make a change to the sample application, then update the version already deployed to your AKS cluster.</span></span> <span data-ttu-id="602fe-125">The sample application source code can be found inside of the *azure-vote* directory.</span><span class="sxs-lookup"><span data-stu-id="602fe-125">The sample application source code can be found inside of the *azure-vote* directory.</span></span> <span data-ttu-id="602fe-126">Open the *config_file.cfg* file with an editor, such as `vi`:</span><span class="sxs-lookup"><span data-stu-id="602fe-126">Open the *config_file.cfg* file with an editor, such as `vi`:</span></span>

```console
vi azure-vote/azure-vote/config_file.cfg
```

<span data-ttu-id="602fe-127">Change the values for *VOTE1VALUE* and *VOTE2VALUE* to different colors.</span><span class="sxs-lookup"><span data-stu-id="602fe-127">Change the values for *VOTE1VALUE* and *VOTE2VALUE* to different colors.</span></span> <span data-ttu-id="602fe-128">The following example shows the updated color values:</span><span class="sxs-lookup"><span data-stu-id="602fe-128">The following example shows the updated color values:</span></span>

```
# UI Configurations
TITLE = 'Azure Voting App'
VOTE1VALUE = 'Blue'
VOTE2VALUE = 'Purple'
SHOWHOST = 'false'
```

<span data-ttu-id="602fe-129">Save and close the file.</span><span class="sxs-lookup"><span data-stu-id="602fe-129">Save and close the file.</span></span>

## <a name="update-the-container-image"></a><span data-ttu-id="602fe-130">Update the container image</span><span class="sxs-lookup"><span data-stu-id="602fe-130">Update the container image</span></span>

<span data-ttu-id="602fe-131">To re-create the front-end image and test the updated application, use [docker-compose][docker-compose].</span><span class="sxs-lookup"><span data-stu-id="602fe-131">To re-create the front-end image and test the updated application, use [docker-compose][docker-compose].</span></span> <span data-ttu-id="602fe-132">The `--build` argument is used to instruct Docker Compose to re-create the application image:</span><span class="sxs-lookup"><span data-stu-id="602fe-132">The `--build` argument is used to instruct Docker Compose to re-create the application image:</span></span>

```console
docker-compose up --build -d
```

## <a name="test-the-application-locally"></a><span data-ttu-id="602fe-133">Test the application locally</span><span class="sxs-lookup"><span data-stu-id="602fe-133">Test the application locally</span></span>

<span data-ttu-id="602fe-134">To verify that the updated container image shows your changes, open a local web browser to http://localhost:8080.</span><span class="sxs-lookup"><span data-stu-id="602fe-134">To verify that the updated container image shows your changes, open a local web browser to http://localhost:8080.</span></span>

![Image of Kubernetes cluster on Azure](media/container-service-kubernetes-tutorials/vote-app-updated.png)

<span data-ttu-id="602fe-136">The updated color values provided in the *config_file.cfg* file are displayed on your running application.</span><span class="sxs-lookup"><span data-stu-id="602fe-136">The updated color values provided in the *config_file.cfg* file are displayed on your running application.</span></span>

## <a name="tag-and-push-the-image"></a><span data-ttu-id="602fe-137">Tag and push the image</span><span class="sxs-lookup"><span data-stu-id="602fe-137">Tag and push the image</span></span>

<span data-ttu-id="602fe-138">To correctly use the updated image, tag the *azure-vote-front* image with the login server name of your ACR registry.</span><span class="sxs-lookup"><span data-stu-id="602fe-138">To correctly use the updated image, tag the *azure-vote-front* image with the login server name of your ACR registry.</span></span> <span data-ttu-id="602fe-139">Get the login server name with the [az acr list](/cli/azure/acr#az_acr_list) command:</span><span class="sxs-lookup"><span data-stu-id="602fe-139">Get the login server name with the [az acr list](/cli/azure/acr#az_acr_list) command:</span></span>

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="602fe-140">Use [docker tag][docker-tag] to tag the image.</span><span class="sxs-lookup"><span data-stu-id="602fe-140">Use [docker tag][docker-tag] to tag the image.</span></span> <span data-ttu-id="602fe-141">Replace `<acrLoginServer>` with your ACR login server name or public registry hostname, and update the image version to *:v2* as follows:</span><span class="sxs-lookup"><span data-stu-id="602fe-141">Replace `<acrLoginServer>` with your ACR login server name or public registry hostname, and update the image version to *:v2* as follows:</span></span>

```console
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:v2
```

<span data-ttu-id="602fe-142">Now use [docker push][docker-push] to upload the image to your registry.</span><span class="sxs-lookup"><span data-stu-id="602fe-142">Now use [docker push][docker-push] to upload the image to your registry.</span></span> <span data-ttu-id="602fe-143">Replace `<acrLoginServer>` with your ACR login server name.</span><span class="sxs-lookup"><span data-stu-id="602fe-143">Replace `<acrLoginServer>` with your ACR login server name.</span></span> <span data-ttu-id="602fe-144">If you experience issues pushing to your ACR registry, ensure that you have run the [az acr login][az-acr-login] command.</span><span class="sxs-lookup"><span data-stu-id="602fe-144">If you experience issues pushing to your ACR registry, ensure that you have run the [az acr login][az-acr-login] command.</span></span>

```console
docker push <acrLoginServer>/azure-vote-front:v2
```

## <a name="deploy-the-updated-application"></a><span data-ttu-id="602fe-145">Deploy the updated application</span><span class="sxs-lookup"><span data-stu-id="602fe-145">Deploy the updated application</span></span>

<span data-ttu-id="602fe-146">To ensure maximum uptime, multiple instances of the application pod must be running.</span><span class="sxs-lookup"><span data-stu-id="602fe-146">To ensure maximum uptime, multiple instances of the application pod must be running.</span></span> <span data-ttu-id="602fe-147">Verify the number of running front-end instances with the [kubectl get pods][kubectl-get] command:</span><span class="sxs-lookup"><span data-stu-id="602fe-147">Verify the number of running front-end instances with the [kubectl get pods][kubectl-get] command:</span></span>

```
$ kubectl get pods

NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-217588096-5w632    1/1       Running   0          10m
azure-vote-front-233282510-b5pkz   1/1       Running   0          10m
azure-vote-front-233282510-dhrtr   1/1       Running   0          10m
azure-vote-front-233282510-pqbfk   1/1       Running   0          10m
```

<span data-ttu-id="602fe-148">If you do not have multiple front-end pods, scale the *azure-vote-front* deployment as follows:</span><span class="sxs-lookup"><span data-stu-id="602fe-148">If you do not have multiple front-end pods, scale the *azure-vote-front* deployment as follows:</span></span>

```console
kubectl scale --replicas=3 deployment/azure-vote-front
```

<span data-ttu-id="602fe-149">To update the application, use the [kubectl set][kubectl-set] command.</span><span class="sxs-lookup"><span data-stu-id="602fe-149">To update the application, use the [kubectl set][kubectl-set] command.</span></span> <span data-ttu-id="602fe-150">Update `<acrLoginServer>` with the login server or host name of your container registry, and specify the *v2* application version:</span><span class="sxs-lookup"><span data-stu-id="602fe-150">Update `<acrLoginServer>` with the login server or host name of your container registry, and specify the *v2* application version:</span></span>

```console
kubectl set image deployment azure-vote-front azure-vote-front=<acrLoginServer>/azure-vote-front:v2
```

<span data-ttu-id="602fe-151">To monitor the deployment, use the [kubectl get pod][kubectl-get] command.</span><span class="sxs-lookup"><span data-stu-id="602fe-151">To monitor the deployment, use the [kubectl get pod][kubectl-get] command.</span></span> <span data-ttu-id="602fe-152">As the updated application is deployed, your pods are terminated and re-created with the new container image.</span><span class="sxs-lookup"><span data-stu-id="602fe-152">As the updated application is deployed, your pods are terminated and re-created with the new container image.</span></span>

```console
kubectl get pods
```

<span data-ttu-id="602fe-153">The following example output shows pods terminating and new instances running as the deployment progresses:</span><span class="sxs-lookup"><span data-stu-id="602fe-153">The following example output shows pods terminating and new instances running as the deployment progresses:</span></span>

```
$ kubectl get pods

NAME                               READY     STATUS        RESTARTS   AGE
azure-vote-back-2978095810-gq9g0   1/1       Running       0          5m
azure-vote-front-1297194256-tpjlg  1/1       Running       0          1m
azure-vote-front-1297194256-tptnx  1/1       Running       0          5m
azure-vote-front-1297194256-zktw9  1/1       Terminating   0          1m
```

## <a name="test-the-updated-application"></a><span data-ttu-id="602fe-154">Test the updated application</span><span class="sxs-lookup"><span data-stu-id="602fe-154">Test the updated application</span></span>

<span data-ttu-id="602fe-155">To view the update application, first get the external IP address of the `azure-vote-front` service:</span><span class="sxs-lookup"><span data-stu-id="602fe-155">To view the update application, first get the external IP address of the `azure-vote-front` service:</span></span>

```console
kubectl get service azure-vote-front
```

<span data-ttu-id="602fe-156">Now open a local web browser to the IP address.</span><span class="sxs-lookup"><span data-stu-id="602fe-156">Now open a local web browser to the IP address.</span></span>

![Image of Kubernetes cluster on Azure](media/container-service-kubernetes-tutorials/vote-app-updated-external.png)

## <a name="next-steps"></a><span data-ttu-id="602fe-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="602fe-158">Next steps</span></span>

<span data-ttu-id="602fe-159">In this tutorial, you updated an application and rolled out this update to a Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="602fe-159">In this tutorial, you updated an application and rolled out this update to a Kubernetes cluster.</span></span> <span data-ttu-id="602fe-160">You learned how to:</span><span class="sxs-lookup"><span data-stu-id="602fe-160">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="602fe-161">Update the front-end application code</span><span class="sxs-lookup"><span data-stu-id="602fe-161">Update the front-end application code</span></span>
> * <span data-ttu-id="602fe-162">Create an updated container image</span><span class="sxs-lookup"><span data-stu-id="602fe-162">Create an updated container image</span></span>
> * <span data-ttu-id="602fe-163">Push the container image to Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="602fe-163">Push the container image to Azure Container Registry</span></span>
> * <span data-ttu-id="602fe-164">Deploy the updated container image</span><span class="sxs-lookup"><span data-stu-id="602fe-164">Deploy the updated container image</span></span>

<span data-ttu-id="602fe-165">Advance to the next tutorial to learn how to upgrade an AKS cluster to a new version of Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="602fe-165">Advance to the next tutorial to learn how to upgrade an AKS cluster to a new version of Kubernetes.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="602fe-166">[Upgrade Kubernetes][aks-tutorial-upgrade]</span><span class="sxs-lookup"><span data-stu-id="602fe-166">[Upgrade Kubernetes][aks-tutorial-upgrade]</span></span>

<!-- LINKS - external -->
[docker-compose]: https://docs.docker.com/compose/
[docker-push]: https://docs.docker.com/engine/reference/commandline/push/
[docker-tag]: https://docs.docker.com/engine/reference/commandline/tag/
[kubectl-get]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get
[kubectl-set]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#set

<!-- LINKS - internal -->
[aks-tutorial-prepare-app]: ./tutorial-kubernetes-prepare-app.md
[aks-tutorial-upgrade]: ./tutorial-kubernetes-upgrade-cluster.md
[az-acr-login]: /cli/azure/acr#az_acr_login
[azure-cli-install]: /cli/azure/install-azure-cli
