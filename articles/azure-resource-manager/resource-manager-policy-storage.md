---
title: Azure resource policies for storage accounts | Microsoft Docs
description: Describes Azure Resource Manager policies for managing the deployment of storage accounts.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ''
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: tomfitz
ms.openlocfilehash: 75685a21ce4a212638016be62640badd4870454a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671384"
---
# <a name="apply-resource-policies-to-storage-accounts"></a><span data-ttu-id="15481-103">Apply resource policies to storage accounts</span><span class="sxs-lookup"><span data-stu-id="15481-103">Apply resource policies to storage accounts</span></span>
<span data-ttu-id="15481-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply to Azure storage accounts.</span><span class="sxs-lookup"><span data-stu-id="15481-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply to Azure storage accounts.</span></span> <span data-ttu-id="15481-105">These policies ensure consistency for the storage accounts deployed in your organization.</span><span class="sxs-lookup"><span data-stu-id="15481-105">These policies ensure consistency for the storage accounts deployed in your organization.</span></span> 

## <a name="define-permitted-storage-account-types"></a><span data-ttu-id="15481-106">Define permitted storage account types</span><span class="sxs-lookup"><span data-stu-id="15481-106">Define permitted storage account types</span></span>

<span data-ttu-id="15481-107">The following policy restricts which [storage account types](../storage/storage-redundancy.md) can be deployed:</span><span class="sxs-lookup"><span data-stu-id="15481-107">The following policy restricts which [storage account types](../storage/storage-redundancy.md) can be deployed:</span></span>

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/sku.name",
          "in": [
            "Standard_LRS",
            "Standard_GRS"
          ]
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

<span data-ttu-id="15481-108">A similar policy rule with a parameter for accepting the allowed SKUs is available as a built-in policy definition.</span><span class="sxs-lookup"><span data-stu-id="15481-108">A similar policy rule with a parameter for accepting the allowed SKUs is available as a built-in policy definition.</span></span> <span data-ttu-id="15481-109">The built-in policy has the resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`.</span><span class="sxs-lookup"><span data-stu-id="15481-109">The built-in policy has the resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`.</span></span> 

## <a name="define-permitted-access-tier"></a><span data-ttu-id="15481-110">Define permitted access tier</span><span class="sxs-lookup"><span data-stu-id="15481-110">Define permitted access tier</span></span>

<span data-ttu-id="15481-111">The following policy specifies the type of [access tier](../storage/storage-blob-storage-tiers.md) that can be specified for storage accounts:</span><span class="sxs-lookup"><span data-stu-id="15481-111">The following policy specifies the type of [access tier](../storage/storage-blob-storage-tiers.md) that can be specified for storage accounts:</span></span>

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "field": "kind",
        "equals": "BlobStorage"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/accessTier",
          "equals": "cool"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="ensure-encryption-is-enabled"></a><span data-ttu-id="15481-112">Ensure encryption is enabled</span><span class="sxs-lookup"><span data-stu-id="15481-112">Ensure encryption is enabled</span></span>

<span data-ttu-id="15481-113">The following policy requires all storage accounts to enable [Storage service encryption](../storage/storage-service-encryption.md):</span><span class="sxs-lookup"><span data-stu-id="15481-113">The following policy requires all storage accounts to enable [Storage service encryption](../storage/storage-service-encryption.md):</span></span>

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/enableBlobEncryption",
          "equals": "true"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

<span data-ttu-id="15481-114">This policy rule is also available as a built-in policy definition with the resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.</span><span class="sxs-lookup"><span data-stu-id="15481-114">This policy rule is also available as a built-in policy definition with the resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15481-115">Next steps</span><span class="sxs-lookup"><span data-stu-id="15481-115">Next steps</span></span>
* <span data-ttu-id="15481-116">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span><span class="sxs-lookup"><span data-stu-id="15481-116">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="15481-117">The scope can be a subscription, resource group, or resource.</span><span class="sxs-lookup"><span data-stu-id="15481-117">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="15481-118">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="15481-118">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="15481-119">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="15481-119">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="15481-120">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="15481-120">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

