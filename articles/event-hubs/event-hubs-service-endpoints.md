---
title: Virtual Network service endpoints and rules for Azure Event Hubs | Microsoft Docs
description: Add a Microsoft.EventHub service endpoint to a virtual network.
services: event-hubs
documentationcenter: ''
author: ShubhaVijayasarathy
manager: timlt
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.date: 08/16/2018
ms.author: shvija
ms.openlocfilehash: b8c3270149c254898ad3180b92a4ff398f3efb6c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870653"
---
# <a name="use-virtual-network-service-endpoints-with-azure-event-hubs"></a><span data-ttu-id="6ebd8-103">Use Virtual Network service endpoints with Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="6ebd8-103">Use Virtual Network service endpoints with Azure Event Hubs</span></span>

<span data-ttu-id="6ebd8-104">The integration of Event Hubs with [Virtual Network (VNet) Service Endpoints][vnet-sep] enables secure access to messaging capabilities from workloads such as virtual machines that are bound to virtual networks, with the network traffic path being secured on both ends.</span><span class="sxs-lookup"><span data-stu-id="6ebd8-104">The integration of Event Hubs with [Virtual Network (VNet) Service Endpoints][vnet-sep] enables secure access to messaging capabilities from workloads such as virtual machines that are bound to virtual networks, with the network traffic path being secured on both ends.</span></span> 

<span data-ttu-id="6ebd8-105">Once configured to be bound to at least one virtual network subnet service endpoint, the respective Event Hubs namespace no longer accepts traffic from anywhere but authorized virtual network(s).</span><span class="sxs-lookup"><span data-stu-id="6ebd8-105">Once configured to be bound to at least one virtual network subnet service endpoint, the respective Event Hubs namespace no longer accepts traffic from anywhere but authorized virtual network(s).</span></span> <span data-ttu-id="6ebd8-106">From the virtual network perspective, binding an Event Hubs namespace to a service endpoint configures an isolated networking tunnel from the virtual network subnet to the messaging service.</span><span class="sxs-lookup"><span data-stu-id="6ebd8-106">From the virtual network perspective, binding an Event Hubs namespace to a service endpoint configures an isolated networking tunnel from the virtual network subnet to the messaging service.</span></span>

<span data-ttu-id="6ebd8-107">The result is a private and isolated relationship between the workloads bound to the subnet and the respective Event Hubs namespace, in spite of the observable network address of the messaging service endpoint being in a public IP range.</span><span class="sxs-lookup"><span data-stu-id="6ebd8-107">The result is a private and isolated relationship between the workloads bound to the subnet and the respective Event Hubs namespace, in spite of the observable network address of the messaging service endpoint being in a public IP range.</span></span>

## <a name="advanced-security-scenarios-enabled-by-vnet-integration"></a><span data-ttu-id="6ebd8-108">Advanced security scenarios enabled by VNet integration</span><span class="sxs-lookup"><span data-stu-id="6ebd8-108">Advanced security scenarios enabled by VNet integration</span></span> 

<span data-ttu-id="6ebd8-109">Solutions that require tight and compartmentalized security, and where virtual network subnets provide the segmentation between the compartmentalized services, generally still need communication paths between services residing in those compartments.</span><span class="sxs-lookup"><span data-stu-id="6ebd8-109">Solutions that require tight and compartmentalized security, and where virtual network subnets provide the segmentation between the compartmentalized services, generally still need communication paths between services residing in those compartments.</span></span>

<span data-ttu-id="6ebd8-110">Any immediate IP route between the compartments, including those carrying HTTPS over TCP/IP, carries the risk of exploitation of vulnerabilities from the network layer on up.</span><span class="sxs-lookup"><span data-stu-id="6ebd8-110">Any immediate IP route between the compartments, including those carrying HTTPS over TCP/IP, carries the risk of exploitation of vulnerabilities from the network layer on up.</span></span> <span data-ttu-id="6ebd8-111">Messaging services provide completely insulated communication paths, where messages are even written to disk as they transition between parties.</span><span class="sxs-lookup"><span data-stu-id="6ebd8-111">Messaging services provide completely insulated communication paths, where messages are even written to disk as they transition between parties.</span></span> <span data-ttu-id="6ebd8-112">Workloads in two distinct virtual networks that are both bound to the same Event Hubs instance can communicate efficiently and reliably via messages, while the respective network isolation boundary integrity is preserved.</span><span class="sxs-lookup"><span data-stu-id="6ebd8-112">Workloads in two distinct virtual networks that are both bound to the same Event Hubs instance can communicate efficiently and reliably via messages, while the respective network isolation boundary integrity is preserved.</span></span>
 
<span data-ttu-id="6ebd8-113">That means your security sensitive cloud solutions not only gain access to Azure industry-leading reliable and scalable asynchronous messaging capabilities, but they can now use messaging to create communication paths between secure solution compartments that are inherently more secure than what is achievable with any peer-to-peer communication mode, including HTTPS and other TLS-secured socket protocols.</span><span class="sxs-lookup"><span data-stu-id="6ebd8-113">That means your security sensitive cloud solutions not only gain access to Azure industry-leading reliable and scalable asynchronous messaging capabilities, but they can now use messaging to create communication paths between secure solution compartments that are inherently more secure than what is achievable with any peer-to-peer communication mode, including HTTPS and other TLS-secured socket protocols.</span></span>

## <a name="bind-event-hubs-to-virtual-networks"></a><span data-ttu-id="6ebd8-114">Bind Event Hubs to Virtual Networks</span><span class="sxs-lookup"><span data-stu-id="6ebd8-114">Bind Event Hubs to Virtual Networks</span></span>

<span data-ttu-id="6ebd8-115">*Virtual network rules* are the firewall security feature that controls whether your Azure Event Hubs server accepts connections from a particular virtual network subnet.</span><span class="sxs-lookup"><span data-stu-id="6ebd8-115">*Virtual network rules* are the firewall security feature that controls whether your Azure Event Hubs server accepts connections from a particular virtual network subnet.</span></span>

<span data-ttu-id="6ebd8-116">Binding an Event Hubs namespace to a virtual network is a two-step process.</span><span class="sxs-lookup"><span data-stu-id="6ebd8-116">Binding an Event Hubs namespace to a virtual network is a two-step process.</span></span> <span data-ttu-id="6ebd8-117">You first need to create a **Virtual Network service endpoint** on a Virtual Network subnet and enable it for "Microsoft.EventHub" as explained in the [service endpoint overview][vnet-sep].</span><span class="sxs-lookup"><span data-stu-id="6ebd8-117">You first need to create a **Virtual Network service endpoint** on a Virtual Network subnet and enable it for "Microsoft.EventHub" as explained in the [service endpoint overview][vnet-sep].</span></span> <span data-ttu-id="6ebd8-118">Once you have added the service endpoint, you bind the Event Hubs namespace to it with a *virtual network rule*.</span><span class="sxs-lookup"><span data-stu-id="6ebd8-118">Once you have added the service endpoint, you bind the Event Hubs namespace to it with a *virtual network rule*.</span></span>

<span data-ttu-id="6ebd8-119">The virtual network rule is a named association of the Event Hubs namespace with a virtual network subnet.</span><span class="sxs-lookup"><span data-stu-id="6ebd8-119">The virtual network rule is a named association of the Event Hubs namespace with a virtual network subnet.</span></span> <span data-ttu-id="6ebd8-120">While the rule exists, all workloads bound to the subnet are granted access to the Event Hubs namespace.</span><span class="sxs-lookup"><span data-stu-id="6ebd8-120">While the rule exists, all workloads bound to the subnet are granted access to the Event Hubs namespace.</span></span> <span data-ttu-id="6ebd8-121">Event Hubs itself never establishes outbound connections, does not need to gain access, and is therefore never granted access to your subnet by enabling this rule.</span><span class="sxs-lookup"><span data-stu-id="6ebd8-121">Event Hubs itself never establishes outbound connections, does not need to gain access, and is therefore never granted access to your subnet by enabling this rule.</span></span>

### <a name="create-a-virtual-network-rule-with-azure-resource-manager-templates"></a><span data-ttu-id="6ebd8-122">Create a virtual network rule with Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="6ebd8-122">Create a virtual network rule with Azure Resource Manager templates</span></span>

<span data-ttu-id="6ebd8-123">The following Resource Manager template enables adding a virtual network rule to an existing Event Hubs namespace.</span><span class="sxs-lookup"><span data-stu-id="6ebd8-123">The following Resource Manager template enables adding a virtual network rule to an existing Event Hubs namespace.</span></span>

<span data-ttu-id="6ebd8-124">Template parameters:</span><span class="sxs-lookup"><span data-stu-id="6ebd8-124">Template parameters:</span></span>

* <span data-ttu-id="6ebd8-125">**namespaceName**: Event Hubs namespace.</span><span class="sxs-lookup"><span data-stu-id="6ebd8-125">**namespaceName**: Event Hubs namespace.</span></span>
* <span data-ttu-id="6ebd8-126">**vnetRuleName**: Name for the Virtual Network rule to be created.</span><span class="sxs-lookup"><span data-stu-id="6ebd8-126">**vnetRuleName**: Name for the Virtual Network rule to be created.</span></span>
* <span data-ttu-id="6ebd8-127">**virtualNetworkingSubnetId**: Fully qualified Resource Manager path for the virtual network subnet; for example, `subscriptions/{id}/resourceGroups/{rg}/providers/Microsoft.Network/virtualNetworks/{vnet}/subnets/default` for the default subnet of a virtual network.</span><span class="sxs-lookup"><span data-stu-id="6ebd8-127">**virtualNetworkingSubnetId**: Fully qualified Resource Manager path for the virtual network subnet; for example, `subscriptions/{id}/resourceGroups/{rg}/providers/Microsoft.Network/virtualNetworks/{vnet}/subnets/default` for the default subnet of a virtual network.</span></span>

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
          "vnetRuleName":{  
             "type":"string",
             "metadata":{  
                "description":"Name of the Authorization rule"
             }
          },
          "virtualNetworkSubnetId":{  
             "type":"string",
             "metadata":{  
                "description":"subnet Azure Resource Manager ID"
             }
          }
      },
    "resources": [
        {
            "apiVersion": "2018-01-01-preview",
            "name": "[concat(parameters('namespaceName'), '/', parameters('vnetRuleName'))]",
            "type":"Microsoft.EventHub/namespaces/VirtualNetworkRules",         
            "properties": {             
                "virtualNetworkSubnetId": "[parameters('virtualNetworkSubnetId')]"  
            }
        } 
    ]
}
```

<span data-ttu-id="6ebd8-128">To deploy the template, follow the instructions for [Azure Resource Manager][lnk-deploy].</span><span class="sxs-lookup"><span data-stu-id="6ebd8-128">To deploy the template, follow the instructions for [Azure Resource Manager][lnk-deploy].</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ebd8-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="6ebd8-129">Next steps</span></span>

<span data-ttu-id="6ebd8-130">For more information about virtual networks, see the following links:</span><span class="sxs-lookup"><span data-stu-id="6ebd8-130">For more information about virtual networks, see the following links:</span></span>

- <span data-ttu-id="6ebd8-131">[Azure virtual network service endpoints][vnet-sep]</span><span class="sxs-lookup"><span data-stu-id="6ebd8-131">[Azure virtual network service endpoints][vnet-sep]</span></span>
- <span data-ttu-id="6ebd8-132">[Azure Event Hubs IP filtering][ip-filtering]</span><span class="sxs-lookup"><span data-stu-id="6ebd8-132">[Azure Event Hubs IP filtering][ip-filtering]</span></span>

[vnet-sep]: ../virtual-network/virtual-network-service-endpoints-overview.md
[lnk-deploy]: ../azure-resource-manager/resource-group-template-deploy.md
[ip-filtering]: event-hubs-ip-filtering.md