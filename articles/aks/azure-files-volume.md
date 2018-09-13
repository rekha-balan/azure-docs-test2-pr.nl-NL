---
title: Use Azure File with AKS
description: Use Azure Disks with AKS
services: container-service
author: iainfoulds
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 03/08/2018
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 8136c939e33465bf3284a9c9521d2dde4609ea4d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864493"
---
# <a name="volumes-with-azure-files"></a><span data-ttu-id="403d1-103">Volumes with Azure files</span><span class="sxs-lookup"><span data-stu-id="403d1-103">Volumes with Azure files</span></span>

<span data-ttu-id="403d1-104">Container-based applications often need to access and persist data in an external data volume.</span><span class="sxs-lookup"><span data-stu-id="403d1-104">Container-based applications often need to access and persist data in an external data volume.</span></span> <span data-ttu-id="403d1-105">Azure files can be used as this external data store.</span><span class="sxs-lookup"><span data-stu-id="403d1-105">Azure files can be used as this external data store.</span></span> <span data-ttu-id="403d1-106">This article details using Azure files as a Kubernetes volume in Azure Kubernetes Service.</span><span class="sxs-lookup"><span data-stu-id="403d1-106">This article details using Azure files as a Kubernetes volume in Azure Kubernetes Service.</span></span>

<span data-ttu-id="403d1-107">For more information on Kubernetes volumes, see [Kubernetes volumes][kubernetes-volumes].</span><span class="sxs-lookup"><span data-stu-id="403d1-107">For more information on Kubernetes volumes, see [Kubernetes volumes][kubernetes-volumes].</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="403d1-108">Create an Azure file share</span><span class="sxs-lookup"><span data-stu-id="403d1-108">Create an Azure file share</span></span>

<span data-ttu-id="403d1-109">Before using an Azure File Share as a Kubernetes volume, you must create an Azure Storage account and the file share.</span><span class="sxs-lookup"><span data-stu-id="403d1-109">Before using an Azure File Share as a Kubernetes volume, you must create an Azure Storage account and the file share.</span></span> <span data-ttu-id="403d1-110">The following script can be used to complete these tasks.</span><span class="sxs-lookup"><span data-stu-id="403d1-110">The following script can be used to complete these tasks.</span></span> <span data-ttu-id="403d1-111">Take note or update the parameter values, some of these are needed when creating the Kubernetes volume.</span><span class="sxs-lookup"><span data-stu-id="403d1-111">Take note or update the parameter values, some of these are needed when creating the Kubernetes volume.</span></span>

```azurecli-interactive
#!/bin/bash

# Change these four parameters
AKS_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
AKS_PERS_RESOURCE_GROUP=myAKSShare
AKS_PERS_LOCATION=eastus
AKS_PERS_SHARE_NAME=aksshare

# Create the Resource Group
az group create --name $AKS_PERS_RESOURCE_GROUP --location $AKS_PERS_LOCATION

# Create the storage account
az storage account create -n $AKS_PERS_STORAGE_ACCOUNT_NAME -g $AKS_PERS_RESOURCE_GROUP -l $AKS_PERS_LOCATION --sku Standard_LRS

# Export the connection string as an environment variable, this is used when creating the Azure file share
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string -n $AKS_PERS_STORAGE_ACCOUNT_NAME -g $AKS_PERS_RESOURCE_GROUP -o tsv`

# Create the file share
az storage share create -n $AKS_PERS_SHARE_NAME

# Get storage account key
STORAGE_KEY=$(az storage account keys list --resource-group $AKS_PERS_RESOURCE_GROUP --account-name $AKS_PERS_STORAGE_ACCOUNT_NAME --query "[0].value" -o tsv)

# Echo storage account name and key
echo Storage account name: $AKS_PERS_STORAGE_ACCOUNT_NAME
echo Storage account key: $STORAGE_KEY
```

## <a name="create-kubernetes-secret"></a><span data-ttu-id="403d1-112">Create Kubernetes Secret</span><span class="sxs-lookup"><span data-stu-id="403d1-112">Create Kubernetes Secret</span></span>

<span data-ttu-id="403d1-113">Kubernetes needs credentials to access the file share.</span><span class="sxs-lookup"><span data-stu-id="403d1-113">Kubernetes needs credentials to access the file share.</span></span> <span data-ttu-id="403d1-114">These credentials are stored in a [Kubernetes secret][kubernetes-secret], which is referenced when creating a Kubernetes pod.</span><span class="sxs-lookup"><span data-stu-id="403d1-114">These credentials are stored in a [Kubernetes secret][kubernetes-secret], which is referenced when creating a Kubernetes pod.</span></span>

<span data-ttu-id="403d1-115">Use the following command to create the secret.</span><span class="sxs-lookup"><span data-stu-id="403d1-115">Use the following command to create the secret.</span></span> <span data-ttu-id="403d1-116">Replace `STORAGE_ACCOUNT_NAME` with your storage account name, and `STORAGE_ACCOUNT_KEY` with your storage key.</span><span class="sxs-lookup"><span data-stu-id="403d1-116">Replace `STORAGE_ACCOUNT_NAME` with your storage account name, and `STORAGE_ACCOUNT_KEY` with your storage key.</span></span>

```console
kubectl create secret generic azure-secret --from-literal=azurestorageaccountname=STORAGE_ACCOUNT_NAME --from-literal=azurestorageaccountkey=STORAGE_ACCOUNT_KEY
```

## <a name="mount-file-share-as-volume"></a><span data-ttu-id="403d1-117">Mount file share as volume</span><span class="sxs-lookup"><span data-stu-id="403d1-117">Mount file share as volume</span></span>

<span data-ttu-id="403d1-118">Mount your Azure Files share into your pod by configuring the volume in its spec. Create a new file named `azure-files-pod.yaml` with the following contents.</span><span class="sxs-lookup"><span data-stu-id="403d1-118">Mount your Azure Files share into your pod by configuring the volume in its spec. Create a new file named `azure-files-pod.yaml` with the following contents.</span></span> <span data-ttu-id="403d1-119">Update `aksshare` with the name given to the Azure Files share.</span><span class="sxs-lookup"><span data-stu-id="403d1-119">Update `aksshare` with the name given to the Azure Files share.</span></span>

```yaml
apiVersion: v1
kind: Pod
metadata:
 name: azure-files-pod
spec:
 containers:
  - image: microsoft/sample-aks-helloworld
    name: azure
    volumeMounts:
      - name: azure
        mountPath: /mnt/azure
 volumes:
  - name: azure
    azureFile:
      secretName: azure-secret
      shareName: aksshare
      readOnly: false
```

<span data-ttu-id="403d1-120">Use kubectl to create a pod.</span><span class="sxs-lookup"><span data-stu-id="403d1-120">Use kubectl to create a pod.</span></span>

```azurecli-interactive
kubectl apply -f azure-files-pod.yaml
```

<span data-ttu-id="403d1-121">You now have a running container with your Azure file share mounted in the `/mnt/azure` directory.</span><span class="sxs-lookup"><span data-stu-id="403d1-121">You now have a running container with your Azure file share mounted in the `/mnt/azure` directory.</span></span>  <span data-ttu-id="403d1-122">You can see the volume mount when inspecting your pod via `kubectl describe pod azure-files-pod`.</span><span class="sxs-lookup"><span data-stu-id="403d1-122">You can see the volume mount when inspecting your pod via `kubectl describe pod azure-files-pod`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="403d1-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="403d1-123">Next steps</span></span>

<span data-ttu-id="403d1-124">Learn more about Kubernetes volumes using Azure Files.</span><span class="sxs-lookup"><span data-stu-id="403d1-124">Learn more about Kubernetes volumes using Azure Files.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="403d1-125">[Kubernetes plugin for Azure Files][kubernetes-files]</span><span class="sxs-lookup"><span data-stu-id="403d1-125">[Kubernetes plugin for Azure Files][kubernetes-files]</span></span>

<!-- LINKS - external -->
[kubectl-create]: https://kubernetes.io/docs/user-guide/kubectl/v1.8/#create
[kubernetes-files]: https://github.com/kubernetes/examples/blob/master/staging/volumes/azure_file/README.md
[kubernetes-secret]: https://kubernetes.io/docs/concepts/configuration/secret/
[kubernetes-volumes]: https://kubernetes.io/docs/concepts/storage/volumes/

<!-- LINKS - internal -->
[az-group-create]: /cli/azure/group#az-group-create
[az-storage-create]: /cli/azure/storage/account#az-storage-account-create
[az-storage-key-list]: /cli/azure/storage/account/keys#az-storage-account-keys-list
[az-storage-share-create]: /cli/azure/storage/share#az-storage-share-create
