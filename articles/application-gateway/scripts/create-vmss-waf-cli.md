---
title: Azure CLI Script Sample - Restrict web traffic | Microsoft Docs
description: Azure CLI Script Sample - Create an application gateway with a web application firewall and a virtual machine scale set that uses OWASP rules to restrict traffic.
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
ms.openlocfilehash: 76c45c985f95979caf6a00a7d2e3a36d9ec3ff77
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856222"
---
# <a name="restrict-web-traffic-using-the-azure-cli"></a><span data-ttu-id="3c0fe-103">Restrict web traffic using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3c0fe-103">Restrict web traffic using the Azure CLI</span></span>

<span data-ttu-id="3c0fe-104">This script creates an application gateway with a web application firewall that uses a virtual machine scale set for backend servers.</span><span class="sxs-lookup"><span data-stu-id="3c0fe-104">This script creates an application gateway with a web application firewall that uses a virtual machine scale set for backend servers.</span></span> <span data-ttu-id="3c0fe-105">The web application firewall restricts web traffic based on OWASP rules.</span><span class="sxs-lookup"><span data-stu-id="3c0fe-105">The web application firewall restricts web traffic based on OWASP rules.</span></span> <span data-ttu-id="3c0fe-106">After running the script, you can test the application gateway using its public IP address.</span><span class="sxs-lookup"><span data-stu-id="3c0fe-106">After running the script, you can test the application gateway using its public IP address.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="3c0fe-107">Sample script</span><span class="sxs-lookup"><span data-stu-id="3c0fe-107">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/application-gateway/create-vmss/create-vmss-waf.sh "Create application gateway")]

## <a name="clean-up-deployment"></a><span data-ttu-id="3c0fe-108">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="3c0fe-108">Clean up deployment</span></span> 

<span data-ttu-id="3c0fe-109">Run the following command to remove the resource group, application gateway, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="3c0fe-109">Run the following command to remove the resource group, application gateway, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroupAG --yes
```

## <a name="script-explanation"></a><span data-ttu-id="3c0fe-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="3c0fe-110">Script explanation</span></span>

<span data-ttu-id="3c0fe-111">This script uses the following commands to create the deployment.</span><span class="sxs-lookup"><span data-stu-id="3c0fe-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="3c0fe-112">Each item in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="3c0fe-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="3c0fe-113">Command</span><span class="sxs-lookup"><span data-stu-id="3c0fe-113">Command</span></span> | <span data-ttu-id="3c0fe-114">Notes</span><span class="sxs-lookup"><span data-stu-id="3c0fe-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3c0fe-115">az group create</span><span class="sxs-lookup"><span data-stu-id="3c0fe-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#az-group-create) | <span data-ttu-id="3c0fe-116">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="3c0fe-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3c0fe-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="3c0fe-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#az-net) | <span data-ttu-id="3c0fe-118">Creates a virtual network.</span><span class="sxs-lookup"><span data-stu-id="3c0fe-118">Creates a virtual network.</span></span> |
| [<span data-ttu-id="3c0fe-119">az network vnet subnet create</span><span class="sxs-lookup"><span data-stu-id="3c0fe-119">az network vnet subnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/subnet#az-network_vnet_subnet_create) | <span data-ttu-id="3c0fe-120">Creates a subnet in a virtual network.</span><span class="sxs-lookup"><span data-stu-id="3c0fe-120">Creates a subnet in a virtual network.</span></span> |
| [<span data-ttu-id="3c0fe-121">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="3c0fe-121">az network public-ip create</span></span>](https://docs.microsoft.com/en-us/cli/azure/network/public-ip?view=azure-cli-latest) | <span data-ttu-id="3c0fe-122">Creates the public IP address for the application gateway.</span><span class="sxs-lookup"><span data-stu-id="3c0fe-122">Creates the public IP address for the application gateway.</span></span> |
| [<span data-ttu-id="3c0fe-123">az network application-gateway create</span><span class="sxs-lookup"><span data-stu-id="3c0fe-123">az network application-gateway create</span></span>](https://docs.microsoft.com/en-us/cli/azure/network/application-gateway?view=azure-cli-latest) | <span data-ttu-id="3c0fe-124">Create an application gateway.</span><span class="sxs-lookup"><span data-stu-id="3c0fe-124">Create an application gateway.</span></span> |
| [<span data-ttu-id="3c0fe-125">az vmss create</span><span class="sxs-lookup"><span data-stu-id="3c0fe-125">az vmss create</span></span>](https://docs.microsoft.com/cli/azure/vmss#az-vmss-create) | <span data-ttu-id="3c0fe-126">Creates a virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="3c0fe-126">Creates a virtual machine scale set.</span></span> |
| [<span data-ttu-id="3c0fe-127">az storage account create</span><span class="sxs-lookup"><span data-stu-id="3c0fe-127">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#az-storage-account-create) | <span data-ttu-id="3c0fe-128">Creates a storage account.</span><span class="sxs-lookup"><span data-stu-id="3c0fe-128">Creates a storage account.</span></span> |
| [<span data-ttu-id="3c0fe-129">az monitor diagnostic-settings create</span><span class="sxs-lookup"><span data-stu-id="3c0fe-129">az monitor diagnostic-settings create</span></span>](https://docs.microsoft.com/cli/azure/monitor/diagnostic-settings#az-monitor-diagnostic-settings-create) | <span data-ttu-id="3c0fe-130">Creates a storage account.</span><span class="sxs-lookup"><span data-stu-id="3c0fe-130">Creates a storage account.</span></span> |
| [<span data-ttu-id="3c0fe-131">az network public-ip show</span><span class="sxs-lookup"><span data-stu-id="3c0fe-131">az network public-ip show</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#az-network_public_ip_show) | <span data-ttu-id="3c0fe-132">Gets the public IP address of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="3c0fe-132">Gets the public IP address of the application gateway.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3c0fe-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="3c0fe-133">Next steps</span></span>

<span data-ttu-id="3c0fe-134">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3c0fe-134">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="3c0fe-135">Additional application gateway CLI script samples can be found in the [Azure application gateway documentation](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3c0fe-135">Additional application gateway CLI script samples can be found in the [Azure application gateway documentation](../cli-samples.md).</span></span>
