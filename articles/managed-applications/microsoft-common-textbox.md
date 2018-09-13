---
title: Azure TextBox UI element | Microsoft Docs
description: Describes the Microsoft.Common.TextBox UI element for Azure portal.
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
ms.openlocfilehash: fa3e5fff8080acb9e824ffe27f6c149054804830
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870119"
---
# <a name="microsoftcommontextbox-ui-element"></a><span data-ttu-id="752c3-103">Microsoft.Common.TextBox UI element</span><span class="sxs-lookup"><span data-stu-id="752c3-103">Microsoft.Common.TextBox UI element</span></span>
<span data-ttu-id="752c3-104">A control that can be used to edit unformatted text.</span><span class="sxs-lookup"><span data-stu-id="752c3-104">A control that can be used to edit unformatted text.</span></span>

## <a name="ui-sample"></a><span data-ttu-id="752c3-105">UI sample</span><span class="sxs-lookup"><span data-stu-id="752c3-105">UI sample</span></span>
![Microsoft.Common.TextBox](./media/managed-application-elements/microsoft.common.textbox.png)

## <a name="schema"></a><span data-ttu-id="752c3-107">Schema</span><span class="sxs-lookup"><span data-stu-id="752c3-107">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.TextBox",
  "label": "Example text box 1",
  "defaultValue": "my text value",
  "toolTip": "Use only allowed characters",
  "constraints": {
    "required": true,
    "regex": "^[a-z0-9A-Z]{1,30}$",
    "validationMessage": "Only alphanumeric characters are allowed, and the value must be 1-30 characters long."
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="752c3-108">Remarks</span><span class="sxs-lookup"><span data-stu-id="752c3-108">Remarks</span></span>
- <span data-ttu-id="752c3-109">If `constraints.required` is set to **true**, then the text box must have a value to validate successfully.</span><span class="sxs-lookup"><span data-stu-id="752c3-109">If `constraints.required` is set to **true**, then the text box must have a value to validate successfully.</span></span> <span data-ttu-id="752c3-110">The default value is **false**.</span><span class="sxs-lookup"><span data-stu-id="752c3-110">The default value is **false**.</span></span>
- <span data-ttu-id="752c3-111">`constraints.regex` is a JavaScript regular expression pattern.</span><span class="sxs-lookup"><span data-stu-id="752c3-111">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="752c3-112">If specified, then the text box's value must match the pattern to validate successfully.</span><span class="sxs-lookup"><span data-stu-id="752c3-112">If specified, then the text box's value must match the pattern to validate successfully.</span></span> <span data-ttu-id="752c3-113">The default value is **null**.</span><span class="sxs-lookup"><span data-stu-id="752c3-113">The default value is **null**.</span></span>
- <span data-ttu-id="752c3-114">`constraints.validationMessage` is a string to display when the text box's value fails validation.</span><span class="sxs-lookup"><span data-stu-id="752c3-114">`constraints.validationMessage` is a string to display when the text box's value fails validation.</span></span> <span data-ttu-id="752c3-115">If not specified, then the text box's built-in validation messages are used.</span><span class="sxs-lookup"><span data-stu-id="752c3-115">If not specified, then the text box's built-in validation messages are used.</span></span> <span data-ttu-id="752c3-116">The default value is **null**.</span><span class="sxs-lookup"><span data-stu-id="752c3-116">The default value is **null**.</span></span>
- <span data-ttu-id="752c3-117">It's possible to specify a value for `constraints.regex` when `constraints.required` is set to **false**.</span><span class="sxs-lookup"><span data-stu-id="752c3-117">It's possible to specify a value for `constraints.regex` when `constraints.required` is set to **false**.</span></span> <span data-ttu-id="752c3-118">In this scenario, a value isn't required for the text box to validate successfully.</span><span class="sxs-lookup"><span data-stu-id="752c3-118">In this scenario, a value isn't required for the text box to validate successfully.</span></span> <span data-ttu-id="752c3-119">If one is specified, it must match the regular expression pattern.</span><span class="sxs-lookup"><span data-stu-id="752c3-119">If one is specified, it must match the regular expression pattern.</span></span>

## <a name="sample-output"></a><span data-ttu-id="752c3-120">Sample output</span><span class="sxs-lookup"><span data-stu-id="752c3-120">Sample output</span></span>

```json
"my text value"
```

## <a name="next-steps"></a><span data-ttu-id="752c3-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="752c3-121">Next steps</span></span>
* <span data-ttu-id="752c3-122">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="752c3-122">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).</span></span>
* <span data-ttu-id="752c3-123">For a description of common properties in UI elements, see [CreateUiDefinition elements](create-uidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="752c3-123">For a description of common properties in UI elements, see [CreateUiDefinition elements](create-uidefinition-elements.md).</span></span>
