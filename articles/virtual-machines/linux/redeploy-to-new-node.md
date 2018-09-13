---
title: Redeploy Linux Virtual Machines in Azure | Microsoft Docs
description: How to redeploy Linux virtual machines in Azure to mitigate SSH connection issues.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: jeconnoc
tags: azure-resource-manager,top-support-issue
ms.assetid: e9530dd6-f5b0-4160-b36b-d75151d99eb7
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/14/2017
ms.author: cynthn
ms.openlocfilehash: 8c3532232d796b96f9ed583504ba7ab28b499e6d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44812044"
---
# <a name="redeploy-linux-virtual-machine-to-new-azure-node"></a><span data-ttu-id="5d416-103">Redeploy Linux virtual machine to new Azure node</span><span class="sxs-lookup"><span data-stu-id="5d416-103">Redeploy Linux virtual machine to new Azure node</span></span>
<span data-ttu-id="5d416-104">If you face difficulties troubleshooting SSH or application access to a Linux virtual machine (VM) in Azure, redeploying the VM may help.</span><span class="sxs-lookup"><span data-stu-id="5d416-104">If you face difficulties troubleshooting SSH or application access to a Linux virtual machine (VM) in Azure, redeploying the VM may help.</span></span> <span data-ttu-id="5d416-105">When you redeploy a VM, it moves the VM to a new node within the Azure infrastructure and then powers it back on.</span><span class="sxs-lookup"><span data-stu-id="5d416-105">When you redeploy a VM, it moves the VM to a new node within the Azure infrastructure and then powers it back on.</span></span> <span data-ttu-id="5d416-106">All your configuration options and associated resources are retained.</span><span class="sxs-lookup"><span data-stu-id="5d416-106">All your configuration options and associated resources are retained.</span></span> <span data-ttu-id="5d416-107">This article shows you how to redeploy a VM using Azure CLI or the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="5d416-107">This article shows you how to redeploy a VM using Azure CLI or the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="5d416-108">After you redeploy a VM, the temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span><span class="sxs-lookup"><span data-stu-id="5d416-108">After you redeploy a VM, the temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span> 

<span data-ttu-id="5d416-109">You can redeploy a VM using one of the following options.</span><span class="sxs-lookup"><span data-stu-id="5d416-109">You can redeploy a VM using one of the following options.</span></span> <span data-ttu-id="5d416-110">You only need to choose one option to redeploy your VM:</span><span class="sxs-lookup"><span data-stu-id="5d416-110">You only need to choose one option to redeploy your VM:</span></span>

- [<span data-ttu-id="5d416-111">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5d416-111">Azure CLI 2.0</span></span>](#azure-cli-20)
- [<span data-ttu-id="5d416-112">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5d416-112">Azure CLI 1.0</span></span>](#azure-cli-10)
- [<span data-ttu-id="5d416-113">Azure portal</span><span class="sxs-lookup"><span data-stu-id="5d416-113">Azure portal</span></span>](#using-azure-portal)

## <a name="use-the-azure-cli-20"></a><span data-ttu-id="5d416-114">Use the Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5d416-114">Use the Azure CLI 2.0</span></span>
<span data-ttu-id="5d416-115">Install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to your Azure account using [az login](/cli/azure/reference-index#az_login).</span><span class="sxs-lookup"><span data-stu-id="5d416-115">Install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to your Azure account using [az login](/cli/azure/reference-index#az_login).</span></span>

<span data-ttu-id="5d416-116">Redeploy your VM with [az vm redeploy](/cli/azure/vm#az_vm_redeploy).</span><span class="sxs-lookup"><span data-stu-id="5d416-116">Redeploy your VM with [az vm redeploy](/cli/azure/vm#az_vm_redeploy).</span></span> <span data-ttu-id="5d416-117">The following example redeploys the VM named *myVM* in the resource group named *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="5d416-117">The following example redeploys the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM 
```

## <a name="use-the-azure-cli-10"></a><span data-ttu-id="5d416-118">Use the Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5d416-118">Use the Azure CLI 1.0</span></span>
<span data-ttu-id="5d416-119">Install the [latest Azure CLI 1.0](../../cli-install-nodejs.md) and log in to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="5d416-119">Install the [latest Azure CLI 1.0](../../cli-install-nodejs.md) and log in to your Azure account.</span></span> <span data-ttu-id="5d416-120">Make sure that you are in Resource Manager mode (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="5d416-120">Make sure that you are in Resource Manager mode (`azure config mode arm`).</span></span>

<span data-ttu-id="5d416-121">The following example redeploys the VM named *myVM* in the resource group named *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="5d416-121">The following example redeploys the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --vm-name myVM 
```

[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a><span data-ttu-id="5d416-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="5d416-122">Next steps</span></span>
<span data-ttu-id="5d416-123">If you are having issues connecting to your VM, you can find specific help on [troubleshooting SSH connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [detailed SSH troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5d416-123">If you are having issues connecting to your VM, you can find specific help on [troubleshooting SSH connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [detailed SSH troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="5d416-124">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5d416-124">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

