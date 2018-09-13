---
title: Kubernetes on Azure tutorial - Upgrade a cluster
description: In this Azure Kubernetes Service (AKS) tutorial, you learn how to upgrade an existing AKS cluster to the latest available Kubernetes version.
services: container-service
author: iainfoulds
manager: jeconnoc
ms.service: container-service
ms.topic: tutorial
ms.date: 08/14/2018
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 11e082ae235706613b0a60b12bc2b27896953508
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868197"
---
# <a name="tutorial-upgrade-kubernetes-in-azure-kubernetes-service-aks"></a><span data-ttu-id="a75df-103">Tutorial: Upgrade Kubernetes in Azure Kubernetes Service (AKS)</span><span class="sxs-lookup"><span data-stu-id="a75df-103">Tutorial: Upgrade Kubernetes in Azure Kubernetes Service (AKS)</span></span>

<span data-ttu-id="a75df-104">As part of the application and cluster lifecycle, you may wish to upgrade to the latest available version of Kubernetes and use new features.</span><span class="sxs-lookup"><span data-stu-id="a75df-104">As part of the application and cluster lifecycle, you may wish to upgrade to the latest available version of Kubernetes and use new features.</span></span> <span data-ttu-id="a75df-105">An Azure Kubernetes Service (AKS) cluster can be upgraded using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a75df-105">An Azure Kubernetes Service (AKS) cluster can be upgraded using the Azure CLI.</span></span> <span data-ttu-id="a75df-106">To minimize disruption to running applications, Kubernetes nodes are carefully [cordoned and drained][kubernetes-drain] during the upgrade process.</span><span class="sxs-lookup"><span data-stu-id="a75df-106">To minimize disruption to running applications, Kubernetes nodes are carefully [cordoned and drained][kubernetes-drain] during the upgrade process.</span></span>

<span data-ttu-id="a75df-107">In this tutorial, part seven of seven, a Kubernetes cluster is upgraded.</span><span class="sxs-lookup"><span data-stu-id="a75df-107">In this tutorial, part seven of seven, a Kubernetes cluster is upgraded.</span></span> <span data-ttu-id="a75df-108">You learn how to:</span><span class="sxs-lookup"><span data-stu-id="a75df-108">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a75df-109">Identify current and available Kubernetes versions</span><span class="sxs-lookup"><span data-stu-id="a75df-109">Identify current and available Kubernetes versions</span></span>
> * <span data-ttu-id="a75df-110">Upgrade the Kubernetes nodes</span><span class="sxs-lookup"><span data-stu-id="a75df-110">Upgrade the Kubernetes nodes</span></span>
> * <span data-ttu-id="a75df-111">Validate a successful upgrade</span><span class="sxs-lookup"><span data-stu-id="a75df-111">Validate a successful upgrade</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a75df-112">Before you begin</span><span class="sxs-lookup"><span data-stu-id="a75df-112">Before you begin</span></span>

<span data-ttu-id="a75df-113">In previous tutorials, an application was packaged into a container image, this image uploaded to Azure Container Registry, and a Kubernetes cluster created.</span><span class="sxs-lookup"><span data-stu-id="a75df-113">In previous tutorials, an application was packaged into a container image, this image uploaded to Azure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="a75df-114">The application was then run on the Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="a75df-114">The application was then run on the Kubernetes cluster.</span></span> <span data-ttu-id="a75df-115">If you have not done these steps, and would like to follow along, return to the [Tutorial 1 – Create container images][aks-tutorial-prepare-app].</span><span class="sxs-lookup"><span data-stu-id="a75df-115">If you have not done these steps, and would like to follow along, return to the [Tutorial 1 – Create container images][aks-tutorial-prepare-app].</span></span>

<span data-ttu-id="a75df-116">This tutorial requires that you are running the Azure CLI version 2.0.44 or later.</span><span class="sxs-lookup"><span data-stu-id="a75df-116">This tutorial requires that you are running the Azure CLI version 2.0.44 or later.</span></span> <span data-ttu-id="a75df-117">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="a75df-117">Run `az --version` to find the version.</span></span> <span data-ttu-id="a75df-118">If you need to install or upgrade, see [Install Azure CLI][azure-cli-install].</span><span class="sxs-lookup"><span data-stu-id="a75df-118">If you need to install or upgrade, see [Install Azure CLI][azure-cli-install].</span></span>

## <a name="get-available-cluster-versions"></a><span data-ttu-id="a75df-119">Get available cluster versions</span><span class="sxs-lookup"><span data-stu-id="a75df-119">Get available cluster versions</span></span>

<span data-ttu-id="a75df-120">Before you upgrade a cluster, use the [az aks get-upgrades][] command to check which Kubernetes releases are available for upgrade:</span><span class="sxs-lookup"><span data-stu-id="a75df-120">Before you upgrade a cluster, use the [az aks get-upgrades][] command to check which Kubernetes releases are available for upgrade:</span></span>

```azurecli
az aks get-upgrades --resource-group myResourceGroup --name myAKSCluster --output table
```

<span data-ttu-id="a75df-121">In the following example, the current version is *1.9.6*, and the available versions are shown under the *Upgrades* column.</span><span class="sxs-lookup"><span data-stu-id="a75df-121">In the following example, the current version is *1.9.6*, and the available versions are shown under the *Upgrades* column.</span></span>

```
Name     ResourceGroup    MasterVersion    NodePoolVersion    Upgrades
-------  ---------------  ---------------  -----------------  ----------------------
default  myResourceGroup  1.9.9            1.9.9              1.10.3, 1.10.5, 1.10.6
```

## <a name="upgrade-a-cluster"></a><span data-ttu-id="a75df-122">Upgrade a cluster</span><span class="sxs-lookup"><span data-stu-id="a75df-122">Upgrade a cluster</span></span>

<span data-ttu-id="a75df-123">Use the [az aks upgrade][] command to upgrade the AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="a75df-123">Use the [az aks upgrade][] command to upgrade the AKS cluster.</span></span> <span data-ttu-id="a75df-124">The following example upgrades the cluster to Kubernetes version *1.10.6*.</span><span class="sxs-lookup"><span data-stu-id="a75df-124">The following example upgrades the cluster to Kubernetes version *1.10.6*.</span></span>

> [!NOTE]
> <span data-ttu-id="a75df-125">You can only upgrade one minor version at a time.</span><span class="sxs-lookup"><span data-stu-id="a75df-125">You can only upgrade one minor version at a time.</span></span> <span data-ttu-id="a75df-126">For example, you can upgrade from *1.9.6* to *1.10.3*, but cannot upgrade from *1.9.6* to *1.11.x* directly.</span><span class="sxs-lookup"><span data-stu-id="a75df-126">For example, you can upgrade from *1.9.6* to *1.10.3*, but cannot upgrade from *1.9.6* to *1.11.x* directly.</span></span> <span data-ttu-id="a75df-127">To upgrade from *1.9.6* to *1.11.x*, first upgrade from *1.9.6* to *1.10.3*, then perform another upgrade from *1.10.3* to *1.11.x*.</span><span class="sxs-lookup"><span data-stu-id="a75df-127">To upgrade from *1.9.6* to *1.11.x*, first upgrade from *1.9.6* to *1.10.3*, then perform another upgrade from *1.10.3* to *1.11.x*.</span></span>

```azurecli
az aks upgrade --resource-group myResourceGroup --name myAKSCluster --kubernetes-version 1.10.6
```

<span data-ttu-id="a75df-128">The following condensed example output shows the *kubernetesVersion* now reports *1.10.6*:</span><span class="sxs-lookup"><span data-stu-id="a75df-128">The following condensed example output shows the *kubernetesVersion* now reports *1.10.6*:</span></span>

```json
{
  "agentPoolProfiles": [
    {
      "count": 3,
      "maxPods": 110,
      "name": "nodepool1",
      "osType": "Linux",
      "storageProfile": "ManagedDisks",
      "vmSize": "Standard_DS1_v2",
    }
  ],
  "dnsPrefix": "myAKSClust-myResourceGroup-19da35",
  "enableRbac": false,
  "fqdn": "myaksclust-myresourcegroup-19da35-bd54a4be.hcp.eastus.azmk8s.io",
  "id": "/subscriptions/<Subscription ID>/resourcegroups/myResourceGroup/providers/Microsoft.ContainerService/managedClusters/myAKSCluster",
  "kubernetesVersion": "1.10.6",
  "location": "eastus",
  "name": "myAKSCluster",
  "type": "Microsoft.ContainerService/ManagedClusters"
}
```

## <a name="validate-an-upgrade"></a><span data-ttu-id="a75df-129">Validate an upgrade</span><span class="sxs-lookup"><span data-stu-id="a75df-129">Validate an upgrade</span></span>

<span data-ttu-id="a75df-130">Confirm that the upgrade was successful using the [az aks show][] command as follows:</span><span class="sxs-lookup"><span data-stu-id="a75df-130">Confirm that the upgrade was successful using the [az aks show][] command as follows:</span></span>

```azurecli
az aks show --resource-group myResourceGroup --name myAKSCluster --output table
```

<span data-ttu-id="a75df-131">The following example output shows the AKS cluster runs *KubernetesVersion 1.10.6*:</span><span class="sxs-lookup"><span data-stu-id="a75df-131">The following example output shows the AKS cluster runs *KubernetesVersion 1.10.6*:</span></span>

```
Name          Location    ResourceGroup    KubernetesVersion    ProvisioningState    Fqdn
------------  ----------  ---------------  -------------------  -------------------  ----------------------------------------------------------------
myAKSCluster  eastus      myResourceGroup  1.10.6               Succeeded            myaksclust-myresourcegroup-19da35-bd54a4be.hcp.eastus.azmk8s.io
```

## <a name="next-steps"></a><span data-ttu-id="a75df-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="a75df-132">Next steps</span></span>

<span data-ttu-id="a75df-133">In this tutorial, you upgraded Kubernetes in an AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="a75df-133">In this tutorial, you upgraded Kubernetes in an AKS cluster.</span></span> <span data-ttu-id="a75df-134">You learned how to:</span><span class="sxs-lookup"><span data-stu-id="a75df-134">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a75df-135">Identify current and available Kubernetes versions</span><span class="sxs-lookup"><span data-stu-id="a75df-135">Identify current and available Kubernetes versions</span></span>
> * <span data-ttu-id="a75df-136">Upgrade the Kubernetes nodes</span><span class="sxs-lookup"><span data-stu-id="a75df-136">Upgrade the Kubernetes nodes</span></span>
> * <span data-ttu-id="a75df-137">Validate a successful upgrade</span><span class="sxs-lookup"><span data-stu-id="a75df-137">Validate a successful upgrade</span></span>

<span data-ttu-id="a75df-138">Follow this link to learn more about AKS.</span><span class="sxs-lookup"><span data-stu-id="a75df-138">Follow this link to learn more about AKS.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="a75df-139">[AKS overview][aks-intro]</span><span class="sxs-lookup"><span data-stu-id="a75df-139">[AKS overview][aks-intro]</span></span>

<!-- LINKS - external -->
[kubernetes-drain]: https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/

<!-- LINKS - internal -->
[aks-intro]: ./intro-kubernetes.md
[aks-tutorial-prepare-app]: ./tutorial-kubernetes-prepare-app.md
[az aks show]: /cli/azure/aks#az-aks-show
[az aks get-upgrades]: /cli/azure/aks#az-aks-get-upgrades
[az aks upgrade]: /cli/azure/aks#az-aks-upgrade
[azure-cli-install]: /cli/azure/install-azure-cli