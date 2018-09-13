---
title: Azure MultiStorageAccountCombo UI element | Microsoft Docs
description: Describes the Microsoft.Storage.MultiStorageAccountCombo UI element for Azure portal.
services: managed-applications
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: managed-applications
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2018
ms.author: tomfitz
ms.openlocfilehash: f5fa81d53e1728e8f566a2a39aed8311828b20c7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869325"
---
# <a name="microsoftstoragemultistorageaccountcombo-ui-element"></a><span data-ttu-id="e4852-103">Microsoft.Storage.MultiStorageAccountCombo UI element</span><span class="sxs-lookup"><span data-stu-id="e4852-103">Microsoft.Storage.MultiStorageAccountCombo UI element</span></span>
<span data-ttu-id="e4852-104">A group of controls for creating several storage accounts with names that start with a common prefix.</span><span class="sxs-lookup"><span data-stu-id="e4852-104">A group of controls for creating several storage accounts with names that start with a common prefix.</span></span>

## <a name="ui-sample"></a><span data-ttu-id="e4852-105">UI sample</span><span class="sxs-lookup"><span data-stu-id="e4852-105">UI sample</span></span>
![Microsoft.Storage.MultiStorageAccountCombo](./media/managed-application-elements/microsoft.storage.multistorageaccountcombo.png)

## <a name="schema"></a><span data-ttu-id="e4852-107">Schema</span><span class="sxs-lookup"><span data-stu-id="e4852-107">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Storage.MultiStorageAccountCombo",
  "label": {
    "prefix": "Storage account prefix",
    "type": "Storage account type"
  },
  "toolTip": {
    "prefix": "",
    "type": ""
  },
  "defaultValue": {
    "prefix": "sa",
    "type": "Premium_LRS"
  },
  "constraints": {
    "allowedTypes": [],
    "excludedTypes": []
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="e4852-108">Remarks</span><span class="sxs-lookup"><span data-stu-id="e4852-108">Remarks</span></span>
- <span data-ttu-id="e4852-109">The value for `defaultValue.prefix` is concatenated with one or more integers to generate the sequence of storage account names.</span><span class="sxs-lookup"><span data-stu-id="e4852-109">The value for `defaultValue.prefix` is concatenated with one or more integers to generate the sequence of storage account names.</span></span> <span data-ttu-id="e4852-110">For example, if `defaultValue.prefix` is **sa** and `count` is **2**, then storage account names **sa1** and **sa2** are generated.</span><span class="sxs-lookup"><span data-stu-id="e4852-110">For example, if `defaultValue.prefix` is **sa** and `count` is **2**, then storage account names **sa1** and **sa2** are generated.</span></span> <span data-ttu-id="e4852-111">Generated storage account names are validated for uniqueness automatically.</span><span class="sxs-lookup"><span data-stu-id="e4852-111">Generated storage account names are validated for uniqueness automatically.</span></span>
- <span data-ttu-id="e4852-112">The storage account names are generated lexicographically based on `count`.</span><span class="sxs-lookup"><span data-stu-id="e4852-112">The storage account names are generated lexicographically based on `count`.</span></span> <span data-ttu-id="e4852-113">For example, if `count` is 10, then the storage account names end with two-digit integers (01, 02, 03).</span><span class="sxs-lookup"><span data-stu-id="e4852-113">For example, if `count` is 10, then the storage account names end with two-digit integers (01, 02, 03).</span></span>
- <span data-ttu-id="e4852-114">The default value for `defaultValue.prefix` is **null**, and for `defaultValue.type` is **Premium_LRS**.</span><span class="sxs-lookup"><span data-stu-id="e4852-114">The default value for `defaultValue.prefix` is **null**, and for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="e4852-115">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span><span class="sxs-lookup"><span data-stu-id="e4852-115">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span> <span data-ttu-id="e4852-116">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but can't be used simultaneously.</span><span class="sxs-lookup"><span data-stu-id="e4852-116">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but can't be used simultaneously.</span></span>
- <span data-ttu-id="e4852-117">In addition to generating storage account names, `count` is used to set the appropriate multiplier for the element.</span><span class="sxs-lookup"><span data-stu-id="e4852-117">In addition to generating storage account names, `count` is used to set the appropriate multiplier for the element.</span></span> <span data-ttu-id="e4852-118">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').storageAccountCount]`.</span><span class="sxs-lookup"><span data-stu-id="e4852-118">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').storageAccountCount]`.</span></span> <span data-ttu-id="e4852-119">The default value is **1**.</span><span class="sxs-lookup"><span data-stu-id="e4852-119">The default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="e4852-120">Sample output</span><span class="sxs-lookup"><span data-stu-id="e4852-120">Sample output</span></span>

```json
{
  "prefix": "sa",
  "count": 2,
  "resourceGroup": "rg01",
  "type": "Premium_LRS"
}
```

## <a name="next-steps"></a><span data-ttu-id="e4852-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="e4852-121">Next steps</span></span>
* <span data-ttu-id="e4852-122">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e4852-122">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).</span></span>
* <span data-ttu-id="e4852-123">For a description of common properties in UI elements, see [CreateUiDefinition elements](create-uidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="e4852-123">For a description of common properties in UI elements, see [CreateUiDefinition elements](create-uidefinition-elements.md).</span></span>
