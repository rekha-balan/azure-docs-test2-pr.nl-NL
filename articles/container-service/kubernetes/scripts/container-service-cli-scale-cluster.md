---
title: Azure CLI Script Sample - Scale an ACS Cluster | Microsoft Docs
description: Azure CLI Script Sample - Scale an ACS Cluster
services: container-service
documentationcenter: ''
author: neilpeterson
manager: jeconnoc
editor: ''
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Kubernetes, DC/OS, Azure
ms.assetid: ''
ms.service: container-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: nepeters
ms.openlocfilehash: 1e5ca9fb44ea3ad15206f36a16e61f2865d79f5f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864853"
---
# <a name="scale-an-azure-container-service-cluster"></a><span data-ttu-id="da846-104">Scale an Azure Container Service Cluster</span><span class="sxs-lookup"><span data-stu-id="da846-104">Scale an Azure Container Service Cluster</span></span>

<span data-ttu-id="da846-105">This sample scales and Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="da846-105">This sample scales and Azure Container Service.</span></span> 

[!INCLUDE [sample-cli-install](../../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="da846-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="da846-106">Sample script</span></span>

```azurecli
az acs scale --resource-group myResourceGroup --name myK8SCluster --new-agent-count 5
```

## <a name="clean-up-deployment"></a><span data-ttu-id="da846-107">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="da846-107">Clean up deployment</span></span> 

<span data-ttu-id="da846-108">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="da846-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="da846-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="da846-109">Script explanation</span></span>

<span data-ttu-id="da846-110">This script uses the following commands to create the deployment.</span><span class="sxs-lookup"><span data-stu-id="da846-110">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="da846-111">Each item in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="da846-111">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="da846-112">Command</span><span class="sxs-lookup"><span data-stu-id="da846-112">Command</span></span> | <span data-ttu-id="da846-113">Notes</span><span class="sxs-lookup"><span data-stu-id="da846-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="da846-114">az acs scale</span><span class="sxs-lookup"><span data-stu-id="da846-114">az acs scale</span></span>](/cli/azure/acs#az-acs-scale) | <span data-ttu-id="da846-115">Scale an ACS cluster.</span><span class="sxs-lookup"><span data-stu-id="da846-115">Scale an ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="da846-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="da846-116">Next steps</span></span>

<span data-ttu-id="da846-117">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="da846-117">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="da846-118">Additional Azure Container Service CLI script samples can be found in the [Azure Container Service documentation](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="da846-118">Additional Azure Container Service CLI script samples can be found in the [Azure Container Service documentation](../cli-samples.md).</span></span>

