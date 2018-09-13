---
title: File share for Azure DC/OS cluster
description: Create and mount a file share to a DC/OS cluster in Azure Container Service
services: container-service
author: julienstroheker
manager: dcaro
ms.service: container-service
ms.topic: tutorial
ms.date: 06/07/2017
ms.author: juliens
ms.custom: mvc
ms.openlocfilehash: c1c318f4204efd24a2d9d3d83bb1cb71f5775bdb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866254"
---
# <a name="create-and-mount-a-file-share-to-a-dcos-cluster"></a><span data-ttu-id="6de50-103">Create and mount a file share to a DC/OS cluster</span><span class="sxs-lookup"><span data-stu-id="6de50-103">Create and mount a file share to a DC/OS cluster</span></span>

<span data-ttu-id="6de50-104">This tutorial details how to create a file share in Azure and mount it on each agent and master of the DC/OS cluster.</span><span class="sxs-lookup"><span data-stu-id="6de50-104">This tutorial details how to create a file share in Azure and mount it on each agent and master of the DC/OS cluster.</span></span> <span data-ttu-id="6de50-105">Setting up a file share makes it easier to share files across your cluster such as configuration, access, logs, and more.</span><span class="sxs-lookup"><span data-stu-id="6de50-105">Setting up a file share makes it easier to share files across your cluster such as configuration, access, logs, and more.</span></span> <span data-ttu-id="6de50-106">The following tasks are completed in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="6de50-106">The following tasks are completed in this tutorial:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6de50-107">Create an Azure storage account</span><span class="sxs-lookup"><span data-stu-id="6de50-107">Create an Azure storage account</span></span>
> * <span data-ttu-id="6de50-108">Create a file share</span><span class="sxs-lookup"><span data-stu-id="6de50-108">Create a file share</span></span>
> * <span data-ttu-id="6de50-109">Mount the share in the DC/OS cluster</span><span class="sxs-lookup"><span data-stu-id="6de50-109">Mount the share in the DC/OS cluster</span></span>

<span data-ttu-id="6de50-110">You need an ACS DC/OS cluster to complete the steps in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="6de50-110">You need an ACS DC/OS cluster to complete the steps in this tutorial.</span></span> <span data-ttu-id="6de50-111">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span><span class="sxs-lookup"><span data-stu-id="6de50-111">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="6de50-112">This tutorial requires the Azure CLI version 2.0.4 or later.</span><span class="sxs-lookup"><span data-stu-id="6de50-112">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="6de50-113">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="6de50-113">Run `az --version` to find the version.</span></span> <span data-ttu-id="6de50-114">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6de50-114">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="create-a-file-share-on-microsoft-azure"></a><span data-ttu-id="6de50-115">Create a file share on Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="6de50-115">Create a file share on Microsoft Azure</span></span>

<span data-ttu-id="6de50-116">Before using an Azure file share with an ACS DC/OS cluster, the storage account and file share must be created.</span><span class="sxs-lookup"><span data-stu-id="6de50-116">Before using an Azure file share with an ACS DC/OS cluster, the storage account and file share must be created.</span></span> <span data-ttu-id="6de50-117">Run the following script to create the storage and file share.</span><span class="sxs-lookup"><span data-stu-id="6de50-117">Run the following script to create the storage and file share.</span></span> <span data-ttu-id="6de50-118">Update the parameters with thoes from your environment.</span><span class="sxs-lookup"><span data-stu-id="6de50-118">Update the parameters with thoes from your environment.</span></span>

```azurecli-interactive
# Change these four parameters
DCOS_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
DCOS_PERS_RESOURCE_GROUP=myResourceGroup
DCOS_PERS_LOCATION=eastus
DCOS_PERS_SHARE_NAME=dcosshare

# Create the storage account with the parameters
az storage account create -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -l $DCOS_PERS_LOCATION --sku Standard_LRS

# Export the connection string as an environment variable, this is used when creating the Azure file share
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -o tsv`

# Create the share
az storage share create -n $DCOS_PERS_SHARE_NAME
```

## <a name="mount-the-share-in-your-cluster"></a><span data-ttu-id="6de50-119">Mount the share in your cluster</span><span class="sxs-lookup"><span data-stu-id="6de50-119">Mount the share in your cluster</span></span>

<span data-ttu-id="6de50-120">Next, the file share needs to be mounted on every virtual machine inside your cluster.</span><span class="sxs-lookup"><span data-stu-id="6de50-120">Next, the file share needs to be mounted on every virtual machine inside your cluster.</span></span> <span data-ttu-id="6de50-121">This task is completed using the cifs tool/protocol.</span><span class="sxs-lookup"><span data-stu-id="6de50-121">This task is completed using the cifs tool/protocol.</span></span> <span data-ttu-id="6de50-122">The mount operation can be completed manually on each node of the cluster, or by running a script against each node in the cluster.</span><span class="sxs-lookup"><span data-stu-id="6de50-122">The mount operation can be completed manually on each node of the cluster, or by running a script against each node in the cluster.</span></span>

<span data-ttu-id="6de50-123">In this example, two scripts are run, one to mount the Azure file share, and a second to run this script on each node of the DC/OS cluster.</span><span class="sxs-lookup"><span data-stu-id="6de50-123">In this example, two scripts are run, one to mount the Azure file share, and a second to run this script on each node of the DC/OS cluster.</span></span>

<span data-ttu-id="6de50-124">First, the Azure storage account name, and access key are needed.</span><span class="sxs-lookup"><span data-stu-id="6de50-124">First, the Azure storage account name, and access key are needed.</span></span> <span data-ttu-id="6de50-125">Run the following commands to get this information.</span><span class="sxs-lookup"><span data-stu-id="6de50-125">Run the following commands to get this information.</span></span> <span data-ttu-id="6de50-126">Take note of each, these values are used in a later step.</span><span class="sxs-lookup"><span data-stu-id="6de50-126">Take note of each, these values are used in a later step.</span></span>

<span data-ttu-id="6de50-127">Storage account name:</span><span class="sxs-lookup"><span data-stu-id="6de50-127">Storage account name:</span></span>

```azurecli-interactive
STORAGE_ACCT=$(az storage account list --resource-group $DCOS_PERS_RESOURCE_GROUP --query "[?contains(name, '$DCOS_PERS_STORAGE_ACCOUNT_NAME')].[name]" -o tsv)
echo $STORAGE_ACCT
```

<span data-ttu-id="6de50-128">Storage account access key:</span><span class="sxs-lookup"><span data-stu-id="6de50-128">Storage account access key:</span></span>

```azurecli-interactive
az storage account keys list --resource-group $DCOS_PERS_RESOURCE_GROUP --account-name $STORAGE_ACCT --query "[0].value" -o tsv
```

<span data-ttu-id="6de50-129">Next, get the FQDN of the DC/OS master and store it in a variable.</span><span class="sxs-lookup"><span data-stu-id="6de50-129">Next, get the FQDN of the DC/OS master and store it in a variable.</span></span>

```azurecli-interactive
FQDN=$(az acs list --resource-group $DCOS_PERS_RESOURCE_GROUP --query "[0].masterProfile.fqdn" --output tsv)
```

<span data-ttu-id="6de50-130">Copy your private key to the master node.</span><span class="sxs-lookup"><span data-stu-id="6de50-130">Copy your private key to the master node.</span></span> <span data-ttu-id="6de50-131">This key is needed to create an ssh connection with all nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="6de50-131">This key is needed to create an ssh connection with all nodes in the cluster.</span></span> <span data-ttu-id="6de50-132">Update the user name if a non-default value was used when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="6de50-132">Update the user name if a non-default value was used when creating the cluster.</span></span> 

```azurecli-interactive
scp ~/.ssh/id_rsa azureuser@$FQDN:~/.ssh
```

<span data-ttu-id="6de50-133">Create an SSH connection with the master (or the first master) of your DC/OS-based cluster.</span><span class="sxs-lookup"><span data-stu-id="6de50-133">Create an SSH connection with the master (or the first master) of your DC/OS-based cluster.</span></span> <span data-ttu-id="6de50-134">Update the user name if a non-default value was used when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="6de50-134">Update the user name if a non-default value was used when creating the cluster.</span></span>

```azurecli-interactive
ssh azureuser@$FQDN
```

<span data-ttu-id="6de50-135">Create a file named **cifsMount.sh**, and copy the following contents into it.</span><span class="sxs-lookup"><span data-stu-id="6de50-135">Create a file named **cifsMount.sh**, and copy the following contents into it.</span></span> 

<span data-ttu-id="6de50-136">This script is used to mount the Azure file share.</span><span class="sxs-lookup"><span data-stu-id="6de50-136">This script is used to mount the Azure file share.</span></span> <span data-ttu-id="6de50-137">Update the `STORAGE_ACCT_NAME` and `ACCESS_KEY` variables with the information collected earlier.</span><span class="sxs-lookup"><span data-stu-id="6de50-137">Update the `STORAGE_ACCT_NAME` and `ACCESS_KEY` variables with the information collected earlier.</span></span>

```azurecli-interactive
#!/bin/bash

# Azure storage account name and access key
SHARE_NAME=dcosshare
STORAGE_ACCT_NAME=mystorageaccount
ACCESS_KEY=mystorageaccountKey

# Install the cifs utils, should be already installed
sudo apt-get update && sudo apt-get -y install cifs-utils

# Create the local folder that will contain our share
if [ ! -d "/mnt/share/$SHARE_NAME" ]; then sudo mkdir -p "/mnt/share/$SHARE_NAME" ; fi

# Mount the share under the previous local folder created
sudo mount -t cifs //$STORAGE_ACCT_NAME.file.core.windows.net/$SHARE_NAME /mnt/share/$SHARE_NAME -o vers=3.0,username=$STORAGE_ACCT_NAME,password=$ACCESS_KEY,dir_mode=0777,file_mode=0777
```
<span data-ttu-id="6de50-138">Create a second file named **getNodesRunScript.sh** and copy the following contents into the file.</span><span class="sxs-lookup"><span data-stu-id="6de50-138">Create a second file named **getNodesRunScript.sh** and copy the following contents into the file.</span></span> 

<span data-ttu-id="6de50-139">This script discovers all cluster nodes, and then runs the **cifsMount.sh** script to mount the file share on each.</span><span class="sxs-lookup"><span data-stu-id="6de50-139">This script discovers all cluster nodes, and then runs the **cifsMount.sh** script to mount the file share on each.</span></span>

```azurecli-interactive
#!/bin/bash

# Install jq used for the next command
sudo apt-get install jq -y

# Get the IP address of each node using the mesos API and store it inside a file called nodes
curl http://leader.mesos:1050/system/health/v1/nodes | jq '.nodes[].host_ip' | sed 's/\"//g' | sed '/172/d' > nodes

# From the previous file created, run our script to mount our share on each node
cat nodes | while read line
do
  ssh `whoami`@$line -o StrictHostKeyChecking=no < ./cifsMount.sh
  done
```

<span data-ttu-id="6de50-140">Run the script to mount the Azure file share on all nodes of the cluster.</span><span class="sxs-lookup"><span data-stu-id="6de50-140">Run the script to mount the Azure file share on all nodes of the cluster.</span></span>

```azurecli-interactive
sh ./getNodesRunScript.sh
```  

<span data-ttu-id="6de50-141">The file share is now accessible at `/mnt/share/dcosshare` on each node of the cluster.</span><span class="sxs-lookup"><span data-stu-id="6de50-141">The file share is now accessible at `/mnt/share/dcosshare` on each node of the cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6de50-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="6de50-142">Next steps</span></span>

<span data-ttu-id="6de50-143">In this tutorial an Azure file share was made available to a DC/OS cluster using the steps:</span><span class="sxs-lookup"><span data-stu-id="6de50-143">In this tutorial an Azure file share was made available to a DC/OS cluster using the steps:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6de50-144">Create an Azure storage account</span><span class="sxs-lookup"><span data-stu-id="6de50-144">Create an Azure storage account</span></span>
> * <span data-ttu-id="6de50-145">Create a file share</span><span class="sxs-lookup"><span data-stu-id="6de50-145">Create a file share</span></span>
> * <span data-ttu-id="6de50-146">Mount the share in the DC/OS cluster</span><span class="sxs-lookup"><span data-stu-id="6de50-146">Mount the share in the DC/OS cluster</span></span>

<span data-ttu-id="6de50-147">Advance to the next tutorial to learn about integrating an Azure Container Registry with DC/OS in Azure.</span><span class="sxs-lookup"><span data-stu-id="6de50-147">Advance to the next tutorial to learn about integrating an Azure Container Registry with DC/OS in Azure.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="6de50-148">Load balance applications</span><span class="sxs-lookup"><span data-stu-id="6de50-148">Load balance applications</span></span>](container-service-dcos-acr.md)
