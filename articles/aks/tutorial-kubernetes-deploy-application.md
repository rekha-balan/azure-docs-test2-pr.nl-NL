---
title: Kubernetes on Azure tutorial  - Deploy an application
description: In this Azure Kubernetes Service (AKS) tutorial, you deploy a multi-container application to your cluster using a custom image stored in Azure Container Registry.
services: container-service
author: iainfoulds
manager: jeconnoc
ms.service: container-service
ms.topic: tutorial
ms.date: 08/14/2018
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: bf817f553250ead449ec0d5db3d33acc2eff23f3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865943"
---
# <a name="tutorial-run-applications-in-azure-kubernetes-service-aks"></a><span data-ttu-id="95524-103">Tutorial: Run applications in Azure Kubernetes Service (AKS)</span><span class="sxs-lookup"><span data-stu-id="95524-103">Tutorial: Run applications in Azure Kubernetes Service (AKS)</span></span>

<span data-ttu-id="95524-104">Kubernetes provides a distributed platform for containerized applications.</span><span class="sxs-lookup"><span data-stu-id="95524-104">Kubernetes provides a distributed platform for containerized applications.</span></span> <span data-ttu-id="95524-105">You build and deploy your own applications and services into a Kubernetes cluster, and let the cluster manage the availability and connectivity.</span><span class="sxs-lookup"><span data-stu-id="95524-105">You build and deploy your own applications and services into a Kubernetes cluster, and let the cluster manage the availability and connectivity.</span></span> <span data-ttu-id="95524-106">In this tutorial, part four of seven, a sample application is deployed into a Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="95524-106">In this tutorial, part four of seven, a sample application is deployed into a Kubernetes cluster.</span></span> <span data-ttu-id="95524-107">You learn how to:</span><span class="sxs-lookup"><span data-stu-id="95524-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="95524-108">Update a Kubernetes manifest files</span><span class="sxs-lookup"><span data-stu-id="95524-108">Update a Kubernetes manifest files</span></span>
> * <span data-ttu-id="95524-109">Run an application in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="95524-109">Run an application in Kubernetes</span></span>
> * <span data-ttu-id="95524-110">Test the application</span><span class="sxs-lookup"><span data-stu-id="95524-110">Test the application</span></span>

<span data-ttu-id="95524-111">In subsequent tutorials, this application is scaled out and updated.</span><span class="sxs-lookup"><span data-stu-id="95524-111">In subsequent tutorials, this application is scaled out and updated.</span></span>

<span data-ttu-id="95524-112">This tutorial assumes a basic understanding of Kubernetes concepts, for detailed information on Kubernetes see the [Kubernetes documentation][kubernetes-documentation].</span><span class="sxs-lookup"><span data-stu-id="95524-112">This tutorial assumes a basic understanding of Kubernetes concepts, for detailed information on Kubernetes see the [Kubernetes documentation][kubernetes-documentation].</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="95524-113">Before you begin</span><span class="sxs-lookup"><span data-stu-id="95524-113">Before you begin</span></span>

<span data-ttu-id="95524-114">In previous tutorials, an application was packaged into a container image, this image was uploaded to Azure Container Registry, and a Kubernetes cluster was created.</span><span class="sxs-lookup"><span data-stu-id="95524-114">In previous tutorials, an application was packaged into a container image, this image was uploaded to Azure Container Registry, and a Kubernetes cluster was created.</span></span>

<span data-ttu-id="95524-115">To complete this tutorial, you need the pre-created `azure-vote-all-in-one-redis.yaml` Kubernetes manifest file.</span><span class="sxs-lookup"><span data-stu-id="95524-115">To complete this tutorial, you need the pre-created `azure-vote-all-in-one-redis.yaml` Kubernetes manifest file.</span></span> <span data-ttu-id="95524-116">This file was downloaded with the application source code in a previous tutorial.</span><span class="sxs-lookup"><span data-stu-id="95524-116">This file was downloaded with the application source code in a previous tutorial.</span></span> <span data-ttu-id="95524-117">Verify that you have cloned the repo, and that you have changed directories into the cloned repo.</span><span class="sxs-lookup"><span data-stu-id="95524-117">Verify that you have cloned the repo, and that you have changed directories into the cloned repo.</span></span> <span data-ttu-id="95524-118">If you have not done these steps, and would like to follow along, return to [Tutorial 1 – Create container images][aks-tutorial-prepare-app].</span><span class="sxs-lookup"><span data-stu-id="95524-118">If you have not done these steps, and would like to follow along, return to [Tutorial 1 – Create container images][aks-tutorial-prepare-app].</span></span>

<span data-ttu-id="95524-119">This tutorial requires that you are running the Azure CLI version 2.0.44 or later.</span><span class="sxs-lookup"><span data-stu-id="95524-119">This tutorial requires that you are running the Azure CLI version 2.0.44 or later.</span></span> <span data-ttu-id="95524-120">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="95524-120">Run `az --version` to find the version.</span></span> <span data-ttu-id="95524-121">If you need to install or upgrade, see [Install Azure CLI][azure-cli-install].</span><span class="sxs-lookup"><span data-stu-id="95524-121">If you need to install or upgrade, see [Install Azure CLI][azure-cli-install].</span></span>

## <a name="update-the-manifest-file"></a><span data-ttu-id="95524-122">Update the manifest file</span><span class="sxs-lookup"><span data-stu-id="95524-122">Update the manifest file</span></span>

<span data-ttu-id="95524-123">In these tutorials, an Azure Container Registry (ACR) instance stores the container image for the sample application.</span><span class="sxs-lookup"><span data-stu-id="95524-123">In these tutorials, an Azure Container Registry (ACR) instance stores the container image for the sample application.</span></span> <span data-ttu-id="95524-124">To deploy the application, you must update the image name in the Kubernetes manifest file to include the ACR login server name.</span><span class="sxs-lookup"><span data-stu-id="95524-124">To deploy the application, you must update the image name in the Kubernetes manifest file to include the ACR login server name.</span></span>

<span data-ttu-id="95524-125">Get the ACR login server name using the [az acr list][az-acr-list] command as follows:</span><span class="sxs-lookup"><span data-stu-id="95524-125">Get the ACR login server name using the [az acr list][az-acr-list] command as follows:</span></span>

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="95524-126">The sample manifest file from the git repo cloned in the first tutorial uses the login server name of *microsoft*.</span><span class="sxs-lookup"><span data-stu-id="95524-126">The sample manifest file from the git repo cloned in the first tutorial uses the login server name of *microsoft*.</span></span> <span data-ttu-id="95524-127">Open this manifest file with a text editor, such as `vi`:</span><span class="sxs-lookup"><span data-stu-id="95524-127">Open this manifest file with a text editor, such as `vi`:</span></span>

```console
vi azure-vote-all-in-one-redis.yaml
```

<span data-ttu-id="95524-128">Replace *microsoft* with your ACR login server name.</span><span class="sxs-lookup"><span data-stu-id="95524-128">Replace *microsoft* with your ACR login server name.</span></span> <span data-ttu-id="95524-129">The image name is found on line 47 of the manifest file.</span><span class="sxs-lookup"><span data-stu-id="95524-129">The image name is found on line 47 of the manifest file.</span></span> <span data-ttu-id="95524-130">The following example shows the default image name:</span><span class="sxs-lookup"><span data-stu-id="95524-130">The following example shows the default image name:</span></span>

```yaml
containers:
- name: azure-vote-front
  image: microsoft/azure-vote-front:v1
```

<span data-ttu-id="95524-131">Provide your own ACR login server name so that your manifest file looks like the following example:</span><span class="sxs-lookup"><span data-stu-id="95524-131">Provide your own ACR login server name so that your manifest file looks like the following example:</span></span>

```yaml
containers:
- name: azure-vote-front
  image: <acrName>.azurecr.io/azure-vote-front:v1
```

<span data-ttu-id="95524-132">Save and close the file.</span><span class="sxs-lookup"><span data-stu-id="95524-132">Save and close the file.</span></span>

## <a name="deploy-the-application"></a><span data-ttu-id="95524-133">Deploy the application</span><span class="sxs-lookup"><span data-stu-id="95524-133">Deploy the application</span></span>

<span data-ttu-id="95524-134">To deploy your application, use the [kubectl apply][kubectl-apply] command.</span><span class="sxs-lookup"><span data-stu-id="95524-134">To deploy your application, use the [kubectl apply][kubectl-apply] command.</span></span> <span data-ttu-id="95524-135">This command parses the manifest file and creates the defined Kubernetes objects.</span><span class="sxs-lookup"><span data-stu-id="95524-135">This command parses the manifest file and creates the defined Kubernetes objects.</span></span> <span data-ttu-id="95524-136">Specify the sample manifest file, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="95524-136">Specify the sample manifest file, as shown in the following example:</span></span>

```console
kubectl apply -f azure-vote-all-in-one-redis.yaml
```

<span data-ttu-id="95524-137">The Kubernetes objects are created within the cluster, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="95524-137">The Kubernetes objects are created within the cluster, as shown in the following example:</span></span>

```
$ kubectl apply -f azure-vote-all-in-one-redis.yaml

deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-the-application"></a><span data-ttu-id="95524-138">Test the application</span><span class="sxs-lookup"><span data-stu-id="95524-138">Test the application</span></span>

<span data-ttu-id="95524-139">A [Kubernetes service][kubernetes-service] is created which exposes the application to the internet.</span><span class="sxs-lookup"><span data-stu-id="95524-139">A [Kubernetes service][kubernetes-service] is created which exposes the application to the internet.</span></span> <span data-ttu-id="95524-140">This process can take a few minutes.</span><span class="sxs-lookup"><span data-stu-id="95524-140">This process can take a few minutes.</span></span> <span data-ttu-id="95524-141">To monitor progress, use the [kubectl get service][kubectl-get] command with the `--watch` argument:</span><span class="sxs-lookup"><span data-stu-id="95524-141">To monitor progress, use the [kubectl get service][kubectl-get] command with the `--watch` argument:</span></span>

```console
kubectl get service azure-vote-front --watch
```

<span data-ttu-id="95524-142">The *EXTERNAL-IP* for the *azure-vote-front* service initially appears as *pending*, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="95524-142">The *EXTERNAL-IP* for the *azure-vote-front* service initially appears as *pending*, as shown in the following example:</span></span>

```
azure-vote-front   10.0.34.242   <pending>     80:30676/TCP   7s
```

<span data-ttu-id="95524-143">When the *EXTERNAL-IP* address changes from *pending* to an actual public IP address, use `CTRL-C` to stop the kubectl watch process.</span><span class="sxs-lookup"><span data-stu-id="95524-143">When the *EXTERNAL-IP* address changes from *pending* to an actual public IP address, use `CTRL-C` to stop the kubectl watch process.</span></span> <span data-ttu-id="95524-144">The following example shows a public IP address is now assigned:</span><span class="sxs-lookup"><span data-stu-id="95524-144">The following example shows a public IP address is now assigned:</span></span>

```
azure-vote-front   10.0.34.242   52.179.23.131   80:30676/TCP   2m
```

<span data-ttu-id="95524-145">To see the application in action, open a web browser to the external IP address.</span><span class="sxs-lookup"><span data-stu-id="95524-145">To see the application in action, open a web browser to the external IP address.</span></span>

![Image of Kubernetes cluster on Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

<span data-ttu-id="95524-147">If the application did not load, it might be due to an authorization problem with your image registry.</span><span class="sxs-lookup"><span data-stu-id="95524-147">If the application did not load, it might be due to an authorization problem with your image registry.</span></span> <span data-ttu-id="95524-148">To view the status of your containers, use the `kubectl get pods` command.</span><span class="sxs-lookup"><span data-stu-id="95524-148">To view the status of your containers, use the `kubectl get pods` command.</span></span> <span data-ttu-id="95524-149">If the container images cannot be pulled, see [allow access to Container Registry with a Kubernetes secret](https://docs.microsoft.com/azure/container-registry/container-registry-auth-aks#access-with-kubernetes-secret).</span><span class="sxs-lookup"><span data-stu-id="95524-149">If the container images cannot be pulled, see [allow access to Container Registry with a Kubernetes secret](https://docs.microsoft.com/azure/container-registry/container-registry-auth-aks#access-with-kubernetes-secret).</span></span>

## <a name="next-steps"></a><span data-ttu-id="95524-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="95524-150">Next steps</span></span>

<span data-ttu-id="95524-151">In this tutorial, the Azure vote application was deployed to a Kubernetes cluster in AKS.</span><span class="sxs-lookup"><span data-stu-id="95524-151">In this tutorial, the Azure vote application was deployed to a Kubernetes cluster in AKS.</span></span> <span data-ttu-id="95524-152">You learned how to:</span><span class="sxs-lookup"><span data-stu-id="95524-152">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="95524-153">Update a Kubernetes manifest files</span><span class="sxs-lookup"><span data-stu-id="95524-153">Update a Kubernetes manifest files</span></span>
> * <span data-ttu-id="95524-154">Run an application in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="95524-154">Run an application in Kubernetes</span></span>
> * <span data-ttu-id="95524-155">Test the application</span><span class="sxs-lookup"><span data-stu-id="95524-155">Test the application</span></span>

<span data-ttu-id="95524-156">Advance to the next tutorial to learn how to scale a Kubernetes application and the underlying Kubernetes infrastructure.</span><span class="sxs-lookup"><span data-stu-id="95524-156">Advance to the next tutorial to learn how to scale a Kubernetes application and the underlying Kubernetes infrastructure.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="95524-157">[Scale Kubernetes application and infrastructure][aks-tutorial-scale]</span><span class="sxs-lookup"><span data-stu-id="95524-157">[Scale Kubernetes application and infrastructure][aks-tutorial-scale]</span></span>

<!-- LINKS - external -->
[kubectl-apply]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply
[kubectl-create]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#create
[kubectl-get]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get
[kubernetes-documentation]: https://kubernetes.io/docs/home/
[kubernetes-service]: https://kubernetes.io/docs/concepts/services-networking/service/

<!-- LINKS - internal -->
[aks-tutorial-prepare-app]: ./tutorial-kubernetes-prepare-app.md
[aks-tutorial-scale]: ./tutorial-kubernetes-scale.md
[az-acr-list]: /cli/azure/acr#list
[azure-cli-install]: /cli/azure/install-azure-cli
