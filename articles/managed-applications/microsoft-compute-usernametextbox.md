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
# <a name="microsoftcomputeusernametextbox-ui-element"></a>Microsoft.Compute.UserNameTextBox UI element
A text box control with built-in validation for Windows and Linux user names.

## <a name="ui-sample"></a>UI sample
![Microsoft.Compute.UserNameTextBox](./media/managed-application-elements/microsoft.compute.usernametextbox.png)

## <a name="schema"></a>Schema
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

## <a name="remarks"></a>Remarks
- If `constraints.required` is set to **true**, then the text box must have a value to validate successfully. The default value is **true**.
- `osPlatform` must be specified, and can be either **Windows** or **Linux**.
- `constraints.regex` is a JavaScript regular expression pattern. If specified, then the text box's value must match the pattern to validate successfully. The default value is **null**.
- `constraints.validationMessage` is a string to display when the text box's value fails the validation specified by `constraints.regex`. If not specified, then the text box's built-in validation messages are used. The default value is **null**.
- This element has built-in validation that is based on the value specified for `osPlatform`. The built-in validation can be used along with a custom regular expression. If a value for `constraints.regex` is specified, then both the built-in and custom validations are triggered.

## <a name="sample-output"></a>Sample output
```json
"Example name"
```

## <a name="next-steps"></a>Next steps
* For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).
* For a description of common properties in UI elements, see [CreateUiDefinition elements](create-uidefinition-elements.md).
