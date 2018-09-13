---
title: Quickstart - Create a Linux VM with the Azure CLI 2.0 | Microsoft Docs
description: In this quickstart, you learn how to use the Azure CLI 2.0 to create a Linux virtual machine
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: jeconnoc
editor: tysonn
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/24/2018
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 6536860bb75d068a96899f2d30ec7a6126a28436
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44818706"
---
# <a name="quickstart-create-a-linux-virtual-machine-with-the-azure-cli-20"></a><span data-ttu-id="e75c5-103">Quickstart: Create a Linux virtual machine with the Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e75c5-103">Quickstart: Create a Linux virtual machine with the Azure CLI 2.0</span></span>

<span data-ttu-id="e75c5-104">The Azure CLI 2.0 is used to create and manage Azure resources from the command line or in scripts.</span><span class="sxs-lookup"><span data-stu-id="e75c5-104">The Azure CLI 2.0 is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="e75c5-105">This quickstart shows you how to use the Azure CLI 2.0 to deploy a Linux virtual machine (VM) in Azure that runs Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="e75c5-105">This quickstart shows you how to use the Azure CLI 2.0 to deploy a Linux virtual machine (VM) in Azure that runs Ubuntu.</span></span> <span data-ttu-id="e75c5-106">To see your VM in action, you then SSH to the VM and install the NGINX web server.</span><span class="sxs-lookup"><span data-stu-id="e75c5-106">To see your VM in action, you then SSH to the VM and install the NGINX web server.</span></span>

<span data-ttu-id="e75c5-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="e75c5-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e75c5-108">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.30 or later.</span><span class="sxs-lookup"><span data-stu-id="e75c5-108">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.30 or later.</span></span> <span data-ttu-id="e75c5-109">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="e75c5-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="e75c5-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e75c5-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="e75c5-111">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="e75c5-111">Create a resource group</span></span>

<span data-ttu-id="e75c5-112">Create a resource group with the [az group create](/cli/azure/group#az_group_create) command.</span><span class="sxs-lookup"><span data-stu-id="e75c5-112">Create a resource group with the [az group create](/cli/azure/group#az_group_create) command.</span></span> <span data-ttu-id="e75c5-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="e75c5-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="e75c5-114">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span><span class="sxs-lookup"><span data-stu-id="e75c5-114">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="e75c5-115">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="e75c5-115">Create virtual machine</span></span>

<span data-ttu-id="e75c5-116">Create a VM with the [az vm create](/cli/azure/vm#az_vm_create) command.</span><span class="sxs-lookup"><span data-stu-id="e75c5-116">Create a VM with the [az vm create](/cli/azure/vm#az_vm_create) command.</span></span>

<span data-ttu-id="e75c5-117">The following example creates a VM named *myVM*, adds a user account named *azureuser*, and generates SSH keys if they do not already exist in the default key location (*~/.ssh*).</span><span class="sxs-lookup"><span data-stu-id="e75c5-117">The following example creates a VM named *myVM*, adds a user account named *azureuser*, and generates SSH keys if they do not already exist in the default key location (*~/.ssh*).</span></span> <span data-ttu-id="e75c5-118">To use a specific set of keys, use the `--ssh-key-value` option:</span><span class="sxs-lookup"><span data-stu-id="e75c5-118">To use a specific set of keys, use the `--ssh-key-value` option:</span></span>

```azurecli-interactive
az vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```

<span data-ttu-id="e75c5-119">It takes a few minutes to create the VM and supporting resources.</span><span class="sxs-lookup"><span data-stu-id="e75c5-119">It takes a few minutes to create the VM and supporting resources.</span></span> <span data-ttu-id="e75c5-120">The following example output shows the VM create operation was successful.</span><span class="sxs-lookup"><span data-stu-id="e75c5-120">The following example output shows the VM create operation was successful.</span></span>

```azurecli-interactive
{
  "fqdns": "",
  "id": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```

<span data-ttu-id="e75c5-121">Note your own `publicIpAddress` in the output from your VM.</span><span class="sxs-lookup"><span data-stu-id="e75c5-121">Note your own `publicIpAddress` in the output from your VM.</span></span> <span data-ttu-id="e75c5-122">This address is used to access the VM in the next steps.</span><span class="sxs-lookup"><span data-stu-id="e75c5-122">This address is used to access the VM in the next steps.</span></span>

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="e75c5-123">Open port 80 for web traffic</span><span class="sxs-lookup"><span data-stu-id="e75c5-123">Open port 80 for web traffic</span></span>

<span data-ttu-id="e75c5-124">By default, only SSH connections are opened when you create a Linux VM in Azure.</span><span class="sxs-lookup"><span data-stu-id="e75c5-124">By default, only SSH connections are opened when you create a Linux VM in Azure.</span></span> <span data-ttu-id="e75c5-125">Use [az vm open-port](/cli/azure/vm#az_vm_open_port) to open TCP port 80 for use with the NGINX web server:</span><span class="sxs-lookup"><span data-stu-id="e75c5-125">Use [az vm open-port](/cli/azure/vm#az_vm_open_port) to open TCP port 80 for use with the NGINX web server:</span></span>

```azurecli-interactive
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```

## <a name="connect-to-virtual-machine"></a><span data-ttu-id="e75c5-126">Connect to virtual machine</span><span class="sxs-lookup"><span data-stu-id="e75c5-126">Connect to virtual machine</span></span>

<span data-ttu-id="e75c5-127">SSH to your VM as normal.</span><span class="sxs-lookup"><span data-stu-id="e75c5-127">SSH to your VM as normal.</span></span> <span data-ttu-id="e75c5-128">Replace **publicIpAddress** with the public IP address of your VM as noted in the previous output from your VM:</span><span class="sxs-lookup"><span data-stu-id="e75c5-128">Replace **publicIpAddress** with the public IP address of your VM as noted in the previous output from your VM:</span></span>

```bash
ssh azureuser@publicIpAddress
```

## <a name="install-web-server"></a><span data-ttu-id="e75c5-129">Install web server</span><span class="sxs-lookup"><span data-stu-id="e75c5-129">Install web server</span></span>

<span data-ttu-id="e75c5-130">To see your VM in action, install the NGINX web server.</span><span class="sxs-lookup"><span data-stu-id="e75c5-130">To see your VM in action, install the NGINX web server.</span></span> <span data-ttu-id="e75c5-131">To update package sources and install the latest NGINX package, run the following commands from your SSH session:</span><span class="sxs-lookup"><span data-stu-id="e75c5-131">To update package sources and install the latest NGINX package, run the following commands from your SSH session:</span></span>

```bash
# update packages
sudo apt-get -y update

# install NGINX
sudo apt-get -y install nginx
```

<span data-ttu-id="e75c5-132">When done, `exit` the SSH session.</span><span class="sxs-lookup"><span data-stu-id="e75c5-132">When done, `exit` the SSH session.</span></span>

## <a name="view-the-web-server-in-action"></a><span data-ttu-id="e75c5-133">View the web server in action</span><span class="sxs-lookup"><span data-stu-id="e75c5-133">View the web server in action</span></span>

<span data-ttu-id="e75c5-134">With NGINX installed and port 80 now open on your VM from the Internet, use a web browser of your choice to view the default NGINX welcome page.</span><span class="sxs-lookup"><span data-stu-id="e75c5-134">With NGINX installed and port 80 now open on your VM from the Internet, use a web browser of your choice to view the default NGINX welcome page.</span></span> <span data-ttu-id="e75c5-135">Use the public IP address of your VM obtained in a previous step.</span><span class="sxs-lookup"><span data-stu-id="e75c5-135">Use the public IP address of your VM obtained in a previous step.</span></span> <span data-ttu-id="e75c5-136">The following example shows the default NGINX web site:</span><span class="sxs-lookup"><span data-stu-id="e75c5-136">The following example shows the default NGINX web site:</span></span>

![NGINX default site](./media/quick-create-cli/nginx.png)

## <a name="clean-up-resources"></a><span data-ttu-id="e75c5-138">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="e75c5-138">Clean up resources</span></span>

<span data-ttu-id="e75c5-139">When no longer needed, you can use the [az group delete](/cli/azure/group#az_group_delete) command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="e75c5-139">When no longer needed, you can use the [az group delete](/cli/azure/group#az_group_delete) command to remove the resource group, VM, and all related resources.</span></span> <span data-ttu-id="e75c5-140">Make sure that you have exited the SSH session to your VM, then delete the resources as follows:</span><span class="sxs-lookup"><span data-stu-id="e75c5-140">Make sure that you have exited the SSH session to your VM, then delete the resources as follows:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="e75c5-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="e75c5-141">Next steps</span></span>

<span data-ttu-id="e75c5-142">In this quickstart, you deployed a simple virtual machine, open a network port for web traffic, and installed a basic web server.</span><span class="sxs-lookup"><span data-stu-id="e75c5-142">In this quickstart, you deployed a simple virtual machine, open a network port for web traffic, and installed a basic web server.</span></span> <span data-ttu-id="e75c5-143">To learn more about Azure virtual machines, continue to the tutorial for Linux VMs.</span><span class="sxs-lookup"><span data-stu-id="e75c5-143">To learn more about Azure virtual machines, continue to the tutorial for Linux VMs.</span></span>


> [!div class="nextstepaction"]
> [<span data-ttu-id="e75c5-144">Azure Linux virtual machine tutorials</span><span class="sxs-lookup"><span data-stu-id="e75c5-144">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
