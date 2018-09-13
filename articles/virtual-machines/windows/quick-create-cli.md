---
title: Azure Quick Start - Create Windows VM CLI | Microsoft Docs
description: Quickly learn to create a Windows virtual machines with the Azure CLI.
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 04/03/2017
ms.author: nepeters
ms.openlocfilehash: b2065c8524872d4d0537b9d93e23289e85567770
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553343"
---
# <a name="create-a-windows-virtual-machine-with-the-azure-cli"></a><span data-ttu-id="9f74a-103">Create a Windows virtual machine with the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9f74a-103">Create a Windows virtual machine with the Azure CLI</span></span>

<span data-ttu-id="9f74a-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span><span class="sxs-lookup"><span data-stu-id="9f74a-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="9f74a-105">This guide details using the Azure CLI to deploy a virtual machine running Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="9f74a-105">This guide details using the Azure CLI to deploy a virtual machine running Windows Server 2016.</span></span> <span data-ttu-id="9f74a-106">Once deployment is complete, we connect to the server and install IIS.</span><span class="sxs-lookup"><span data-stu-id="9f74a-106">Once deployment is complete, we connect to the server and install IIS.</span></span>

<span data-ttu-id="9f74a-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/en-us/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="9f74a-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/en-us/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="9f74a-108">Also, make sure that the Azure CLI has been installed.</span><span class="sxs-lookup"><span data-stu-id="9f74a-108">Also, make sure that the Azure CLI has been installed.</span></span> <span data-ttu-id="9f74a-109">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9f74a-109">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="9f74a-110">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="9f74a-110">Log in to Azure</span></span> 

<span data-ttu-id="9f74a-111">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span><span class="sxs-lookup"><span data-stu-id="9f74a-111">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

```azurecli
az login
```

## <a name="create-a-resource-group"></a><span data-ttu-id="9f74a-112">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="9f74a-112">Create a resource group</span></span>

<span data-ttu-id="9f74a-113">Create a resource group with [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="9f74a-113">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="9f74a-114">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="9f74a-114">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="9f74a-115">The following example creates a resource group named `myResourceGroup` in the `westeurope` location.</span><span class="sxs-lookup"><span data-stu-id="9f74a-115">The following example creates a resource group named `myResourceGroup` in the `westeurope` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

## <a name="create-virtual-machine"></a><span data-ttu-id="9f74a-116">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="9f74a-116">Create virtual machine</span></span>

<span data-ttu-id="9f74a-117">Create a VM with [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="9f74a-117">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> 

<span data-ttu-id="9f74a-118">The following example creates a VM named `myVM`.</span><span class="sxs-lookup"><span data-stu-id="9f74a-118">The following example creates a VM named `myVM`.</span></span> <span data-ttu-id="9f74a-119">This example uses `azureuser` for an administrative user name and ` myPassword12` as the password.</span><span class="sxs-lookup"><span data-stu-id="9f74a-119">This example uses `azureuser` for an administrative user name and ` myPassword12` as the password.</span></span> <span data-ttu-id="9f74a-120">Update these values to something appropriate to your environment.</span><span class="sxs-lookup"><span data-stu-id="9f74a-120">Update these values to something appropriate to your environment.</span></span> <span data-ttu-id="9f74a-121">These values are needed when creating a connection with the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="9f74a-121">These values are needed when creating a connection with the virtual machine.</span></span>

```azurecli
az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter --admin-username azureuser --admin-password myPassword12
```

<span data-ttu-id="9f74a-122">When the VM has been created, the Azure CLI shows information similar to the following example.</span><span class="sxs-lookup"><span data-stu-id="9f74a-122">When the VM has been created, the Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="9f74a-123">Take note of the public IP address.</span><span class="sxs-lookup"><span data-stu-id="9f74a-123">Take note of the public IP address.</span></span> <span data-ttu-id="9f74a-124">This address is used to access the VM.</span><span class="sxs-lookup"><span data-stu-id="9f74a-124">This address is used to access the VM.</span></span>

```azurecli
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "westeurope",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="9f74a-125">Open port 80 for web traffic</span><span class="sxs-lookup"><span data-stu-id="9f74a-125">Open port 80 for web traffic</span></span> 

<span data-ttu-id="9f74a-126">By default only RDP connections are allowed into Windows virtual machines deployed in Azure.</span><span class="sxs-lookup"><span data-stu-id="9f74a-126">By default only RDP connections are allowed into Windows virtual machines deployed in Azure.</span></span> <span data-ttu-id="9f74a-127">If this VM is going to be a webserver, you need to open port 80 from the Internet.</span><span class="sxs-lookup"><span data-stu-id="9f74a-127">If this VM is going to be a webserver, you need to open port 80 from the Internet.</span></span>  <span data-ttu-id="9f74a-128">A single command is required to open the desired port.</span><span class="sxs-lookup"><span data-stu-id="9f74a-128">A single command is required to open the desired port.</span></span>  
 
 ```azurecli 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```


## <a name="connect-to-virtual-machine"></a><span data-ttu-id="9f74a-129">Connect to virtual machine</span><span class="sxs-lookup"><span data-stu-id="9f74a-129">Connect to virtual machine</span></span>

<span data-ttu-id="9f74a-130">Use the following command to create a remote desktop session with the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="9f74a-130">Use the following command to create a remote desktop session with the virtual machine.</span></span> <span data-ttu-id="9f74a-131">Replace the IP address with the public IP address of your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="9f74a-131">Replace the IP address with the public IP address of your virtual machine.</span></span> <span data-ttu-id="9f74a-132">When prompted, enter the credentials used when creating the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="9f74a-132">When prompted, enter the credentials used when creating the virtual machine.</span></span>

```bash 
mstsc /v:<Public IP Address>
```

## <a name="install-iis-using-powershell"></a><span data-ttu-id="9f74a-133">Install IIS using PowerShell</span><span class="sxs-lookup"><span data-stu-id="9f74a-133">Install IIS using PowerShell</span></span>

<span data-ttu-id="9f74a-134">Now that you have logged into the Azure VM, you can use a single line of PowerShell to install IIS and enable the local firewall rule to allow web traffic.</span><span class="sxs-lookup"><span data-stu-id="9f74a-134">Now that you have logged into the Azure VM, you can use a single line of PowerShell to install IIS and enable the local firewall rule to allow web traffic.</span></span>  <span data-ttu-id="9f74a-135">Open a PowerShell prompt and run the following command:</span><span class="sxs-lookup"><span data-stu-id="9f74a-135">Open a PowerShell prompt and run the following command:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-the-iis-welcome-page"></a><span data-ttu-id="9f74a-136">View the IIS welcome page</span><span class="sxs-lookup"><span data-stu-id="9f74a-136">View the IIS welcome page</span></span>

<span data-ttu-id="9f74a-137">With IIS installed and port 80 now open on your VM from the Internet, you can use a web browser of your choice to view the default IIS welcome page.</span><span class="sxs-lookup"><span data-stu-id="9f74a-137">With IIS installed and port 80 now open on your VM from the Internet, you can use a web browser of your choice to view the default IIS welcome page.</span></span> <span data-ttu-id="9f74a-138">Be sure to use the `publicIpAddress` you documented above to visit the default page.</span><span class="sxs-lookup"><span data-stu-id="9f74a-138">Be sure to use the `publicIpAddress` you documented above to visit the default page.</span></span> 

![IIS default site](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/quick-create-powershell/default-iis-website.png) 
## <a name="delete-virtual-machine"></a><span data-ttu-id="9f74a-140">Delete virtual machine</span><span class="sxs-lookup"><span data-stu-id="9f74a-140">Delete virtual machine</span></span>

<span data-ttu-id="9f74a-141">When no longer needed, the following command can be used to remove the Resource Group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="9f74a-141">When no longer needed, the following command can be used to remove the Resource Group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="9f74a-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="9f74a-142">Next steps</span></span>

[<span data-ttu-id="9f74a-143">Install a role and configure firewall tutorial</span><span class="sxs-lookup"><span data-stu-id="9f74a-143">Install a role and configure firewall tutorial</span></span>](hero-role.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="9f74a-144">Explore VM deployment CLI samples</span><span class="sxs-lookup"><span data-stu-id="9f74a-144">Explore VM deployment CLI samples</span></span>](cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
