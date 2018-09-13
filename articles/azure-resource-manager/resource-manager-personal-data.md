---
title: Azure Resource Manager personal data | Microsoft Docs
description: Learn how to manage personal data associated with Azure Resource Manager operations.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/14/2018
ms.author: tomfitz
ms.openlocfilehash: 71928be07080ed14fdcb93f33ea64d2572955b53
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865816"
---
# <a name="manage-personal-data-associated-with-azure-resource-manager"></a><span data-ttu-id="a3337-103">Manage personal data associated with Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a3337-103">Manage personal data associated with Azure Resource Manager</span></span>

<span data-ttu-id="a3337-104">To avoid exposing sensitive information, delete any personal information you may have provided in deployments, resource groups, or tags.</span><span class="sxs-lookup"><span data-stu-id="a3337-104">To avoid exposing sensitive information, delete any personal information you may have provided in deployments, resource groups, or tags.</span></span> <span data-ttu-id="a3337-105">Azure Resource Manager provides operations that let you manage personal data you may have provided in deployments, resource groups, or tags.</span><span class="sxs-lookup"><span data-stu-id="a3337-105">Azure Resource Manager provides operations that let you manage personal data you may have provided in deployments, resource groups, or tags.</span></span>

[!INCLUDE [Handle personal data](../../includes/gdpr-intro-sentence.md)]

## <a name="delete-personal-data-in-deployment-history"></a><span data-ttu-id="a3337-106">Delete personal data in deployment history</span><span class="sxs-lookup"><span data-stu-id="a3337-106">Delete personal data in deployment history</span></span>

<span data-ttu-id="a3337-107">For deployments, Resource Manager retains parameter values and status messages in the deployment history.</span><span class="sxs-lookup"><span data-stu-id="a3337-107">For deployments, Resource Manager retains parameter values and status messages in the deployment history.</span></span> <span data-ttu-id="a3337-108">These values persist until you delete the deployment from the history.</span><span class="sxs-lookup"><span data-stu-id="a3337-108">These values persist until you delete the deployment from the history.</span></span> <span data-ttu-id="a3337-109">To see if you have provided personal data in these values, list the deployments.</span><span class="sxs-lookup"><span data-stu-id="a3337-109">To see if you have provided personal data in these values, list the deployments.</span></span> <span data-ttu-id="a3337-110">If you find personal data, delete the deployments from the history.</span><span class="sxs-lookup"><span data-stu-id="a3337-110">If you find personal data, delete the deployments from the history.</span></span>

<span data-ttu-id="a3337-111">To list **deployments** in the history, use:</span><span class="sxs-lookup"><span data-stu-id="a3337-111">To list **deployments** in the history, use:</span></span>

* [<span data-ttu-id="a3337-112">List By Resource Group</span><span class="sxs-lookup"><span data-stu-id="a3337-112">List By Resource Group</span></span>](/rest/api/resources/deployments/listbyresourcegroup)
* [<span data-ttu-id="a3337-113">Get-AzureRmResourceGroupDeployment</span><span class="sxs-lookup"><span data-stu-id="a3337-113">Get-AzureRmResourceGroupDeployment</span></span>](/powershell/module/azurerm.resources/Get-AzureRmResourceGroupDeployment)
* [<span data-ttu-id="a3337-114">az group deployment list</span><span class="sxs-lookup"><span data-stu-id="a3337-114">az group deployment list</span></span>](/cli/azure/group/deployment#az-group-deployment-list)

<span data-ttu-id="a3337-115">To delete **deployments** from the history, use:</span><span class="sxs-lookup"><span data-stu-id="a3337-115">To delete **deployments** from the history, use:</span></span>

* [<span data-ttu-id="a3337-116">Delete</span><span class="sxs-lookup"><span data-stu-id="a3337-116">Delete</span></span>](/rest/api/resources/deployments/delete)
* [<span data-ttu-id="a3337-117">Remove-AzureRmResourceGroupDeployment</span><span class="sxs-lookup"><span data-stu-id="a3337-117">Remove-AzureRmResourceGroupDeployment</span></span>](/powershell/module/azurerm.resources/Remove-AzureRmResourceGroupDeployment)
* [<span data-ttu-id="a3337-118">az group deployment delete</span><span class="sxs-lookup"><span data-stu-id="a3337-118">az group deployment delete</span></span>](/cli/azure/group/deployment#az-group-deployment-delete)

## <a name="delete-personal-data-in-resource-group-names"></a><span data-ttu-id="a3337-119">Delete personal data in resource group names</span><span class="sxs-lookup"><span data-stu-id="a3337-119">Delete personal data in resource group names</span></span>

<span data-ttu-id="a3337-120">The name of the resource group persists until you delete the resource group.</span><span class="sxs-lookup"><span data-stu-id="a3337-120">The name of the resource group persists until you delete the resource group.</span></span> <span data-ttu-id="a3337-121">To see if you have provided personal data in the names, list the resource groups.</span><span class="sxs-lookup"><span data-stu-id="a3337-121">To see if you have provided personal data in the names, list the resource groups.</span></span> <span data-ttu-id="a3337-122">If you find personal data, [move the resources](resource-group-move-resources.md) to a new resource group, and delete the resource group with personal data in the name.</span><span class="sxs-lookup"><span data-stu-id="a3337-122">If you find personal data, [move the resources](resource-group-move-resources.md) to a new resource group, and delete the resource group with personal data in the name.</span></span>

<span data-ttu-id="a3337-123">To list **resource groups**, use:</span><span class="sxs-lookup"><span data-stu-id="a3337-123">To list **resource groups**, use:</span></span>

* [<span data-ttu-id="a3337-124">List</span><span class="sxs-lookup"><span data-stu-id="a3337-124">List</span></span>](/rest/api/resources/resourcegroups/list)
* [<span data-ttu-id="a3337-125">Get-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a3337-125">Get-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/Get-AzureRmResourceGroup)
* [<span data-ttu-id="a3337-126">az group list</span><span class="sxs-lookup"><span data-stu-id="a3337-126">az group list</span></span>](/cli/azure/group#az-group-list)

<span data-ttu-id="a3337-127">To delete **resource groups**, use:</span><span class="sxs-lookup"><span data-stu-id="a3337-127">To delete **resource groups**, use:</span></span>

* [<span data-ttu-id="a3337-128">Delete</span><span class="sxs-lookup"><span data-stu-id="a3337-128">Delete</span></span>](/rest/api/resources/resourcegroups/delete)
* [<span data-ttu-id="a3337-129">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a3337-129">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/Remove-AzureRmResourceGroup)
* [<span data-ttu-id="a3337-130">az group delete</span><span class="sxs-lookup"><span data-stu-id="a3337-130">az group delete</span></span>](/cli/azure/group#az-group-delete)

## <a name="delete-personal-data-in-tags"></a><span data-ttu-id="a3337-131">Delete personal data in tags</span><span class="sxs-lookup"><span data-stu-id="a3337-131">Delete personal data in tags</span></span>

<span data-ttu-id="a3337-132">Tags names and values persist until you delete or modify the tag.</span><span class="sxs-lookup"><span data-stu-id="a3337-132">Tags names and values persist until you delete or modify the tag.</span></span> <span data-ttu-id="a3337-133">To see if you have provided personal data in the tags, list the tags.</span><span class="sxs-lookup"><span data-stu-id="a3337-133">To see if you have provided personal data in the tags, list the tags.</span></span> <span data-ttu-id="a3337-134">If you find personal data, delete the tags.</span><span class="sxs-lookup"><span data-stu-id="a3337-134">If you find personal data, delete the tags.</span></span>

<span data-ttu-id="a3337-135">To list **tags**, use:</span><span class="sxs-lookup"><span data-stu-id="a3337-135">To list **tags**, use:</span></span>

* [<span data-ttu-id="a3337-136">List</span><span class="sxs-lookup"><span data-stu-id="a3337-136">List</span></span>](/rest/api/resources/tags/list)
* [<span data-ttu-id="a3337-137">Get-AzureRmTag</span><span class="sxs-lookup"><span data-stu-id="a3337-137">Get-AzureRmTag</span></span>](/powershell/module/azurerm.tags/get-azurermtag)
* [<span data-ttu-id="a3337-138">az tag list</span><span class="sxs-lookup"><span data-stu-id="a3337-138">az tag list</span></span>](/cli/azure/tag#az-tag-list)

<span data-ttu-id="a3337-139">To delete **tags**, use:</span><span class="sxs-lookup"><span data-stu-id="a3337-139">To delete **tags**, use:</span></span>

* [<span data-ttu-id="a3337-140">Delete</span><span class="sxs-lookup"><span data-stu-id="a3337-140">Delete</span></span>](/rest/api/resources/tags/delete)
* [<span data-ttu-id="a3337-141">Remove-AzureRmTag</span><span class="sxs-lookup"><span data-stu-id="a3337-141">Remove-AzureRmTag</span></span>](/powershell/module/azurerm.tags/remove-azurermtag)
* [<span data-ttu-id="a3337-142">az tag delete</span><span class="sxs-lookup"><span data-stu-id="a3337-142">az tag delete</span></span>](/cli/azure/tag#az-tag-delete)

## <a name="next-steps"></a><span data-ttu-id="a3337-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="a3337-143">Next steps</span></span>
* <span data-ttu-id="a3337-144">For an overview of Azure Resource Manager, see the [What is Resource Manager?](resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="a3337-144">For an overview of Azure Resource Manager, see the [What is Resource Manager?](resource-group-overview.md)</span></span>