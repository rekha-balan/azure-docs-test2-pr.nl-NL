---
title: Azure AvailabilityZoneDropdown UI element | Microsoft Docs
description: Describes the Microsoft.Network.AvailabilityZoneDropdown UI element for Azure portal.
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
ms.date: 06/28/2018
ms.author: tomfitz
ms.openlocfilehash: 1698bae19ad8ec5c3076db1489ac513e304a4e13
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866629"
---
# <a name="microsoftnetworkavailabilityzonedropdown-ui-element"></a><span data-ttu-id="d0589-103">Microsoft.Network.AvailabilityZoneDropdown UI element</span><span class="sxs-lookup"><span data-stu-id="d0589-103">Microsoft.Network.AvailabilityZoneDropdown UI element</span></span>
<span data-ttu-id="d0589-104">A control for selecting the availability zone.</span><span class="sxs-lookup"><span data-stu-id="d0589-104">A control for selecting the availability zone.</span></span>

## <a name="ui-sample"></a><span data-ttu-id="d0589-105">UI sample</span><span class="sxs-lookup"><span data-stu-id="d0589-105">UI sample</span></span>
![Microsoft.Network.AvailabilityZoneDropDown](./media/managed-application-elements/microsoft.network.availabilityzonedropdown.png)

## <a name="schema"></a><span data-ttu-id="d0589-107">Schema</span><span class="sxs-lookup"><span data-stu-id="d0589-107">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Network.AvailabilityZoneDropdown",
  "label": "Availability zone dropdown label",
  "toolTip": "This is the tooltip for availability zones",
  "defaultValue": "None",
  "constraints": {
    "required": "true"
  },
  "options": {
  },
  "visible": true
}
```

## <a name="next-steps"></a><span data-ttu-id="d0589-108">Next steps</span><span class="sxs-lookup"><span data-stu-id="d0589-108">Next steps</span></span>
* <span data-ttu-id="d0589-109">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d0589-109">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).</span></span>
* <span data-ttu-id="d0589-110">For a description of common properties in UI elements, see [CreateUiDefinition elements](create-uidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="d0589-110">For a description of common properties in UI elements, see [CreateUiDefinition elements](create-uidefinition-elements.md).</span></span>
