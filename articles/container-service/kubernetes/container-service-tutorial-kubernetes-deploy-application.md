---
title: Azure Container Service tutorial - Deploy Application
description: Azure Container Service tutorial - Deploy Application
services: container-service
author: neilpeterson
manager: jeconnoc
ms.service: container-service
ms.topic: tutorial
ms.date: 02/26/2018
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: e7f9c0c3ad11cb6988f528503d614ab26dcc0968
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856140"
---
# <a name="run-applications-in-kubernetes"></a><span data-ttu-id="4121e-103">Run applications in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="4121e-103">Run applications in Kubernetes</span></span>

[!INCLUDE [aks-preview-redirect.md](../../../includes/aks-preview-redirect.md)]

<span data-ttu-id="4121e-104">In this tutorial, part four of seven, a sample application is deployed into a Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="4121e-104">In this tutorial, part four of seven, a sample application is deployed into a Kubernetes cluster.</span></span> <span data-ttu-id="4121e-105">Steps completed include:</span><span class="sxs-lookup"><span data-stu-id="4121e-105">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4121e-106">Update Kubernetes manifest files</span><span class="sxs-lookup"><span data-stu-id="4121e-106">Update Kubernetes manifest files</span></span>
> * <span data-ttu-id="4121e-107">Run application in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="4121e-107">Run application in Kubernetes</span></span>
> * <span data-ttu-id="4121e-108">Test the application</span><span class="sxs-lookup"><span data-stu-id="4121e-108">Test the application</span></span>

<span data-ttu-id="4121e-109">In subsequent tutorials, this application is scaled out, updated, and Log Analytics is configured to monitor the Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="4121e-109">In subsequent tutorials, this application is scaled out, updated, and Log Analytics is configured to monitor the Kubernetes cluster.</span></span>

<span data-ttu-id="4121e-110">This tutorial assumes a basic understanding of Kubernetes concepts, for detailed information on Kubernetes see the [Kubernetes documentation](https://kubernetes.io/docs/home/).</span><span class="sxs-lookup"><span data-stu-id="4121e-110">This tutorial assumes a basic understanding of Kubernetes concepts, for detailed information on Kubernetes see the [Kubernetes documentation](https://kubernetes.io/docs/home/).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4121e-111">Before you begin</span><span class="sxs-lookup"><span data-stu-id="4121e-111">Before you begin</span></span>

<span data-ttu-id="4121e-112">In previous tutorials, an application was packaged into a container image, this image was uploaded to Azure Container Registry, and a Kubernetes cluster was created.</span><span class="sxs-lookup"><span data-stu-id="4121e-112">In previous tutorials, an application was packaged into a container image, this image was uploaded to Azure Container Registry, and a Kubernetes cluster was created.</span></span> 

<span data-ttu-id="4121e-113">To complete this tutorial, you need the pre-created `azure-vote-all-in-one-redis.yml` Kubernetes manifest file.</span><span class="sxs-lookup"><span data-stu-id="4121e-113">To complete this tutorial, you need the pre-created `azure-vote-all-in-one-redis.yml` Kubernetes manifest file.</span></span> <span data-ttu-id="4121e-114">This file was downloaded with the application source code in a previous tutorial.</span><span class="sxs-lookup"><span data-stu-id="4121e-114">This file was downloaded with the application source code in a previous tutorial.</span></span> <span data-ttu-id="4121e-115">Verify that you have cloned the repo, and that you have changed directories into the cloned repo.</span><span class="sxs-lookup"><span data-stu-id="4121e-115">Verify that you have cloned the repo, and that you have changed directories into the cloned repo.</span></span>

<span data-ttu-id="4121e-116">If you have not done these steps, and would like to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="4121e-116">If you have not done these steps, and would like to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

## <a name="update-manifest-file"></a><span data-ttu-id="4121e-117">Update manifest file</span><span class="sxs-lookup"><span data-stu-id="4121e-117">Update manifest file</span></span>

<span data-ttu-id="4121e-118">In this tutorial, Azure Container Registry (ACR) has been used to store a container image.</span><span class="sxs-lookup"><span data-stu-id="4121e-118">In this tutorial, Azure Container Registry (ACR) has been used to store a container image.</span></span> <span data-ttu-id="4121e-119">Before running the application, the ACR login server name needs to be updated in the Kubernetes manifest file.</span><span class="sxs-lookup"><span data-stu-id="4121e-119">Before running the application, the ACR login server name needs to be updated in the Kubernetes manifest file.</span></span>

<span data-ttu-id="4121e-120">Get the ACR login server name with the [az acr list](/cli/azure/acr#az-acr-list) command.</span><span class="sxs-lookup"><span data-stu-id="4121e-120">Get the ACR login server name with the [az acr list](/cli/azure/acr#az-acr-list) command.</span></span>

```azurecli-interactive
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="4121e-121">The manifest file has been pre-created with a login server name of `microsoft`.</span><span class="sxs-lookup"><span data-stu-id="4121e-121">The manifest file has been pre-created with a login server name of `microsoft`.</span></span> <span data-ttu-id="4121e-122">Open the file with any text editor.</span><span class="sxs-lookup"><span data-stu-id="4121e-122">Open the file with any text editor.</span></span> <span data-ttu-id="4121e-123">In this example, the file is opened with `vi`.</span><span class="sxs-lookup"><span data-stu-id="4121e-123">In this example, the file is opened with `vi`.</span></span>

```bash
vi azure-vote-all-in-one-redis.yml
```

<span data-ttu-id="4121e-124">Replace `microsoft` with the ACR login server name.</span><span class="sxs-lookup"><span data-stu-id="4121e-124">Replace `microsoft` with the ACR login server name.</span></span> <span data-ttu-id="4121e-125">This value is found on line **47** of the manifest file.</span><span class="sxs-lookup"><span data-stu-id="4121e-125">This value is found on line **47** of the manifest file.</span></span>

```yaml
containers:
- name: azure-vote-front
  image: microsoft/azure-vote-front:v1
```

<span data-ttu-id="4121e-126">Save and close the file.</span><span class="sxs-lookup"><span data-stu-id="4121e-126">Save and close the file.</span></span>

## <a name="deploy-application"></a><span data-ttu-id="4121e-127">Deploy application</span><span class="sxs-lookup"><span data-stu-id="4121e-127">Deploy application</span></span>

<span data-ttu-id="4121e-128">Use the [kubectl create](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#create) command to run the application.</span><span class="sxs-lookup"><span data-stu-id="4121e-128">Use the [kubectl create](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#create) command to run the application.</span></span> <span data-ttu-id="4121e-129">This command parses the manifest file and create the defined Kubernetes objects.</span><span class="sxs-lookup"><span data-stu-id="4121e-129">This command parses the manifest file and create the defined Kubernetes objects.</span></span>

```azurecli-interactive
kubectl create -f azure-vote-all-in-one-redis.yml
```

<span data-ttu-id="4121e-130">Output:</span><span class="sxs-lookup"><span data-stu-id="4121e-130">Output:</span></span>

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-application"></a><span data-ttu-id="4121e-131">Test application</span><span class="sxs-lookup"><span data-stu-id="4121e-131">Test application</span></span>

<span data-ttu-id="4121e-132">A [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) is created which exposes the application to the internet.</span><span class="sxs-lookup"><span data-stu-id="4121e-132">A [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) is created which exposes the application to the internet.</span></span> <span data-ttu-id="4121e-133">This process can take a few minutes.</span><span class="sxs-lookup"><span data-stu-id="4121e-133">This process can take a few minutes.</span></span> 

<span data-ttu-id="4121e-134">To monitor progress, use the [kubectl get service](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command with the `--watch` argument.</span><span class="sxs-lookup"><span data-stu-id="4121e-134">To monitor progress, use the [kubectl get service](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command with the `--watch` argument.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

<span data-ttu-id="4121e-135">Initially, the **EXTERNAL-IP** for the `azure-vote-front` service appears as `pending`.</span><span class="sxs-lookup"><span data-stu-id="4121e-135">Initially, the **EXTERNAL-IP** for the `azure-vote-front` service appears as `pending`.</span></span> <span data-ttu-id="4121e-136">Once the EXTERNAL-IP address has changed from `pending` to an `IP address`, use `CTRL-C` to stop the kubectl watch process.</span><span class="sxs-lookup"><span data-stu-id="4121e-136">Once the EXTERNAL-IP address has changed from `pending` to an `IP address`, use `CTRL-C` to stop the kubectl watch process.</span></span>

```bash
NAME               CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
azure-vote-front   10.0.42.158   <pending>     80:31873/TCP   1m
azure-vote-front   10.0.42.158   52.179.23.131 80:31873/TCP   2m
```

<span data-ttu-id="4121e-137">To see the application, browse to the external IP address.</span><span class="sxs-lookup"><span data-stu-id="4121e-137">To see the application, browse to the external IP address.</span></span>

![Image of Kubernetes cluster on Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="next-steps"></a><span data-ttu-id="4121e-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="4121e-139">Next steps</span></span>

<span data-ttu-id="4121e-140">In this tutorial, the Azure vote application was deployed to an Azure Container Service Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="4121e-140">In this tutorial, the Azure vote application was deployed to an Azure Container Service Kubernetes cluster.</span></span> <span data-ttu-id="4121e-141">Tasks completed include:</span><span class="sxs-lookup"><span data-stu-id="4121e-141">Tasks completed include:</span></span>  

> [!div class="checklist"]
> * <span data-ttu-id="4121e-142">Download Kubernetes manifest files</span><span class="sxs-lookup"><span data-stu-id="4121e-142">Download Kubernetes manifest files</span></span>
> * <span data-ttu-id="4121e-143">Run the application in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="4121e-143">Run the application in Kubernetes</span></span>
> * <span data-ttu-id="4121e-144">Tested the application</span><span class="sxs-lookup"><span data-stu-id="4121e-144">Tested the application</span></span>

<span data-ttu-id="4121e-145">Advance to the next tutorial to learn about scaling both a Kubernetes application and the underlying Kubernetes infrastructure.</span><span class="sxs-lookup"><span data-stu-id="4121e-145">Advance to the next tutorial to learn about scaling both a Kubernetes application and the underlying Kubernetes infrastructure.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="4121e-146">Scale Kubernetes application and infrastructure</span><span class="sxs-lookup"><span data-stu-id="4121e-146">Scale Kubernetes application and infrastructure</span></span>](./container-service-tutorial-kubernetes-scale.md)