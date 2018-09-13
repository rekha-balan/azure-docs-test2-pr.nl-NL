---
title: Delete an Azure Kubernetes Service (AKS) cluster
description: Delete and AKS cluster with the CLI or Azure portal.
services: container-service
author: iainfoulds
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 2/05/2018
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: c8eab17a5c635560d9a5274eb038845238968e02
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866164"
---
# <a name="delete-an-azure-kubernetes-service-aks-cluster"></a><span data-ttu-id="da995-103">Delete an Azure Kubernetes Service (AKS) cluster</span><span class="sxs-lookup"><span data-stu-id="da995-103">Delete an Azure Kubernetes Service (AKS) cluster</span></span>

<span data-ttu-id="da995-104">When deleting an Azure Kubernetes Service cluster, the resource group in which the cluster was deployed remains, however all AKS-related resources are deleted.</span><span class="sxs-lookup"><span data-stu-id="da995-104">When deleting an Azure Kubernetes Service cluster, the resource group in which the cluster was deployed remains, however all AKS-related resources are deleted.</span></span> <span data-ttu-id="da995-105">This document shows how to delete an AKS cluster using the Azure CLI and Azure portal.</span><span class="sxs-lookup"><span data-stu-id="da995-105">This document shows how to delete an AKS cluster using the Azure CLI and Azure portal.</span></span>

<span data-ttu-id="da995-106">In addition to deleting the cluster, the resource group in which it was deployed can be deleted, which also deletes the AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="da995-106">In addition to deleting the cluster, the resource group in which it was deployed can be deleted, which also deletes the AKS cluster.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="da995-107">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="da995-107">Azure CLI</span></span>

<span data-ttu-id="da995-108">Use the [az aks delete][az-aks-delete] command to delete the AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="da995-108">Use the [az aks delete][az-aks-delete] command to delete the AKS cluster.</span></span>

```azurecli-interactive
az aks delete --resource-group myResourceGroup --name myAKSCluster
```

<span data-ttu-id="da995-109">The following options are available with the `az aks delete` command.</span><span class="sxs-lookup"><span data-stu-id="da995-109">The following options are available with the `az aks delete` command.</span></span>

| <span data-ttu-id="da995-110">Argument</span><span class="sxs-lookup"><span data-stu-id="da995-110">Argument</span></span> | <span data-ttu-id="da995-111">Description</span><span class="sxs-lookup"><span data-stu-id="da995-111">Description</span></span> | <span data-ttu-id="da995-112">Required</span><span class="sxs-lookup"><span data-stu-id="da995-112">Required</span></span> |
|---|---|:---:|
| <span data-ttu-id="da995-113">`--name` `-n`</span><span class="sxs-lookup"><span data-stu-id="da995-113">`--name` `-n`</span></span> | <span data-ttu-id="da995-114">Resource name for the managed cluster.</span><span class="sxs-lookup"><span data-stu-id="da995-114">Resource name for the managed cluster.</span></span> | <span data-ttu-id="da995-115">yes</span><span class="sxs-lookup"><span data-stu-id="da995-115">yes</span></span> |
| <span data-ttu-id="da995-116">`--resource-group` `-g`</span><span class="sxs-lookup"><span data-stu-id="da995-116">`--resource-group` `-g`</span></span> | <span data-ttu-id="da995-117">Name of the Azure Kubernetes Service resource group.</span><span class="sxs-lookup"><span data-stu-id="da995-117">Name of the Azure Kubernetes Service resource group.</span></span> | <span data-ttu-id="da995-118">yes</span><span class="sxs-lookup"><span data-stu-id="da995-118">yes</span></span> |
| `--no-wait` | <span data-ttu-id="da995-119">Do not wait for the long-running operation to finish.</span><span class="sxs-lookup"><span data-stu-id="da995-119">Do not wait for the long-running operation to finish.</span></span> | <span data-ttu-id="da995-120">no</span><span class="sxs-lookup"><span data-stu-id="da995-120">no</span></span> |
| <span data-ttu-id="da995-121">`--yes` `-y`</span><span class="sxs-lookup"><span data-stu-id="da995-121">`--yes` `-y`</span></span> | <span data-ttu-id="da995-122">Do not prompt for confirmation.</span><span class="sxs-lookup"><span data-stu-id="da995-122">Do not prompt for confirmation.</span></span> | <span data-ttu-id="da995-123">no</span><span class="sxs-lookup"><span data-stu-id="da995-123">no</span></span> |

## <a name="azure-portal"></a><span data-ttu-id="da995-124">Azure portal</span><span class="sxs-lookup"><span data-stu-id="da995-124">Azure portal</span></span>

<span data-ttu-id="da995-125">While in the Azure portal, browse to the resource group containing the Azure Kubernetes Service (AKS) resource, select the resource, and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="da995-125">While in the Azure portal, browse to the resource group containing the Azure Kubernetes Service (AKS) resource, select the resource, and click **Delete**.</span></span> <span data-ttu-id="da995-126">You are prompted to confirm the delete operation.</span><span class="sxs-lookup"><span data-stu-id="da995-126">You are prompted to confirm the delete operation.</span></span>

![Delete AKS cluster portal](media/container-service-delete-cluster/delete-aks-portal.png)

<!-- LINKS - internal -->
[az-aks-delete]: /cli/azure/aks?view=azure-cli-latest#az-aks-delete