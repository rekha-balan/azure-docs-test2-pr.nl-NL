---
title: Use Azure File with AKS
description: Use Azure Disks with AKS
services: container-service
author: iainfoulds
ms.service: container-service
ms.topic: article
ms.date: 08/15/2018
ms.author: iainfou
ms.openlocfilehash: dfc9171f54effe3da7a0f13695ab233d561357d4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866324"
---
# <a name="persistent-volumes-with-azure-files"></a><span data-ttu-id="779e8-103">Persistent volumes with Azure files</span><span class="sxs-lookup"><span data-stu-id="779e8-103">Persistent volumes with Azure files</span></span>

<span data-ttu-id="779e8-104">A persistent volume is a piece of storage that has been created for use in a Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="779e8-104">A persistent volume is a piece of storage that has been created for use in a Kubernetes cluster.</span></span> <span data-ttu-id="779e8-105">A persistent volume can be used by one or many pods and can be dynamically or statically created.</span><span class="sxs-lookup"><span data-stu-id="779e8-105">A persistent volume can be used by one or many pods and can be dynamically or statically created.</span></span> <span data-ttu-id="779e8-106">This document details **dynamic creation** of an Azure file share as a persistent volume.</span><span class="sxs-lookup"><span data-stu-id="779e8-106">This document details **dynamic creation** of an Azure file share as a persistent volume.</span></span>

<span data-ttu-id="779e8-107">For more information on Kubernetes persistent volumes, including static creation, see [Kubernetes persistent volumes][kubernetes-volumes].</span><span class="sxs-lookup"><span data-stu-id="779e8-107">For more information on Kubernetes persistent volumes, including static creation, see [Kubernetes persistent volumes][kubernetes-volumes].</span></span>

## <a name="create-a-storage-account"></a><span data-ttu-id="779e8-108">Create a storage account</span><span class="sxs-lookup"><span data-stu-id="779e8-108">Create a storage account</span></span>

<span data-ttu-id="779e8-109">When dynamically creating an Azure file share as a Kubernetes volume, any storage account can be used as long as it is in the AKS **node** resource group.</span><span class="sxs-lookup"><span data-stu-id="779e8-109">When dynamically creating an Azure file share as a Kubernetes volume, any storage account can be used as long as it is in the AKS **node** resource group.</span></span> <span data-ttu-id="779e8-110">This group is the one with the *MC_* prefix that was created by the provisioning of the resources for the AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="779e8-110">This group is the one with the *MC_* prefix that was created by the provisioning of the resources for the AKS cluster.</span></span> <span data-ttu-id="779e8-111">Get the resource group name with the [az aks show][az-aks-show] command.</span><span class="sxs-lookup"><span data-stu-id="779e8-111">Get the resource group name with the [az aks show][az-aks-show] command.</span></span>

```azurecli
$ az aks show --resource-group myResourceGroup --name myAKSCluster --query nodeResourceGroup -o tsv

MC_myResourceGroup_myAKSCluster_eastus
```

<span data-ttu-id="779e8-112">Use the [az storage account create][az-storage-account-create] command to create the storage account.</span><span class="sxs-lookup"><span data-stu-id="779e8-112">Use the [az storage account create][az-storage-account-create] command to create the storage account.</span></span>

<span data-ttu-id="779e8-113">Update `--resource-group` with the name of the resource group gathered in the last step, and `--name` to a name of your choice.</span><span class="sxs-lookup"><span data-stu-id="779e8-113">Update `--resource-group` with the name of the resource group gathered in the last step, and `--name` to a name of your choice.</span></span> <span data-ttu-id="779e8-114">Provide your own unique storage account name:</span><span class="sxs-lookup"><span data-stu-id="779e8-114">Provide your own unique storage account name:</span></span>

```azurecli
az storage account create --resource-group MC_myResourceGroup_myAKSCluster_eastus --name mystorageaccount --sku Standard_LRS
```

> [!NOTE]
> <span data-ttu-id="779e8-115">Azure Files currently only work with Standard storage.</span><span class="sxs-lookup"><span data-stu-id="779e8-115">Azure Files currently only work with Standard storage.</span></span> <span data-ttu-id="779e8-116">If you use Premium storage, the volume fails to provision.</span><span class="sxs-lookup"><span data-stu-id="779e8-116">If you use Premium storage, the volume fails to provision.</span></span>

## <a name="create-a-storage-class"></a><span data-ttu-id="779e8-117">Create a storage class</span><span class="sxs-lookup"><span data-stu-id="779e8-117">Create a storage class</span></span>

<span data-ttu-id="779e8-118">A storage class is used to define how an Azure file share is created.</span><span class="sxs-lookup"><span data-stu-id="779e8-118">A storage class is used to define how an Azure file share is created.</span></span> <span data-ttu-id="779e8-119">A storage account can be specified in the class.</span><span class="sxs-lookup"><span data-stu-id="779e8-119">A storage account can be specified in the class.</span></span> <span data-ttu-id="779e8-120">If a storage account is not specified, a *skuName* and *location* must be specified, and all storage accounts in the associated resource group are evaluated for a match.</span><span class="sxs-lookup"><span data-stu-id="779e8-120">If a storage account is not specified, a *skuName* and *location* must be specified, and all storage accounts in the associated resource group are evaluated for a match.</span></span> <span data-ttu-id="779e8-121">For more information on Kubernetes storage classes for Azure Files, see [Kubernetes Storage Classes][kubernetes-storage-classes].</span><span class="sxs-lookup"><span data-stu-id="779e8-121">For more information on Kubernetes storage classes for Azure Files, see [Kubernetes Storage Classes][kubernetes-storage-classes].</span></span>

<span data-ttu-id="779e8-122">Create a file named `azure-file-sc.yaml` and copy in the following example manifest.</span><span class="sxs-lookup"><span data-stu-id="779e8-122">Create a file named `azure-file-sc.yaml` and copy in the following example manifest.</span></span> <span data-ttu-id="779e8-123">Update the *storageAccount* value with the name of your storage account created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="779e8-123">Update the *storageAccount* value with the name of your storage account created in the previous step.</span></span> <span data-ttu-id="779e8-124">For more information on *mountOptions*, see the [Mount options][mount-options] section.</span><span class="sxs-lookup"><span data-stu-id="779e8-124">For more information on *mountOptions*, see the [Mount options][mount-options] section.</span></span>

```yaml
kind: StorageClass
apiVersion: storage.k8s.io/v1
metadata:
  name: azurefile
provisioner: kubernetes.io/azure-file
mountOptions:
  - dir_mode=0777
  - file_mode=0777
  - uid=1000
  - gid=1000
parameters:
  skuName: Standard_LRS
  storageAccount: mystorageaccount
```

<span data-ttu-id="779e8-125">Create the storage class with the [kubectl apply][kubectl-apply] command:</span><span class="sxs-lookup"><span data-stu-id="779e8-125">Create the storage class with the [kubectl apply][kubectl-apply] command:</span></span>

```console
kubectl apply -f azure-file-sc.yaml
```

## <a name="create-a-cluster-role-and-binding"></a><span data-ttu-id="779e8-126">Create a cluster role and binding</span><span class="sxs-lookup"><span data-stu-id="779e8-126">Create a cluster role and binding</span></span>

<span data-ttu-id="779e8-127">AKS clusters use Kubernetes role-based access control (RBAC) to limit actions that can be performed.</span><span class="sxs-lookup"><span data-stu-id="779e8-127">AKS clusters use Kubernetes role-based access control (RBAC) to limit actions that can be performed.</span></span> <span data-ttu-id="779e8-128">*Roles* define the permissions to grant, and *bindings* apply them to desired users.</span><span class="sxs-lookup"><span data-stu-id="779e8-128">*Roles* define the permissions to grant, and *bindings* apply them to desired users.</span></span> <span data-ttu-id="779e8-129">These assignments can be applied to a given namespace, or across the entire cluster.</span><span class="sxs-lookup"><span data-stu-id="779e8-129">These assignments can be applied to a given namespace, or across the entire cluster.</span></span> <span data-ttu-id="779e8-130">For more information, see [Using RBAC authorization][kubernetes-rbac].</span><span class="sxs-lookup"><span data-stu-id="779e8-130">For more information, see [Using RBAC authorization][kubernetes-rbac].</span></span>

<span data-ttu-id="779e8-131">To allow the Azure platform to create the required storage resources, create a *ClusterRole* and *ClusterRoleBinding*.</span><span class="sxs-lookup"><span data-stu-id="779e8-131">To allow the Azure platform to create the required storage resources, create a *ClusterRole* and *ClusterRoleBinding*.</span></span> <span data-ttu-id="779e8-132">Create a file named `azure-pvc-roles.yaml` and copy in the following YAML:</span><span class="sxs-lookup"><span data-stu-id="779e8-132">Create a file named `azure-pvc-roles.yaml` and copy in the following YAML:</span></span>

```yaml
---
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: ClusterRole
metadata:
  name: system:azure-cloud-provider
rules:
- apiGroups: ['']
  resources: ['secrets']
  verbs:     ['get','create']
---
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: ClusterRoleBinding
metadata:
  name: system:azure-cloud-provider
roleRef:
  kind: ClusterRole
  apiGroup: rbac.authorization.k8s.io
  name: system:azure-cloud-provider
subjects:
- kind: ServiceAccount
  name: persistent-volume-binder
  namespace: kube-system
```

<span data-ttu-id="779e8-133">Assign the permissions with the [kubectl apply][kubectl-apply] command:</span><span class="sxs-lookup"><span data-stu-id="779e8-133">Assign the permissions with the [kubectl apply][kubectl-apply] command:</span></span>

```console
kubectl apply -f azure-pvc-roles.yaml
```

## <a name="create-a-persistent-volume-claim"></a><span data-ttu-id="779e8-134">Create a persistent volume claim</span><span class="sxs-lookup"><span data-stu-id="779e8-134">Create a persistent volume claim</span></span>

<span data-ttu-id="779e8-135">A persistent volume claim (PVC) uses the storage class object to dynamically provision an Azure file share.</span><span class="sxs-lookup"><span data-stu-id="779e8-135">A persistent volume claim (PVC) uses the storage class object to dynamically provision an Azure file share.</span></span> <span data-ttu-id="779e8-136">The following YAML can be used to create a persistent volume claim *5GB* in size with *ReadWriteMany* access.</span><span class="sxs-lookup"><span data-stu-id="779e8-136">The following YAML can be used to create a persistent volume claim *5GB* in size with *ReadWriteMany* access.</span></span> <span data-ttu-id="779e8-137">For more information on access modes, see the [Kubernetes persistent volume][access-modes] documentation.</span><span class="sxs-lookup"><span data-stu-id="779e8-137">For more information on access modes, see the [Kubernetes persistent volume][access-modes] documentation.</span></span>

<span data-ttu-id="779e8-138">Now create a file named `azure-file-pvc.yaml` and copy in the following YAML.</span><span class="sxs-lookup"><span data-stu-id="779e8-138">Now create a file named `azure-file-pvc.yaml` and copy in the following YAML.</span></span> <span data-ttu-id="779e8-139">Make sure that the *storageClassName* matches the storage class created in the last step:</span><span class="sxs-lookup"><span data-stu-id="779e8-139">Make sure that the *storageClassName* matches the storage class created in the last step:</span></span>

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: azurefile
spec:
  accessModes:
    - ReadWriteMany
  storageClassName: azurefile
  resources:
    requests:
      storage: 5Gi
```

<span data-ttu-id="779e8-140">Create the persistent volume claim with the [kubectl apply][kubectl-apply] command:</span><span class="sxs-lookup"><span data-stu-id="779e8-140">Create the persistent volume claim with the [kubectl apply][kubectl-apply] command:</span></span>

```console
kubectl apply -f azure-file-pvc.yaml
```

<span data-ttu-id="779e8-141">Once completed, the file share will be created.</span><span class="sxs-lookup"><span data-stu-id="779e8-141">Once completed, the file share will be created.</span></span> <span data-ttu-id="779e8-142">A Kubernetes secret is also created that includes connection information and credentials.</span><span class="sxs-lookup"><span data-stu-id="779e8-142">A Kubernetes secret is also created that includes connection information and credentials.</span></span> <span data-ttu-id="779e8-143">You can use the [kubectl get][kubectl-get] command to view the status of the PVC:</span><span class="sxs-lookup"><span data-stu-id="779e8-143">You can use the [kubectl get][kubectl-get] command to view the status of the PVC:</span></span>

```
$ kubectl get pvc azurefile

NAME        STATUS    VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
azurefile   Bound     pvc-8436e62e-a0d9-11e5-8521-5a8664dc0477   5Gi        RWX            azurefile      5m
```

## <a name="use-the-persistent-volume"></a><span data-ttu-id="779e8-144">Use the persistent volume</span><span class="sxs-lookup"><span data-stu-id="779e8-144">Use the persistent volume</span></span>

<span data-ttu-id="779e8-145">The following YAML creates a pod that uses the persistent volume claim *azurefile* to mount the Azure file share at the */mnt/azure* path.</span><span class="sxs-lookup"><span data-stu-id="779e8-145">The following YAML creates a pod that uses the persistent volume claim *azurefile* to mount the Azure file share at the */mnt/azure* path.</span></span>

<span data-ttu-id="779e8-146">Create a file named `azure-pvc-files.yaml`, and copy in the following YAML.</span><span class="sxs-lookup"><span data-stu-id="779e8-146">Create a file named `azure-pvc-files.yaml`, and copy in the following YAML.</span></span> <span data-ttu-id="779e8-147">Make sure that the *claimName* matches the PVC created in the last step.</span><span class="sxs-lookup"><span data-stu-id="779e8-147">Make sure that the *claimName* matches the PVC created in the last step.</span></span>

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
        claimName: azurefile
```

<span data-ttu-id="779e8-148">Create the pod with the [kubectl apply][kubectl-apply] command.</span><span class="sxs-lookup"><span data-stu-id="779e8-148">Create the pod with the [kubectl apply][kubectl-apply] command.</span></span>

```console
kubectl apply -f azure-pvc-files.yaml
```

<span data-ttu-id="779e8-149">You now have a running pod with your Azure disk mounted in the */mnt/azure* directory.</span><span class="sxs-lookup"><span data-stu-id="779e8-149">You now have a running pod with your Azure disk mounted in the */mnt/azure* directory.</span></span> <span data-ttu-id="779e8-150">This configuration can be seen when inspecting your pod via `kubectl describe pod mypod`.</span><span class="sxs-lookup"><span data-stu-id="779e8-150">This configuration can be seen when inspecting your pod via `kubectl describe pod mypod`.</span></span> <span data-ttu-id="779e8-151">The following condensed example output shows the volume mounted in the container:</span><span class="sxs-lookup"><span data-stu-id="779e8-151">The following condensed example output shows the volume mounted in the container:</span></span>

```
Containers:
  myfrontend:
    Container ID:   docker://053bc9c0df72232d755aa040bfba8b533fa696b123876108dec400e364d2523e
    Image:          nginx
    Image ID:       docker-pullable://nginx@sha256:d85914d547a6c92faa39ce7058bd7529baacab7e0cd4255442b04577c4d1f424
    State:          Running
      Started:      Wed, 15 Aug 2018 22:22:27 +0000
    Ready:          True
    Mounts:
      /mnt/azure from volume (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-8rv4z (ro)
[...]
Volumes:
  volume:
    Type:       PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace)
    ClaimName:  azurefile2
    ReadOnly:   false
[...]
```

## <a name="mount-options"></a><span data-ttu-id="779e8-152">Mount options</span><span class="sxs-lookup"><span data-stu-id="779e8-152">Mount options</span></span>

<span data-ttu-id="779e8-153">Default *fileMode* and *dirMode* values differ between Kubernetes versions as described in the following table.</span><span class="sxs-lookup"><span data-stu-id="779e8-153">Default *fileMode* and *dirMode* values differ between Kubernetes versions as described in the following table.</span></span>

| <span data-ttu-id="779e8-154">version</span><span class="sxs-lookup"><span data-stu-id="779e8-154">version</span></span> | <span data-ttu-id="779e8-155">value</span><span class="sxs-lookup"><span data-stu-id="779e8-155">value</span></span> |
| ---- | ---- |
| <span data-ttu-id="779e8-156">v1.6.x, v1.7.x</span><span class="sxs-lookup"><span data-stu-id="779e8-156">v1.6.x, v1.7.x</span></span> | <span data-ttu-id="779e8-157">0777</span><span class="sxs-lookup"><span data-stu-id="779e8-157">0777</span></span> |
| <span data-ttu-id="779e8-158">v1.8.0-v1.8.5</span><span class="sxs-lookup"><span data-stu-id="779e8-158">v1.8.0-v1.8.5</span></span> | <span data-ttu-id="779e8-159">0700</span><span class="sxs-lookup"><span data-stu-id="779e8-159">0700</span></span> |
| <span data-ttu-id="779e8-160">v1.8.6 or above</span><span class="sxs-lookup"><span data-stu-id="779e8-160">v1.8.6 or above</span></span> | <span data-ttu-id="779e8-161">0755</span><span class="sxs-lookup"><span data-stu-id="779e8-161">0755</span></span> |
| <span data-ttu-id="779e8-162">v1.9.0</span><span class="sxs-lookup"><span data-stu-id="779e8-162">v1.9.0</span></span> | <span data-ttu-id="779e8-163">0700</span><span class="sxs-lookup"><span data-stu-id="779e8-163">0700</span></span> |
| <span data-ttu-id="779e8-164">v1.9.1 or above</span><span class="sxs-lookup"><span data-stu-id="779e8-164">v1.9.1 or above</span></span> | <span data-ttu-id="779e8-165">0755</span><span class="sxs-lookup"><span data-stu-id="779e8-165">0755</span></span> |

<span data-ttu-id="779e8-166">If using a cluster of version 1.8.5 or greater and dynamically creating the persistent volume with a storage class, mount options can be specified on the storage class object.</span><span class="sxs-lookup"><span data-stu-id="779e8-166">If using a cluster of version 1.8.5 or greater and dynamically creating the persistent volume with a storage class, mount options can be specified on the storage class object.</span></span> <span data-ttu-id="779e8-167">The following example sets *0777*:</span><span class="sxs-lookup"><span data-stu-id="779e8-167">The following example sets *0777*:</span></span>

```yaml
kind: StorageClass
apiVersion: storage.k8s.io/v1
metadata:
  name: azurefile
provisioner: kubernetes.io/azure-file
mountOptions:
  - dir_mode=0777
  - file_mode=0777
  - uid=1000
  - gid=1000
parameters:
  skuName: Standard_LRS
```

<span data-ttu-id="779e8-168">If using a cluster of version 1.8.5 or greater and statically creating the persistent volume object, mount options need to be specified on the *PersistentVolume* object.</span><span class="sxs-lookup"><span data-stu-id="779e8-168">If using a cluster of version 1.8.5 or greater and statically creating the persistent volume object, mount options need to be specified on the *PersistentVolume* object.</span></span> <span data-ttu-id="779e8-169">for more information on statically creating a persistent volume, see [Static Persistent Volumes][pv-static].</span><span class="sxs-lookup"><span data-stu-id="779e8-169">for more information on statically creating a persistent volume, see [Static Persistent Volumes][pv-static].</span></span>

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: azurefile
spec:
  capacity:
    storage: 5Gi
  accessModes:
    - ReadWriteMany
  azureFile:
    secretName: azure-secret
    shareName: azurefile
    readOnly: false
  mountOptions:
  - dir_mode=0777
  - file_mode=0777
  - uid=1000
  - gid=1000
  ```

<span data-ttu-id="779e8-170">If using a cluster of version 1.8.0 - 1.8.4, a security context can be specified with the *runAsUser* value set to *0*.</span><span class="sxs-lookup"><span data-stu-id="779e8-170">If using a cluster of version 1.8.0 - 1.8.4, a security context can be specified with the *runAsUser* value set to *0*.</span></span> <span data-ttu-id="779e8-171">For more information on Pod security context, see [Configure a Security Context][kubernetes-security-context].</span><span class="sxs-lookup"><span data-stu-id="779e8-171">For more information on Pod security context, see [Configure a Security Context][kubernetes-security-context].</span></span>

## <a name="next-steps"></a><span data-ttu-id="779e8-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="779e8-172">Next steps</span></span>

<span data-ttu-id="779e8-173">Learn more about Kubernetes persistent volumes using Azure Files.</span><span class="sxs-lookup"><span data-stu-id="779e8-173">Learn more about Kubernetes persistent volumes using Azure Files.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="779e8-174">[Kubernetes plugin for Azure Files][kubernetes-files]</span><span class="sxs-lookup"><span data-stu-id="779e8-174">[Kubernetes plugin for Azure Files][kubernetes-files]</span></span>

<!-- LINKS - external -->
[access-modes]: https://kubernetes.io/docs/concepts/storage/persistent-volumes
[kubectl-apply]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply
[kubectl-describe]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#describe
[kubectl-get]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get
[kubernetes-files]: https://github.com/kubernetes/examples/blob/master/staging/volumes/azure_file/README.md
[kubernetes-secret]: https://kubernetes.io/docs/concepts/configuration/secret/
[kubernetes-security-context]: https://kubernetes.io/docs/tasks/configure-pod-container/security-context/
[kubernetes-storage-classes]: https://kubernetes.io/docs/concepts/storage/storage-classes/#azure-file
[kubernetes-volumes]: https://kubernetes.io/docs/concepts/storage/persistent-volumes/
[pv-static]: https://kubernetes.io/docs/concepts/storage/persistent-volumes/#static
[kubernetes-rbac]: https://kubernetes.io/docs/reference/access-authn-authz/rbac/

<!-- LINKS - internal -->
[az-group-create]: /cli/azure/group#az-group-create
[az-group-list]: /cli/azure/group#az-group-list
[az-resource-show]: /cli/azure/aks#az-aks-show
[az-storage-account-create]: /cli/azure/storage/account#az-storage-account-create
[az-storage-create]: /cli/azure/storage/account#az-storage-account-create
[az-storage-key-list]: /cli/azure/storage/account/keys#az-storage-account-keys-list
[az-storage-share-create]: /cli/azure/storage/share#az-storage-share-create
[mount-options]: #mount-options
