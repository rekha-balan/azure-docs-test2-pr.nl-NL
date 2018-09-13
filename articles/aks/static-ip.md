---
title: Use a static IP address with the Azure Kubernetes Service (AKS) load balancer
description: Use a static IP address with the Azure Kubernetes Service (AKS) load balancer.
services: container-service
author: iainfoulds
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 05/21/2018
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 87fe014d5c19be675d4f6cac876548a31a4484b4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864846"
---
# <a name="use-a-static-ip-address-with-the-azure-kubernetes-service-aks-load-balancer"></a><span data-ttu-id="36fc8-103">Use a static IP address with the Azure Kubernetes Service (AKS) load balancer</span><span class="sxs-lookup"><span data-stu-id="36fc8-103">Use a static IP address with the Azure Kubernetes Service (AKS) load balancer</span></span>

<span data-ttu-id="36fc8-104">In some cases, such as when the Azure Kubernetes Service (AKS) load balancer is recreated, or Kubernetes services with a type of LoadBalancer are recreated, the public IP address of the Kubernetes service may change.</span><span class="sxs-lookup"><span data-stu-id="36fc8-104">In some cases, such as when the Azure Kubernetes Service (AKS) load balancer is recreated, or Kubernetes services with a type of LoadBalancer are recreated, the public IP address of the Kubernetes service may change.</span></span> <span data-ttu-id="36fc8-105">This document details configuring a static IP address for your Kubernetes services.</span><span class="sxs-lookup"><span data-stu-id="36fc8-105">This document details configuring a static IP address for your Kubernetes services.</span></span>

## <a name="create-static-ip-address"></a><span data-ttu-id="36fc8-106">Create static IP address</span><span class="sxs-lookup"><span data-stu-id="36fc8-106">Create static IP address</span></span>

<span data-ttu-id="36fc8-107">Create a static public IP address for the Kubernetes service.</span><span class="sxs-lookup"><span data-stu-id="36fc8-107">Create a static public IP address for the Kubernetes service.</span></span> <span data-ttu-id="36fc8-108">The IP address needs to be created in the AKS **node** resource group.</span><span class="sxs-lookup"><span data-stu-id="36fc8-108">The IP address needs to be created in the AKS **node** resource group.</span></span> <span data-ttu-id="36fc8-109">Get the resource group name with the [az resource show][az-resource-show] command.</span><span class="sxs-lookup"><span data-stu-id="36fc8-109">Get the resource group name with the [az resource show][az-resource-show] command.</span></span>

```azurecli-interactive
$ az resource show --resource-group myResourceGroup --name myAKSCluster --resource-type Microsoft.ContainerService/managedClusters --query properties.nodeResourceGroup -o tsv

MC_myResourceGroup_myAKSCluster_eastus
```

<span data-ttu-id="36fc8-110">Use the [az network public ip create][az-network-public-ip-create] command to create the IP address.</span><span class="sxs-lookup"><span data-stu-id="36fc8-110">Use the [az network public ip create][az-network-public-ip-create] command to create the IP address.</span></span>

```azurecli-interactive
az network public-ip create --resource-group MC_myResourceGroup_myAKSCluster_eastus --name myAKSPublicIP --allocation-method static
```

<span data-ttu-id="36fc8-111">Take note of the IP address.</span><span class="sxs-lookup"><span data-stu-id="36fc8-111">Take note of the IP address.</span></span>

```json
{
  "publicIp": {
    "dnsSettings": null,
    "etag": "W/\"6b6fb15c-5281-4f64-b332-8f68f46e1358\"",
    "id": "/subscriptions/<SubscriptionID>/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myAKSPublicIP",
    "idleTimeoutInMinutes": 4,
    "ipAddress": "40.121.183.52",
    "ipConfiguration": null,
    "ipTags": [],
    "location": "eastus",
    "name": "myAKSPublicIP",
    "provisioningState": "Succeeded",
    "publicIpAddressVersion": "IPv4",
    "publicIpAllocationMethod": "Static",
    "resourceGroup": "myResourceGroup",
    "resourceGuid": "56ec8760-a3b8-4aeb-a89d-42e68d2cbc8c",
    "sku": {
      "name": "Basic"
    },
    "tags": null,
    "type": "Microsoft.Network/publicIPAddresses",
    "zones": null
  }
````

 <span data-ttu-id="36fc8-112">If needed, the address can be retrieved using the [az network public-ip list][az-network-public-ip-list] command.</span><span class="sxs-lookup"><span data-stu-id="36fc8-112">If needed, the address can be retrieved using the [az network public-ip list][az-network-public-ip-list] command.</span></span>

```azurecli-interactive
az network public-ip list --resource-group MC_myResourceGroup_myAKSCluster_eastus --query [0].ipAddress --output tsv
```

```console
40.121.183.52
```

## <a name="create-service-with-ip-address"></a><span data-ttu-id="36fc8-113">Create service with IP address</span><span class="sxs-lookup"><span data-stu-id="36fc8-113">Create service with IP address</span></span>

<span data-ttu-id="36fc8-114">Once the static IP address has been provisioned, a Kubernetes service can be created with the `loadBalancerIP` property and a value of the static IP address.</span><span class="sxs-lookup"><span data-stu-id="36fc8-114">Once the static IP address has been provisioned, a Kubernetes service can be created with the `loadBalancerIP` property and a value of the static IP address.</span></span>

```yaml
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-front
spec:
  loadBalancerIP: 40.121.183.52
  type: LoadBalancer
  ports:
  - port: 80
  selector:
    app: azure-vote-front
```

## <a name="troubleshooting"></a><span data-ttu-id="36fc8-115">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="36fc8-115">Troubleshooting</span></span>

<span data-ttu-id="36fc8-116">If the static IP address has not been created, or has been created in the wrong resource group, service creation fails.</span><span class="sxs-lookup"><span data-stu-id="36fc8-116">If the static IP address has not been created, or has been created in the wrong resource group, service creation fails.</span></span> <span data-ttu-id="36fc8-117">To troubleshoot, return service creation events with the [kubectl describe][kubectl-describe] command.</span><span class="sxs-lookup"><span data-stu-id="36fc8-117">To troubleshoot, return service creation events with the [kubectl describe][kubectl-describe] command.</span></span>

```azurecli-interactive
kubectl describe service azure-vote-front
```

```console
Name:                     azure-vote-front
Namespace:                default
Labels:                   <none>
Annotations:              <none>
Selector:                 app=azure-vote-front
Type:                     LoadBalancer
IP:                       10.0.18.125
IP:                       40.121.183.52
Port:                     <unset>  80/TCP
TargetPort:               80/TCP
NodePort:                 <unset>  32582/TCP
Endpoints:                <none>
Session Affinity:         None
External Traffic Policy:  Cluster
Events:
  Type     Reason                      Age               From                Message
  ----     ------                      ----              ----                -------
  Normal   CreatingLoadBalancer        7s (x2 over 22s)  service-controller  Creating load balancer
  Warning  CreatingLoadBalancerFailed  6s (x2 over 12s)  service-controller  Error creating load balancer (will retry): Failed to create load balancer for service default/azure-vote-front: user supplied IP Address 40.121.183.52 was not found
```

<!-- LINKS - External -->
[kubectl-describe]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#describe
<!-- LINKS - Internal -->
[aks-faq-resource-group]: faq.md#why-are-two-resource-groups-created-with-aks
[az-network-public-ip-create]: /cli/azure/network/public-ip#az-network-public-ip-create
[az-network-public-ip-list]: /cli/azure/network/public-ip#az-network-public-ip-list
[az-resource-show]: /cli/azure/resource#az-resource-show
