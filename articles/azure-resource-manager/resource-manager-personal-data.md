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
# <a name="manage-personal-data-associated-with-azure-resource-manager"></a>Manage personal data associated with Azure Resource Manager

To avoid exposing sensitive information, delete any personal information you may have provided in deployments, resource groups, or tags. Azure Resource Manager provides operations that let you manage personal data you may have provided in deployments, resource groups, or tags.

[!INCLUDE [Handle personal data](../../includes/gdpr-intro-sentence.md)]

## <a name="delete-personal-data-in-deployment-history"></a>Delete personal data in deployment history

For deployments, Resource Manager retains parameter values and status messages in the deployment history. These values persist until you delete the deployment from the history. To see if you have provided personal data in these values, list the deployments. If you find personal data, delete the deployments from the history.

To list **deployments** in the history, use:

* [List By Resource Group](/rest/api/resources/deployments/listbyresourcegroup)
* [Get-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/Get-AzureRmResourceGroupDeployment)
* [az group deployment list](/cli/azure/group/deployment#az-group-deployment-list)

To delete **deployments** from the history, use:

* [Delete](/rest/api/resources/deployments/delete)
* [Remove-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/Remove-AzureRmResourceGroupDeployment)
* [az group deployment delete](/cli/azure/group/deployment#az-group-deployment-delete)

## <a name="delete-personal-data-in-resource-group-names"></a>Delete personal data in resource group names

The name of the resource group persists until you delete the resource group. To see if you have provided personal data in the names, list the resource groups. If you find personal data, [move the resources](resource-group-move-resources.md) to a new resource group, and delete the resource group with personal data in the name.

To list **resource groups**, use:

* [List](/rest/api/resources/resourcegroups/list)
* [Get-AzureRmResourceGroup](/powershell/module/azurerm.resources/Get-AzureRmResourceGroup)
* [az group list](/cli/azure/group#az-group-list)

To delete **resource groups**, use:

* [Delete](/rest/api/resources/resourcegroups/delete)
* [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/Remove-AzureRmResourceGroup)
* [az group delete](/cli/azure/group#az-group-delete)

## <a name="delete-personal-data-in-tags"></a>Delete personal data in tags

Tags names and values persist until you delete or modify the tag. To see if you have provided personal data in the tags, list the tags. If you find personal data, delete the tags.

To list **tags**, use:

* [List](/rest/api/resources/tags/list)
* [Get-AzureRmTag](/powershell/module/azurerm.tags/get-azurermtag)
* [az tag list](/cli/azure/tag#az-tag-list)

To delete **tags**, use:

* [Delete](/rest/api/resources/tags/delete)
* [Remove-AzureRmTag](/powershell/module/azurerm.tags/remove-azurermtag)
* [az tag delete](/cli/azure/tag#az-tag-delete)

## <a name="next-steps"></a>Next steps
* For an overview of Azure Resource Manager, see the [What is Resource Manager?](resource-group-overview.md)