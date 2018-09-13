---
title: Azure PublicIpAddressCombo UI element | Microsoft Docs
description: Describes the Microsoft.Network.PublicIpAddressCombo UI element for Azure portal.
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
ms.openlocfilehash: d06a450595a53fdc65fba74791345abe3a1b3db4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857731"
---
# <a name="microsoftnetworkpublicipaddresscombo-ui-element"></a><span data-ttu-id="54507-103">Microsoft.Network.PublicIpAddressCombo UI element</span><span class="sxs-lookup"><span data-stu-id="54507-103">Microsoft.Network.PublicIpAddressCombo UI element</span></span>
<span data-ttu-id="54507-104">A group of controls for selecting a new or existing public IP address.</span><span class="sxs-lookup"><span data-stu-id="54507-104">A group of controls for selecting a new or existing public IP address.</span></span>

## <a name="ui-sample"></a><span data-ttu-id="54507-105">UI sample</span><span class="sxs-lookup"><span data-stu-id="54507-105">UI sample</span></span>
![Microsoft.Network.PublicIpAddressCombo](./media/managed-application-elements/microsoft.network.publicipaddresscombo.png)

- <span data-ttu-id="54507-107">If the user selects 'None' for public IP address, the domain name label text box is hidden.</span><span class="sxs-lookup"><span data-stu-id="54507-107">If the user selects 'None' for public IP address, the domain name label text box is hidden.</span></span>
- <span data-ttu-id="54507-108">If the user selects an existing public IP address, the domain name label text box is disabled.</span><span class="sxs-lookup"><span data-stu-id="54507-108">If the user selects an existing public IP address, the domain name label text box is disabled.</span></span> <span data-ttu-id="54507-109">Its value is the domain name label of the selected IP address.</span><span class="sxs-lookup"><span data-stu-id="54507-109">Its value is the domain name label of the selected IP address.</span></span>
- <span data-ttu-id="54507-110">The domain name suffix (for example, westus.cloudapp.azure.com) updates automatically based on the selected location.</span><span class="sxs-lookup"><span data-stu-id="54507-110">The domain name suffix (for example, westus.cloudapp.azure.com) updates automatically based on the selected location.</span></span>

## <a name="schema"></a><span data-ttu-id="54507-111">Schema</span><span class="sxs-lookup"><span data-stu-id="54507-111">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Network.PublicIpAddressCombo",
  "label": {
    "publicIpAddress": "Public IP address",
    "domainNameLabel": "Domain name label"
  },
  "toolTip": {
    "publicIpAddress": "",
    "domainNameLabel": ""
  },
  "defaultValue": {
    "publicIpAddressName": "ip01",
    "domainNameLabel": "mydomain"
  },
  "constraints": {
    "required": {
      "domainNameLabel": true
    }
  },
  "options": {
    "hideNone": false,
    "hideDomainNameLabel": false,
    "hideExisting": false,
    "zone": 3
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="54507-112">Remarks</span><span class="sxs-lookup"><span data-stu-id="54507-112">Remarks</span></span>
- <span data-ttu-id="54507-113">If `constraints.required.domainNameLabel` is set to **true**, the user must provide a domain name label when creating a new public IP address.</span><span class="sxs-lookup"><span data-stu-id="54507-113">If `constraints.required.domainNameLabel` is set to **true**, the user must provide a domain name label when creating a new public IP address.</span></span> <span data-ttu-id="54507-114">Existing public IP addresses without a label aren't available for selection.</span><span class="sxs-lookup"><span data-stu-id="54507-114">Existing public IP addresses without a label aren't available for selection.</span></span>
- <span data-ttu-id="54507-115">If `options.hideNone` is set to **true**, then the option to select **None** for the public IP address is hidden.</span><span class="sxs-lookup"><span data-stu-id="54507-115">If `options.hideNone` is set to **true**, then the option to select **None** for the public IP address is hidden.</span></span> <span data-ttu-id="54507-116">The default value is **false**.</span><span class="sxs-lookup"><span data-stu-id="54507-116">The default value is **false**.</span></span>
- <span data-ttu-id="54507-117">If `options.hideDomainNameLabel` is set to **true**, then the text box for domain name label is hidden.</span><span class="sxs-lookup"><span data-stu-id="54507-117">If `options.hideDomainNameLabel` is set to **true**, then the text box for domain name label is hidden.</span></span> <span data-ttu-id="54507-118">The default value is **false**.</span><span class="sxs-lookup"><span data-stu-id="54507-118">The default value is **false**.</span></span>
- <span data-ttu-id="54507-119">If `options.hideExisting` is true, then the user isn't able to choose an existing public IP address.</span><span class="sxs-lookup"><span data-stu-id="54507-119">If `options.hideExisting` is true, then the user isn't able to choose an existing public IP address.</span></span> <span data-ttu-id="54507-120">The default value is **false**.</span><span class="sxs-lookup"><span data-stu-id="54507-120">The default value is **false**.</span></span>
- <span data-ttu-id="54507-121">For `zone`, only public IP addresses for the specified zone or zone resilient public IP addresses are available.</span><span class="sxs-lookup"><span data-stu-id="54507-121">For `zone`, only public IP addresses for the specified zone or zone resilient public IP addresses are available.</span></span>

## <a name="sample-output"></a><span data-ttu-id="54507-122">Sample output</span><span class="sxs-lookup"><span data-stu-id="54507-122">Sample output</span></span>
<span data-ttu-id="54507-123">If the user selects no public IP address, the control returns the following output:</span><span class="sxs-lookup"><span data-stu-id="54507-123">If the user selects no public IP address, the control returns the following output:</span></span>

```json
{
  "newOrExistingOrNone": "none"
}
```

<span data-ttu-id="54507-124">If the user selects a new or existing IP address, the control returns the following output:</span><span class="sxs-lookup"><span data-stu-id="54507-124">If the user selects a new or existing IP address, the control returns the following output:</span></span>

```json
{
  "name": "ip01",
  "resourceGroup": "rg01",
  "domainNameLabel": "mydomain",
  "publicIPAllocationMethod": "Dynamic",
  "newOrExistingOrNone": "new"
}
```

- <span data-ttu-id="54507-125">When `options.hideNone` is specified as **true**, `newOrExistingOrNone` will only have a value of **new** or **existing**.</span><span class="sxs-lookup"><span data-stu-id="54507-125">When `options.hideNone` is specified as **true**, `newOrExistingOrNone` will only have a value of **new** or **existing**.</span></span>
- <span data-ttu-id="54507-126">When `options.hideDomainNameLabel` is specified as **true**, `domainNameLabel` is undeclared.</span><span class="sxs-lookup"><span data-stu-id="54507-126">When `options.hideDomainNameLabel` is specified as **true**, `domainNameLabel` is undeclared.</span></span>

## <a name="next-steps"></a><span data-ttu-id="54507-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="54507-127">Next steps</span></span>
* <span data-ttu-id="54507-128">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="54507-128">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).</span></span>
* <span data-ttu-id="54507-129">For a description of common properties in UI elements, see [CreateUiDefinition elements](create-uidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="54507-129">For a description of common properties in UI elements, see [CreateUiDefinition elements](create-uidefinition-elements.md).</span></span>
