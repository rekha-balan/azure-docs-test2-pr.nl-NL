---
title: Azure VirtualNetworkCombo UI element | Microsoft Docs
description: Describes the Microsoft.Network.VirtualNetworkCombo UI element for Azure portal.
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
ms.openlocfilehash: 2c2553d9ffb1dfbe032385fb77e234a8b96cb239
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870033"
---
# <a name="microsoftnetworkvirtualnetworkcombo-ui-element"></a><span data-ttu-id="6aec5-103">Microsoft.Network.VirtualNetworkCombo UI element</span><span class="sxs-lookup"><span data-stu-id="6aec5-103">Microsoft.Network.VirtualNetworkCombo UI element</span></span>
<span data-ttu-id="6aec5-104">A group of controls for selecting a new or existing virtual network.</span><span class="sxs-lookup"><span data-stu-id="6aec5-104">A group of controls for selecting a new or existing virtual network.</span></span>

## <a name="ui-sample"></a><span data-ttu-id="6aec5-105">UI sample</span><span class="sxs-lookup"><span data-stu-id="6aec5-105">UI sample</span></span>
<span data-ttu-id="6aec5-106">When the user picks a new virtual network, the user can customize each subnet's name and address prefix.</span><span class="sxs-lookup"><span data-stu-id="6aec5-106">When the user picks a new virtual network, the user can customize each subnet's name and address prefix.</span></span> <span data-ttu-id="6aec5-107">Configuring subnets is optional.</span><span class="sxs-lookup"><span data-stu-id="6aec5-107">Configuring subnets is optional.</span></span>

![Microsoft.Network.VirtualNetworkCombo new](./media/managed-application-elements/microsoft.network.virtualnetworkcombo-new.png)

<span data-ttu-id="6aec5-109">When the user picks an existing virtual network, the user must map each subnet the deployment template requires to an existing subnet.</span><span class="sxs-lookup"><span data-stu-id="6aec5-109">When the user picks an existing virtual network, the user must map each subnet the deployment template requires to an existing subnet.</span></span> <span data-ttu-id="6aec5-110">Configuring subnets in this case is required.</span><span class="sxs-lookup"><span data-stu-id="6aec5-110">Configuring subnets in this case is required.</span></span>

![Microsoft.Network.VirtualNetworkCombo existing](./media/managed-application-elements/microsoft.network.virtualnetworkcombo-existing.png)

## <a name="schema"></a><span data-ttu-id="6aec5-112">Schema</span><span class="sxs-lookup"><span data-stu-id="6aec5-112">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Network.VirtualNetworkCombo",
  "label": {
    "virtualNetwork": "Virtual network",
    "subnets": "Subnets"
  },
  "toolTip": {
    "virtualNetwork": "",
    "subnets": ""
  },
  "defaultValue": {
    "name": "vnet01",
    "addressPrefixSize": "/16"
  },
  "constraints": {
    "minAddressPrefixSize": "/16"
  },
  "options": {
    "hideExisting": false
  },
  "subnets": {
    "subnet1": {
      "label": "First subnet",
      "defaultValue": {
        "name": "subnet-1",
        "addressPrefixSize": "/24"
      },
      "constraints": {
        "minAddressPrefixSize": "/24",
        "minAddressCount": 12,
        "requireContiguousAddresses": true
      }
    },
    "subnet2": {
      "label": "Second subnet",
      "defaultValue": {
        "name": "subnet-2",
        "addressPrefixSize": "/26"
      },
      "constraints": {
        "minAddressPrefixSize": "/26",
        "minAddressCount": 8,
        "requireContiguousAddresses": true
      }
    }
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="6aec5-113">Remarks</span><span class="sxs-lookup"><span data-stu-id="6aec5-113">Remarks</span></span>
- <span data-ttu-id="6aec5-114">If specified, the first non-overlapping address prefix of size `defaultValue.addressPrefixSize` is determined automatically based on the existing virtual networks in the user's subscription.</span><span class="sxs-lookup"><span data-stu-id="6aec5-114">If specified, the first non-overlapping address prefix of size `defaultValue.addressPrefixSize` is determined automatically based on the existing virtual networks in the user's subscription.</span></span>
- <span data-ttu-id="6aec5-115">The default value for `defaultValue.name` and `defaultValue.addressPrefixSize` is **null**.</span><span class="sxs-lookup"><span data-stu-id="6aec5-115">The default value for `defaultValue.name` and `defaultValue.addressPrefixSize` is **null**.</span></span>
- <span data-ttu-id="6aec5-116">`constraints.minAddressPrefixSize` must be specified.</span><span class="sxs-lookup"><span data-stu-id="6aec5-116">`constraints.minAddressPrefixSize` must be specified.</span></span> <span data-ttu-id="6aec5-117">Any existing virtual networks with an address space smaller than the specified value are unavailable for selection.</span><span class="sxs-lookup"><span data-stu-id="6aec5-117">Any existing virtual networks with an address space smaller than the specified value are unavailable for selection.</span></span>
- <span data-ttu-id="6aec5-118">`subnets` must be specified, and `constraints.minAddressPrefixSize` must be specified for each subnet.</span><span class="sxs-lookup"><span data-stu-id="6aec5-118">`subnets` must be specified, and `constraints.minAddressPrefixSize` must be specified for each subnet.</span></span>
- <span data-ttu-id="6aec5-119">When creating a new virtual network, each subnet's address prefix is calculated automatically based on the virtual network's address prefix and the respective `addressPrefixSize`.</span><span class="sxs-lookup"><span data-stu-id="6aec5-119">When creating a new virtual network, each subnet's address prefix is calculated automatically based on the virtual network's address prefix and the respective `addressPrefixSize`.</span></span>
- <span data-ttu-id="6aec5-120">When using an existing virtual network, any subnets smaller than the respective `constraints.minAddressPrefixSize` are unavailable for selection.</span><span class="sxs-lookup"><span data-stu-id="6aec5-120">When using an existing virtual network, any subnets smaller than the respective `constraints.minAddressPrefixSize` are unavailable for selection.</span></span> <span data-ttu-id="6aec5-121">Additionally, if specified, subnets that don't have at least `minAddressCount` available addresses are unavailable for selection.</span><span class="sxs-lookup"><span data-stu-id="6aec5-121">Additionally, if specified, subnets that don't have at least `minAddressCount` available addresses are unavailable for selection.</span></span> <span data-ttu-id="6aec5-122">The default value is **0**.</span><span class="sxs-lookup"><span data-stu-id="6aec5-122">The default value is **0**.</span></span> <span data-ttu-id="6aec5-123">To ensure that the available addresses are contiguous, specify **true** for `requireContiguousAddresses`.</span><span class="sxs-lookup"><span data-stu-id="6aec5-123">To ensure that the available addresses are contiguous, specify **true** for `requireContiguousAddresses`.</span></span> <span data-ttu-id="6aec5-124">The default value is **true**.</span><span class="sxs-lookup"><span data-stu-id="6aec5-124">The default value is **true**.</span></span>
- <span data-ttu-id="6aec5-125">Creating subnets in an existing virtual network isn't supported.</span><span class="sxs-lookup"><span data-stu-id="6aec5-125">Creating subnets in an existing virtual network isn't supported.</span></span>
- <span data-ttu-id="6aec5-126">If `options.hideExisting` is **true**, the user can't choose an existing virtual network.</span><span class="sxs-lookup"><span data-stu-id="6aec5-126">If `options.hideExisting` is **true**, the user can't choose an existing virtual network.</span></span> <span data-ttu-id="6aec5-127">The default value is **false**.</span><span class="sxs-lookup"><span data-stu-id="6aec5-127">The default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="6aec5-128">Sample output</span><span class="sxs-lookup"><span data-stu-id="6aec5-128">Sample output</span></span>

```json
{
  "name": "vnet01",
  "resourceGroup": "rg01",
  "addressPrefixes": ["10.0.0.0/16"],
  "newOrExisting": "new",
  "subnets": {
    "subnet1": {
      "name": "subnet-1",
      "addressPrefix": "10.0.0.0/24",
      "startAddress": "10.0.0.1"
    },
    "subnet2": {
      "name": "subnet-2",
      "addressPrefix": "10.0.1.0/26",
      "startAddress": "10.0.1.1"
    }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="6aec5-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="6aec5-129">Next steps</span></span>
* <span data-ttu-id="6aec5-130">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6aec5-130">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).</span></span>
* <span data-ttu-id="6aec5-131">For a description of common properties in UI elements, see [CreateUiDefinition elements](create-uidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="6aec5-131">For a description of common properties in UI elements, see [CreateUiDefinition elements](create-uidefinition-elements.md).</span></span>
