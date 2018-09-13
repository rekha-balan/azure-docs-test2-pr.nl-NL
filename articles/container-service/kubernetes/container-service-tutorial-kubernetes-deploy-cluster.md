---
title: Azure Container Service tutorial - Deploy Cluster
description: Azure Container Service tutorial - Deploy Cluster
services: container-service
author: neilpeterson
manager: jeconnoc
ms.service: container-service
ms.topic: tutorial
ms.date: 09/14/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 8403e5d8dd3bad07e412b08709dcb8c28201bcdf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870386"
---
# <a name="deploy-a-kubernetes-cluster-in-azure-container-service"></a><span data-ttu-id="f55d0-103">Deploy a Kubernetes cluster in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="f55d0-103">Deploy a Kubernetes cluster in Azure Container Service</span></span>

[!INCLUDE [aks-preview-redirect.md](../../../includes/aks-preview-redirect.md)]

<span data-ttu-id="f55d0-104">Kubernetes provides a distributed platform for containerized applications.</span><span class="sxs-lookup"><span data-stu-id="f55d0-104">Kubernetes provides a distributed platform for containerized applications.</span></span> <span data-ttu-id="f55d0-105">With Azure Container Service, provisioning of a production ready Kubernetes cluster is simple and quick.</span><span class="sxs-lookup"><span data-stu-id="f55d0-105">With Azure Container Service, provisioning of a production ready Kubernetes cluster is simple and quick.</span></span> <span data-ttu-id="f55d0-106">In this tutorial, part 3 of 7, an Azure Container Service Kubernetes cluster is deployed.</span><span class="sxs-lookup"><span data-stu-id="f55d0-106">In this tutorial, part 3 of 7, an Azure Container Service Kubernetes cluster is deployed.</span></span> <span data-ttu-id="f55d0-107">Steps completed include:</span><span class="sxs-lookup"><span data-stu-id="f55d0-107">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f55d0-108">Deploying a Kubernetes ACS cluster</span><span class="sxs-lookup"><span data-stu-id="f55d0-108">Deploying a Kubernetes ACS cluster</span></span>
> * <span data-ttu-id="f55d0-109">Installation of the Kubernetes CLI (kubectl)</span><span class="sxs-lookup"><span data-stu-id="f55d0-109">Installation of the Kubernetes CLI (kubectl)</span></span>
> * <span data-ttu-id="f55d0-110">Configuration of kubectl</span><span class="sxs-lookup"><span data-stu-id="f55d0-110">Configuration of kubectl</span></span>

<span data-ttu-id="f55d0-111">In subsequent tutorials, the Azure Vote application is deployed to the cluster, scaled, updated, and Log Analytics is configured to monitor the Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="f55d0-111">In subsequent tutorials, the Azure Vote application is deployed to the cluster, scaled, updated, and Log Analytics is configured to monitor the Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f55d0-112">Before you begin</span><span class="sxs-lookup"><span data-stu-id="f55d0-112">Before you begin</span></span>

<span data-ttu-id="f55d0-113">In previous tutorials, a container image was created and uploaded to an Azure Container Registry instance.</span><span class="sxs-lookup"><span data-stu-id="f55d0-113">In previous tutorials, a container image was created and uploaded to an Azure Container Registry instance.</span></span> <span data-ttu-id="f55d0-114">If you have not done these steps, and would like to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="f55d0-114">If you have not done these steps, and would like to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span>

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="f55d0-115">Create Kubernetes cluster</span><span class="sxs-lookup"><span data-stu-id="f55d0-115">Create Kubernetes cluster</span></span>

<span data-ttu-id="f55d0-116">Create a Kubernetes cluster in Azure Container Service with the [az acs create](/cli/azure/acs#az-acs-create) command.</span><span class="sxs-lookup"><span data-stu-id="f55d0-116">Create a Kubernetes cluster in Azure Container Service with the [az acs create](/cli/azure/acs#az-acs-create) command.</span></span> 

<span data-ttu-id="f55d0-117">The following example creates a cluster named `myK8sCluster` in a Resource Group named `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="f55d0-117">The following example creates a cluster named `myK8sCluster` in a Resource Group named `myResourceGroup`.</span></span> <span data-ttu-id="f55d0-118">This Resource Group was created in the [previous tutorial](./container-service-tutorial-kubernetes-prepare-acr.md).</span><span class="sxs-lookup"><span data-stu-id="f55d0-118">This Resource Group was created in the [previous tutorial](./container-service-tutorial-kubernetes-prepare-acr.md).</span></span>

```azurecli-interactive 
az acs create --orchestrator-type kubernetes --resource-group myResourceGroup --name myK8SCluster --generate-ssh-keys 
```

<span data-ttu-id="f55d0-119">In some cases, such as with a limited trial, an Azure subscription has limited access to Azure resources.</span><span class="sxs-lookup"><span data-stu-id="f55d0-119">In some cases, such as with a limited trial, an Azure subscription has limited access to Azure resources.</span></span> <span data-ttu-id="f55d0-120">If the deployment fails due to limited available cores, reduce the default agent count by adding `--agent-count 1` to the [az acs create](/cli/azure/acs#az-acs-create) command.</span><span class="sxs-lookup"><span data-stu-id="f55d0-120">If the deployment fails due to limited available cores, reduce the default agent count by adding `--agent-count 1` to the [az acs create](/cli/azure/acs#az-acs-create) command.</span></span> 

<span data-ttu-id="f55d0-121">After several minutes, the deployment completes, and returns json formatted information about the ACS deployment.</span><span class="sxs-lookup"><span data-stu-id="f55d0-121">After several minutes, the deployment completes, and returns json formatted information about the ACS deployment.</span></span>

## <a name="install-the-kubectl-cli"></a><span data-ttu-id="f55d0-122">Install the kubectl CLI</span><span class="sxs-lookup"><span data-stu-id="f55d0-122">Install the kubectl CLI</span></span>

<span data-ttu-id="f55d0-123">To connect to the Kubernetes cluster from your client computer, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), the Kubernetes command-line client.</span><span class="sxs-lookup"><span data-stu-id="f55d0-123">To connect to the Kubernetes cluster from your client computer, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), the Kubernetes command-line client.</span></span> 

<span data-ttu-id="f55d0-124">If you're using Azure CloudShell, kubectl is already installed.</span><span class="sxs-lookup"><span data-stu-id="f55d0-124">If you're using Azure CloudShell, kubectl is already installed.</span></span> <span data-ttu-id="f55d0-125">If you want to install it locally, use the [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span><span class="sxs-lookup"><span data-stu-id="f55d0-125">If you want to install it locally, use the [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="f55d0-126">If running in Linux or macOS, you may need to run with sudo.</span><span class="sxs-lookup"><span data-stu-id="f55d0-126">If running in Linux or macOS, you may need to run with sudo.</span></span> <span data-ttu-id="f55d0-127">On Windows, ensure your shell has been run as administrator.</span><span class="sxs-lookup"><span data-stu-id="f55d0-127">On Windows, ensure your shell has been run as administrator.</span></span>

```azurecli-interactive 
az acs kubernetes install-cli 
```

<span data-ttu-id="f55d0-128">On Windows, the default installation is *c:\program files (x86)\kubectl.exe*.</span><span class="sxs-lookup"><span data-stu-id="f55d0-128">On Windows, the default installation is *c:\program files (x86)\kubectl.exe*.</span></span> <span data-ttu-id="f55d0-129">You may need to add this file to the Windows path.</span><span class="sxs-lookup"><span data-stu-id="f55d0-129">You may need to add this file to the Windows path.</span></span> 

## <a name="connect-with-kubectl"></a><span data-ttu-id="f55d0-130">Connect with kubectl</span><span class="sxs-lookup"><span data-stu-id="f55d0-130">Connect with kubectl</span></span>

<span data-ttu-id="f55d0-131">To configure kubectl to connect to your Kubernetes cluster, run the [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span><span class="sxs-lookup"><span data-stu-id="f55d0-131">To configure kubectl to connect to your Kubernetes cluster, run the [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group myResourceGroup --name myK8SCluster
```

<span data-ttu-id="f55d0-132">To verify the connection to your cluster, run the [kubectl get nodes](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command.</span><span class="sxs-lookup"><span data-stu-id="f55d0-132">To verify the connection to your cluster, run the [kubectl get nodes](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command.</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="f55d0-133">Output:</span><span class="sxs-lookup"><span data-stu-id="f55d0-133">Output:</span></span>

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.6.2
k8s-agent-98dc3136-1    Ready                      5m        v1.6.2
k8s-agent-98dc3136-2    Ready                      5m        v1.6.2
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.6.2
```

<span data-ttu-id="f55d0-134">At tutorial completion, you have an ACS Kubernetes cluster ready for workloads.</span><span class="sxs-lookup"><span data-stu-id="f55d0-134">At tutorial completion, you have an ACS Kubernetes cluster ready for workloads.</span></span> <span data-ttu-id="f55d0-135">In subsequent tutorials, a multi-container application is deployed to this cluster, scaled out, updated, and monitored.</span><span class="sxs-lookup"><span data-stu-id="f55d0-135">In subsequent tutorials, a multi-container application is deployed to this cluster, scaled out, updated, and monitored.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f55d0-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="f55d0-136">Next steps</span></span>

<span data-ttu-id="f55d0-137">In this tutorial, an Azure Container Service Kubernetes cluster was deployed.</span><span class="sxs-lookup"><span data-stu-id="f55d0-137">In this tutorial, an Azure Container Service Kubernetes cluster was deployed.</span></span> <span data-ttu-id="f55d0-138">The following steps were completed:</span><span class="sxs-lookup"><span data-stu-id="f55d0-138">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f55d0-139">Deployed a Kubernetes ACS cluster</span><span class="sxs-lookup"><span data-stu-id="f55d0-139">Deployed a Kubernetes ACS cluster</span></span>
> * <span data-ttu-id="f55d0-140">Installed the Kubernetes CLI (kubectl)</span><span class="sxs-lookup"><span data-stu-id="f55d0-140">Installed the Kubernetes CLI (kubectl)</span></span>
> * <span data-ttu-id="f55d0-141">Configured kubectl</span><span class="sxs-lookup"><span data-stu-id="f55d0-141">Configured kubectl</span></span>

<span data-ttu-id="f55d0-142">Advance to the next tutorial to learn about running application on the cluster.</span><span class="sxs-lookup"><span data-stu-id="f55d0-142">Advance to the next tutorial to learn about running application on the cluster.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f55d0-143">Deploy application in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="f55d0-143">Deploy application in Kubernetes</span></span>](./container-service-tutorial-kubernetes-deploy-application.md)
