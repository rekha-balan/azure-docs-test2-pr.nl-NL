---
title: Mount an Azure Files volume in Azure Container Instances
description: Learn how to mount an Azure Files volume to persist state with Azure Container Instances
services: container-instances
author: seanmck
manager: jeconnoc
ms.service: container-instances
ms.topic: article
ms.date: 02/20/2018
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 83c86d8310aff80f148e878261ba33b01846006b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967260"
---
# <a name="mount-an-azure-file-share-in-azure-container-instances"></a><span data-ttu-id="c6e22-103">Mount an Azure file share in Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="c6e22-103">Mount an Azure file share in Azure Container Instances</span></span>

<span data-ttu-id="c6e22-104">By default, Azure Container Instances are stateless.</span><span class="sxs-lookup"><span data-stu-id="c6e22-104">By default, Azure Container Instances are stateless.</span></span> <span data-ttu-id="c6e22-105">If the container crashes or stops, all of its state is lost.</span><span class="sxs-lookup"><span data-stu-id="c6e22-105">If the container crashes or stops, all of its state is lost.</span></span> <span data-ttu-id="c6e22-106">To persist state beyond the lifetime of the container, you must mount a volume from an external store.</span><span class="sxs-lookup"><span data-stu-id="c6e22-106">To persist state beyond the lifetime of the container, you must mount a volume from an external store.</span></span> <span data-ttu-id="c6e22-107">This article shows how to mount an Azure file share for use with Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="c6e22-107">This article shows how to mount an Azure file share for use with Azure Container Instances.</span></span>

> [!NOTE]
> <span data-ttu-id="c6e22-108">Mounting an Azure Files share is currently restricted to Linux containers.</span><span class="sxs-lookup"><span data-stu-id="c6e22-108">Mounting an Azure Files share is currently restricted to Linux containers.</span></span> <span data-ttu-id="c6e22-109">While we are working to bring all features to Windows containers, you can find current platform differences in [Quotas and region availability for Azure Container Instances](container-instances-quotas.md).</span><span class="sxs-lookup"><span data-stu-id="c6e22-109">While we are working to bring all features to Windows containers, you can find current platform differences in [Quotas and region availability for Azure Container Instances](container-instances-quotas.md).</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="c6e22-110">Create an Azure file share</span><span class="sxs-lookup"><span data-stu-id="c6e22-110">Create an Azure file share</span></span>

<span data-ttu-id="c6e22-111">Before using an Azure file share with Azure Container Instances, you must create it.</span><span class="sxs-lookup"><span data-stu-id="c6e22-111">Before using an Azure file share with Azure Container Instances, you must create it.</span></span> <span data-ttu-id="c6e22-112">Run the following script to create a storage account to host the file share, and the share itself.</span><span class="sxs-lookup"><span data-stu-id="c6e22-112">Run the following script to create a storage account to host the file share, and the share itself.</span></span> <span data-ttu-id="c6e22-113">The storage account name must be globally unique, so the script adds a random value to the base string.</span><span class="sxs-lookup"><span data-stu-id="c6e22-113">The storage account name must be globally unique, so the script adds a random value to the base string.</span></span>

```azurecli-interactive
# Change these four parameters as needed
ACI_PERS_RESOURCE_GROUP=myResourceGroup
ACI_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
ACI_PERS_LOCATION=eastus
ACI_PERS_SHARE_NAME=acishare

# Create the storage account with the parameters
az storage account create \
    --resource-group $ACI_PERS_RESOURCE_GROUP \
    --name $ACI_PERS_STORAGE_ACCOUNT_NAME \
    --location $ACI_PERS_LOCATION \
    --sku Standard_LRS

# Export the connection string as an environment variable. The following 'az storage share create' command
# references this environment variable when creating the Azure file share.
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string --resource-group $ACI_PERS_RESOURCE_GROUP --name $ACI_PERS_STORAGE_ACCOUNT_NAME --output tsv`

# Create the file share
az storage share create -n $ACI_PERS_SHARE_NAME
```

## <a name="get-storage-credentials"></a><span data-ttu-id="c6e22-114">Get storage credentials</span><span class="sxs-lookup"><span data-stu-id="c6e22-114">Get storage credentials</span></span>

<span data-ttu-id="c6e22-115">To mount an Azure file share as a volume in Azure Container Instances, you need three values: the storage account name, the share name, and the storage access key.</span><span class="sxs-lookup"><span data-stu-id="c6e22-115">To mount an Azure file share as a volume in Azure Container Instances, you need three values: the storage account name, the share name, and the storage access key.</span></span>

<span data-ttu-id="c6e22-116">If you used the script above, the storage account name was created with a random value at the end.</span><span class="sxs-lookup"><span data-stu-id="c6e22-116">If you used the script above, the storage account name was created with a random value at the end.</span></span> <span data-ttu-id="c6e22-117">To query the final string (including the random portion), use the following commands:</span><span class="sxs-lookup"><span data-stu-id="c6e22-117">To query the final string (including the random portion), use the following commands:</span></span>

```azurecli-interactive
STORAGE_ACCOUNT=$(az storage account list --resource-group $ACI_PERS_RESOURCE_GROUP --query "[?contains(name,'$ACI_PERS_STORAGE_ACCOUNT_NAME')].[name]" --output tsv)
echo $STORAGE_ACCOUNT
```

<span data-ttu-id="c6e22-118">The share name is already known (defined as *acishare* in the script above), so all that remains is the storage account key, which can be found using the following command:</span><span class="sxs-lookup"><span data-stu-id="c6e22-118">The share name is already known (defined as *acishare* in the script above), so all that remains is the storage account key, which can be found using the following command:</span></span>

```azurecli-interactive
STORAGE_KEY=$(az storage account keys list --resource-group $ACI_PERS_RESOURCE_GROUP --account-name $STORAGE_ACCOUNT --query "[0].value" --output tsv)
echo $STORAGE_KEY
```

## <a name="deploy-container-and-mount-volume"></a><span data-ttu-id="c6e22-119">Deploy container and mount volume</span><span class="sxs-lookup"><span data-stu-id="c6e22-119">Deploy container and mount volume</span></span>

<span data-ttu-id="c6e22-120">To mount an Azure file share as a volume in a container, specify the share and volume mount point when you create the container with [az container create][az-container-create].</span><span class="sxs-lookup"><span data-stu-id="c6e22-120">To mount an Azure file share as a volume in a container, specify the share and volume mount point when you create the container with [az container create][az-container-create].</span></span> <span data-ttu-id="c6e22-121">If you've followed the previous steps, you can mount the share you created earlier by using the following command to create a container:</span><span class="sxs-lookup"><span data-stu-id="c6e22-121">If you've followed the previous steps, you can mount the share you created earlier by using the following command to create a container:</span></span>

```azurecli-interactive
az container create \
    --resource-group $ACI_PERS_RESOURCE_GROUP \
    --name hellofiles \
    --image microsoft/aci-hellofiles \
    --dns-name-label aci-demo \
    --ports 80 \
    --azure-file-volume-account-name $ACI_PERS_STORAGE_ACCOUNT_NAME \
    --azure-file-volume-account-key $STORAGE_KEY \
    --azure-file-volume-share-name $ACI_PERS_SHARE_NAME \
    --azure-file-volume-mount-path /aci/logs/
```

<span data-ttu-id="c6e22-122">The `--dns-name-label` value must be unique within the Azure region you create the container instance.</span><span class="sxs-lookup"><span data-stu-id="c6e22-122">The `--dns-name-label` value must be unique within the Azure region you create the container instance.</span></span> <span data-ttu-id="c6e22-123">Update the value in the preceding command if you receive a **DNS name label** error message when you execute the command.</span><span class="sxs-lookup"><span data-stu-id="c6e22-123">Update the value in the preceding command if you receive a **DNS name label** error message when you execute the command.</span></span>

## <a name="manage-files-in-mounted-volume"></a><span data-ttu-id="c6e22-124">Manage files in mounted volume</span><span class="sxs-lookup"><span data-stu-id="c6e22-124">Manage files in mounted volume</span></span>

<span data-ttu-id="c6e22-125">Once the container starts up, you can use the simple web app deployed via the [microsoft/aci-hellofiles][aci-hellofiles] image to manage the files in the Azure file share at the mount path you specified.</span><span class="sxs-lookup"><span data-stu-id="c6e22-125">Once the container starts up, you can use the simple web app deployed via the [microsoft/aci-hellofiles][aci-hellofiles] image to manage the files in the Azure file share at the mount path you specified.</span></span> <span data-ttu-id="c6e22-126">Obtain the web app's fully qualified domain name (FQDN) with the [az container show][az-container-show] command:</span><span class="sxs-lookup"><span data-stu-id="c6e22-126">Obtain the web app's fully qualified domain name (FQDN) with the [az container show][az-container-show] command:</span></span>

```azurecli-interactive
az container show --resource-group $ACI_PERS_RESOURCE_GROUP --name hellofiles --query ipAddress.fqdn
```

<span data-ttu-id="c6e22-127">You can use the [Azure portal][portal] or a tool like the [Microsoft Azure Storage Explorer][storage-explorer] to retrieve and inspect the file written to the file share.</span><span class="sxs-lookup"><span data-stu-id="c6e22-127">You can use the [Azure portal][portal] or a tool like the [Microsoft Azure Storage Explorer][storage-explorer] to retrieve and inspect the file written to the file share.</span></span>

## <a name="mount-multiple-volumes"></a><span data-ttu-id="c6e22-128">Mount multiple volumes</span><span class="sxs-lookup"><span data-stu-id="c6e22-128">Mount multiple volumes</span></span>

<span data-ttu-id="c6e22-129">To mount multiple volumes in a container instance, you must deploy using an [Azure Resource Manager template](/azure/templates/microsoft.containerinstance/containergroups).</span><span class="sxs-lookup"><span data-stu-id="c6e22-129">To mount multiple volumes in a container instance, you must deploy using an [Azure Resource Manager template](/azure/templates/microsoft.containerinstance/containergroups).</span></span>

<span data-ttu-id="c6e22-130">First, provide the share details and define the volumes by populating the `volumes` array in the `properties` section of the template.</span><span class="sxs-lookup"><span data-stu-id="c6e22-130">First, provide the share details and define the volumes by populating the `volumes` array in the `properties` section of the template.</span></span> <span data-ttu-id="c6e22-131">For example, if you've created two Azure Files shares named *share1* and *share2* in storage account *myStorageAccount*, the `volumes` array would appear similar to the following:</span><span class="sxs-lookup"><span data-stu-id="c6e22-131">For example, if you've created two Azure Files shares named *share1* and *share2* in storage account *myStorageAccount*, the `volumes` array would appear similar to the following:</span></span>

```json
"volumes": [{
  "name": "myvolume1",
  "azureFile": {
    "shareName": "share1",
    "storageAccountName": "myStorageAccount",
    "storageAccountKey": "<storage-account-key>"
  }
},
{
  "name": "myvolume2",
  "azureFile": {
    "shareName": "share2",
    "storageAccountName": "myStorageAccount",
    "storageAccountKey": "<storage-account-key>"
  }
}]
```

<span data-ttu-id="c6e22-132">Next, for each container in the container group in which you'd like to mount the volumes, populate the `volumeMounts` array in the `properties` section of the container definition.</span><span class="sxs-lookup"><span data-stu-id="c6e22-132">Next, for each container in the container group in which you'd like to mount the volumes, populate the `volumeMounts` array in the `properties` section of the container definition.</span></span> <span data-ttu-id="c6e22-133">For example, this mounts the two volumes, *myvolume1* and *myvolume2*, previously defined:</span><span class="sxs-lookup"><span data-stu-id="c6e22-133">For example, this mounts the two volumes, *myvolume1* and *myvolume2*, previously defined:</span></span>

```json
"volumeMounts": [{
  "name": "myvolume1",
  "mountPath": "/mnt/share1/"
},
{
  "name": "myvolume2",
  "mountPath": "/mnt/share2/"
}]
```

<span data-ttu-id="c6e22-134">To see an example of container instance deployment with an Azure Resource Manager template, see [Deploy multi-container groups in Azure Container Instances](container-instances-multi-container-group.md).</span><span class="sxs-lookup"><span data-stu-id="c6e22-134">To see an example of container instance deployment with an Azure Resource Manager template, see [Deploy multi-container groups in Azure Container Instances](container-instances-multi-container-group.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6e22-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="c6e22-135">Next steps</span></span>

<span data-ttu-id="c6e22-136">Learn how to mount other volume types in Azure Container Instances:</span><span class="sxs-lookup"><span data-stu-id="c6e22-136">Learn how to mount other volume types in Azure Container Instances:</span></span>

* [<span data-ttu-id="c6e22-137">Mount an emptyDir volume in Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="c6e22-137">Mount an emptyDir volume in Azure Container Instances</span></span>](container-instances-volume-emptydir.md)
* [<span data-ttu-id="c6e22-138">Mount a gitRepo volume in Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="c6e22-138">Mount a gitRepo volume in Azure Container Instances</span></span>](container-instances-volume-gitrepo.md)
* [<span data-ttu-id="c6e22-139">Mount a secret volume in Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="c6e22-139">Mount a secret volume in Azure Container Instances</span></span>](container-instances-volume-secret.md)

<!-- LINKS - External -->
[aci-hellofiles]: https://hub.docker.com/r/microsoft/aci-hellofiles/
[portal]: https://portal.azure.com
[storage-explorer]: https://storageexplorer.com

<!-- LINKS - Internal -->
[az-container-create]: /cli/azure/container#az-container-create
[az-container-show]: /cli/azure/container#az-container-show