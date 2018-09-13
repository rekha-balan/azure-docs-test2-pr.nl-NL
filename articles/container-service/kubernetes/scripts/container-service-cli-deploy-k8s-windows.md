---
title: Azure CLI Script Sample - Create ACS Windows Kubernetes Cluster | Microsoft Docs
description: Azure CLI Script Sample - Create ACS Windows Kubernetes Cluster
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
ms.openlocfilehash: 7078b79685cbb8c593de4832377e841914082abe
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871168"
---
# <a name="create-an-azure-container-service-kubernetes-windows-cluster"></a><span data-ttu-id="4214a-104">Create an Azure Container Service Kubernetes Windows Cluster</span><span class="sxs-lookup"><span data-stu-id="4214a-104">Create an Azure Container Service Kubernetes Windows Cluster</span></span>

<span data-ttu-id="4214a-105">This sample creates an Azure Container Service cluster running Kubernetes for Windows based containers.</span><span class="sxs-lookup"><span data-stu-id="4214a-105">This sample creates an Azure Container Service cluster running Kubernetes for Windows based containers.</span></span>

[!INCLUDE [sample-cli-install](../../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="4214a-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="4214a-106">Sample script</span></span>

```azurecli
az group create --name myResourceGroup --location eastus

az acs create \
  --orchestrator-type kubernetes \
  --resource-group myResourceGroup \
  --name myK8SCluster \
  --generate-ssh-keys \
  --admin-username azureuser \
  --admin-password Password12 \
  --windows
```

## <a name="clean-up-deployment"></a><span data-ttu-id="4214a-107">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="4214a-107">Clean up deployment</span></span> 

<span data-ttu-id="4214a-108">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="4214a-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="4214a-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="4214a-109">Script explanation</span></span>

<span data-ttu-id="4214a-110">This script uses the following commands to create the deployment.</span><span class="sxs-lookup"><span data-stu-id="4214a-110">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="4214a-111">Each item in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="4214a-111">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="4214a-112">Command</span><span class="sxs-lookup"><span data-stu-id="4214a-112">Command</span></span> | <span data-ttu-id="4214a-113">Notes</span><span class="sxs-lookup"><span data-stu-id="4214a-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4214a-114">az group create</span><span class="sxs-lookup"><span data-stu-id="4214a-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#az-group-create) | <span data-ttu-id="4214a-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="4214a-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4214a-116">az acs create</span><span class="sxs-lookup"><span data-stu-id="4214a-116">az acs create</span></span>](https://docs.microsoft.com/cli/azure/acs#az-acs-create) | <span data-ttu-id="4214a-117">Creates and ACS cluster.</span><span class="sxs-lookup"><span data-stu-id="4214a-117">Creates and ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4214a-118">Next steps</span><span class="sxs-lookup"><span data-stu-id="4214a-118">Next steps</span></span>

<span data-ttu-id="4214a-119">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="4214a-119">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="4214a-120">Additional Azure Container Service CLI script samples can be found in the [Azure Container Service documentation](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4214a-120">Additional Azure Container Service CLI script samples can be found in the [Azure Container Service documentation](../cli-samples.md).</span></span>
