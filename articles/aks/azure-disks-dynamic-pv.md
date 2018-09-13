---
title: Create persistent volumes with Azure Kubernetes Service
description: Learn how to use Azure disks to create persistent volumes for pods in Azure Kubernetes Service (AKS)
services: container-service
author: iainfoulds
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 07/20/2018
ms.author: iainfou
ms.openlocfilehash: 7048ab4e08d25fd5181857a4e7592d0bcb7d3b5f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867773"
---
# <a name="create-persistent-volumes-with-azure-disks-for-azure-kubernetes-service-aks"></a><span data-ttu-id="6b4f8-103">Create persistent volumes with Azure disks for Azure Kubernetes Service (AKS)</span><span class="sxs-lookup"><span data-stu-id="6b4f8-103">Create persistent volumes with Azure disks for Azure Kubernetes Service (AKS)</span></span>

<span data-ttu-id="6b4f8-104">A persistent volume represents a piece of storage that has been provisioned for use with Kubernetes pods.</span><span class="sxs-lookup"><span data-stu-id="6b4f8-104">A persistent volume represents a piece of storage that has been provisioned for use with Kubernetes pods.</span></span> <span data-ttu-id="6b4f8-105">A persistent volume can be used by one or many pods and can be dynamically or statically provisioned.</span><span class="sxs-lookup"><span data-stu-id="6b4f8-105">A persistent volume can be used by one or many pods and can be dynamically or statically provisioned.</span></span> <span data-ttu-id="6b4f8-106">For more information on Kubernetes persistent volumes, see [Kubernetes persistent volumes][kubernetes-volumes].</span><span class="sxs-lookup"><span data-stu-id="6b4f8-106">For more information on Kubernetes persistent volumes, see [Kubernetes persistent volumes][kubernetes-volumes].</span></span> <span data-ttu-id="6b4f8-107">This article shows you how to use persistent volumes with Azure disks in an Azure Kubernetes Service (AKS) cluster.</span><span class="sxs-lookup"><span data-stu-id="6b4f8-107">This article shows you how to use persistent volumes with Azure disks in an Azure Kubernetes Service (AKS) cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="6b4f8-108">An Azure disk can only be mounted with *Access mode* type *ReadWriteOnce*, which makes it available to only a single AKS node.</span><span class="sxs-lookup"><span data-stu-id="6b4f8-108">An Azure disk can only be mounted with *Access mode* type *ReadWriteOnce*, which makes it available to only a single AKS node.</span></span> <span data-ttu-id="6b4f8-109">If needing to share a persistent volume across multiple nodes, consider using [Azure Files][azure-files-pvc].</span><span class="sxs-lookup"><span data-stu-id="6b4f8-109">If needing to share a persistent volume across multiple nodes, consider using [Azure Files][azure-files-pvc].</span></span>

## <a name="built-in-storage-classes"></a><span data-ttu-id="6b4f8-110">Built in storage classes</span><span class="sxs-lookup"><span data-stu-id="6b4f8-110">Built in storage classes</span></span>

<span data-ttu-id="6b4f8-111">A storage class is used to define how a unit of storage is dynamically created with a persistent volume.</span><span class="sxs-lookup"><span data-stu-id="6b4f8-111">A storage class is used to define how a unit of storage is dynamically created with a persistent volume.</span></span> <span data-ttu-id="6b4f8-112">For more information on Kubernetes storage classes, see [Kubernetes Storage Classes][kubernetes-storage-classes].</span><span class="sxs-lookup"><span data-stu-id="6b4f8-112">For more information on Kubernetes storage classes, see [Kubernetes Storage Classes][kubernetes-storage-classes].</span></span>

<span data-ttu-id="6b4f8-113">Each AKS cluster includes two pre-created storage classes, both configured to work with Azure disks:</span><span class="sxs-lookup"><span data-stu-id="6b4f8-113">Each AKS cluster includes two pre-created storage classes, both configured to work with Azure disks:</span></span>

* <span data-ttu-id="6b4f8-114">The *default* storage class provisions a standard Azure disk.</span><span class="sxs-lookup"><span data-stu-id="6b4f8-114">The *default* storage class provisions a standard Azure disk.</span></span>
    * <span data-ttu-id="6b4f8-115">Standard storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span><span class="sxs-lookup"><span data-stu-id="6b4f8-115">Standard storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="6b4f8-116">Standard disks are ideal for a cost effective dev and test workload.</span><span class="sxs-lookup"><span data-stu-id="6b4f8-116">Standard disks are ideal for a cost effective dev and test workload.</span></span>
* <span data-ttu-id="6b4f8-117">The *managed-premium* storage class provisions a premium Azure disk.</span><span class="sxs-lookup"><span data-stu-id="6b4f8-117">The *managed-premium* storage class provisions a premium Azure disk.</span></span>
    * <span data-ttu-id="6b4f8-118">Premium disks are backed by SSD-based high-performance, low-latency disk.</span><span class="sxs-lookup"><span data-stu-id="6b4f8-118">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="6b4f8-119">Perfect for VMs running production workload.</span><span class="sxs-lookup"><span data-stu-id="6b4f8-119">Perfect for VMs running production workload.</span></span> <span data-ttu-id="6b4f8-120">If the AKS nodes in your cluster use premium storage, select the *managed-premium* class.</span><span class="sxs-lookup"><span data-stu-id="6b4f8-120">If the AKS nodes in your cluster use premium storage, select the *managed-premium* class.</span></span>

<span data-ttu-id="6b4f8-121">Use the [kubectl get sc][kubectl-get] command to see the pre-created storage classes.</span><span class="sxs-lookup"><span data-stu-id="6b4f8-121">Use the [kubectl get sc][kubectl-get] command to see the pre-created storage classes.</span></span> <span data-ttu-id="6b4f8-122">The following example shows the pre-create storage classes available within an AKS cluster:</span><span class="sxs-lookup"><span data-stu-id="6b4f8-122">The following example shows the pre-create storage classes available within an AKS cluster:</span></span>

```
$ kubectl get sc

NAME                PROVISIONER                AGE
default (default)   kubernetes.io/azure-disk   1h
managed-premium     kubernetes.io/azure-disk   1h
```

> [!NOTE]
> <span data-ttu-id="6b4f8-123">Persistent volume claims are specified in GiB but Azure managed disks are billed by SKU for a specific size.</span><span class="sxs-lookup"><span data-stu-id="6b4f8-123">Persistent volume claims are specified in GiB but Azure managed disks are billed by SKU for a specific size.</span></span> <span data-ttu-id="6b4f8-124">These SKUs range from 32GiB for S4 or P4 disks to 4TiB for S50 or P50 disks.</span><span class="sxs-lookup"><span data-stu-id="6b4f8-124">These SKUs range from 32GiB for S4 or P4 disks to 4TiB for S50 or P50 disks.</span></span> <span data-ttu-id="6b4f8-125">The throughput and IOPS performance of a Premium managed disk depends on the both the SKU and the instance size of the nodes in the AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="6b4f8-125">The throughput and IOPS performance of a Premium managed disk depends on the both the SKU and the instance size of the nodes in the AKS cluster.</span></span> <span data-ttu-id="6b4f8-126">For more information, see [Pricing and Performance of Managed Disks][managed-disk-pricing-performance].</span><span class="sxs-lookup"><span data-stu-id="6b4f8-126">For more information, see [Pricing and Performance of Managed Disks][managed-disk-pricing-performance].</span></span>

## <a name="create-a-persistent-volume-claim"></a><span data-ttu-id="6b4f8-127">Create a persistent volume claim</span><span class="sxs-lookup"><span data-stu-id="6b4f8-127">Create a persistent volume claim</span></span>

<span data-ttu-id="6b4f8-128">A persistent volume claim (PVC) is used to automatically provision storage based on a storage class.</span><span class="sxs-lookup"><span data-stu-id="6b4f8-128">A persistent volume claim (PVC) is used to automatically provision storage based on a storage class.</span></span> <span data-ttu-id="6b4f8-129">In this case, a PVC can use one of the pre-created storage classes to create a standard or premium Azure managed disk.</span><span class="sxs-lookup"><span data-stu-id="6b4f8-129">In this case, a PVC can use one of the pre-created storage classes to create a standard or premium Azure managed disk.</span></span>

<span data-ttu-id="6b4f8-130">Create a file named `azure-premium.yaml`, and copy in the following manifest.</span><span class="sxs-lookup"><span data-stu-id="6b4f8-130">Create a file named `azure-premium.yaml`, and copy in the following manifest.</span></span> <span data-ttu-id="6b4f8-131">The claim requests a disk named `azure-managed-disk` that is *5GB* in size with *ReadWriteOnce* access.</span><span class="sxs-lookup"><span data-stu-id="6b4f8-131">The claim requests a disk named `azure-managed-disk` that is *5GB* in size with *ReadWriteOnce* access.</span></span> <span data-ttu-id="6b4f8-132">The *managed-premium* storage class is specified as the storage class.</span><span class="sxs-lookup"><span data-stu-id="6b4f8-132">The *managed-premium* storage class is specified as the storage class.</span></span>

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: azure-managed-disk
spec:
  accessModes:
  - ReadWriteOnce
  storageClassName: managed-premium
  resources:
    requests:
      storage: 5Gi
```

> [!TIP]
> <span data-ttu-id="6b4f8-133">To create a disk that uses standard storage, use `storageClassName: default` rather than *managed-premium*.</span><span class="sxs-lookup"><span data-stu-id="6b4f8-133">To create a disk that uses standard storage, use `storageClassName: default` rather than *managed-premium*.</span></span>

<span data-ttu-id="6b4f8-134">Create the persistent volume claim with the [kubectl create][kubectl-create] command and specify your *azure-premium.yaml* file:</span><span class="sxs-lookup"><span data-stu-id="6b4f8-134">Create the persistent volume claim with the [kubectl create][kubectl-create] command and specify your *azure-premium.yaml* file:</span></span>

```
$ kubectl create -f azure-premium.yaml

persistentvolumeclaim/azure-managed-disk created
```

## <a name="use-the-persistent-volume"></a><span data-ttu-id="6b4f8-135">Use the persistent volume</span><span class="sxs-lookup"><span data-stu-id="6b4f8-135">Use the persistent volume</span></span>

<span data-ttu-id="6b4f8-136">Once the persistent volume claim has been created and the disk successfully provisioned, a pod can be created with access to the disk.</span><span class="sxs-lookup"><span data-stu-id="6b4f8-136">Once the persistent volume claim has been created and the disk successfully provisioned, a pod can be created with access to the disk.</span></span> <span data-ttu-id="6b4f8-137">The following manifest creates a basic NGINX pod that uses the persistent volume claim named *azure-managed-disk* to mount the Azure disk at the path `/mnt/azure`.</span><span class="sxs-lookup"><span data-stu-id="6b4f8-137">The following manifest creates a basic NGINX pod that uses the persistent volume claim named *azure-managed-disk* to mount the Azure disk at the path `/mnt/azure`.</span></span>

<span data-ttu-id="6b4f8-138">Create a file named `azure-pvc-disk.yaml`, and copy in the following manifest.</span><span class="sxs-lookup"><span data-stu-id="6b4f8-138">Create a file named `azure-pvc-disk.yaml`, and copy in the following manifest.</span></span>

```yaml
kind: Pod
apiVersion: v1
metadata:
  name: mypod
spec:
  containers:
    - name: myfrontend
      image: nginx
      volumeMounts:
      - mountPath: "/mnt/azure"
        name: volume
  volumes:
    - name: volume
      persistentVolumeClaim:
        claimName: azure-managed-disk
```

<span data-ttu-id="6b4f8-139">Create the pod with the [kubectl create][kubectl-create] command, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="6b4f8-139">Create the pod with the [kubectl create][kubectl-create] command, as shown in the following example:</span></span>

```
$ kubectl create -f azure-pvc-disk.yaml

pod/mypod created
```

<span data-ttu-id="6b4f8-140">You now have a running pod with your Azure disk mounted in the `/mnt/azure` directory.</span><span class="sxs-lookup"><span data-stu-id="6b4f8-140">You now have a running pod with your Azure disk mounted in the `/mnt/azure` directory.</span></span> <span data-ttu-id="6b4f8-141">This configuration can be seen when inspecting your pod via `kubectl describe pod mypod`, as shown in the following condensed example:</span><span class="sxs-lookup"><span data-stu-id="6b4f8-141">This configuration can be seen when inspecting your pod via `kubectl describe pod mypod`, as shown in the following condensed example:</span></span>

```
$ kubectl describe pod mypod

[...]
Volumes:
  volume:
    Type:       PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace)
    ClaimName:  azure-managed-disk
    ReadOnly:   false
  default-token-smm2n:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-smm2n
    Optional:    false

Events:
  Type    Reason                 Age   From                               Message
  ----    ------                 ----  ----                               -------
  Normal  Scheduled              2m    default-scheduler                  Successfully assigned mypod to aks-nodepool1-79590246-0
  Normal  SuccessfulMountVolume  2m    kubelet, aks-nodepool1-79590246-0  MountVolume.SetUp succeeded for volume "default-token-smm2n"
  Normal  SuccessfulMountVolume  1m    kubelet, aks-nodepool1-79590246-0  MountVolume.SetUp succeeded for volume "pvc-faf0f176-8b8d-11e8-923b-deb28c58d242"
[...]
```

## <a name="back-up-a-persistent-volume"></a><span data-ttu-id="6b4f8-142">Back up a persistent volume</span><span class="sxs-lookup"><span data-stu-id="6b4f8-142">Back up a persistent volume</span></span>

<span data-ttu-id="6b4f8-143">To back up the data in your persistent volume, take a snapshot of the managed disk for the volume.</span><span class="sxs-lookup"><span data-stu-id="6b4f8-143">To back up the data in your persistent volume, take a snapshot of the managed disk for the volume.</span></span> <span data-ttu-id="6b4f8-144">You can then use this snapshot to create a restored disk and attach to pods as a means of restoring the data.</span><span class="sxs-lookup"><span data-stu-id="6b4f8-144">You can then use this snapshot to create a restored disk and attach to pods as a means of restoring the data.</span></span>

<span data-ttu-id="6b4f8-145">First, get the volume name with the `kubectl get pvc` command, such as for the PVC named *azure-managed-disk*:</span><span class="sxs-lookup"><span data-stu-id="6b4f8-145">First, get the volume name with the `kubectl get pvc` command, such as for the PVC named *azure-managed-disk*:</span></span>

```
$ kubectl get pvc azure-managed-disk

NAME                 STATUS    VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS      AGE
azure-managed-disk   Bound     pvc-faf0f176-8b8d-11e8-923b-deb28c58d242   5Gi        RWO            managed-premium   3m
```

<span data-ttu-id="6b4f8-146">This volume name forms the underlying Azure disk name.</span><span class="sxs-lookup"><span data-stu-id="6b4f8-146">This volume name forms the underlying Azure disk name.</span></span> <span data-ttu-id="6b4f8-147">Query for the disk ID with [az disk list][az-disk-list] and provide your PVC volume name, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="6b4f8-147">Query for the disk ID with [az disk list][az-disk-list] and provide your PVC volume name, as shown in the following example:</span></span>

```
$ az disk list --query '[].id | [?contains(@,`pvc-faf0f176-8b8d-11e8-923b-deb28c58d242`)]' -o tsv

/subscriptions/<guid>/resourceGroups/MC_MYRESOURCEGROUP_MYAKSCLUSTER_EASTUS/providers/MicrosoftCompute/disks/kubernetes-dynamic-pvc-faf0f176-8b8d-11e8-923b-deb28c58d242
```

<span data-ttu-id="6b4f8-148">Use the disk ID to create a snapshot disk with [az snapshot create][az-snapshot-create].</span><span class="sxs-lookup"><span data-stu-id="6b4f8-148">Use the disk ID to create a snapshot disk with [az snapshot create][az-snapshot-create].</span></span> <span data-ttu-id="6b4f8-149">The following example creates a snapshot named *pvcSnapshot* in the same resource group as the AKS cluster (*MC_myResourceGroup_myAKSCluster_eastus*).</span><span class="sxs-lookup"><span data-stu-id="6b4f8-149">The following example creates a snapshot named *pvcSnapshot* in the same resource group as the AKS cluster (*MC_myResourceGroup_myAKSCluster_eastus*).</span></span> <span data-ttu-id="6b4f8-150">You may encounter permission issues if you create snapshots and restore disks in resource groups that the AKS cluster does not have access to.</span><span class="sxs-lookup"><span data-stu-id="6b4f8-150">You may encounter permission issues if you create snapshots and restore disks in resource groups that the AKS cluster does not have access to.</span></span>

```azurecli
$ az snapshot create \
    --resource-group MC_myResourceGroup_myAKSCluster_eastus \
    --name pvcSnapshot \
    --source /subscriptions/<guid>/resourceGroups/MC_myResourceGroup_myAKSCluster_eastus/providers/MicrosoftCompute/disks/kubernetes-dynamic-pvc-faf0f176-8b8d-11e8-923b-deb28c58d242
```

<span data-ttu-id="6b4f8-151">Depending on the amount of data on your disk, it may take a few minutes to create the snapshot.</span><span class="sxs-lookup"><span data-stu-id="6b4f8-151">Depending on the amount of data on your disk, it may take a few minutes to create the snapshot.</span></span>

## <a name="restore-and-use-a-snapshot"></a><span data-ttu-id="6b4f8-152">Restore and use a snapshot</span><span class="sxs-lookup"><span data-stu-id="6b4f8-152">Restore and use a snapshot</span></span>

<span data-ttu-id="6b4f8-153">To restore the disk and use it with a Kubernetes pod, use the snapshot as a source when you create a disk with [az disk create][az-disk-create].</span><span class="sxs-lookup"><span data-stu-id="6b4f8-153">To restore the disk and use it with a Kubernetes pod, use the snapshot as a source when you create a disk with [az disk create][az-disk-create].</span></span> <span data-ttu-id="6b4f8-154">This operation preserves the original resource if you then need to access the original data snapshot.</span><span class="sxs-lookup"><span data-stu-id="6b4f8-154">This operation preserves the original resource if you then need to access the original data snapshot.</span></span> <span data-ttu-id="6b4f8-155">The following example creates a disk named *pvcRestored* from the snapshot named *pvcSnapshot*:</span><span class="sxs-lookup"><span data-stu-id="6b4f8-155">The following example creates a disk named *pvcRestored* from the snapshot named *pvcSnapshot*:</span></span>

```azurecli
az disk create --resource-group MC_myResourceGroup_myAKSCluster_eastus --name pvcRestored --source pvcSnapshot
```

<span data-ttu-id="6b4f8-156">To use the restored disk with a pod, specify the ID of the disk in the manifest.</span><span class="sxs-lookup"><span data-stu-id="6b4f8-156">To use the restored disk with a pod, specify the ID of the disk in the manifest.</span></span> <span data-ttu-id="6b4f8-157">Get the disk ID with the [az disk show][az-disk-show] command.</span><span class="sxs-lookup"><span data-stu-id="6b4f8-157">Get the disk ID with the [az disk show][az-disk-show] command.</span></span> <span data-ttu-id="6b4f8-158">The following example gets the disk ID for *pvcRestored* created in the previous step:</span><span class="sxs-lookup"><span data-stu-id="6b4f8-158">The following example gets the disk ID for *pvcRestored* created in the previous step:</span></span>

```azurecli
az disk show --resource-group MC_myResourceGroup_myAKSCluster_eastus --name pvcRestored --query id -o tsv
```

<span data-ttu-id="6b4f8-159">Create a pod manifest named `azure-restored.yaml` and specify the disk URI obtained in the previous step.</span><span class="sxs-lookup"><span data-stu-id="6b4f8-159">Create a pod manifest named `azure-restored.yaml` and specify the disk URI obtained in the previous step.</span></span> <span data-ttu-id="6b4f8-160">The following example creates a basic NGINX web server, with the restored disk mounted as a volume at */mnt/azure*:</span><span class="sxs-lookup"><span data-stu-id="6b4f8-160">The following example creates a basic NGINX web server, with the restored disk mounted as a volume at */mnt/azure*:</span></span>

```yaml
kind: Pod
apiVersion: v1
metadata:
  name: mypodrestored
spec:
  containers:
    - name: myfrontendrestored
      image: nginx
      volumeMounts:
      - mountPath: "/mnt/azure"
        name: volume
  volumes:
    - name: volume
      azureDisk:
        kind: Managed
        diskName: pvcRestored
        diskURI: /subscriptions/<guid>/resourceGroups/MC_myResourceGroupAKS_myAKSCluster_eastus/providers/Microsoft.Compute/disks/pvcRestored
```

<span data-ttu-id="6b4f8-161">Create the pod with the [kubectl create][kubectl-create] command, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="6b4f8-161">Create the pod with the [kubectl create][kubectl-create] command, as shown in the following example:</span></span>

```
$ kubectl create -f azure-restored.yaml

pod/mypodrestored created
```

<span data-ttu-id="6b4f8-162">You can use `kubectl describe pod mypodrestored` to view details of the pod, such as the following condensed example that shows the volume information:</span><span class="sxs-lookup"><span data-stu-id="6b4f8-162">You can use `kubectl describe pod mypodrestored` to view details of the pod, such as the following condensed example that shows the volume information:</span></span>

```
$ kubectl describe pod mypodrestored

[...]
Volumes:
  volume:
    Type:         AzureDisk (an Azure Data Disk mount on the host and bind mount to the pod)
    DiskName:     pvcRestored
    DiskURI:      /subscriptions/19da35d3-9a1a-4f3b-9b9c-3c56ef409565/resourceGroups/MC_myResourceGroupAKS_myAKSCluster_eastus/providers/Microsoft.Compute/disks/pvcRestored
    Kind:         Managed
    FSType:       ext4
    CachingMode:  ReadWrite
    ReadOnly:     false
[...]
```

## <a name="next-steps"></a><span data-ttu-id="6b4f8-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="6b4f8-163">Next steps</span></span>

<span data-ttu-id="6b4f8-164">Learn more about Kubernetes persistent volumes using Azure disks.</span><span class="sxs-lookup"><span data-stu-id="6b4f8-164">Learn more about Kubernetes persistent volumes using Azure disks.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="6b4f8-165">[Kubernetes plugin for Azure disks][azure-disk-volume]</span><span class="sxs-lookup"><span data-stu-id="6b4f8-165">[Kubernetes plugin for Azure disks][azure-disk-volume]</span></span>

<!-- LINKS - external -->
[access-modes]: https://kubernetes.io/docs/concepts/storage/persistent-volumes/#access-modes
[kubectl-create]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#create
[kubectl-get]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get
[kubernetes-storage-classes]: https://kubernetes.io/docs/concepts/storage/storage-classes/
[kubernetes-volumes]: https://kubernetes.io/docs/concepts/storage/persistent-volumes/
[managed-disk-pricing-performance]: https://azure.microsoft.com/pricing/details/managed-disks/

<!-- LINKS - internal -->
[azure-disk-volume]: azure-disk-volume.md
[azure-files-pvc]: azure-files-dynamic-pv.md
[premium-storage]: ../virtual-machines/windows/premium-storage.md
[az-disk-list]: /cli/azure/disk#az-disk-list
[az-snapshot-create]: /cli/azure/snapshot#az-snapshot-create
[az-disk-create]: /cli/azure/disk#az-disk-create
[az-disk-show]: /cli/azure/disk#az-disk-show
