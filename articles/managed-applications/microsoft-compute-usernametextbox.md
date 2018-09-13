---
title: Azure UserNameTextBox UI element | Microsoft Docs
description: Describes the Microsoft.Compute.UserNameTextBox UI element for Azure portal.
services: managed-applications
documentationcenter: na
author: tfitzmac
editor: tysonn
ms.service: managed-applications
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2018
ms.author: tomfitz
ms.openlocfilehash: 9f07c5bf9ba1f1880fa142beb52455522425e68d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967628"
---
# <a name="microsoftcomputeusernametextbox-ui-element"></a><span data-ttu-id="aa9bb-103">Microsoft.Compute.UserNameTextBox UI element</span><span class="sxs-lookup"><span data-stu-id="aa9bb-103">Microsoft.Compute.UserNameTextBox UI element</span></span>
<span data-ttu-id="aa9bb-104">A text box control with built-in validation for Windows and Linux user names.</span><span class="sxs-lookup"><span data-stu-id="aa9bb-104">A text box control with built-in validation for Windows and Linux user names.</span></span>

## <a name="ui-sample"></a><span data-ttu-id="aa9bb-105">UI sample</span><span class="sxs-lookup"><span data-stu-id="aa9bb-105">UI sample</span></span>
![Microsoft.Compute.UserNameTextBox](./media/managed-application-elements/microsoft.compute.usernametextbox.png)

## <a name="schema"></a><span data-ttu-id="aa9bb-107">Schema</span><span class="sxs-lookup"><span data-stu-id="aa9bb-107">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.UserNameTextBox",
  "label": "User name",
  "defaultValue": "",
  "toolTip": "",
  "constraints": {
    "required": true,
    "regex": "^[a-z0-9A-Z]{1,30}$",
    "validationMessage": "Only alphanumeric characters are allowed, and the value must be 1-30 characters long."
  },
  "osPlatform": "Windows",
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="aa9bb-108">Remarks</span><span class="sxs-lookup"><span data-stu-id="aa9bb-108">Remarks</span></span>
- <span data-ttu-id="aa9bb-109">If `constraints.required` is set to **true**, then the text box must have a value to validate successfully.</span><span class="sxs-lookup"><span data-stu-id="aa9bb-109">If `constraints.required` is set to **true**, then the text box must have a value to validate successfully.</span></span> <span data-ttu-id="aa9bb-110">The default value is **true**.</span><span class="sxs-lookup"><span data-stu-id="aa9bb-110">The default value is **true**.</span></span>
- <span data-ttu-id="aa9bb-111">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span><span class="sxs-lookup"><span data-stu-id="aa9bb-111">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="aa9bb-112">`constraints.regex` is a JavaScript regular expression pattern.</span><span class="sxs-lookup"><span data-stu-id="aa9bb-112">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="aa9bb-113">If specified, then the text box's value must match the pattern to validate successfully.</span><span class="sxs-lookup"><span data-stu-id="aa9bb-113">If specified, then the text box's value must match the pattern to validate successfully.</span></span> <span data-ttu-id="aa9bb-114">The default value is **null**.</span><span class="sxs-lookup"><span data-stu-id="aa9bb-114">The default value is **null**.</span></span>
- <span data-ttu-id="aa9bb-115">`constraints.validationMessage` is a string to display when the text box's value fails the validation specified by `constraints.regex`.</span><span class="sxs-lookup"><span data-stu-id="aa9bb-115">`constraints.validationMessage` is a string to display when the text box's value fails the validation specified by `constraints.regex`.</span></span> <span data-ttu-id="aa9bb-116">If not specified, then the text box's built-in validation messages are used.</span><span class="sxs-lookup"><span data-stu-id="aa9bb-116">If not specified, then the text box's built-in validation messages are used.</span></span> <span data-ttu-id="aa9bb-117">The default value is **null**.</span><span class="sxs-lookup"><span data-stu-id="aa9bb-117">The default value is **null**.</span></span>
- <span data-ttu-id="aa9bb-118">This element has built-in validation that is based on the value specified for `osPlatform`.</span><span class="sxs-lookup"><span data-stu-id="aa9bb-118">This element has built-in validation that is based on the value specified for `osPlatform`.</span></span> <span data-ttu-id="aa9bb-119">The built-in validation can be used along with a custom regular expression.</span><span class="sxs-lookup"><span data-stu-id="aa9bb-119">The built-in validation can be used along with a custom regular expression.</span></span> <span data-ttu-id="aa9bb-120">If a value for `constraints.regex` is specified, then both the built-in and custom validations are triggered.</span><span class="sxs-lookup"><span data-stu-id="aa9bb-120">If a value for `constraints.regex` is specified, then both the built-in and custom validations are triggered.</span></span>

## <a name="sample-output"></a><span data-ttu-id="aa9bb-121">Sample output</span><span class="sxs-lookup"><span data-stu-id="aa9bb-121">Sample output</span></span>
```json
"Example name"
```

## <a name="next-steps"></a><span data-ttu-id="aa9bb-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="aa9bb-122">Next steps</span></span>
* <span data-ttu-id="aa9bb-123">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aa9bb-123">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).</span></span>
* <span data-ttu-id="aa9bb-124">For a description of common properties in UI elements, see [CreateUiDefinition elements](create-uidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="aa9bb-124">For a description of common properties in UI elements, see [CreateUiDefinition elements](create-uidefinition-elements.md).</span></span>
