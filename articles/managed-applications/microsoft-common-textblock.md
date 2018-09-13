---
title: Azure TextBlock UI element | Microsoft Docs
description: Describes the Microsoft.Common.TextBlock UI element for Azure portal.
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
ms.openlocfilehash: cd4d1aed666b2c64ade700a768df0525029b392c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966037"
---
# <a name="microsoftcommontextblock-ui-element"></a><span data-ttu-id="41038-103">Microsoft.Common.TextBlock UI element</span><span class="sxs-lookup"><span data-stu-id="41038-103">Microsoft.Common.TextBlock UI element</span></span>
<span data-ttu-id="41038-104">A control that can be used to add text to the portal interface.</span><span class="sxs-lookup"><span data-stu-id="41038-104">A control that can be used to add text to the portal interface.</span></span>

## <a name="ui-sample"></a><span data-ttu-id="41038-105">UI sample</span><span class="sxs-lookup"><span data-stu-id="41038-105">UI sample</span></span>
![Microsoft.Common.TextBox](./media/managed-application-elements/microsoft.common.textblock.png)

## <a name="schema"></a><span data-ttu-id="41038-107">Schema</span><span class="sxs-lookup"><span data-stu-id="41038-107">Schema</span></span>
```json
{
  "name": "text1",
  "type": "Microsoft.Common.TextBlock",
  "visible": true,
  "options": {
    "text": "Please provide the configuration values for your application.",
    "link": {
      "label": "Learn more",
      "uri": "https://www.microsoft.com"
    }
  }
}
```

## <a name="sample-output"></a><span data-ttu-id="41038-108">Sample output</span><span class="sxs-lookup"><span data-stu-id="41038-108">Sample output</span></span>

```json
"Please provide the configuration values for your application. Learn more"
```

## <a name="next-steps"></a><span data-ttu-id="41038-109">Next steps</span><span class="sxs-lookup"><span data-stu-id="41038-109">Next steps</span></span>
* <span data-ttu-id="41038-110">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="41038-110">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).</span></span>
* <span data-ttu-id="41038-111">For a description of common properties in UI elements, see [CreateUiDefinition elements](create-uidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="41038-111">For a description of common properties in UI elements, see [CreateUiDefinition elements](create-uidefinition-elements.md).</span></span>
