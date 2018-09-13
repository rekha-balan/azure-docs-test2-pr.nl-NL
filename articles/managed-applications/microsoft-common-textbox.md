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
# <a name="microsoftcommontextbox-ui-element"></a>Microsoft.Common.TextBox UI element
A control that can be used to edit unformatted text.

## <a name="ui-sample"></a>UI sample
![Microsoft.Common.TextBox](./media/managed-application-elements/microsoft.common.textbox.png)

## <a name="schema"></a>Schema
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

## <a name="remarks"></a>Remarks
- If `constraints.required` is set to **true**, then the text box must have a value to validate successfully. The default value is **false**.
- `constraints.regex` is a JavaScript regular expression pattern. If specified, then the text box's value must match the pattern to validate successfully. The default value is **null**.
- `constraints.validationMessage` is a string to display when the text box's value fails validation. If not specified, then the text box's built-in validation messages are used. The default value is **null**.
- It's possible to specify a value for `constraints.regex` when `constraints.required` is set to **false**. In this scenario, a value isn't required for the text box to validate successfully. If one is specified, it must match the regular expression pattern.

## <a name="sample-output"></a>Sample output

```json
"my text value"
```

## <a name="next-steps"></a>Next steps
* For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).
* For a description of common properties in UI elements, see [CreateUiDefinition elements](create-uidefinition-elements.md).
