---
title: Whitelist Egress Traffic from Azure Kubernetes Service (AKS) cluster
description: Whitelist egress traffic from an Azure Kubernetes Service (AKS) cluster
services: container-service
author: iainfoulds
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 05/23/2018
ms.author: iainfou
ms.openlocfilehash: e2793a72fcbc20b79bdd564e331426fedf1ae34b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865672"
---
# <a name="azure-kubernetes-service-aks-egress"></a><span data-ttu-id="5db55-103">Azure Kubernetes Service (AKS) egress</span><span class="sxs-lookup"><span data-stu-id="5db55-103">Azure Kubernetes Service (AKS) egress</span></span>

<span data-ttu-id="5db55-104">By default, the egress address from an Azure Kubernetes Service (AKS) cluster is randomly assigned.</span><span class="sxs-lookup"><span data-stu-id="5db55-104">By default, the egress address from an Azure Kubernetes Service (AKS) cluster is randomly assigned.</span></span> <span data-ttu-id="5db55-105">This configuration is not ideal when needing to identify an IP address for accessing external services.</span><span class="sxs-lookup"><span data-stu-id="5db55-105">This configuration is not ideal when needing to identify an IP address for accessing external services.</span></span> <span data-ttu-id="5db55-106">This document details how to create and maintain a statically assigned egress IP address in an AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="5db55-106">This document details how to create and maintain a statically assigned egress IP address in an AKS cluster.</span></span>

## <a name="egress-overview"></a><span data-ttu-id="5db55-107">Egress overview</span><span class="sxs-lookup"><span data-stu-id="5db55-107">Egress overview</span></span>

<span data-ttu-id="5db55-108">Outbound traffic from an AKS cluster follows Azure Load Balancer conventions, which are documented [here][outbound-connections].</span><span class="sxs-lookup"><span data-stu-id="5db55-108">Outbound traffic from an AKS cluster follows Azure Load Balancer conventions, which are documented [here][outbound-connections].</span></span> <span data-ttu-id="5db55-109">Before the first Kubernetes service of type `LoadBalancer` is created, the agent nodes are not part of any Azure Load Balancer pool.</span><span class="sxs-lookup"><span data-stu-id="5db55-109">Before the first Kubernetes service of type `LoadBalancer` is created, the agent nodes are not part of any Azure Load Balancer pool.</span></span> <span data-ttu-id="5db55-110">In this configuration, the nodes are without an instance level Public IP address.</span><span class="sxs-lookup"><span data-stu-id="5db55-110">In this configuration, the nodes are without an instance level Public IP address.</span></span> <span data-ttu-id="5db55-111">Azure translates the outbound flow to a public source IP address that is not configurable or deterministic.</span><span class="sxs-lookup"><span data-stu-id="5db55-111">Azure translates the outbound flow to a public source IP address that is not configurable or deterministic.</span></span>

<span data-ttu-id="5db55-112">Once a Kubernetes service of type `LoadBalancer` is created, agent nodes are added to an Azure Load Balancer pool.</span><span class="sxs-lookup"><span data-stu-id="5db55-112">Once a Kubernetes service of type `LoadBalancer` is created, agent nodes are added to an Azure Load Balancer pool.</span></span> <span data-ttu-id="5db55-113">For outbound flow, Azure translates it to the first public IP address configured on the load balancer.</span><span class="sxs-lookup"><span data-stu-id="5db55-113">For outbound flow, Azure translates it to the first public IP address configured on the load balancer.</span></span>

## <a name="create-a-static-public-ip"></a><span data-ttu-id="5db55-114">Create a static public IP</span><span class="sxs-lookup"><span data-stu-id="5db55-114">Create a static public IP</span></span>

<span data-ttu-id="5db55-115">To prevent random IP addresses from being used, create a static IP address and ensure the load balancer uses this address.</span><span class="sxs-lookup"><span data-stu-id="5db55-115">To prevent random IP addresses from being used, create a static IP address and ensure the load balancer uses this address.</span></span> <span data-ttu-id="5db55-116">The IP address needs to be created in the AKS **node** resource group.</span><span class="sxs-lookup"><span data-stu-id="5db55-116">The IP address needs to be created in the AKS **node** resource group.</span></span>

<span data-ttu-id="5db55-117">Get the resource group name with the [az resource show][az-resource-show] command.</span><span class="sxs-lookup"><span data-stu-id="5db55-117">Get the resource group name with the [az resource show][az-resource-show] command.</span></span> <span data-ttu-id="5db55-118">Update the resource group name and cluster name to match your environment.</span><span class="sxs-lookup"><span data-stu-id="5db55-118">Update the resource group name and cluster name to match your environment.</span></span>

```
$ az resource show --resource-group myResourceGroup --name myAKSCluster --resource-type Microsoft.ContainerService/managedClusters --query properties.nodeResourceGroup -o tsv

MC_myResourceGroup_myAKSCluster_eastus
```

<span data-ttu-id="5db55-119">Next, use the [az network public-ip create][public-ip-create] command to create a static public IP address.</span><span class="sxs-lookup"><span data-stu-id="5db55-119">Next, use the [az network public-ip create][public-ip-create] command to create a static public IP address.</span></span> <span data-ttu-id="5db55-120">Update the resource group name to match the name gatherred in the last step.</span><span class="sxs-lookup"><span data-stu-id="5db55-120">Update the resource group name to match the name gatherred in the last step.</span></span>

```console
$ az network public-ip create --resource-group MC_myResourceGroup_myAKSCluster_eastus --name myAKSPublicIP --allocation-method static --query publicIp.ipAddress -o table

Result
-------------
23.101.128.81
```

## <a name="create-a-service-with-the-static-ip"></a><span data-ttu-id="5db55-121">Create a service with the static IP</span><span class="sxs-lookup"><span data-stu-id="5db55-121">Create a service with the static IP</span></span>

<span data-ttu-id="5db55-122">Now that you have an IP address, create a Kubernetes service with the type `LoadBalancer` and assign the IP address to the service.</span><span class="sxs-lookup"><span data-stu-id="5db55-122">Now that you have an IP address, create a Kubernetes service with the type `LoadBalancer` and assign the IP address to the service.</span></span>

<span data-ttu-id="5db55-123">Create a file named `egress-service.yaml` and copy in the following YAML.</span><span class="sxs-lookup"><span data-stu-id="5db55-123">Create a file named `egress-service.yaml` and copy in the following YAML.</span></span> <span data-ttu-id="5db55-124">Update the IP address to match your environment.</span><span class="sxs-lookup"><span data-stu-id="5db55-124">Update the IP address to match your environment.</span></span>

```yaml
apiVersion: v1
kind: Service
metadata:
  name: aks-egress
spec:
  loadBalancerIP: 23.101.128.81
  type: LoadBalancer
  ports:
  - port: 8080
```

<span data-ttu-id="5db55-125">Create the service and deployment with the `kubectl apply` command.</span><span class="sxs-lookup"><span data-stu-id="5db55-125">Create the service and deployment with the `kubectl apply` command.</span></span>

```console
$ kubectl apply -f egress-service.yaml

service "aks-egress" created
```

<span data-ttu-id="5db55-126">Creating this service configures a new frontend IP on the Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="5db55-126">Creating this service configures a new frontend IP on the Azure Load Balancer.</span></span> <span data-ttu-id="5db55-127">If you do not have any other IPs configured, then **all** egress traffic should now use this address.</span><span class="sxs-lookup"><span data-stu-id="5db55-127">If you do not have any other IPs configured, then **all** egress traffic should now use this address.</span></span> <span data-ttu-id="5db55-128">When multiple addresses are configured on the Azure Load Balancer, egress uses the first IP on that load balancer.</span><span class="sxs-lookup"><span data-stu-id="5db55-128">When multiple addresses are configured on the Azure Load Balancer, egress uses the first IP on that load balancer.</span></span>

## <a name="verify-egress-address"></a><span data-ttu-id="5db55-129">Verify egress address</span><span class="sxs-lookup"><span data-stu-id="5db55-129">Verify egress address</span></span>

<span data-ttu-id="5db55-130">To verify that the public IP address is being used, use a service such as `checkip.dyndns.org`.</span><span class="sxs-lookup"><span data-stu-id="5db55-130">To verify that the public IP address is being used, use a service such as `checkip.dyndns.org`.</span></span>

<span data-ttu-id="5db55-131">Start and attach to a pod:</span><span class="sxs-lookup"><span data-stu-id="5db55-131">Start and attach to a pod:</span></span>

```console
$ kubectl run -it --rm aks-ip --image=debian
```

<span data-ttu-id="5db55-132">If needed, install curl in the container:</span><span class="sxs-lookup"><span data-stu-id="5db55-132">If needed, install curl in the container:</span></span>

```console
$ apt-get update && apt-get install curl -y
```

<span data-ttu-id="5db55-133">Curl `checkip.dyndns.org`, which returns the egress IP address:</span><span class="sxs-lookup"><span data-stu-id="5db55-133">Curl `checkip.dyndns.org`, which returns the egress IP address:</span></span>

```console
$ curl -s checkip.dyndns.org

<html><head><title>Current IP Check</title></head><body>Current IP Address: 23.101.128.81</body></html>
```

<span data-ttu-id="5db55-134">You should see that the IP address matches the static IP address attached to the Azure load balancer.</span><span class="sxs-lookup"><span data-stu-id="5db55-134">You should see that the IP address matches the static IP address attached to the Azure load balancer.</span></span>

## <a name="ingress-controller"></a><span data-ttu-id="5db55-135">Ingress controller</span><span class="sxs-lookup"><span data-stu-id="5db55-135">Ingress controller</span></span>

<span data-ttu-id="5db55-136">To avoid maintaining multiple public IP addresses on the Azure Load Balancer, consider using an ingress controller.</span><span class="sxs-lookup"><span data-stu-id="5db55-136">To avoid maintaining multiple public IP addresses on the Azure Load Balancer, consider using an ingress controller.</span></span> <span data-ttu-id="5db55-137">Ingress-controllers provide benefits such as load balancing, SSL/TLS termination, support for URI rewrites, and upstream SSL/TLS encryption.</span><span class="sxs-lookup"><span data-stu-id="5db55-137">Ingress-controllers provide benefits such as load balancing, SSL/TLS termination, support for URI rewrites, and upstream SSL/TLS encryption.</span></span> <span data-ttu-id="5db55-138">For more information about ingress-controllers in AKS, see the [Configure NGINX ingress controller in an AKS cluster][ingress-aks-cluster] guide.</span><span class="sxs-lookup"><span data-stu-id="5db55-138">For more information about ingress-controllers in AKS, see the [Configure NGINX ingress controller in an AKS cluster][ingress-aks-cluster] guide.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5db55-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="5db55-139">Next steps</span></span>

<span data-ttu-id="5db55-140">Learn more about the software demonstrated in this document.</span><span class="sxs-lookup"><span data-stu-id="5db55-140">Learn more about the software demonstrated in this document.</span></span>

- <span data-ttu-id="5db55-141">[Helm CLI][helm-cli-install]</span><span class="sxs-lookup"><span data-stu-id="5db55-141">[Helm CLI][helm-cli-install]</span></span>
- <span data-ttu-id="5db55-142">[NGINX ingress controller][nginx-ingress]</span><span class="sxs-lookup"><span data-stu-id="5db55-142">[NGINX ingress controller][nginx-ingress]</span></span>
- <span data-ttu-id="5db55-143">[Azure Load Balancer Outbound Connections][outbound-connections]</span><span class="sxs-lookup"><span data-stu-id="5db55-143">[Azure Load Balancer Outbound Connections][outbound-connections]</span></span>

<!-- LINKS - internal -->
[az-resource-show]: /cli/azure/resource#az-resource-show
[azure-cli-install]: /cli/azure/install-azure-cli
[azure-cloud-shell]: ../cloud-shell/overview.md
[aks-faq-resource-group]: faq.md#why-are-two-resource-groups-created-with-aks
[create-aks-cluster]: ./kubernetes-walkthrough.md
[helm-cli-install]: ./kubernetes-helm.md#install-helm-cli
[ingress-aks-cluster]: ./ingress-basic.md
[outbound-connections]: ../load-balancer/load-balancer-outbound-connections.md#scenarios
[public-ip-create]: /cli/azure/network/public-ip#az-network-public-ip-create

<!-- LINKS - external -->
[nginx-ingress]: https://github.com/kubernetes/ingress-nginx
