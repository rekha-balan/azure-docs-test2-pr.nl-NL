---
title: Create an Azure Kubernetes Service (AKS) internal load balancer
description: Learn how to create and use an internal load balancer to expose your services with Azure Kubernetes Service (AKS).
services: container-service
author: iainfoulds
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 07/12/2018
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 123fc08995416e0ff9c7e12a526deadc34b3a4a2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866169"
---
# <a name="use-an-internal-load-balancer-with-azure-kubernetes-service-aks"></a><span data-ttu-id="5ea6c-103">Use an internal load balancer with Azure Kubernetes Service (AKS)</span><span class="sxs-lookup"><span data-stu-id="5ea6c-103">Use an internal load balancer with Azure Kubernetes Service (AKS)</span></span>

<span data-ttu-id="5ea6c-104">Internal load balancing makes a Kubernetes service accessible to applications running in the same virtual network as the Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="5ea6c-104">Internal load balancing makes a Kubernetes service accessible to applications running in the same virtual network as the Kubernetes cluster.</span></span> <span data-ttu-id="5ea6c-105">This article shows you how to create and use an internal load balancer with Azure Kubernetes Service (AKS).</span><span class="sxs-lookup"><span data-stu-id="5ea6c-105">This article shows you how to create and use an internal load balancer with Azure Kubernetes Service (AKS).</span></span> <span data-ttu-id="5ea6c-106">Azure Load Balancer is available in two SKUs: Basic and Standard.</span><span class="sxs-lookup"><span data-stu-id="5ea6c-106">Azure Load Balancer is available in two SKUs: Basic and Standard.</span></span> <span data-ttu-id="5ea6c-107">AKS uses the Basic SKU.</span><span class="sxs-lookup"><span data-stu-id="5ea6c-107">AKS uses the Basic SKU.</span></span>

## <a name="create-an-internal-load-balancer"></a><span data-ttu-id="5ea6c-108">Create an internal load balancer</span><span class="sxs-lookup"><span data-stu-id="5ea6c-108">Create an internal load balancer</span></span>

<span data-ttu-id="5ea6c-109">To create an internal load balancer, create a service manifest with the service type *LoadBalancer* and the *azure-load-balancer-internal* annotation as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="5ea6c-109">To create an internal load balancer, create a service manifest with the service type *LoadBalancer* and the *azure-load-balancer-internal* annotation as shown in the following example:</span></span>

```yaml
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-front
  annotations:
    service.beta.kubernetes.io/azure-load-balancer-internal: "true"
spec:
  type: LoadBalancer
  ports:
  - port: 80
  selector:
    app: azure-vote-front
```

<span data-ttu-id="5ea6c-110">Once deployed with `kubetctl apply`, an Azure load balancer is created and made available on the same virtual network as the AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="5ea6c-110">Once deployed with `kubetctl apply`, an Azure load balancer is created and made available on the same virtual network as the AKS cluster.</span></span>

![Image of AKS internal load balancer](media/internal-lb/internal-lb.png)

<span data-ttu-id="5ea6c-112">When you view the service details, the IP address in the *EXTERNAL-IP* column is the IP address of the internal load balancer, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="5ea6c-112">When you view the service details, the IP address in the *EXTERNAL-IP* column is the IP address of the internal load balancer, as shown in the following example:</span></span>

```
$ kubectl get service azure-vote-front

NAME               TYPE           CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
azure-vote-front   LoadBalancer   10.0.248.59   10.240.0.7    80:30555/TCP   10s
```

## <a name="specify-an-ip-address"></a><span data-ttu-id="5ea6c-113">Specify an IP address</span><span class="sxs-lookup"><span data-stu-id="5ea6c-113">Specify an IP address</span></span>

<span data-ttu-id="5ea6c-114">If you would like to use a specific IP address with the internal load balancer, add the *loadBalancerIP* property to the load balancer spec. The specified IP address must reside in the same subnet as the AKS cluster and must not already be assigned to a resource.</span><span class="sxs-lookup"><span data-stu-id="5ea6c-114">If you would like to use a specific IP address with the internal load balancer, add the *loadBalancerIP* property to the load balancer spec. The specified IP address must reside in the same subnet as the AKS cluster and must not already be assigned to a resource.</span></span>

```yaml
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-front
  annotations:
    service.beta.kubernetes.io/azure-load-balancer-internal: "true"
spec:
  type: LoadBalancer
  loadBalancerIP: 10.240.0.25
  ports:
  - port: 80
  selector:
    app: azure-vote-front
```

<span data-ttu-id="5ea6c-115">When you view the service details, the IP address on the *EXTERNAL-IP* reflects the specified IP address:</span><span class="sxs-lookup"><span data-stu-id="5ea6c-115">When you view the service details, the IP address on the *EXTERNAL-IP* reflects the specified IP address:</span></span>

```
$ kubectl get service azure-vote-front

NAME               TYPE           CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE
azure-vote-front   LoadBalancer   10.0.184.168   10.240.0.25   80:30225/TCP   4m
```

## <a name="use-private-networks"></a><span data-ttu-id="5ea6c-116">Use private networks</span><span class="sxs-lookup"><span data-stu-id="5ea6c-116">Use private networks</span></span>

<span data-ttu-id="5ea6c-117">When you create your AKS cluster, you can specify advanced networking settings.</span><span class="sxs-lookup"><span data-stu-id="5ea6c-117">When you create your AKS cluster, you can specify advanced networking settings.</span></span> <span data-ttu-id="5ea6c-118">This approach lets you deploy the cluster into an existing Azure virtual network and subnets.</span><span class="sxs-lookup"><span data-stu-id="5ea6c-118">This approach lets you deploy the cluster into an existing Azure virtual network and subnets.</span></span> <span data-ttu-id="5ea6c-119">One scenario is to deploy your AKS cluster into a private network connected to your on-premises environment and run services only accessible internally.</span><span class="sxs-lookup"><span data-stu-id="5ea6c-119">One scenario is to deploy your AKS cluster into a private network connected to your on-premises environment and run services only accessible internally.</span></span> <span data-ttu-id="5ea6c-120">For more information, see [advanced network configuration in AKS][advanced-networking].</span><span class="sxs-lookup"><span data-stu-id="5ea6c-120">For more information, see [advanced network configuration in AKS][advanced-networking].</span></span>

<span data-ttu-id="5ea6c-121">No changes to the previous steps are needed to deploy an internal load balancer in an AKS cluster that uses a private network.</span><span class="sxs-lookup"><span data-stu-id="5ea6c-121">No changes to the previous steps are needed to deploy an internal load balancer in an AKS cluster that uses a private network.</span></span> <span data-ttu-id="5ea6c-122">The load balancer is created in the same resource group as your AKS cluster but connected to your private virtual network and subnet, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="5ea6c-122">The load balancer is created in the same resource group as your AKS cluster but connected to your private virtual network and subnet, as shown in the following example:</span></span>

```
$ kubectl get service azure-vote-front

NAME               TYPE           CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
azure-vote-front   LoadBalancer   10.1.15.188   10.0.0.35     80:31669/TCP   1m
```

> [!NOTE]
> <span data-ttu-id="5ea6c-123">You may need to grant the service principal for your AKS cluster the *Network Contributor* role to the resource group where your Azure virtual network resources are deployed.</span><span class="sxs-lookup"><span data-stu-id="5ea6c-123">You may need to grant the service principal for your AKS cluster the *Network Contributor* role to the resource group where your Azure virtual network resources are deployed.</span></span> <span data-ttu-id="5ea6c-124">View the service principal with [az aks show][az-aks-show], such as `az aks show --resource-group myResourceGroup --name myAKSCluster --query "servicePrincipalProfile.clientId"`.</span><span class="sxs-lookup"><span data-stu-id="5ea6c-124">View the service principal with [az aks show][az-aks-show], such as `az aks show --resource-group myResourceGroup --name myAKSCluster --query "servicePrincipalProfile.clientId"`.</span></span> <span data-ttu-id="5ea6c-125">To create a role assignment, use the [az role assignment create][az-role-assignment-create] command.</span><span class="sxs-lookup"><span data-stu-id="5ea6c-125">To create a role assignment, use the [az role assignment create][az-role-assignment-create] command.</span></span>

## <a name="specify-a-different-subnet"></a><span data-ttu-id="5ea6c-126">Specify a different subnet</span><span class="sxs-lookup"><span data-stu-id="5ea6c-126">Specify a different subnet</span></span>

<span data-ttu-id="5ea6c-127">To specify a subnet for your load balancer, add the *azure-load-balancer-internal-subnet* annotation to your service.</span><span class="sxs-lookup"><span data-stu-id="5ea6c-127">To specify a subnet for your load balancer, add the *azure-load-balancer-internal-subnet* annotation to your service.</span></span> <span data-ttu-id="5ea6c-128">The subnet specified must be in the same virtual network as your AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="5ea6c-128">The subnet specified must be in the same virtual network as your AKS cluster.</span></span> <span data-ttu-id="5ea6c-129">When deployed, the load balancer *EXTERNAL-IP* address is part of the specified subnet.</span><span class="sxs-lookup"><span data-stu-id="5ea6c-129">When deployed, the load balancer *EXTERNAL-IP* address is part of the specified subnet.</span></span>

```yaml
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-front
  annotations:
    service.beta.kubernetes.io/azure-load-balancer-internal: "true"
    service.beta.kubernetes.io/azure-load-balancer-internal-subnet: "apps-subnet"
spec:
  type: LoadBalancer
  ports:
  - port: 80
  selector:
    app: azure-vote-front
```

## <a name="delete-the-load-balancer"></a><span data-ttu-id="5ea6c-130">Delete the load balancer</span><span class="sxs-lookup"><span data-stu-id="5ea6c-130">Delete the load balancer</span></span>

<span data-ttu-id="5ea6c-131">When all services that use the internal load balancer are deleted, the load balancer itself is also deleted.</span><span class="sxs-lookup"><span data-stu-id="5ea6c-131">When all services that use the internal load balancer are deleted, the load balancer itself is also deleted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ea6c-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="5ea6c-132">Next steps</span></span>

<span data-ttu-id="5ea6c-133">Learn more about Kubernetes services at the [Kubernetes services documentation][kubernetes-services].</span><span class="sxs-lookup"><span data-stu-id="5ea6c-133">Learn more about Kubernetes services at the [Kubernetes services documentation][kubernetes-services].</span></span>

<!-- LINKS - External -->
[kubernetes-services]: https://kubernetes.io/docs/concepts/services-networking/service/

<!-- LINKS - Internal -->
[advanced-networking]: networking-overview.md
[deploy-advanced-networking]: networking-overview.md#configure-networking---cli
[az-aks-show]: /cli/azure/aks#az-aks-show
[az-role-assignment-create]: /cli/azure/role/assignment#az-role-assignment-create