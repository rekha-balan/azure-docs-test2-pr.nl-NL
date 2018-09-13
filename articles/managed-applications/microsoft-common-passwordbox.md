---
title: Azure PasswordBox UI element | Microsoft Docs
description: Describes the Microsoft.Common.PasswordBox UI element for Azure portal.
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
ms.openlocfilehash: adaece4a450f758c22ffecb356826962806d9d9b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864823"
---
# <a name="microsoftcommonpasswordbox-ui-element"></a><span data-ttu-id="4c628-103">Microsoft.Common.PasswordBox UI element</span><span class="sxs-lookup"><span data-stu-id="4c628-103">Microsoft.Common.PasswordBox UI element</span></span>
<span data-ttu-id="4c628-104">A control that can be used to provide and confirm a password.</span><span class="sxs-lookup"><span data-stu-id="4c628-104">A control that can be used to provide and confirm a password.</span></span>

## <a name="ui-sample"></a><span data-ttu-id="4c628-105">UI sample</span><span class="sxs-lookup"><span data-stu-id="4c628-105">UI sample</span></span>
![Microsoft.Common.PasswordBox](./media/managed-application-elements/microsoft.common.passwordbox.png)

## <a name="schema"></a><span data-ttu-id="4c628-107">Schema</span><span class="sxs-lookup"><span data-stu-id="4c628-107">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.PasswordBox",
  "label": {
    "password": "Password",
    "confirmPassword": "Confirm password"
  },
  "toolTip": "",
  "constraints": {
    "required": true,
    "regex": "",
    "validationMessage": ""
  },
  "options": {
    "hideConfirmation": false
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="4c628-108">Remarks</span><span class="sxs-lookup"><span data-stu-id="4c628-108">Remarks</span></span>
- <span data-ttu-id="4c628-109">This element doesn't support the `defaultValue` property.</span><span class="sxs-lookup"><span data-stu-id="4c628-109">This element doesn't support the `defaultValue` property.</span></span>
- <span data-ttu-id="4c628-110">For implementation details of `constraints`, see [Microsoft.Common.TextBox](microsoft-common-textbox.md).</span><span class="sxs-lookup"><span data-stu-id="4c628-110">For implementation details of `constraints`, see [Microsoft.Common.TextBox](microsoft-common-textbox.md).</span></span>
- <span data-ttu-id="4c628-111">If `options.hideConfirmation` is set to **true**, the second text box for confirming the user's password is hidden.</span><span class="sxs-lookup"><span data-stu-id="4c628-111">If `options.hideConfirmation` is set to **true**, the second text box for confirming the user's password is hidden.</span></span> <span data-ttu-id="4c628-112">The default value is **false**.</span><span class="sxs-lookup"><span data-stu-id="4c628-112">The default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="4c628-113">Sample output</span><span class="sxs-lookup"><span data-stu-id="4c628-113">Sample output</span></span>
```json
"p4ssw0rd"
```

## <a name="next-steps"></a><span data-ttu-id="4c628-114">Next steps</span><span class="sxs-lookup"><span data-stu-id="4c628-114">Next steps</span></span>
* <span data-ttu-id="4c628-115">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4c628-115">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).</span></span>
* <span data-ttu-id="4c628-116">For a description of common properties in UI elements, see [CreateUiDefinition elements](create-uidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="4c628-116">For a description of common properties in UI elements, see [CreateUiDefinition elements](create-uidefinition-elements.md).</span></span>
