---
title: Azure DropDown UI element | Microsoft Docs
description: Describes the Microsoft.Common.DropDown UI element for Azure portal.
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
ms.openlocfilehash: f953e1dc15e12c37c30a86ebd7536b1126bf18f7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857542"
---
# <a name="microsoftcommondropdown-ui-element"></a><span data-ttu-id="d2444-103">Microsoft.Common.DropDown UI element</span><span class="sxs-lookup"><span data-stu-id="d2444-103">Microsoft.Common.DropDown UI element</span></span>
<span data-ttu-id="d2444-104">A selection control with a dropdown list.</span><span class="sxs-lookup"><span data-stu-id="d2444-104">A selection control with a dropdown list.</span></span>

## <a name="ui-sample"></a><span data-ttu-id="d2444-105">UI sample</span><span class="sxs-lookup"><span data-stu-id="d2444-105">UI sample</span></span>
![Microsoft.Common.DropDown](./media/managed-application-elements/microsoft.common.dropdown.png)

## <a name="schema"></a><span data-ttu-id="d2444-107">Schema</span><span class="sxs-lookup"><span data-stu-id="d2444-107">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.DropDown",
  "label": "Example drop down",
  "defaultValue": "Value two",
  "toolTip": "",
  "constraints": {
    "allowedValues": [
      {
        "label": "Value one",
        "value": "one"
      },
      {
        "label": "Value two",
        "value": "two"
      }
    ],
    "required": true
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="d2444-108">Remarks</span><span class="sxs-lookup"><span data-stu-id="d2444-108">Remarks</span></span>

- <span data-ttu-id="d2444-109">The label for `constraints.allowedValues` is the display text for an item, and its value is the output value of the element when selected.</span><span class="sxs-lookup"><span data-stu-id="d2444-109">The label for `constraints.allowedValues` is the display text for an item, and its value is the output value of the element when selected.</span></span>
- <span data-ttu-id="d2444-110">If specified, the default value must be a label present in `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="d2444-110">If specified, the default value must be a label present in `constraints.allowedValues`.</span></span> <span data-ttu-id="d2444-111">If not specified, the first item in `constraints.allowedValues` is selected.</span><span class="sxs-lookup"><span data-stu-id="d2444-111">If not specified, the first item in `constraints.allowedValues` is selected.</span></span> <span data-ttu-id="d2444-112">The default value is **null**.</span><span class="sxs-lookup"><span data-stu-id="d2444-112">The default value is **null**.</span></span>
- <span data-ttu-id="d2444-113">`constraints.allowedValues` must have at least one item.</span><span class="sxs-lookup"><span data-stu-id="d2444-113">`constraints.allowedValues` must have at least one item.</span></span>
- <span data-ttu-id="d2444-114">To emulate a value not being required, add an item with a label and value of `""` (empty string) to `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="d2444-114">To emulate a value not being required, add an item with a label and value of `""` (empty string) to `constraints.allowedValues`.</span></span>

## <a name="sample-output"></a><span data-ttu-id="d2444-115">Sample output</span><span class="sxs-lookup"><span data-stu-id="d2444-115">Sample output</span></span>
```json
"two"
```

## <a name="next-steps"></a><span data-ttu-id="d2444-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="d2444-116">Next steps</span></span>
* <span data-ttu-id="d2444-117">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d2444-117">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).</span></span>
* <span data-ttu-id="d2444-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](create-uidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="d2444-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](create-uidefinition-elements.md).</span></span>
