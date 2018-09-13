---
title: Azure InfoBox UI element | Microsoft Docs
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
ms.date: 06/15/2018
ms.author: tomfitz
ms.openlocfilehash: abd1329f2ebac90bf846dfd5fc5b307ddb5e52bd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858007"
---
# <a name="microsoftcommoninfobox-ui-element"></a><span data-ttu-id="f317e-103">Microsoft.Common.InfoBox UI element</span><span class="sxs-lookup"><span data-stu-id="f317e-103">Microsoft.Common.InfoBox UI element</span></span>
<span data-ttu-id="f317e-104">A control that adds an information box.</span><span class="sxs-lookup"><span data-stu-id="f317e-104">A control that adds an information box.</span></span> <span data-ttu-id="f317e-105">The box contains important text or warnings that help users understand the values they're providing.</span><span class="sxs-lookup"><span data-stu-id="f317e-105">The box contains important text or warnings that help users understand the values they're providing.</span></span> <span data-ttu-id="f317e-106">It can also link to a URI for more information.</span><span class="sxs-lookup"><span data-stu-id="f317e-106">It can also link to a URI for more information.</span></span>

## <a name="ui-sample"></a><span data-ttu-id="f317e-107">UI sample</span><span class="sxs-lookup"><span data-stu-id="f317e-107">UI sample</span></span>
![Microsoft.Common.InfoBox](./media/managed-application-elements/microsoft.common.infobox.png)


## <a name="schema"></a><span data-ttu-id="f317e-109">Schema</span><span class="sxs-lookup"><span data-stu-id="f317e-109">Schema</span></span>
```json
{
  "name": "text1",
  "type": "Microsoft.Common.InfoBox",
  "visible": true,
  "options": {
    "icon": "None",
    "text": "Nullam eros mi, mollis in sollicitudin non, tincidunt sed enim. Sed et felis metus, rhoncus ornare nibh. Ut at magna leo.",
    "uri": "https://www.microsoft.com"
  }
}
```

## <a name="remarks"></a><span data-ttu-id="f317e-110">Remarks</span><span class="sxs-lookup"><span data-stu-id="f317e-110">Remarks</span></span>

* <span data-ttu-id="f317e-111">For `icon`, use **None**, **Info**, **Warning**, or **Error**.</span><span class="sxs-lookup"><span data-stu-id="f317e-111">For `icon`, use **None**, **Info**, **Warning**, or **Error**.</span></span>
* <span data-ttu-id="f317e-112">The `uri` property is optional.</span><span class="sxs-lookup"><span data-stu-id="f317e-112">The `uri` property is optional.</span></span>

## <a name="sample-output"></a><span data-ttu-id="f317e-113">Sample output</span><span class="sxs-lookup"><span data-stu-id="f317e-113">Sample output</span></span>

```json
"Nullam eros mi, mollis in sollicitudin non, tincidunt sed enim. Sed et felis metus, rhoncus ornare nibh. Ut at magna leo."
```

## <a name="next-steps"></a><span data-ttu-id="f317e-114">Next steps</span><span class="sxs-lookup"><span data-stu-id="f317e-114">Next steps</span></span>
* <span data-ttu-id="f317e-115">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f317e-115">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).</span></span>
* <span data-ttu-id="f317e-116">For a description of common properties in UI elements, see [CreateUiDefinition elements](create-uidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="f317e-116">For a description of common properties in UI elements, see [CreateUiDefinition elements](create-uidefinition-elements.md).</span></span>
