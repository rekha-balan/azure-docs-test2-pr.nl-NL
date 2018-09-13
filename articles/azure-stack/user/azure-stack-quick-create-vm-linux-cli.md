---
title: Create a Linux virtual machine by using Azure CLI in Azure Stack | Microsoft Docs
description: Create a Linux virtual machine with CLI in Azure Stack.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 09/10/2018
ms.author: mabrigg
ms.custom: mvc
ms.openlocfilehash: 6fa68fcc4732241b30609f476a09643e458065db
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868674"
---
# <a name="quickstart-create-a-linux-server-virtual-machine-by-using-azure-cli-in-azure-stack"></a><span data-ttu-id="ac74e-103">Quickstart: create a Linux server virtual machine by using Azure CLI in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="ac74e-103">Quickstart: create a Linux server virtual machine by using Azure CLI in Azure Stack</span></span>

<span data-ttu-id="ac74e-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="ac74e-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="ac74e-105">You can create a Ubuntu Server 16.04 LTS virtual machine by using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="ac74e-105">You can create a Ubuntu Server 16.04 LTS virtual machine by using the Azure CLI.</span></span> <span data-ttu-id="ac74e-106">Follow the steps in this article to create and use a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="ac74e-106">Follow the steps in this article to create and use a virtual machine.</span></span> <span data-ttu-id="ac74e-107">This article also gives you the steps to:</span><span class="sxs-lookup"><span data-stu-id="ac74e-107">This article also gives you the steps to:</span></span>

* <span data-ttu-id="ac74e-108">Connect to the virtual machine with a remote client.</span><span class="sxs-lookup"><span data-stu-id="ac74e-108">Connect to the virtual machine with a remote client.</span></span>
* <span data-ttu-id="ac74e-109">Install the NGINX web server and view the default home page.</span><span class="sxs-lookup"><span data-stu-id="ac74e-109">Install the NGINX web server and view the default home page.</span></span>
* <span data-ttu-id="ac74e-110">Clean up unused resources.</span><span class="sxs-lookup"><span data-stu-id="ac74e-110">Clean up unused resources.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac74e-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ac74e-111">Prerequisites</span></span>

* <span data-ttu-id="ac74e-112">**A Linux image in the Azure Stack marketplace**</span><span class="sxs-lookup"><span data-stu-id="ac74e-112">**A Linux image in the Azure Stack marketplace**</span></span>

   <span data-ttu-id="ac74e-113">The Azure Stack marketplace doesn't contain a Linux image by default.</span><span class="sxs-lookup"><span data-stu-id="ac74e-113">The Azure Stack marketplace doesn't contain a Linux image by default.</span></span> <span data-ttu-id="ac74e-114">Get the Azure Stack operator to provide the **Ubuntu Server 16.04 LTS** image you need.</span><span class="sxs-lookup"><span data-stu-id="ac74e-114">Get the Azure Stack operator to provide the **Ubuntu Server 16.04 LTS** image you need.</span></span> <span data-ttu-id="ac74e-115">The operator can use the steps described in the [Download marketplace items from Azure to Azure Stack](../azure-stack-download-azure-marketplace-item.md) article.</span><span class="sxs-lookup"><span data-stu-id="ac74e-115">The operator can use the steps described in the [Download marketplace items from Azure to Azure Stack](../azure-stack-download-azure-marketplace-item.md) article.</span></span>

* <span data-ttu-id="ac74e-116">Azure Stack requires a specific version of the Azure CLI to create and manage the resources.</span><span class="sxs-lookup"><span data-stu-id="ac74e-116">Azure Stack requires a specific version of the Azure CLI to create and manage the resources.</span></span> <span data-ttu-id="ac74e-117">If you don't have the Azure CLI configured for Azure Stack, sign in to the [development kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) and follow the steps to [install and configure Azure CLI](azure-stack-version-profiles-azurecli2.md).</span><span class="sxs-lookup"><span data-stu-id="ac74e-117">If you don't have the Azure CLI configured for Azure Stack, sign in to the [development kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) and follow the steps to [install and configure Azure CLI](azure-stack-version-profiles-azurecli2.md).</span></span>

* <span data-ttu-id="ac74e-118">A public SSH key with the name id_rsa.pub saved in the .ssh directory of your Windows user profile.</span><span class="sxs-lookup"><span data-stu-id="ac74e-118">A public SSH key with the name id_rsa.pub saved in the .ssh directory of your Windows user profile.</span></span> <span data-ttu-id="ac74e-119">For detailed information about creating SSH keys, see [Creating SSH keys on Windows](../../virtual-machines/linux/ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="ac74e-119">For detailed information about creating SSH keys, see [Creating SSH keys on Windows](../../virtual-machines/linux/ssh-from-windows.md).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="ac74e-120">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="ac74e-120">Create a resource group</span></span>

<span data-ttu-id="ac74e-121">A resource group is a logical container where you can deploy and manage Azure Stack resources.</span><span class="sxs-lookup"><span data-stu-id="ac74e-121">A resource group is a logical container where you can deploy and manage Azure Stack resources.</span></span> <span data-ttu-id="ac74e-122">From your development kit or the Azure Stack integrated system, run the [az group create](/cli/azure/group#az-group-create) command to create a resource group.</span><span class="sxs-lookup"><span data-stu-id="ac74e-122">From your development kit or the Azure Stack integrated system, run the [az group create](/cli/azure/group#az-group-create) command to create a resource group.</span></span>

>[!NOTE]
 <span data-ttu-id="ac74e-123">Values are assigned for all the variables in the code examples.</span><span class="sxs-lookup"><span data-stu-id="ac74e-123">Values are assigned for all the variables in the code examples.</span></span> <span data-ttu-id="ac74e-124">However, you can assign new values if you want to.</span><span class="sxs-lookup"><span data-stu-id="ac74e-124">However, you can assign new values if you want to.</span></span>

<span data-ttu-id="ac74e-125">The following example creates a resource group named myResourceGroup in the local location.</span><span class="sxs-lookup"><span data-stu-id="ac74e-125">The following example creates a resource group named myResourceGroup in the local location.</span></span>

```cli
az group create --name myResourceGroup --location local
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="ac74e-126">Create a virtual machine</span><span class="sxs-lookup"><span data-stu-id="ac74e-126">Create a virtual machine</span></span>

<span data-ttu-id="ac74e-127">Create a virtual machine by using the [az vm create](/cli/azure/vm#az-vm-create) command.</span><span class="sxs-lookup"><span data-stu-id="ac74e-127">Create a virtual machine by using the [az vm create](/cli/azure/vm#az-vm-create) command.</span></span> <span data-ttu-id="ac74e-128">The following example creates a VM named myVM.</span><span class="sxs-lookup"><span data-stu-id="ac74e-128">The following example creates a VM named myVM.</span></span> <span data-ttu-id="ac74e-129">This example uses Demouser for an administrative user name and Demouser@123 as the user password.</span><span class="sxs-lookup"><span data-stu-id="ac74e-129">This example uses Demouser for an administrative user name and Demouser@123 as the user password.</span></span> <span data-ttu-id="ac74e-130">Change these values to something that is appropriate for your environment.</span><span class="sxs-lookup"><span data-stu-id="ac74e-130">Change these values to something that is appropriate for your environment.</span></span>

```cli
az vm create \
  --resource-group "myResourceGroup" \
  --name "myVM" \
  --image "UbuntuLTS" \
  --admin-username "Demouser" \
  --admin-password "Demouser@123" \
  --use-unmanaged-disk \
  --location local
```

<span data-ttu-id="ac74e-131">The public IP address is returned in the **PublicIpAddress** parameter.</span><span class="sxs-lookup"><span data-stu-id="ac74e-131">The public IP address is returned in the **PublicIpAddress** parameter.</span></span> <span data-ttu-id="ac74e-132">Write down this address because you need it to access the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="ac74e-132">Write down this address because you need it to access the virtual machine.</span></span>

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="ac74e-133">Open port 80 for web traffic</span><span class="sxs-lookup"><span data-stu-id="ac74e-133">Open port 80 for web traffic</span></span>

<span data-ttu-id="ac74e-134">Because this virtual machine is going to run the IIS web server, you need to open port 80 to Internet traffic.</span><span class="sxs-lookup"><span data-stu-id="ac74e-134">Because this virtual machine is going to run the IIS web server, you need to open port 80 to Internet traffic.</span></span> <span data-ttu-id="ac74e-135">Use the [az vm open-port](/cli/azure/vm#open-port) command to open the desired port.</span><span class="sxs-lookup"><span data-stu-id="ac74e-135">Use the [az vm open-port](/cli/azure/vm#open-port) command to open the desired port.</span></span>

```cli
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```

## <a name="use-ssh-to-connect-to-the-virtual-machine"></a><span data-ttu-id="ac74e-136">Use SSH to connect to the virtual machine</span><span class="sxs-lookup"><span data-stu-id="ac74e-136">Use SSH to connect to the virtual machine</span></span>

<span data-ttu-id="ac74e-137">From a client computer with SSH installed, connect to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="ac74e-137">From a client computer with SSH installed, connect to the virtual machine.</span></span> <span data-ttu-id="ac74e-138">If you're working on a Windows client, use [Putty](http://www.putty.org/) to create the connection.</span><span class="sxs-lookup"><span data-stu-id="ac74e-138">If you're working on a Windows client, use [Putty](http://www.putty.org/) to create the connection.</span></span> <span data-ttu-id="ac74e-139">To connect to the virtual machine, use the following command:</span><span class="sxs-lookup"><span data-stu-id="ac74e-139">To connect to the virtual machine, use the following command:</span></span>

```bash
ssh <publicIpAddress>
```

## <a name="install-the-nginx-web-server"></a><span data-ttu-id="ac74e-140">Install the NGINX web server</span><span class="sxs-lookup"><span data-stu-id="ac74e-140">Install the NGINX web server</span></span>

<span data-ttu-id="ac74e-141">To update package resources and install the latest NGINX package, run the following script:</span><span class="sxs-lookup"><span data-stu-id="ac74e-141">To update package resources and install the latest NGINX package, run the following script:</span></span>

```bash
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-the-nginx-welcome-page"></a><span data-ttu-id="ac74e-142">View the NGINX welcome page</span><span class="sxs-lookup"><span data-stu-id="ac74e-142">View the NGINX welcome page</span></span>

<span data-ttu-id="ac74e-143">With NGINX installed, and port 80 open on your virtual machine, you can access the web server using the virtual machine's public IP address.</span><span class="sxs-lookup"><span data-stu-id="ac74e-143">With NGINX installed, and port 80 open on your virtual machine, you can access the web server using the virtual machine's public IP address.</span></span> <span data-ttu-id="ac74e-144">Open a web browser, and browse to ```http://<public IP address>```.</span><span class="sxs-lookup"><span data-stu-id="ac74e-144">Open a web browser, and browse to ```http://<public IP address>```.</span></span>

![NGINX web server Welcome page](./media/azure-stack-quick-create-vm-linux-cli/nginx.png)

## <a name="clean-up-resources"></a><span data-ttu-id="ac74e-146">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="ac74e-146">Clean up resources</span></span>

<span data-ttu-id="ac74e-147">Clean up the resources that you don't need any longer.</span><span class="sxs-lookup"><span data-stu-id="ac74e-147">Clean up the resources that you don't need any longer.</span></span> <span data-ttu-id="ac74e-148">You can use the [az group delete](/cli/azure/group#az-group-delete) command to remove these resources.</span><span class="sxs-lookup"><span data-stu-id="ac74e-148">You can use the [az group delete](/cli/azure/group#az-group-delete) command to remove these resources.</span></span> <span data-ttu-id="ac74e-149">To delete the resource group and all its resources, run the following command:</span><span class="sxs-lookup"><span data-stu-id="ac74e-149">To delete the resource group and all its resources, run the following command:</span></span>

```cli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="ac74e-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="ac74e-150">Next steps</span></span>

<span data-ttu-id="ac74e-151">In this quickstart, you deployed a basic Linux server virtual machine with a web server.</span><span class="sxs-lookup"><span data-stu-id="ac74e-151">In this quickstart, you deployed a basic Linux server virtual machine with a web server.</span></span> <span data-ttu-id="ac74e-152">To learn more about Azure Stack virtual machines, continue to [Considerations for Virtual Machines in Azure Stack](azure-stack-vm-considerations.md).</span><span class="sxs-lookup"><span data-stu-id="ac74e-152">To learn more about Azure Stack virtual machines, continue to [Considerations for Virtual Machines in Azure Stack](azure-stack-vm-considerations.md).</span></span>
