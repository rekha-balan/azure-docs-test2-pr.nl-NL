---
title: Azure StorageAccountSelector UI element | Microsoft Docs
description: Describes the Microsoft.Storage.StorageAccountSelector UI element for Azure portal.
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
ms.openlocfilehash: 5de536a562d234a4c463c862aedffc7c7ca5228d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867320"
---
# <a name="microsoftstoragestorageaccountselector-ui-element"></a><span data-ttu-id="6540c-103">Microsoft.Storage.StorageAccountSelector UI element</span><span class="sxs-lookup"><span data-stu-id="6540c-103">Microsoft.Storage.StorageAccountSelector UI element</span></span>
<span data-ttu-id="6540c-104">A control for selecting a new or existing storage account.</span><span class="sxs-lookup"><span data-stu-id="6540c-104">A control for selecting a new or existing storage account.</span></span>

## <a name="ui-sample"></a><span data-ttu-id="6540c-105">UI sample</span><span class="sxs-lookup"><span data-stu-id="6540c-105">UI sample</span></span>

<span data-ttu-id="6540c-106">The control shows the default value.</span><span class="sxs-lookup"><span data-stu-id="6540c-106">The control shows the default value.</span></span>

![Microsoft.Storage.StorageAccountSelector](./media/managed-application-elements/microsoft.storage.storageaccountselector.png)

<span data-ttu-id="6540c-108">The control enables the user to create a new storage account or select an existing storage account.</span><span class="sxs-lookup"><span data-stu-id="6540c-108">The control enables the user to create a new storage account or select an existing storage account.</span></span>

![Microsoft.Storage.StorageAccountSelector new](./media/managed-application-elements/microsoft.storage.storageaccountselector-new.png)

## <a name="schema"></a><span data-ttu-id="6540c-110">Schema</span><span class="sxs-lookup"><span data-stu-id="6540c-110">Schema</span></span>

```json
{
  "name": "element1",
  "type": "Microsoft.Storage.StorageAccountSelector",
  "label": "Storage account",
  "toolTip": "",
  "defaultValue": {
    "name": "storageaccount01",
    "type": "Premium_LRS"
  },
  "constraints": {
    "allowedTypes": [],
    "excludedTypes": []
  },
  "options": {
    "hideExisting": false
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="6540c-111">Remarks</span><span class="sxs-lookup"><span data-stu-id="6540c-111">Remarks</span></span>
- <span data-ttu-id="6540c-112">If specified, `defaultValue.name` is automatically validated for uniqueness.</span><span class="sxs-lookup"><span data-stu-id="6540c-112">If specified, `defaultValue.name` is automatically validated for uniqueness.</span></span> <span data-ttu-id="6540c-113">If the storage account name isn't unique, the user must specify a different name or choose an existing storage account.</span><span class="sxs-lookup"><span data-stu-id="6540c-113">If the storage account name isn't unique, the user must specify a different name or choose an existing storage account.</span></span>
- <span data-ttu-id="6540c-114">The default value for `defaultValue.type` is **Premium_LRS**.</span><span class="sxs-lookup"><span data-stu-id="6540c-114">The default value for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="6540c-115">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span><span class="sxs-lookup"><span data-stu-id="6540c-115">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span> <span data-ttu-id="6540c-116">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but can't be used simultaneously.</span><span class="sxs-lookup"><span data-stu-id="6540c-116">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but can't be used simultaneously.</span></span>
- <span data-ttu-id="6540c-117">If `options.hideExisting` is **true**, the user can't choose an existing storage account.</span><span class="sxs-lookup"><span data-stu-id="6540c-117">If `options.hideExisting` is **true**, the user can't choose an existing storage account.</span></span> <span data-ttu-id="6540c-118">The default value is **false**.</span><span class="sxs-lookup"><span data-stu-id="6540c-118">The default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="6540c-119">Sample output</span><span class="sxs-lookup"><span data-stu-id="6540c-119">Sample output</span></span>

```json
{
  "name": "storageaccount01",
  "resourceGroup": "rg01",
  "type": "Premium_LRS",
  "newOrExisting": "new"
}
```

## <a name="next-steps"></a><span data-ttu-id="6540c-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="6540c-120">Next steps</span></span>
* <span data-ttu-id="6540c-121">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6540c-121">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).</span></span>
* <span data-ttu-id="6540c-122">For a description of common properties in UI elements, see [CreateUiDefinition elements](create-uidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="6540c-122">For a description of common properties in UI elements, see [CreateUiDefinition elements](create-uidefinition-elements.md).</span></span>
