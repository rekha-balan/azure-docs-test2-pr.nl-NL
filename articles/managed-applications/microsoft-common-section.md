---
title: Azure Section UI element | Microsoft Docs
description: Describes the Microsoft.Common.Section UI element for Azure portal.
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
ms.openlocfilehash: 90ffae3dd8b05041c34d766e464eb68f793f6066
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866249"
---
# <a name="microsoftcommonsection-ui-element"></a><span data-ttu-id="48419-103">Microsoft.Common.Section UI element</span><span class="sxs-lookup"><span data-stu-id="48419-103">Microsoft.Common.Section UI element</span></span>
<span data-ttu-id="48419-104">A control that groups one or more elements under a heading.</span><span class="sxs-lookup"><span data-stu-id="48419-104">A control that groups one or more elements under a heading.</span></span>

## <a name="ui-sample"></a><span data-ttu-id="48419-105">UI sample</span><span class="sxs-lookup"><span data-stu-id="48419-105">UI sample</span></span>
![Microsoft.Common.Section](./media/managed-application-elements/microsoft.common.section.png)

## <a name="schema"></a><span data-ttu-id="48419-107">Schema</span><span class="sxs-lookup"><span data-stu-id="48419-107">Schema</span></span>
```json
{
  "name": "section1",
  "type": "Microsoft.Common.Section",
  "label": "Example section",
  "elements": [
    {
      "name": "text1",
      "type": "Microsoft.Common.TextBox",
      "label": "Example text box 1"
    },
    {
      "name": "text2",
      "type": "Microsoft.Common.TextBox",
      "label": "Example text box 2"
    }
  ],
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="48419-108">Remarks</span><span class="sxs-lookup"><span data-stu-id="48419-108">Remarks</span></span>
- <span data-ttu-id="48419-109">`elements` must have at least one element, and can have all element types except `Microsoft.Common.Section`.</span><span class="sxs-lookup"><span data-stu-id="48419-109">`elements` must have at least one element, and can have all element types except `Microsoft.Common.Section`.</span></span>
- <span data-ttu-id="48419-110">This element doesn't support the `toolTip` property.</span><span class="sxs-lookup"><span data-stu-id="48419-110">This element doesn't support the `toolTip` property.</span></span>

## <a name="sample-output"></a><span data-ttu-id="48419-111">Sample output</span><span class="sxs-lookup"><span data-stu-id="48419-111">Sample output</span></span>
<span data-ttu-id="48419-112">To access the output values of elements in `elements`, use the [basics()](create-uidefinition-functions.md#basics) or [steps()](create-uidefinition-functions.md#steps) functions and dot notation:</span><span class="sxs-lookup"><span data-stu-id="48419-112">To access the output values of elements in `elements`, use the [basics()](create-uidefinition-functions.md#basics) or [steps()](create-uidefinition-functions.md#steps) functions and dot notation:</span></span>

```json
steps('configuration').section1.text1
```

<span data-ttu-id="48419-113">Elements of type `Microsoft.Common.Section` have no output values themselves.</span><span class="sxs-lookup"><span data-stu-id="48419-113">Elements of type `Microsoft.Common.Section` have no output values themselves.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48419-114">Next steps</span><span class="sxs-lookup"><span data-stu-id="48419-114">Next steps</span></span>
* <span data-ttu-id="48419-115">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="48419-115">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).</span></span>
* <span data-ttu-id="48419-116">For a description of common properties in UI elements, see [CreateUiDefinition elements](create-uidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="48419-116">For a description of common properties in UI elements, see [CreateUiDefinition elements](create-uidefinition-elements.md).</span></span>
