---
title: Use Azure Disks with AKS
description: Use Azure Disks with AKS
services: container-service
author: iainfoulds
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 05/21/2018
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 82e7d287ffa533fdc9c222bec22487c20705e4fb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867962"
---
# <a name="volumes-with-azure-disks"></a><span data-ttu-id="0220a-103">Volumes with Azure disks</span><span class="sxs-lookup"><span data-stu-id="0220a-103">Volumes with Azure disks</span></span>

<span data-ttu-id="0220a-104">Container-based applications often need to access and persist data in an external data volume.</span><span class="sxs-lookup"><span data-stu-id="0220a-104">Container-based applications often need to access and persist data in an external data volume.</span></span> <span data-ttu-id="0220a-105">Azure disks can be used as this external data store.</span><span class="sxs-lookup"><span data-stu-id="0220a-105">Azure disks can be used as this external data store.</span></span> <span data-ttu-id="0220a-106">This article details using an Azure disk as a Kubernetes volume in an Azure Kubernetes Service (AKS) cluster.</span><span class="sxs-lookup"><span data-stu-id="0220a-106">This article details using an Azure disk as a Kubernetes volume in an Azure Kubernetes Service (AKS) cluster.</span></span>

<span data-ttu-id="0220a-107">For more information on Kubernetes volumes, see [Kubernetes volumes][kubernetes-volumes].</span><span class="sxs-lookup"><span data-stu-id="0220a-107">For more information on Kubernetes volumes, see [Kubernetes volumes][kubernetes-volumes].</span></span>

## <a name="create-an-azure-disk"></a><span data-ttu-id="0220a-108">Create an Azure disk</span><span class="sxs-lookup"><span data-stu-id="0220a-108">Create an Azure disk</span></span>

<span data-ttu-id="0220a-109">Before mounting an Azure-managed disk as a Kubernetes volume, the disk must exist in the AKS **node** resource group.</span><span class="sxs-lookup"><span data-stu-id="0220a-109">Before mounting an Azure-managed disk as a Kubernetes volume, the disk must exist in the AKS **node** resource group.</span></span> <span data-ttu-id="0220a-110">Get the resource group name with the [az resource show][az-resource-show] command.</span><span class="sxs-lookup"><span data-stu-id="0220a-110">Get the resource group name with the [az resource show][az-resource-show] command.</span></span>

```azurecli-interactive
$ az resource show --resource-group myResourceGroup --name myAKSCluster --resource-type Microsoft.ContainerService/managedClusters --query properties.nodeResourceGroup -o tsv

MC_myResourceGroup_myAKSCluster_eastus
```

<span data-ttu-id="0220a-111">Use the [az disk create][az-disk-create] command to create the Azure disk.</span><span class="sxs-lookup"><span data-stu-id="0220a-111">Use the [az disk create][az-disk-create] command to create the Azure disk.</span></span>

<span data-ttu-id="0220a-112">Update `--resource-group` with the name of the resource group gathered in the last step, and `--name` to a name of your choice.</span><span class="sxs-lookup"><span data-stu-id="0220a-112">Update `--resource-group` with the name of the resource group gathered in the last step, and `--name` to a name of your choice.</span></span>

```azurecli-interactive
az disk create \
  --resource-group MC_myResourceGroup_myAKSCluster_eastus \
  --name myAKSDisk  \
  --size-gb 20 \
  --query id --output tsv
```

<span data-ttu-id="0220a-113">Once the disk has been created, you should see output similar to the following.</span><span class="sxs-lookup"><span data-stu-id="0220a-113">Once the disk has been created, you should see output similar to the following.</span></span> <span data-ttu-id="0220a-114">This value is the disk ID, which is used when mounting the disk.</span><span class="sxs-lookup"><span data-stu-id="0220a-114">This value is the disk ID, which is used when mounting the disk.</span></span>

```console
/subscriptions/<subscriptionID>/resourceGroups/MC_myAKSCluster_myAKSCluster_eastus/providers/Microsoft.Compute/disks/myAKSDisk
```
> [!NOTE]
> <span data-ttu-id="0220a-115">Azure managed disks are billed by SKU for a specific size.</span><span class="sxs-lookup"><span data-stu-id="0220a-115">Azure managed disks are billed by SKU for a specific size.</span></span> <span data-ttu-id="0220a-116">These SKUs range from 32GiB for S4 or P4 disks to 4TiB for S50 or P50 disks.</span><span class="sxs-lookup"><span data-stu-id="0220a-116">These SKUs range from 32GiB for S4 or P4 disks to 4TiB for S50 or P50 disks.</span></span> <span data-ttu-id="0220a-117">Furthermore, the throughput and IOPS performance of a Premium managed disk depends on both the SKU and the instance size of the nodes in the AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="0220a-117">Furthermore, the throughput and IOPS performance of a Premium managed disk depends on both the SKU and the instance size of the nodes in the AKS cluster.</span></span> <span data-ttu-id="0220a-118">See [Pricing and Performance of Managed Disks][managed-disk-pricing-performance].</span><span class="sxs-lookup"><span data-stu-id="0220a-118">See [Pricing and Performance of Managed Disks][managed-disk-pricing-performance].</span></span>

> [!NOTE]
> <span data-ttu-id="0220a-119">If you need to create the disk in a separate resource group, you also need to add the Azure Kubernetes Service (AKS) service principal for your cluster to the resource group holding the disk with the `Contributor` role.</span><span class="sxs-lookup"><span data-stu-id="0220a-119">If you need to create the disk in a separate resource group, you also need to add the Azure Kubernetes Service (AKS) service principal for your cluster to the resource group holding the disk with the `Contributor` role.</span></span> 
>

## <a name="mount-disk-as-volume"></a><span data-ttu-id="0220a-120">Mount disk as volume</span><span class="sxs-lookup"><span data-stu-id="0220a-120">Mount disk as volume</span></span>

<span data-ttu-id="0220a-121">Mount the Azure disk into your pod by configuring the volume in the container spec.</span><span class="sxs-lookup"><span data-stu-id="0220a-121">Mount the Azure disk into your pod by configuring the volume in the container spec.</span></span>

<span data-ttu-id="0220a-122">Create a new file named `azure-disk-pod.yaml` with the following contents.</span><span class="sxs-lookup"><span data-stu-id="0220a-122">Create a new file named `azure-disk-pod.yaml` with the following contents.</span></span> <span data-ttu-id="0220a-123">Update `diskName` with the name of the newly created disk and `diskURI` with the disk ID.</span><span class="sxs-lookup"><span data-stu-id="0220a-123">Update `diskName` with the name of the newly created disk and `diskURI` with the disk ID.</span></span> <span data-ttu-id="0220a-124">Also, take note of the `mountPath`, which is the path where the Azure disk is mounted in the pod.</span><span class="sxs-lookup"><span data-stu-id="0220a-124">Also, take note of the `mountPath`, which is the path where the Azure disk is mounted in the pod.</span></span>

```yaml
apiVersion: v1
kind: Pod
metadata:
 name: azure-disk-pod
spec:
 containers:
  - image: microsoft/sample-aks-helloworld
    name: azure
    volumeMounts:
      - name: azure
        mountPath: /mnt/azure
 volumes:
      - name: azure
        azureDisk:
          kind: Managed
          diskName: myAKSDisk
          diskURI: /subscriptions/<subscriptionID>/resourceGroups/MC_myAKSCluster_myAKSCluster_eastus/providers/Microsoft.Compute/disks/myAKSDisk
```

<span data-ttu-id="0220a-125">Use kubectl to create the pod.</span><span class="sxs-lookup"><span data-stu-id="0220a-125">Use kubectl to create the pod.</span></span>

```azurecli-interactive
kubectl apply -f azure-disk-pod.yaml
```

<span data-ttu-id="0220a-126">You now have a running pod with an Azure disk mounted at the `/mnt/azure`.</span><span class="sxs-lookup"><span data-stu-id="0220a-126">You now have a running pod with an Azure disk mounted at the `/mnt/azure`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0220a-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="0220a-127">Next steps</span></span>

<span data-ttu-id="0220a-128">Learn more about Kubernetes volumes using Azure disks.</span><span class="sxs-lookup"><span data-stu-id="0220a-128">Learn more about Kubernetes volumes using Azure disks.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="0220a-129">[Kubernetes plugin for Azure Disks][kubernetes-disks]</span><span class="sxs-lookup"><span data-stu-id="0220a-129">[Kubernetes plugin for Azure Disks][kubernetes-disks]</span></span>

<!-- LINKS - external -->
[kubernetes-disks]: https://github.com/kubernetes/examples/blob/master/staging/volumes/azure_disk/README.md
[kubernetes-volumes]: https://kubernetes.io/docs/concepts/storage/volumes/
[managed-disk-pricing-performance]: https://azure.microsoft.com/pricing/details/managed-disks/

<!-- LINKS - internal -->
[az-disk-list]: /cli/azure/disk#az-disk-list
[az-disk-create]: /cli/azure/disk#az-disk-create
[az-group-list]: /cli/azure/group#az-group-list
[az-resource-show]: /cli/azure/resource#az-resource-show
