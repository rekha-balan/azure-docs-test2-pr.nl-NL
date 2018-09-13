---
title: Kubernetes on Azure tutorial - Deploy a cluster
description: In this Azure Kubernetes Service (AKS) tutorial, you create an AKS cluster and use kubectl to connect to the Kubernetes master node.
services: container-service
author: iainfoulds
manager: jeconnoc
ms.service: container-service
ms.topic: tutorial
ms.date: 08/14/2018
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 80b011f9df389098095f58c02008da891b2aa8a7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866958"
---
# <a name="tutorial-deploy-an-azure-kubernetes-service-aks-cluster"></a><span data-ttu-id="33d3b-103">Tutorial: Deploy an Azure Kubernetes Service (AKS) cluster</span><span class="sxs-lookup"><span data-stu-id="33d3b-103">Tutorial: Deploy an Azure Kubernetes Service (AKS) cluster</span></span>

<span data-ttu-id="33d3b-104">Kubernetes provides a distributed platform for containerized applications.</span><span class="sxs-lookup"><span data-stu-id="33d3b-104">Kubernetes provides a distributed platform for containerized applications.</span></span> <span data-ttu-id="33d3b-105">With AKS, you can quickly provision a production ready Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="33d3b-105">With AKS, you can quickly provision a production ready Kubernetes cluster.</span></span> <span data-ttu-id="33d3b-106">In this tutorial, part three of seven, a Kubernetes cluster is deployed in AKS.</span><span class="sxs-lookup"><span data-stu-id="33d3b-106">In this tutorial, part three of seven, a Kubernetes cluster is deployed in AKS.</span></span> <span data-ttu-id="33d3b-107">You learn how to:</span><span class="sxs-lookup"><span data-stu-id="33d3b-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="33d3b-108">Create a service principal for resource interactions</span><span class="sxs-lookup"><span data-stu-id="33d3b-108">Create a service principal for resource interactions</span></span>
> * <span data-ttu-id="33d3b-109">Deploy a Kubernetes AKS cluster</span><span class="sxs-lookup"><span data-stu-id="33d3b-109">Deploy a Kubernetes AKS cluster</span></span>
> * <span data-ttu-id="33d3b-110">Install the Kubernetes CLI (kubectl)</span><span class="sxs-lookup"><span data-stu-id="33d3b-110">Install the Kubernetes CLI (kubectl)</span></span>
> * <span data-ttu-id="33d3b-111">Configure kubectl to connect to your AKS cluster</span><span class="sxs-lookup"><span data-stu-id="33d3b-111">Configure kubectl to connect to your AKS cluster</span></span>

<span data-ttu-id="33d3b-112">In subsequent tutorials, the Azure Vote application is deployed to the cluster, scaled, and updated.</span><span class="sxs-lookup"><span data-stu-id="33d3b-112">In subsequent tutorials, the Azure Vote application is deployed to the cluster, scaled, and updated.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="33d3b-113">Before you begin</span><span class="sxs-lookup"><span data-stu-id="33d3b-113">Before you begin</span></span>

<span data-ttu-id="33d3b-114">In previous tutorials, a container image was created and uploaded to an Azure Container Registry instance.</span><span class="sxs-lookup"><span data-stu-id="33d3b-114">In previous tutorials, a container image was created and uploaded to an Azure Container Registry instance.</span></span> <span data-ttu-id="33d3b-115">If you have not done these steps, and would like to follow along, return to [Tutorial 1 – Create container images][aks-tutorial-prepare-app].</span><span class="sxs-lookup"><span data-stu-id="33d3b-115">If you have not done these steps, and would like to follow along, return to [Tutorial 1 – Create container images][aks-tutorial-prepare-app].</span></span>

<span data-ttu-id="33d3b-116">This tutorial requires that you are running the Azure CLI version 2.0.44 or later.</span><span class="sxs-lookup"><span data-stu-id="33d3b-116">This tutorial requires that you are running the Azure CLI version 2.0.44 or later.</span></span> <span data-ttu-id="33d3b-117">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="33d3b-117">Run `az --version` to find the version.</span></span> <span data-ttu-id="33d3b-118">If you need to install or upgrade, see [Install Azure CLI][azure-cli-install].</span><span class="sxs-lookup"><span data-stu-id="33d3b-118">If you need to install or upgrade, see [Install Azure CLI][azure-cli-install].</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="33d3b-119">Create a service principal</span><span class="sxs-lookup"><span data-stu-id="33d3b-119">Create a service principal</span></span>

<span data-ttu-id="33d3b-120">To allow an AKS cluster to interact with other Azure resources, an Azure Active Directory service principal is used.</span><span class="sxs-lookup"><span data-stu-id="33d3b-120">To allow an AKS cluster to interact with other Azure resources, an Azure Active Directory service principal is used.</span></span> <span data-ttu-id="33d3b-121">This service principal can be automatically created by the Azure CLI or portal, or you can pre-create one and assign additional permissions.</span><span class="sxs-lookup"><span data-stu-id="33d3b-121">This service principal can be automatically created by the Azure CLI or portal, or you can pre-create one and assign additional permissions.</span></span> <span data-ttu-id="33d3b-122">In this tutorial, you create a service principal, grant access to the Azure Container Registry (ACR) instance created in the previous tutorial, then create an AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="33d3b-122">In this tutorial, you create a service principal, grant access to the Azure Container Registry (ACR) instance created in the previous tutorial, then create an AKS cluster.</span></span>

<span data-ttu-id="33d3b-123">Create a service principal using the [az ad sp create-for-rbac][] command.</span><span class="sxs-lookup"><span data-stu-id="33d3b-123">Create a service principal using the [az ad sp create-for-rbac][] command.</span></span> <span data-ttu-id="33d3b-124">The `--skip-assignment` parameter limits any additional permissions from being assigned.</span><span class="sxs-lookup"><span data-stu-id="33d3b-124">The `--skip-assignment` parameter limits any additional permissions from being assigned.</span></span>

```azurecli
az ad sp create-for-rbac --skip-assignment
```

<span data-ttu-id="33d3b-125">The output is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="33d3b-125">The output is similar to the following example:</span></span>

```
{
  "appId": "e7596ae3-6864-4cb8-94fc-20164b1588a9",
  "displayName": "azure-cli-2018-06-29-19-14-37",
  "name": "http://azure-cli-2018-06-29-19-14-37",
  "password": "52c95f25-bd1e-4314-bd31-d8112b293521",
  "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db48"
}
```

<span data-ttu-id="33d3b-126">Make a note of the *appId* and *password*.</span><span class="sxs-lookup"><span data-stu-id="33d3b-126">Make a note of the *appId* and *password*.</span></span> <span data-ttu-id="33d3b-127">These values are used in the following steps.</span><span class="sxs-lookup"><span data-stu-id="33d3b-127">These values are used in the following steps.</span></span>

## <a name="configure-acr-authentication"></a><span data-ttu-id="33d3b-128">Configure ACR authentication</span><span class="sxs-lookup"><span data-stu-id="33d3b-128">Configure ACR authentication</span></span>

<span data-ttu-id="33d3b-129">To access images stored in ACR, you must grant the AKS service principal the correct rights to pull images from ACR.</span><span class="sxs-lookup"><span data-stu-id="33d3b-129">To access images stored in ACR, you must grant the AKS service principal the correct rights to pull images from ACR.</span></span>

<span data-ttu-id="33d3b-130">First, get the ACR resource ID using [az acr show][].</span><span class="sxs-lookup"><span data-stu-id="33d3b-130">First, get the ACR resource ID using [az acr show][].</span></span> <span data-ttu-id="33d3b-131">Update the `<acrName>` registry name to that of your ACR instance and the resource group where the ACR instance is located.</span><span class="sxs-lookup"><span data-stu-id="33d3b-131">Update the `<acrName>` registry name to that of your ACR instance and the resource group where the ACR instance is located.</span></span>

```azurecli
az acr show --resource-group myResourceGroup --name <acrName> --query "id" --output tsv
```

<span data-ttu-id="33d3b-132">To grant the correct access for the AKS cluster to use images stored in ACR, create a role assignment using the [az role assignment create][] command.</span><span class="sxs-lookup"><span data-stu-id="33d3b-132">To grant the correct access for the AKS cluster to use images stored in ACR, create a role assignment using the [az role assignment create][] command.</span></span> <span data-ttu-id="33d3b-133">Replace `<appId`> and `<acrId>` with the values gathered in the previous two steps.</span><span class="sxs-lookup"><span data-stu-id="33d3b-133">Replace `<appId`> and `<acrId>` with the values gathered in the previous two steps.</span></span>

```azurecli
az role assignment create --assignee <appId> --scope <acrId> --role Reader
```

## <a name="create-a-kubernetes-cluster"></a><span data-ttu-id="33d3b-134">Create a Kubernetes cluster</span><span class="sxs-lookup"><span data-stu-id="33d3b-134">Create a Kubernetes cluster</span></span>

<span data-ttu-id="33d3b-135">AKS clusters can use Kubernetes role-based access controls (RBAC).</span><span class="sxs-lookup"><span data-stu-id="33d3b-135">AKS clusters can use Kubernetes role-based access controls (RBAC).</span></span> <span data-ttu-id="33d3b-136">These controls let you define access to resources based on roles assigned to users.</span><span class="sxs-lookup"><span data-stu-id="33d3b-136">These controls let you define access to resources based on roles assigned to users.</span></span> <span data-ttu-id="33d3b-137">Permissions can be combined if a user is assigned multiple roles, and permissions can be scoped to either a single namespace or across the whole cluster.</span><span class="sxs-lookup"><span data-stu-id="33d3b-137">Permissions can be combined if a user is assigned multiple roles, and permissions can be scoped to either a single namespace or across the whole cluster.</span></span> <span data-ttu-id="33d3b-138">Kubernetes RBAC is currently in preview for AKS clusters.</span><span class="sxs-lookup"><span data-stu-id="33d3b-138">Kubernetes RBAC is currently in preview for AKS clusters.</span></span> <span data-ttu-id="33d3b-139">By default, the Azure CLI automatically enables RBAC when you create an AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="33d3b-139">By default, the Azure CLI automatically enables RBAC when you create an AKS cluster.</span></span>

<span data-ttu-id="33d3b-140">Create an AKS cluster using [az aks create][].</span><span class="sxs-lookup"><span data-stu-id="33d3b-140">Create an AKS cluster using [az aks create][].</span></span> <span data-ttu-id="33d3b-141">The following example creates a cluster named *myAKSCluster* in the resource group named *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="33d3b-141">The following example creates a cluster named *myAKSCluster* in the resource group named *myResourceGroup*.</span></span> <span data-ttu-id="33d3b-142">This resource group was created in the [previous tutorial][aks-tutorial-prepare-acr].</span><span class="sxs-lookup"><span data-stu-id="33d3b-142">This resource group was created in the [previous tutorial][aks-tutorial-prepare-acr].</span></span> <span data-ttu-id="33d3b-143">Provide your own `<appId>` and `<password>` from the previous step where the service principal was created.</span><span class="sxs-lookup"><span data-stu-id="33d3b-143">Provide your own `<appId>` and `<password>` from the previous step where the service principal was created.</span></span>

```azurecli
az aks create \
    --resource-group myResourceGroup \
    --name myAKSCluster \
    --node-count 1 \
    --service-principal <appId> \
    --client-secret <password> \
    --generate-ssh-keys
```

<span data-ttu-id="33d3b-144">After several minutes, the deployment completes, and returns JSON-formatted information about the AKS deployment.</span><span class="sxs-lookup"><span data-stu-id="33d3b-144">After several minutes, the deployment completes, and returns JSON-formatted information about the AKS deployment.</span></span>

## <a name="install-the-kubernetes-cli"></a><span data-ttu-id="33d3b-145">Install the Kubernetes CLI</span><span class="sxs-lookup"><span data-stu-id="33d3b-145">Install the Kubernetes CLI</span></span>

<span data-ttu-id="33d3b-146">To connect to the Kubernetes cluster from your local computer, you use [kubectl][kubectl], the Kubernetes command-line client.</span><span class="sxs-lookup"><span data-stu-id="33d3b-146">To connect to the Kubernetes cluster from your local computer, you use [kubectl][kubectl], the Kubernetes command-line client.</span></span>

<span data-ttu-id="33d3b-147">If you use the Azure Cloud Shell, `kubectl` is already installed.</span><span class="sxs-lookup"><span data-stu-id="33d3b-147">If you use the Azure Cloud Shell, `kubectl` is already installed.</span></span> <span data-ttu-id="33d3b-148">You can also install it locally using the [az aks install-cli][] command:</span><span class="sxs-lookup"><span data-stu-id="33d3b-148">You can also install it locally using the [az aks install-cli][] command:</span></span>

```azurecli
az aks install-cli
```

## <a name="connect-to-cluster-using-kubectl"></a><span data-ttu-id="33d3b-149">Connect to cluster using kubectl</span><span class="sxs-lookup"><span data-stu-id="33d3b-149">Connect to cluster using kubectl</span></span>

<span data-ttu-id="33d3b-150">To configure `kubectl` to connect to your Kubernetes cluster, use [az aks get-credentials][].</span><span class="sxs-lookup"><span data-stu-id="33d3b-150">To configure `kubectl` to connect to your Kubernetes cluster, use [az aks get-credentials][].</span></span> <span data-ttu-id="33d3b-151">The following example gets credentials for the AKS cluster name *myAKSCluster* in the *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="33d3b-151">The following example gets credentials for the AKS cluster name *myAKSCluster* in the *myResourceGroup*:</span></span>

```azurecli
az aks get-credentials --resource-group myResourceGroup --name myAKSCluster
```

<span data-ttu-id="33d3b-152">To verify the connection to your cluster, run the [kubectl get nodes][kubectl-get] command:</span><span class="sxs-lookup"><span data-stu-id="33d3b-152">To verify the connection to your cluster, run the [kubectl get nodes][kubectl-get] command:</span></span>

```
$ kubectl get nodes

NAME                       STATUS    ROLES     AGE       VERSION
aks-nodepool1-66427764-0   Ready     agent     9m        v1.9.9
```

## <a name="next-steps"></a><span data-ttu-id="33d3b-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="33d3b-153">Next steps</span></span>

<span data-ttu-id="33d3b-154">In this tutorial, a Kubernetes cluster was deployed in AKS, and you configured `kubectl` to connect to it.</span><span class="sxs-lookup"><span data-stu-id="33d3b-154">In this tutorial, a Kubernetes cluster was deployed in AKS, and you configured `kubectl` to connect to it.</span></span> <span data-ttu-id="33d3b-155">You learned how to:</span><span class="sxs-lookup"><span data-stu-id="33d3b-155">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="33d3b-156">Create a service principal for resource interactions</span><span class="sxs-lookup"><span data-stu-id="33d3b-156">Create a service principal for resource interactions</span></span>
> * <span data-ttu-id="33d3b-157">Deploy a Kubernetes AKS cluster</span><span class="sxs-lookup"><span data-stu-id="33d3b-157">Deploy a Kubernetes AKS cluster</span></span>
> * <span data-ttu-id="33d3b-158">Install the Kubernetes CLI (kubectl)</span><span class="sxs-lookup"><span data-stu-id="33d3b-158">Install the Kubernetes CLI (kubectl)</span></span>
> * <span data-ttu-id="33d3b-159">Configure kubectl to connect to your AKS cluster</span><span class="sxs-lookup"><span data-stu-id="33d3b-159">Configure kubectl to connect to your AKS cluster</span></span>

<span data-ttu-id="33d3b-160">Advance to the next tutorial to learn how to deploy an application to the cluster.</span><span class="sxs-lookup"><span data-stu-id="33d3b-160">Advance to the next tutorial to learn how to deploy an application to the cluster.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="33d3b-161">[Deploy application in Kubernetes][aks-tutorial-deploy-app]</span><span class="sxs-lookup"><span data-stu-id="33d3b-161">[Deploy application in Kubernetes][aks-tutorial-deploy-app]</span></span>

<!-- LINKS - external -->
[kubectl]: https://kubernetes.io/docs/user-guide/kubectl/
[kubectl-get]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get

<!-- LINKS - internal -->
[aks-tutorial-deploy-app]: ./tutorial-kubernetes-deploy-application.md
[aks-tutorial-prepare-acr]: ./tutorial-kubernetes-prepare-acr.md
[aks-tutorial-prepare-app]: ./tutorial-kubernetes-prepare-app.md
[az ad sp create-for-rbac]: /cli/azure/ad/sp#az-ad-sp-create-for-rbac
[az acr show]: /cli/azure/acr#az-acr-show
[az role assignment create]: /cli/azure/role/assignment#az-role-assignment-create
[az aks create]: /cli/azure/aks#az-aks-create
[az aks install-cli]: /cli/azure/aks#az-aks-install-cli
[az aks get-credentials]: /cli/azure/aks#az-aks-get-credentials
[azure-cli-install]: /cli/azure/install-azure-cli
