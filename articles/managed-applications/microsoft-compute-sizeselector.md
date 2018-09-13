---
title: Azure SizeSelector UI element | Microsoft Docs
description: Describes the Microsoft.Compute.SizeSelector UI element for Azure portal.
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
ms.date: 06/27/2018
ms.author: tomfitz
ms.openlocfilehash: 9009d29e281ace179ad1dd2021c7cf35e3dc611a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857037"
---
# <a name="microsoftcomputesizeselector-ui-element"></a><span data-ttu-id="c6b30-103">Microsoft.Compute.SizeSelector UI element</span><span class="sxs-lookup"><span data-stu-id="c6b30-103">Microsoft.Compute.SizeSelector UI element</span></span>
<span data-ttu-id="c6b30-104">A control for selecting a size for one or more virtual machine instances.</span><span class="sxs-lookup"><span data-stu-id="c6b30-104">A control for selecting a size for one or more virtual machine instances.</span></span>

## <a name="ui-sample"></a><span data-ttu-id="c6b30-105">UI sample</span><span class="sxs-lookup"><span data-stu-id="c6b30-105">UI sample</span></span>

<span data-ttu-id="c6b30-106">The user sees a selector with default values from the element definition.</span><span class="sxs-lookup"><span data-stu-id="c6b30-106">The user sees a selector with default values from the element definition.</span></span>

![Microsoft.Compute.SizeSelector](./media/managed-application-elements/microsoft.compute.sizeselector.png)

<span data-ttu-id="c6b30-108">After selecting the control, the user sees an expanded view of the available sizes.</span><span class="sxs-lookup"><span data-stu-id="c6b30-108">After selecting the control, the user sees an expanded view of the available sizes.</span></span>

![Microsoft.Compute.SizeSelector expanded](./media/managed-application-elements/microsoft.compute.sizeselector-expanded.png)

## <a name="schema"></a><span data-ttu-id="c6b30-110">Schema</span><span class="sxs-lookup"><span data-stu-id="c6b30-110">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.SizeSelector",
  "label": "Size",
  "toolTip": "",
  "recommendedSizes": [
    "Standard_D1",
    "Standard_D2",
    "Standard_D3"
  ],
  "constraints": {
    "allowedSizes": [],
    "excludedSizes": [],
    "numAvailabilityZonesRequired": 3,
    "zone": "3"
  },
  "options": {
    "hideDiskTypeFilter": false
  },
  "osPlatform": "Windows",
  "imageReference": {
    "publisher": "MicrosoftWindowsServer",
    "offer": "WindowsServer",
    "sku": "2012-R2-Datacenter"
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="c6b30-111">Remarks</span><span class="sxs-lookup"><span data-stu-id="c6b30-111">Remarks</span></span>
- <span data-ttu-id="c6b30-112">`recommendedSizes` should have at least one size.</span><span class="sxs-lookup"><span data-stu-id="c6b30-112">`recommendedSizes` should have at least one size.</span></span> <span data-ttu-id="c6b30-113">The first recommended size is used as the default.</span><span class="sxs-lookup"><span data-stu-id="c6b30-113">The first recommended size is used as the default.</span></span> <span data-ttu-id="c6b30-114">The list of available sizes isn't sorted by the recommended state.</span><span class="sxs-lookup"><span data-stu-id="c6b30-114">The list of available sizes isn't sorted by the recommended state.</span></span> <span data-ttu-id="c6b30-115">The user can select that column to sort by recommended state.</span><span class="sxs-lookup"><span data-stu-id="c6b30-115">The user can select that column to sort by recommended state.</span></span>
- <span data-ttu-id="c6b30-116">If a recommended size isn't available in the selected location, the size is automatically skipped.</span><span class="sxs-lookup"><span data-stu-id="c6b30-116">If a recommended size isn't available in the selected location, the size is automatically skipped.</span></span> <span data-ttu-id="c6b30-117">Instead, the next recommended size is used.</span><span class="sxs-lookup"><span data-stu-id="c6b30-117">Instead, the next recommended size is used.</span></span>
- <span data-ttu-id="c6b30-118">`constraints.allowedSizes` and `constraints.excludedSizes` are both optional, but can't be used simultaneously.</span><span class="sxs-lookup"><span data-stu-id="c6b30-118">`constraints.allowedSizes` and `constraints.excludedSizes` are both optional, but can't be used simultaneously.</span></span> <span data-ttu-id="c6b30-119">The list of available sizes can be determined by calling [List available virtual machine sizes for a subscription](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span><span class="sxs-lookup"><span data-stu-id="c6b30-119">The list of available sizes can be determined by calling [List available virtual machine sizes for a subscription](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span></span> <span data-ttu-id="c6b30-120">Any size not specified in the `constraints.allowedSizes` is hidden, and any size not specified in `constraints.excludedSizes` is shown.</span><span class="sxs-lookup"><span data-stu-id="c6b30-120">Any size not specified in the `constraints.allowedSizes` is hidden, and any size not specified in `constraints.excludedSizes` is shown.</span></span>
- <span data-ttu-id="c6b30-121">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span><span class="sxs-lookup"><span data-stu-id="c6b30-121">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span> <span data-ttu-id="c6b30-122">It's used to determine the hardware costs of the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="c6b30-122">It's used to determine the hardware costs of the virtual machines.</span></span>
- <span data-ttu-id="c6b30-123">`imageReference` is omitted for first-party images, but provided for third-party images.</span><span class="sxs-lookup"><span data-stu-id="c6b30-123">`imageReference` is omitted for first-party images, but provided for third-party images.</span></span> <span data-ttu-id="c6b30-124">It's used to determine the software costs of the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="c6b30-124">It's used to determine the software costs of the virtual machines.</span></span>
- <span data-ttu-id="c6b30-125">`count` is used to set the appropriate multiplier for the element.</span><span class="sxs-lookup"><span data-stu-id="c6b30-125">`count` is used to set the appropriate multiplier for the element.</span></span> <span data-ttu-id="c6b30-126">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').vmCount]`.</span><span class="sxs-lookup"><span data-stu-id="c6b30-126">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').vmCount]`.</span></span> <span data-ttu-id="c6b30-127">The default value is **1**.</span><span class="sxs-lookup"><span data-stu-id="c6b30-127">The default value is **1**.</span></span>
- <span data-ttu-id="c6b30-128">The `numAvailabilityZonesRequired` can be 1, 2, or 3.</span><span class="sxs-lookup"><span data-stu-id="c6b30-128">The `numAvailabilityZonesRequired` can be 1, 2, or 3.</span></span>
- <span data-ttu-id="c6b30-129">By default, `hideDiskTypeFilter` is **false**.</span><span class="sxs-lookup"><span data-stu-id="c6b30-129">By default, `hideDiskTypeFilter` is **false**.</span></span> <span data-ttu-id="c6b30-130">The disk type filter enables the user to see all disk types or only SSD.</span><span class="sxs-lookup"><span data-stu-id="c6b30-130">The disk type filter enables the user to see all disk types or only SSD.</span></span>

## <a name="sample-output"></a><span data-ttu-id="c6b30-131">Sample output</span><span class="sxs-lookup"><span data-stu-id="c6b30-131">Sample output</span></span>
```json
"Standard_D1"
```

## <a name="next-steps"></a><span data-ttu-id="c6b30-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="c6b30-132">Next steps</span></span>
* <span data-ttu-id="c6b30-133">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c6b30-133">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).</span></span>
* <span data-ttu-id="c6b30-134">For a description of common properties in UI elements, see [CreateUiDefinition elements](create-uidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="c6b30-134">For a description of common properties in UI elements, see [CreateUiDefinition elements](create-uidefinition-elements.md).</span></span>
