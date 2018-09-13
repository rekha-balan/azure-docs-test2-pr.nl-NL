---
title: Azure Quick Start - Create VM CLI | Microsoft Docs
description: Quickly learn to create virtual machines with the Azure CLI.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/03/2017
ms.author: nepeters
ms.openlocfilehash: c9fdf11ecaf8464aed50bae8136176f84073ace8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549364"
---
# <a name="create-a-linux-virtual-machine-with-the-azure-cli"></a><span data-ttu-id="c5153-103">Create a Linux virtual machine with the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c5153-103">Create a Linux virtual machine with the Azure CLI</span></span>

<span data-ttu-id="c5153-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span><span class="sxs-lookup"><span data-stu-id="c5153-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="c5153-105">This guide details using the Azure CLI to deploy a virtual machine running Ubuntu 16.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="c5153-105">This guide details using the Azure CLI to deploy a virtual machine running Ubuntu 16.04 LTS.</span></span> <span data-ttu-id="c5153-106">Once the server is deployed, we SSH into the VM in order to install NGINX.</span><span class="sxs-lookup"><span data-stu-id="c5153-106">Once the server is deployed, we SSH into the VM in order to install NGINX.</span></span> 

<span data-ttu-id="c5153-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/en-us/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="c5153-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/en-us/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="c5153-108">Also, make sure that the Azure CLI has been installed.</span><span class="sxs-lookup"><span data-stu-id="c5153-108">Also, make sure that the Azure CLI has been installed.</span></span> <span data-ttu-id="c5153-109">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c5153-109">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> 

## <a name="log-in-to-azure"></a><span data-ttu-id="c5153-110">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="c5153-110">Log in to Azure</span></span> 

<span data-ttu-id="c5153-111">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span><span class="sxs-lookup"><span data-stu-id="c5153-111">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

```azurecli
az login
```

## <a name="create-a-resource-group"></a><span data-ttu-id="c5153-112">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="c5153-112">Create a resource group</span></span>

<span data-ttu-id="c5153-113">Create a resource group with the [az group create](/cli/azure/group#create) command.</span><span class="sxs-lookup"><span data-stu-id="c5153-113">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="c5153-114">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="c5153-114">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="c5153-115">The following example creates a resource group named `myResourceGroup` in the `westeurope` location.</span><span class="sxs-lookup"><span data-stu-id="c5153-115">The following example creates a resource group named `myResourceGroup` in the `westeurope` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

## <a name="create-virtual-machine"></a><span data-ttu-id="c5153-116">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="c5153-116">Create virtual machine</span></span>

<span data-ttu-id="c5153-117">Create a VM with the [az vm create](/cli/azure/vm#create) command.</span><span class="sxs-lookup"><span data-stu-id="c5153-117">Create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="c5153-118">The following example creates a VM named `myVM` and creates SSH keys if they do not already exist in a default key location.</span><span class="sxs-lookup"><span data-stu-id="c5153-118">The following example creates a VM named `myVM` and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="c5153-119">To use a specific set of keys, use the `--ssh-key-value` option.</span><span class="sxs-lookup"><span data-stu-id="c5153-119">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

```azurecli
az vm create --resource-group myResourceGroup --name myVM --image UbuntuLTS --generate-ssh-keys
```

<span data-ttu-id="c5153-120">When the VM has been created, the Azure CLI shows information similar to the following example.</span><span class="sxs-lookup"><span data-stu-id="c5153-120">When the VM has been created, the Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="c5153-121">Take note of the `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="c5153-121">Take note of the `publicIpAddress`.</span></span> <span data-ttu-id="c5153-122">This address is used to access the VM.</span><span class="sxs-lookup"><span data-stu-id="c5153-122">This address is used to access the VM.</span></span>

```azurecli
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "westeurope",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="c5153-123">Open port 80 for web traffic</span><span class="sxs-lookup"><span data-stu-id="c5153-123">Open port 80 for web traffic</span></span> 

<span data-ttu-id="c5153-124">By default only SSH connections are allowed into Linux virtual machines deployed in Azure.</span><span class="sxs-lookup"><span data-stu-id="c5153-124">By default only SSH connections are allowed into Linux virtual machines deployed in Azure.</span></span> <span data-ttu-id="c5153-125">If this VM is going to be a webserver, you need to open port 80 from the Internet.</span><span class="sxs-lookup"><span data-stu-id="c5153-125">If this VM is going to be a webserver, you need to open port 80 from the Internet.</span></span>  <span data-ttu-id="c5153-126">A single command is required to open the desired port.</span><span class="sxs-lookup"><span data-stu-id="c5153-126">A single command is required to open the desired port.</span></span>  
 
 ```azurecli 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```

## <a name="ssh-into-your-vm"></a><span data-ttu-id="c5153-127">SSH into your VM</span><span class="sxs-lookup"><span data-stu-id="c5153-127">SSH into your VM</span></span>

<span data-ttu-id="c5153-128">Use the following command to create an SSH session with the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="c5153-128">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="c5153-129">Make sure to replace `<publicIpAddress>` with the correct public IP address of your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="c5153-129">Make sure to replace `<publicIpAddress>` with the correct public IP address of your virtual machine.</span></span>  <span data-ttu-id="c5153-130">In our example above our IP address was `40.68.254.142`.</span><span class="sxs-lookup"><span data-stu-id="c5153-130">In our example above our IP address was `40.68.254.142`.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="install-nginx"></a><span data-ttu-id="c5153-131">Install NGINX</span><span class="sxs-lookup"><span data-stu-id="c5153-131">Install NGINX</span></span>

<span data-ttu-id="c5153-132">Use the following bash script to update package sources and install the latest NGINX package.</span><span class="sxs-lookup"><span data-stu-id="c5153-132">Use the following bash script to update package sources and install the latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-the-ngix-welcome-page"></a><span data-ttu-id="c5153-133">View the NGIX welcome page</span><span class="sxs-lookup"><span data-stu-id="c5153-133">View the NGIX welcome page</span></span>

<span data-ttu-id="c5153-134">With NGINX installed and port 80 now open on your VM from the Internet - you can use a web browser of your choice to view the default NGINX welcome page.</span><span class="sxs-lookup"><span data-stu-id="c5153-134">With NGINX installed and port 80 now open on your VM from the Internet - you can use a web browser of your choice to view the default NGINX welcome page.</span></span> <span data-ttu-id="c5153-135">Be sure to use the `publicIpAddress` you documented above to visit the default page.</span><span class="sxs-lookup"><span data-stu-id="c5153-135">Be sure to use the `publicIpAddress` you documented above to visit the default page.</span></span> 

![NGINX default site](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/quick-create-cli/nginx.png) 


## <a name="delete-virtual-machine"></a><span data-ttu-id="c5153-137">Delete virtual machine</span><span class="sxs-lookup"><span data-stu-id="c5153-137">Delete virtual machine</span></span>

<span data-ttu-id="c5153-138">When no longer needed, the following command can be used to remove the Resource Group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="c5153-138">When no longer needed, the following command can be used to remove the Resource Group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="c5153-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="c5153-139">Next steps</span></span>

[<span data-ttu-id="c5153-140">Create highly available virtual machines tutorial</span><span class="sxs-lookup"><span data-stu-id="c5153-140">Create highly available virtual machines tutorial</span></span>](create-cli-complete.md)

[<span data-ttu-id="c5153-141">Explore VM deployment CLI samples</span><span class="sxs-lookup"><span data-stu-id="c5153-141">Explore VM deployment CLI samples</span></span>](cli-samples.md)

