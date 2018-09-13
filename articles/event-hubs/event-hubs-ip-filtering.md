---
title: Azure Event Hubs IP connection filters | Microsoft Docs
description: Use IP filtering to block connections from specific IP addresses to Azure Event Hubs.
services: event-hubs
documentationcenter: ''
author: ShubhaVijayasarathy
manager: timlt
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.date: 08/26/2018
ms.author: shvija
ms.openlocfilehash: 6d96eac3ecd249de3ba0da82eff95c45e45fa02d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869840"
---
# <a name="use-ip-filters"></a><span data-ttu-id="4ea02-103">Use IP filters</span><span class="sxs-lookup"><span data-stu-id="4ea02-103">Use IP filters</span></span>

<span data-ttu-id="4ea02-104">For scenarios in which Azure Event Hubs is only accessible from certain well-known sites, the *IP filter* feature enables you to configure rules for rejecting or accepting traffic originating from specific IPv4 addresses.</span><span class="sxs-lookup"><span data-stu-id="4ea02-104">For scenarios in which Azure Event Hubs is only accessible from certain well-known sites, the *IP filter* feature enables you to configure rules for rejecting or accepting traffic originating from specific IPv4 addresses.</span></span> <span data-ttu-id="4ea02-105">For example, these addresses may be those of a corporate NAT gateway.</span><span class="sxs-lookup"><span data-stu-id="4ea02-105">For example, these addresses may be those of a corporate NAT gateway.</span></span>

## <a name="when-to-use"></a><span data-ttu-id="4ea02-106">When to use</span><span class="sxs-lookup"><span data-stu-id="4ea02-106">When to use</span></span>

<span data-ttu-id="4ea02-107">Two important use cases in which it is useful to block Event Hubs endpoints for certain IP addresses are as follows:</span><span class="sxs-lookup"><span data-stu-id="4ea02-107">Two important use cases in which it is useful to block Event Hubs endpoints for certain IP addresses are as follows:</span></span>

- <span data-ttu-id="4ea02-108">Your event hubs should receive traffic only from a specified range of IP addresses and reject everything else.</span><span class="sxs-lookup"><span data-stu-id="4ea02-108">Your event hubs should receive traffic only from a specified range of IP addresses and reject everything else.</span></span> <span data-ttu-id="4ea02-109">For example, you are using Event Hubs with [Azure Express Route][express-route] to create private connections to your on-premises infrastructure.</span><span class="sxs-lookup"><span data-stu-id="4ea02-109">For example, you are using Event Hubs with [Azure Express Route][express-route] to create private connections to your on-premises infrastructure.</span></span> 
- <span data-ttu-id="4ea02-110">You need to reject traffic from IP addresses that have been identified as suspicious by the Event Hubs administrator.</span><span class="sxs-lookup"><span data-stu-id="4ea02-110">You need to reject traffic from IP addresses that have been identified as suspicious by the Event Hubs administrator.</span></span>

## <a name="how-filter-rules-are-applied"></a><span data-ttu-id="4ea02-111">How filter rules are applied</span><span class="sxs-lookup"><span data-stu-id="4ea02-111">How filter rules are applied</span></span>

<span data-ttu-id="4ea02-112">The IP filter rules are applied at the Event Hubs namespace level.</span><span class="sxs-lookup"><span data-stu-id="4ea02-112">The IP filter rules are applied at the Event Hubs namespace level.</span></span> <span data-ttu-id="4ea02-113">Therefore, the rules apply to all connections from clients using any supported protocol.</span><span class="sxs-lookup"><span data-stu-id="4ea02-113">Therefore, the rules apply to all connections from clients using any supported protocol.</span></span>

<span data-ttu-id="4ea02-114">Any connection attempt from an IP address that matches a rejecting IP rule on the Event Hubs namespace is rejected as unauthorized.</span><span class="sxs-lookup"><span data-stu-id="4ea02-114">Any connection attempt from an IP address that matches a rejecting IP rule on the Event Hubs namespace is rejected as unauthorized.</span></span> <span data-ttu-id="4ea02-115">The response does not mention the IP rule.</span><span class="sxs-lookup"><span data-stu-id="4ea02-115">The response does not mention the IP rule.</span></span>

## <a name="default-setting"></a><span data-ttu-id="4ea02-116">Default setting</span><span class="sxs-lookup"><span data-stu-id="4ea02-116">Default setting</span></span>

<span data-ttu-id="4ea02-117">By default, the **IP Filter** grid in the portal for Event Hubs is empty.</span><span class="sxs-lookup"><span data-stu-id="4ea02-117">By default, the **IP Filter** grid in the portal for Event Hubs is empty.</span></span> <span data-ttu-id="4ea02-118">This default setting means that your event hub accepts connections from any IP address.</span><span class="sxs-lookup"><span data-stu-id="4ea02-118">This default setting means that your event hub accepts connections from any IP address.</span></span> <span data-ttu-id="4ea02-119">This default setting is equivalent to a rule that accepts the 0.0.0.0/0 IP address range.</span><span class="sxs-lookup"><span data-stu-id="4ea02-119">This default setting is equivalent to a rule that accepts the 0.0.0.0/0 IP address range.</span></span>

## <a name="ip-filter-rule-evaluation"></a><span data-ttu-id="4ea02-120">IP filter rule evaluation</span><span class="sxs-lookup"><span data-stu-id="4ea02-120">IP filter rule evaluation</span></span>

<span data-ttu-id="4ea02-121">IP filter rules are applied in order, and the first rule that matches the IP address determines the accept or reject action.</span><span class="sxs-lookup"><span data-stu-id="4ea02-121">IP filter rules are applied in order, and the first rule that matches the IP address determines the accept or reject action.</span></span>

<span data-ttu-id="4ea02-122">For example, if you want to accept addresses in the range 70.37.104.0/24 and reject everything else, the first rule in the grid should accept the address range 70.37.104.0/24.</span><span class="sxs-lookup"><span data-stu-id="4ea02-122">For example, if you want to accept addresses in the range 70.37.104.0/24 and reject everything else, the first rule in the grid should accept the address range 70.37.104.0/24.</span></span> <span data-ttu-id="4ea02-123">The next rule should reject all addresses by using the range 0.0.0.0/0.</span><span class="sxs-lookup"><span data-stu-id="4ea02-123">The next rule should reject all addresses by using the range 0.0.0.0/0.</span></span>

> [!NOTE]
> <span data-ttu-id="4ea02-124">Rejecting IP addresses can prevent other Azure services (such as Azure Stream Analytics, Azure Virtual Machines, or the Device Explorer in the portal) from interacting with Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="4ea02-124">Rejecting IP addresses can prevent other Azure services (such as Azure Stream Analytics, Azure Virtual Machines, or the Device Explorer in the portal) from interacting with Event Hubs.</span></span>

### <a name="creating-a-virtual-network-rule-with-azure-resource-manager-templates"></a><span data-ttu-id="4ea02-125">Creating a virtual network rule with Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="4ea02-125">Creating a virtual network rule with Azure Resource Manager templates</span></span>

<span data-ttu-id="4ea02-126">The following Resource Manager template enables adding a virtual network rule to an existing Event Hubs namespace.</span><span class="sxs-lookup"><span data-stu-id="4ea02-126">The following Resource Manager template enables adding a virtual network rule to an existing Event Hubs namespace.</span></span>

<span data-ttu-id="4ea02-127">Template parameters:</span><span class="sxs-lookup"><span data-stu-id="4ea02-127">Template parameters:</span></span>

- <span data-ttu-id="4ea02-128">**ipFilterRuleName** must be a unique, case-insensitive, alphanumeric string, up to 128 characters long.</span><span class="sxs-lookup"><span data-stu-id="4ea02-128">**ipFilterRuleName** must be a unique, case-insensitive, alphanumeric string, up to 128 characters long.</span></span>
- <span data-ttu-id="4ea02-129">**ipFilterAction** is either **Reject** or **Accept** as the action to apply for the IP filter rule.</span><span class="sxs-lookup"><span data-stu-id="4ea02-129">**ipFilterAction** is either **Reject** or **Accept** as the action to apply for the IP filter rule.</span></span>
- <span data-ttu-id="4ea02-130">**ipMask** is a single IPv4 address or a block of IP addresses in CIDR notation.</span><span class="sxs-lookup"><span data-stu-id="4ea02-130">**ipMask** is a single IPv4 address or a block of IP addresses in CIDR notation.</span></span> <span data-ttu-id="4ea02-131">For example, in CIDR notation 70.37.104.0/24 represents the 256 IPv4 addresses from 70.37.104.0 to 70.37.104.255, with 24 indicating the number of significant prefix bits for the range.</span><span class="sxs-lookup"><span data-stu-id="4ea02-131">For example, in CIDR notation 70.37.104.0/24 represents the 256 IPv4 addresses from 70.37.104.0 to 70.37.104.255, with 24 indicating the number of significant prefix bits for the range.</span></span>

```json
{  
   "$schema":"http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
   "contentVersion":"1.0.0.0",
   "parameters":{     
          "namespaceName":{  
             "type":"string",
             "metadata":{  
                "description":"Name of the namespace"
             }
          },
          "ipFilterRuleName":{  
             "type":"string",
             "metadata":{  
                "description":"Name of the Authorization rule"
             }
          },
          "ipFilterAction":{  
             "type":"string",
             "allowedValues": ["Reject", "Accept"],
             "metadata":{  
                "description":"IP Filter Action"
             }
          },
          "IpMask":{  
             "type":"string",
             "metadata":{  
                "description":"IP Mask"
             }
          }
      },
    "resources": [
        {
            "apiVersion": "2018-01-01-preview",
            "name": "[concat(parameters('namespaceName'), '/', parameters('ipFilterRuleName'))]",
            "type": "Microsoft.EventHub/Namespaces/IPFilterRules",
            "properties": {
                "FilterName":"[parameters('ipFilterRuleName')]",
                "Action":"[parameters('ipFilterAction')]",              
                "IpMask": "[parameters('IpMask')]"
            }
        } 
    ]
}
```

<span data-ttu-id="4ea02-132">To deploy the template, follow the instructions for [Azure Resource Manager][lnk-deploy].</span><span class="sxs-lookup"><span data-stu-id="4ea02-132">To deploy the template, follow the instructions for [Azure Resource Manager][lnk-deploy].</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ea02-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="4ea02-133">Next steps</span></span>

<span data-ttu-id="4ea02-134">For constraining access to Event Hubs to Azure virtual networks, see the following link:</span><span class="sxs-lookup"><span data-stu-id="4ea02-134">For constraining access to Event Hubs to Azure virtual networks, see the following link:</span></span>

- <span data-ttu-id="4ea02-135">[Virtual Network Service Endpoints for Event Hubs][lnk-vnet]</span><span class="sxs-lookup"><span data-stu-id="4ea02-135">[Virtual Network Service Endpoints for Event Hubs][lnk-vnet]</span></span>

<!-- Links -->

[express-route]:  /azure/expressroute/expressroute-faqs#supported-services
[lnk-deploy]: ../azure-resource-manager/resource-group-template-deploy.md
[lnk-vnet]: event-hubs-service-endpoints.md