---
title: Upgrade an Azure Kubernetes Service (AKS) cluster
description: Upgrade an Azure Kubernetes Service (AKS) cluster
services: container-service
author: gabrtv
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 07/18/2018
ms.author: gamonroy
ms.custom: mvc
ms.openlocfilehash: 4ff2b56afc4496b6344735b4e3c813b06cee17e3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856295"
---
# <a name="upgrade-an-azure-kubernetes-service-aks-cluster"></a><span data-ttu-id="f7079-103">Upgrade an Azure Kubernetes Service (AKS) cluster</span><span class="sxs-lookup"><span data-stu-id="f7079-103">Upgrade an Azure Kubernetes Service (AKS) cluster</span></span>

<span data-ttu-id="f7079-104">Azure Kubernetes Service (AKS) makes it easy to perform common management tasks including upgrading Kubernetes clusters.</span><span class="sxs-lookup"><span data-stu-id="f7079-104">Azure Kubernetes Service (AKS) makes it easy to perform common management tasks including upgrading Kubernetes clusters.</span></span>

## <a name="upgrade-an-aks-cluster"></a><span data-ttu-id="f7079-105">Upgrade an AKS cluster</span><span class="sxs-lookup"><span data-stu-id="f7079-105">Upgrade an AKS cluster</span></span>

<span data-ttu-id="f7079-106">Before upgrading a cluster, use the `az aks get-upgrades` command to check which Kubernetes releases are available for upgrade.</span><span class="sxs-lookup"><span data-stu-id="f7079-106">Before upgrading a cluster, use the `az aks get-upgrades` command to check which Kubernetes releases are available for upgrade.</span></span>

```azurecli-interactive
az aks get-upgrades --name myAKSCluster --resource-group myResourceGroup --output table
```

<span data-ttu-id="f7079-107">Output:</span><span class="sxs-lookup"><span data-stu-id="f7079-107">Output:</span></span>

```console
Name     ResourceGroup    MasterVersion    NodePoolVersion    Upgrades
-------  ---------------  ---------------  -----------------  -------------------
default  mytestaks007     1.8.10           1.8.10             1.9.1, 1.9.2, 1.9.6
```

<span data-ttu-id="f7079-108">We have three versions available for upgrade: 1.9.1, 1.9.2 and 1.9.6.</span><span class="sxs-lookup"><span data-stu-id="f7079-108">We have three versions available for upgrade: 1.9.1, 1.9.2 and 1.9.6.</span></span> <span data-ttu-id="f7079-109">We can use the `az aks upgrade` command to upgrade to the latest available version.</span><span class="sxs-lookup"><span data-stu-id="f7079-109">We can use the `az aks upgrade` command to upgrade to the latest available version.</span></span>  <span data-ttu-id="f7079-110">During the upgrade process, AKS will add a new node to the cluster, then carefully [cordon and drain][kubernetes-drain] one node at a time to minimize disruption to running applications.</span><span class="sxs-lookup"><span data-stu-id="f7079-110">During the upgrade process, AKS will add a new node to the cluster, then carefully [cordon and drain][kubernetes-drain] one node at a time to minimize disruption to running applications.</span></span>

> [!NOTE]
> <span data-ttu-id="f7079-111">When upgrading an AKS cluster, Kubernetes minor versions cannot be skipped.</span><span class="sxs-lookup"><span data-stu-id="f7079-111">When upgrading an AKS cluster, Kubernetes minor versions cannot be skipped.</span></span> <span data-ttu-id="f7079-112">For example, upgrades between 1.8.x -> 1.9.x or 1.9.x -> 1.10.x are allowed, however 1.8 -> 1.10 is not.</span><span class="sxs-lookup"><span data-stu-id="f7079-112">For example, upgrades between 1.8.x -> 1.9.x or 1.9.x -> 1.10.x are allowed, however 1.8 -> 1.10 is not.</span></span> <span data-ttu-id="f7079-113">To upgrade, from 1.8 -> 1.10, you need to upgrade first from 1.8 -> 1.9 and then another do another upgrade from 1.9 -> 1.10</span><span class="sxs-lookup"><span data-stu-id="f7079-113">To upgrade, from 1.8 -> 1.10, you need to upgrade first from 1.8 -> 1.9 and then another do another upgrade from 1.9 -> 1.10</span></span>

```azurecli-interactive
az aks upgrade --name myAKSCluster --resource-group myResourceGroup --kubernetes-version 1.9.6
```

<span data-ttu-id="f7079-114">Output:</span><span class="sxs-lookup"><span data-stu-id="f7079-114">Output:</span></span>

```json
{
  "id": "/subscriptions/<Subscription ID>/resourcegroups/myResourceGroup/providers/Microsoft.ContainerService/managedClusters/myAKSCluster",
  "location": "eastus",
  "name": "myAKSCluster",
  "properties": {
    "accessProfiles": {
      "clusterAdmin": {
        "kubeConfig": "..."
      },
      "clusterUser": {
        "kubeConfig": "..."
      }
    },
    "agentPoolProfiles": [
      {
        "count": 1,
        "dnsPrefix": null,
        "fqdn": null,
        "name": "myAKSCluster",
        "osDiskSizeGb": null,
        "osType": "Linux",
        "ports": null,
        "storageProfile": "ManagedDisks",
        "vmSize": "Standard_D2_v2",
        "vnetSubnetId": null
      }
    ],
    "dnsPrefix": "myK8sClust-myResourceGroup-4f48ee",
    "fqdn": "myk8sclust-myresourcegroup-4f48ee-406cc140.hcp.eastus.azmk8s.io",
    "kubernetesVersion": "1.9.6",
    "linuxProfile": {
      "adminUsername": "azureuser",
      "ssh": {
        "publicKeys": [
          {
            "keyData": "..."
          }
        ]
      }
    },
    "provisioningState": "Succeeded",
    "servicePrincipalProfile": {
      "clientId": "e70c1c1c-0ca4-4e0a-be5e-aea5225af017",
      "keyVaultSecretRef": null,
      "secret": null
    }
  },
  "resourceGroup": "myResourceGroup",
  "tags": null,
  "type": "Microsoft.ContainerService/ManagedClusters"
}
```

<span data-ttu-id="f7079-115">Confirm that the upgrade was successful with the `az aks show` command.</span><span class="sxs-lookup"><span data-stu-id="f7079-115">Confirm that the upgrade was successful with the `az aks show` command.</span></span>

```azurecli-interactive
az aks show --name myAKSCluster --resource-group myResourceGroup --output table
```

<span data-ttu-id="f7079-116">Output:</span><span class="sxs-lookup"><span data-stu-id="f7079-116">Output:</span></span>

```json
Name          Location    ResourceGroup    KubernetesVersion    ProvisioningState    Fqdn
------------  ----------  ---------------  -------------------  -------------------  ----------------------------------------------------------------
myAKSCluster  eastus     myResourceGroup  1.9.6                 Succeeded            myk8sclust-myresourcegroup-3762d8-2f6ca801.hcp.eastus.azmk8s.io
```

## <a name="next-steps"></a><span data-ttu-id="f7079-117">Next steps</span><span class="sxs-lookup"><span data-stu-id="f7079-117">Next steps</span></span>

<span data-ttu-id="f7079-118">Learn more about deploying and managing AKS with the AKS tutorials.</span><span class="sxs-lookup"><span data-stu-id="f7079-118">Learn more about deploying and managing AKS with the AKS tutorials.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="f7079-119">[AKS Tutorial][aks-tutorial-prepare-app]</span><span class="sxs-lookup"><span data-stu-id="f7079-119">[AKS Tutorial][aks-tutorial-prepare-app]</span></span>

<!-- LINKS - external -->
[kubernetes-drain]: https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/

<!-- LINKS - internal -->
[aks-tutorial-prepare-app]: ./tutorial-kubernetes-prepare-app.md
