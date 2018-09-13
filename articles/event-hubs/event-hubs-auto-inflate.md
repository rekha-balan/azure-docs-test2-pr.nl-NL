---
title: Automatically scale up Azure Event Hubs throughput units | Microsoft Docs
description: Enable Auto-inflate on a namespace to automatically scale up throughput units.
services: event-hubs
documentationcenter: na
author: ShubhaVijayasarathy
manager: timlt
editor: ''
ms.assetid: ''
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/02/2018
ms.author: shvija
ms.openlocfilehash: 32f99b43a37277e70d209f1f315dcb398c2b5931
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856789"
---
# <a name="automatically-scale-up-azure-event-hubs-throughput-units"></a><span data-ttu-id="a981e-103">Automatically scale up Azure Event Hubs throughput units</span><span class="sxs-lookup"><span data-stu-id="a981e-103">Automatically scale up Azure Event Hubs throughput units</span></span>

<span data-ttu-id="a981e-104">Azure Event Hubs is a highly scalable data streaming platform.</span><span class="sxs-lookup"><span data-stu-id="a981e-104">Azure Event Hubs is a highly scalable data streaming platform.</span></span> <span data-ttu-id="a981e-105">As such, Event Hubs usage often increases after starting to use the service.</span><span class="sxs-lookup"><span data-stu-id="a981e-105">As such, Event Hubs usage often increases after starting to use the service.</span></span> <span data-ttu-id="a981e-106">Such usage requires increasing the predetermined [throughput units](event-hubs-features.md#throughput-units) to scale Event Hubs and handle larger transfer rates.</span><span class="sxs-lookup"><span data-stu-id="a981e-106">Such usage requires increasing the predetermined [throughput units](event-hubs-features.md#throughput-units) to scale Event Hubs and handle larger transfer rates.</span></span> <span data-ttu-id="a981e-107">The **Auto-inflate** feature of Event Hubs automatically scales up by increasing the number of throughput units, to meet usage needs.</span><span class="sxs-lookup"><span data-stu-id="a981e-107">The **Auto-inflate** feature of Event Hubs automatically scales up by increasing the number of throughput units, to meet usage needs.</span></span> <span data-ttu-id="a981e-108">Increasing throughput units prevents throttling scenarios, in which:</span><span class="sxs-lookup"><span data-stu-id="a981e-108">Increasing throughput units prevents throttling scenarios, in which:</span></span>

* <span data-ttu-id="a981e-109">Data ingress rates exceed set throughput units.</span><span class="sxs-lookup"><span data-stu-id="a981e-109">Data ingress rates exceed set throughput units.</span></span>
* <span data-ttu-id="a981e-110">Data egress request rates exceed set throughput units.</span><span class="sxs-lookup"><span data-stu-id="a981e-110">Data egress request rates exceed set throughput units.</span></span>

## <a name="how-auto-inflate-works"></a><span data-ttu-id="a981e-111">How Auto-inflate works</span><span class="sxs-lookup"><span data-stu-id="a981e-111">How Auto-inflate works</span></span>

<span data-ttu-id="a981e-112">Event Hubs traffic is controlled by [throughput units](event-hubs-features.md#throughput-units).</span><span class="sxs-lookup"><span data-stu-id="a981e-112">Event Hubs traffic is controlled by [throughput units](event-hubs-features.md#throughput-units).</span></span> <span data-ttu-id="a981e-113">A single throughput unit allows 1 MB per second of ingress and twice that amount of egress.</span><span class="sxs-lookup"><span data-stu-id="a981e-113">A single throughput unit allows 1 MB per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="a981e-114">Standard event hubs can be configured with 1-20 throughput units.</span><span class="sxs-lookup"><span data-stu-id="a981e-114">Standard event hubs can be configured with 1-20 throughput units.</span></span> <span data-ttu-id="a981e-115">Auto-inflate enables you to start small with the minimum required throughput units you choose.</span><span class="sxs-lookup"><span data-stu-id="a981e-115">Auto-inflate enables you to start small with the minimum required throughput units you choose.</span></span> <span data-ttu-id="a981e-116">The feature then scales automatically to the maximum limit of throughput units you need, depending on the increase in your traffic.</span><span class="sxs-lookup"><span data-stu-id="a981e-116">The feature then scales automatically to the maximum limit of throughput units you need, depending on the increase in your traffic.</span></span> <span data-ttu-id="a981e-117">Auto-inflate provides the following benefits:</span><span class="sxs-lookup"><span data-stu-id="a981e-117">Auto-inflate provides the following benefits:</span></span>

- <span data-ttu-id="a981e-118">An efficient scaling mechanism to start small and scale up as you grow.</span><span class="sxs-lookup"><span data-stu-id="a981e-118">An efficient scaling mechanism to start small and scale up as you grow.</span></span>
- <span data-ttu-id="a981e-119">Automatically scale to the specified upper limit without throttling issues.</span><span class="sxs-lookup"><span data-stu-id="a981e-119">Automatically scale to the specified upper limit without throttling issues.</span></span>
- <span data-ttu-id="a981e-120">More control over scaling, because you control when and how much to scale.</span><span class="sxs-lookup"><span data-stu-id="a981e-120">More control over scaling, because you control when and how much to scale.</span></span>

## <a name="enable-auto-inflate-on-a-namespace"></a><span data-ttu-id="a981e-121">Enable Auto-inflate on a namespace</span><span class="sxs-lookup"><span data-stu-id="a981e-121">Enable Auto-inflate on a namespace</span></span>

<span data-ttu-id="a981e-122">You can enable or disable Auto-inflate on an Event Hubs namespace by using either of the following methods:</span><span class="sxs-lookup"><span data-stu-id="a981e-122">You can enable or disable Auto-inflate on an Event Hubs namespace by using either of the following methods:</span></span>

- <span data-ttu-id="a981e-123">The [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a981e-123">The [Azure portal](https://portal.azure.com).</span></span>
- <span data-ttu-id="a981e-124">An [Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate).</span><span class="sxs-lookup"><span data-stu-id="a981e-124">An [Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate).</span></span>

### <a name="enable-auto-inflate-through-the-portal"></a><span data-ttu-id="a981e-125">Enable Auto-inflate through the portal</span><span class="sxs-lookup"><span data-stu-id="a981e-125">Enable Auto-inflate through the portal</span></span>

<span data-ttu-id="a981e-126">You can enable the Auto-inflate feature when creating an Event Hubs namespace:</span><span class="sxs-lookup"><span data-stu-id="a981e-126">You can enable the Auto-inflate feature when creating an Event Hubs namespace:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate1.png)

<span data-ttu-id="a981e-127">With this option enabled, you can start small with your throughput units and scale up as your usage needs increase.</span><span class="sxs-lookup"><span data-stu-id="a981e-127">With this option enabled, you can start small with your throughput units and scale up as your usage needs increase.</span></span> <span data-ttu-id="a981e-128">The upper limit for inflation does not immediately affect pricing, which depends on the number of throughput units used per hour.</span><span class="sxs-lookup"><span data-stu-id="a981e-128">The upper limit for inflation does not immediately affect pricing, which depends on the number of throughput units used per hour.</span></span>

<span data-ttu-id="a981e-129">You can also enable Auto-inflate using the **Scale** option on the settings pane in the portal:</span><span class="sxs-lookup"><span data-stu-id="a981e-129">You can also enable Auto-inflate using the **Scale** option on the settings pane in the portal:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate2.png)

### <a name="enable-auto-inflate-using-an-azure-resource-manager-template"></a><span data-ttu-id="a981e-130">Enable Auto-Inflate using an Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="a981e-130">Enable Auto-Inflate using an Azure Resource Manager template</span></span>

<span data-ttu-id="a981e-131">You can enable Auto-inflate during an Azure Resource Manager template deployment.</span><span class="sxs-lookup"><span data-stu-id="a981e-131">You can enable Auto-inflate during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="a981e-132">For example, set the `isAutoInflateEnabled` property to **true** and set `maximumThroughputUnits` to 10.</span><span class="sxs-lookup"><span data-stu-id="a981e-132">For example, set the `isAutoInflateEnabled` property to **true** and set `maximumThroughputUnits` to 10.</span></span> <span data-ttu-id="a981e-133">For example:</span><span class="sxs-lookup"><span data-stu-id="a981e-133">For example:</span></span>

```json
"resources": [
        {
            "apiVersion": "2017-04-01",
            "name": "[parameters('namespaceName')]",
            "type": "Microsoft.EventHub/Namespaces",
            "location": "[variables('location')]",
            "sku": {
                "name": "Standard",
                "tier": "Standard"
            },
            "properties": {
                "isAutoInflateEnabled": true,
                "maximumThroughputUnits": 10
            },
            "resources": [
                {
                    "apiVersion": "2017-04-01",
                    "name": "[parameters('eventHubName')]",
                    "type": "EventHubs",
                    "dependsOn": [
                        "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
                    ],
                    "properties": {},
                    "resources": [
                        {
                            "apiVersion": "2017-04-01",
                            "name": "[parameters('consumerGroupName')]",
                            "type": "ConsumerGroups",
                            "dependsOn": [
                                "[parameters('eventHubName')]"
                            ],
                            "properties": {}
                        }
                    ]
                }
            ]
        }
    ]
```

<span data-ttu-id="a981e-134">For the complete template, see the [Create Event Hubs namespace and enable inflate](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) template on GitHub.</span><span class="sxs-lookup"><span data-stu-id="a981e-134">For the complete template, see the [Create Event Hubs namespace and enable inflate](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) template on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a981e-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="a981e-135">Next steps</span></span>

<span data-ttu-id="a981e-136">You can learn more about Event Hubs by visiting the following links:</span><span class="sxs-lookup"><span data-stu-id="a981e-136">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="a981e-137">Event Hubs overview</span><span class="sxs-lookup"><span data-stu-id="a981e-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)

