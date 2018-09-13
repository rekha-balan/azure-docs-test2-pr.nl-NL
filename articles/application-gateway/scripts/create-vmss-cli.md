---
title: Azure CLI Script Sample - Manage web traffic | Microsoft Docs
description: Azure CLI Script Sample - Manage web traffic with an application gateway and a virtual machine scale set.
services: application-gateway
documentationcenter: networking
author: vhorne
manager: jpconnock
editor: tysonn
tags: azure-resource-manager
ms.service: application-gateway
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 01/29/2018
ms.author: victorh
ms.custom: mvc
ms.openlocfilehash: a2046c6d4bbaf91db6a6c4de2023717eaf13fadb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868733"
---
# <a name="manage-web-traffic-using-the-azure-cli"></a><span data-ttu-id="21f74-103">Manage web traffic using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="21f74-103">Manage web traffic using the Azure CLI</span></span>

<span data-ttu-id="21f74-104">This script creates an application gateway that uses a virtual machine scale set for backend servers.</span><span class="sxs-lookup"><span data-stu-id="21f74-104">This script creates an application gateway that uses a virtual machine scale set for backend servers.</span></span> <span data-ttu-id="21f74-105">The application gateway can then be configured to manage web traffic.</span><span class="sxs-lookup"><span data-stu-id="21f74-105">The application gateway can then be configured to manage web traffic.</span></span> <span data-ttu-id="21f74-106">After running the script, you can test the application gateway using its public IP address.</span><span class="sxs-lookup"><span data-stu-id="21f74-106">After running the script, you can test the application gateway using its public IP address.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="21f74-107">Sample script</span><span class="sxs-lookup"><span data-stu-id="21f74-107">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/application-gateway/create-vmss/create-vmss.sh "Create application gateway")]

## <a name="clean-up-deployment"></a><span data-ttu-id="21f74-108">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="21f74-108">Clean up deployment</span></span> 

<span data-ttu-id="21f74-109">Run the following command to remove the resource group, application gateway, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="21f74-109">Run the following command to remove the resource group, application gateway, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroupAG --yes
```

## <a name="script-explanation"></a><span data-ttu-id="21f74-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="21f74-110">Script explanation</span></span>

<span data-ttu-id="21f74-111">This script uses the following commands to create the deployment.</span><span class="sxs-lookup"><span data-stu-id="21f74-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="21f74-112">Each item in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="21f74-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="21f74-113">Command</span><span class="sxs-lookup"><span data-stu-id="21f74-113">Command</span></span> | <span data-ttu-id="21f74-114">Notes</span><span class="sxs-lookup"><span data-stu-id="21f74-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="21f74-115">az group create</span><span class="sxs-lookup"><span data-stu-id="21f74-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#az-group-create) | <span data-ttu-id="21f74-116">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="21f74-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="21f74-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="21f74-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#az-net) | <span data-ttu-id="21f74-118">Creates a virtual network.</span><span class="sxs-lookup"><span data-stu-id="21f74-118">Creates a virtual network.</span></span> |
| [<span data-ttu-id="21f74-119">az network vnet subnet create</span><span class="sxs-lookup"><span data-stu-id="21f74-119">az network vnet subnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/subnet#az-network_vnet_subnet_create) | <span data-ttu-id="21f74-120">Creates a subnet in a virtual network.</span><span class="sxs-lookup"><span data-stu-id="21f74-120">Creates a subnet in a virtual network.</span></span> |
| [<span data-ttu-id="21f74-121">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="21f74-121">az network public-ip create</span></span>](https://docs.microsoft.com/en-us/cli/azure/network/public-ip?view=azure-cli-latest) | <span data-ttu-id="21f74-122">Creates the public IP address for the application gateway.</span><span class="sxs-lookup"><span data-stu-id="21f74-122">Creates the public IP address for the application gateway.</span></span> |
| [<span data-ttu-id="21f74-123">az network application-gateway create</span><span class="sxs-lookup"><span data-stu-id="21f74-123">az network application-gateway create</span></span>](https://docs.microsoft.com/en-us/cli/azure/network/application-gateway?view=azure-cli-latest) | <span data-ttu-id="21f74-124">Create an application gateway.</span><span class="sxs-lookup"><span data-stu-id="21f74-124">Create an application gateway.</span></span> |
| [<span data-ttu-id="21f74-125">az vmss create</span><span class="sxs-lookup"><span data-stu-id="21f74-125">az vmss create</span></span>](https://docs.microsoft.com/cli/azure/vmss#az-vmss-create) | <span data-ttu-id="21f74-126">Creates a virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="21f74-126">Creates a virtual machine scale set.</span></span> |
| [<span data-ttu-id="21f74-127">az network public-ip show</span><span class="sxs-lookup"><span data-stu-id="21f74-127">az network public-ip show</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#az-network_public_ip_show) | <span data-ttu-id="21f74-128">Gets the public IP address of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="21f74-128">Gets the public IP address of the application gateway.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="21f74-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="21f74-129">Next steps</span></span>

<span data-ttu-id="21f74-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="21f74-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="21f74-131">Additional application gateway CLI script samples can be found in the [Azure Windows VM documentation](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="21f74-131">Additional application gateway CLI script samples can be found in the [Azure Windows VM documentation](../cli-samples.md).</span></span>
