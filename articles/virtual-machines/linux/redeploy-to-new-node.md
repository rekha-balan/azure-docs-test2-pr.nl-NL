---
title: Redeploy Linux Virtual Machines in Azure | Microsoft Docs
description: How to redeploy Linux virtual machines in Azure to mitigate SSH connection issues.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
tags: azure-resource-manager,top-support-issue
ms.assetid: e9530dd6-f5b0-4160-b36b-d75151d99eb7
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/16/2016
ms.author: iainfou
ms.openlocfilehash: e185680119c49b88a13e1265584e22d2eee12658
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563368"
---
# <a name="redeploy-linux-virtual-machine-to-new-azure-node"></a><span data-ttu-id="4cd3a-103">Redeploy Linux virtual machine to new Azure node</span><span class="sxs-lookup"><span data-stu-id="4cd3a-103">Redeploy Linux virtual machine to new Azure node</span></span>
<span data-ttu-id="4cd3a-104">If you have been facing difficulties troubleshooting SSH or application access to a Linux virtual machine (VM) in Azure, redeploying the VM may help.</span><span class="sxs-lookup"><span data-stu-id="4cd3a-104">If you have been facing difficulties troubleshooting SSH or application access to a Linux virtual machine (VM) in Azure, redeploying the VM may help.</span></span> <span data-ttu-id="4cd3a-105">When you redeploy a VM, it moves the VM to a new node within the Azure infrastructure and then powers it back on, retaining all your configuration options and associated resources.</span><span class="sxs-lookup"><span data-stu-id="4cd3a-105">When you redeploy a VM, it moves the VM to a new node within the Azure infrastructure and then powers it back on, retaining all your configuration options and associated resources.</span></span> <span data-ttu-id="4cd3a-106">This article shows you how to redeploy a VM using Azure CLI or the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4cd3a-106">This article shows you how to redeploy a VM using Azure CLI or the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="4cd3a-107">After you redeploy a VM, the temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span><span class="sxs-lookup"><span data-stu-id="4cd3a-107">After you redeploy a VM, the temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span> 

<span data-ttu-id="4cd3a-108">You can redeploy a VM using one of the following options.</span><span class="sxs-lookup"><span data-stu-id="4cd3a-108">You can redeploy a VM using one of the following options.</span></span> <span data-ttu-id="4cd3a-109">You only need to choose one option to redeploy your VM:</span><span class="sxs-lookup"><span data-stu-id="4cd3a-109">You only need to choose one option to redeploy your VM:</span></span>

- [<span data-ttu-id="4cd3a-110">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4cd3a-110">Azure CLI 2.0</span></span>](#azure-cli-20)
- [<span data-ttu-id="4cd3a-111">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="4cd3a-111">Azure CLI 1.0</span></span>](#azure-cli-10)
- [<span data-ttu-id="4cd3a-112">Azure portal</span><span class="sxs-lookup"><span data-stu-id="4cd3a-112">Azure portal</span></span>](#using-azure-portal)

## <a name="azure-cli-20"></a><span data-ttu-id="4cd3a-113">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4cd3a-113">Azure CLI 2.0</span></span>
<span data-ttu-id="4cd3a-114">Install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="4cd3a-114">Install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="4cd3a-115">Redeploy your VM with [az vm redeploy](/cli/azure/vm#redeploy).</span><span class="sxs-lookup"><span data-stu-id="4cd3a-115">Redeploy your VM with [az vm redeploy](/cli/azure/vm#redeploy).</span></span> <span data-ttu-id="4cd3a-116">The following example redeploys the VM named `myVM` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="4cd3a-116">The following example redeploys the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM 
```

## <a name="azure-cli-10"></a><span data-ttu-id="4cd3a-117">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="4cd3a-117">Azure CLI 1.0</span></span>
<span data-ttu-id="4cd3a-118">Install the [latest Azure CLI 1.0](../../cli-install-nodejs.md), log in to an Azure account, and make sure that you are in Resource Manager mode (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="4cd3a-118">Install the [latest Azure CLI 1.0](../../cli-install-nodejs.md), log in to an Azure account, and make sure that you are in Resource Manager mode (`azure config mode arm`).</span></span>

<span data-ttu-id="4cd3a-119">The following example redeploys the VM named `myVM` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="4cd3a-119">The following example redeploys the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --vm-name myVM 
```

[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a><span data-ttu-id="4cd3a-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="4cd3a-120">Next steps</span></span>
<span data-ttu-id="4cd3a-121">If you are having issues connecting to your VM, you can find specific help on [troubleshooting SSH connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [detailed SSH troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4cd3a-121">If you are having issues connecting to your VM, you can find specific help on [troubleshooting SSH connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [detailed SSH troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="4cd3a-122">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4cd3a-122">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

