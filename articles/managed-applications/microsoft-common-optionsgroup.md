---
title: Azure OptionsGroup UI element | Microsoft Docs
description: Describes the Microsoft.Common.OptionsGroup UI element for Azure portal.
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
ms.openlocfilehash: e51061dc781e4ec6e822cde9cc450887ff3b1368
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870903"
---
# <a name="microsoftcommonoptionsgroup-ui-element"></a><span data-ttu-id="fc875-103">Microsoft.Common.OptionsGroup UI element</span><span class="sxs-lookup"><span data-stu-id="fc875-103">Microsoft.Common.OptionsGroup UI element</span></span>
<span data-ttu-id="fc875-104">A selection control with a row of available options.</span><span class="sxs-lookup"><span data-stu-id="fc875-104">A selection control with a row of available options.</span></span>

## <a name="ui-sample"></a><span data-ttu-id="fc875-105">UI sample</span><span class="sxs-lookup"><span data-stu-id="fc875-105">UI sample</span></span>
![Microsoft.Common.OptionsGroup](./media/managed-application-elements/microsoft.common.optionsgroup.png)

## <a name="schema"></a><span data-ttu-id="fc875-107">Schema</span><span class="sxs-lookup"><span data-stu-id="fc875-107">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.OptionsGroup",
  "label": "Some options group",
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

## <a name="remarks"></a><span data-ttu-id="fc875-108">Remarks</span><span class="sxs-lookup"><span data-stu-id="fc875-108">Remarks</span></span>
- <span data-ttu-id="fc875-109">The label for `constraints.allowedValues` is the display text for an item, and its value is the output value of the element when selected.</span><span class="sxs-lookup"><span data-stu-id="fc875-109">The label for `constraints.allowedValues` is the display text for an item, and its value is the output value of the element when selected.</span></span>
- <span data-ttu-id="fc875-110">If specified, the default value must be a label present in `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="fc875-110">If specified, the default value must be a label present in `constraints.allowedValues`.</span></span> <span data-ttu-id="fc875-111">If not specified, the first item in `constraints.allowedValues` is selected by default.</span><span class="sxs-lookup"><span data-stu-id="fc875-111">If not specified, the first item in `constraints.allowedValues` is selected by default.</span></span> <span data-ttu-id="fc875-112">The default value is **null**.</span><span class="sxs-lookup"><span data-stu-id="fc875-112">The default value is **null**.</span></span>
- <span data-ttu-id="fc875-113">`constraints.allowedValues` must have at least one item.</span><span class="sxs-lookup"><span data-stu-id="fc875-113">`constraints.allowedValues` must have at least one item.</span></span>

## <a name="sample-output"></a><span data-ttu-id="fc875-114">Sample output</span><span class="sxs-lookup"><span data-stu-id="fc875-114">Sample output</span></span>
```json
"two"
```

## <a name="next-steps"></a><span data-ttu-id="fc875-115">Next steps</span><span class="sxs-lookup"><span data-stu-id="fc875-115">Next steps</span></span>
* <span data-ttu-id="fc875-116">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fc875-116">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).</span></span>
* <span data-ttu-id="fc875-117">For a description of common properties in UI elements, see [CreateUiDefinition elements](create-uidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="fc875-117">For a description of common properties in UI elements, see [CreateUiDefinition elements](create-uidefinition-elements.md).</span></span>
