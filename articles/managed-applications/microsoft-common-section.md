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
# <a name="microsoftcommonsection-ui-element"></a>Microsoft.Common.Section UI element
A control that groups one or more elements under a heading.

## <a name="ui-sample"></a>UI sample
![Microsoft.Common.Section](./media/managed-application-elements/microsoft.common.section.png)

## <a name="schema"></a>Schema
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

## <a name="remarks"></a>Remarks
- `elements` must have at least one element, and can have all element types except `Microsoft.Common.Section`.
- This element doesn't support the `toolTip` property.

## <a name="sample-output"></a>Sample output
To access the output values of elements in `elements`, use the [basics()](create-uidefinition-functions.md#basics) or [steps()](create-uidefinition-functions.md#steps) functions and dot notation:

```json
steps('configuration').section1.text1
```

Elements of type `Microsoft.Common.Section` have no output values themselves.

## <a name="next-steps"></a>Next steps
* For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).
* For a description of common properties in UI elements, see [CreateUiDefinition elements](create-uidefinition-elements.md).
