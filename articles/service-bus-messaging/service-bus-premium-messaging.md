---
title: Azure Service Bus Premium and Standard Messaging pricing tiers overview | Microsoft Docs
description: Service Bus Premium and Standard Messaging tiers
services: service-bus-messaging
documentationcenter: .net
author: djrosanova
manager: timlt
editor: ''
ms.assetid: e211774d-821c-4d79-8563-57472d746c58
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/30/2018
ms.author: spelluru
ms.openlocfilehash: 8e53cc5487a64fbd0c3a9ca26fc405756f09ce71
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44829205"
---
# <a name="service-bus-premium-and-standard-messaging-tiers"></a><span data-ttu-id="aa020-103">Service Bus Premium and Standard messaging tiers</span><span class="sxs-lookup"><span data-stu-id="aa020-103">Service Bus Premium and Standard messaging tiers</span></span>

<span data-ttu-id="aa020-104">Service Bus Messaging, which includes entities such as queues and topics, combines enterprise messaging capabilities with rich publish-subscribe semantics at cloud scale.</span><span class="sxs-lookup"><span data-stu-id="aa020-104">Service Bus Messaging, which includes entities such as queues and topics, combines enterprise messaging capabilities with rich publish-subscribe semantics at cloud scale.</span></span> <span data-ttu-id="aa020-105">Service Bus Messaging is used as the communication backbone for many sophisticated cloud solutions.</span><span class="sxs-lookup"><span data-stu-id="aa020-105">Service Bus Messaging is used as the communication backbone for many sophisticated cloud solutions.</span></span>

<span data-ttu-id="aa020-106">The *Premium* tier of Service Bus Messaging addresses common customer requests around scale, performance, and availability for mission-critical applications.</span><span class="sxs-lookup"><span data-stu-id="aa020-106">The *Premium* tier of Service Bus Messaging addresses common customer requests around scale, performance, and availability for mission-critical applications.</span></span> <span data-ttu-id="aa020-107">The Premium tier is recommended for production scenarios.</span><span class="sxs-lookup"><span data-stu-id="aa020-107">The Premium tier is recommended for production scenarios.</span></span> <span data-ttu-id="aa020-108">Although the feature sets are nearly identical, these two tiers of Service Bus Messaging are designed to serve different use cases.</span><span class="sxs-lookup"><span data-stu-id="aa020-108">Although the feature sets are nearly identical, these two tiers of Service Bus Messaging are designed to serve different use cases.</span></span>

<span data-ttu-id="aa020-109">Some high-level differences are highlighted in the following table.</span><span class="sxs-lookup"><span data-stu-id="aa020-109">Some high-level differences are highlighted in the following table.</span></span>

| <span data-ttu-id="aa020-110">Premium</span><span class="sxs-lookup"><span data-stu-id="aa020-110">Premium</span></span> | <span data-ttu-id="aa020-111">Standard</span><span class="sxs-lookup"><span data-stu-id="aa020-111">Standard</span></span> |
| --- | --- |
| <span data-ttu-id="aa020-112">High throughput</span><span class="sxs-lookup"><span data-stu-id="aa020-112">High throughput</span></span> |<span data-ttu-id="aa020-113">Variable throughput</span><span class="sxs-lookup"><span data-stu-id="aa020-113">Variable throughput</span></span> |
| <span data-ttu-id="aa020-114">Predictable performance</span><span class="sxs-lookup"><span data-stu-id="aa020-114">Predictable performance</span></span> |<span data-ttu-id="aa020-115">Variable latency</span><span class="sxs-lookup"><span data-stu-id="aa020-115">Variable latency</span></span> |
| <span data-ttu-id="aa020-116">Fixed pricing</span><span class="sxs-lookup"><span data-stu-id="aa020-116">Fixed pricing</span></span> |<span data-ttu-id="aa020-117">Pay as you go variable pricing</span><span class="sxs-lookup"><span data-stu-id="aa020-117">Pay as you go variable pricing</span></span> |
| <span data-ttu-id="aa020-118">Ability to scale workload up and down</span><span class="sxs-lookup"><span data-stu-id="aa020-118">Ability to scale workload up and down</span></span> |<span data-ttu-id="aa020-119">N/A</span><span class="sxs-lookup"><span data-stu-id="aa020-119">N/A</span></span> |
| <span data-ttu-id="aa020-120">Message size up to 1 MB</span><span class="sxs-lookup"><span data-stu-id="aa020-120">Message size up to 1 MB</span></span> |<span data-ttu-id="aa020-121">Message size up to 256 KB</span><span class="sxs-lookup"><span data-stu-id="aa020-121">Message size up to 256 KB</span></span> |

<span data-ttu-id="aa020-122">**Service Bus Premium Messaging** provides resource isolation at the CPU and memory level so that each customer workload runs in isolation.</span><span class="sxs-lookup"><span data-stu-id="aa020-122">**Service Bus Premium Messaging** provides resource isolation at the CPU and memory level so that each customer workload runs in isolation.</span></span> <span data-ttu-id="aa020-123">This resource container is called a *messaging unit*.</span><span class="sxs-lookup"><span data-stu-id="aa020-123">This resource container is called a *messaging unit*.</span></span> <span data-ttu-id="aa020-124">Each premium namespace is allocated at least one messaging unit.</span><span class="sxs-lookup"><span data-stu-id="aa020-124">Each premium namespace is allocated at least one messaging unit.</span></span> <span data-ttu-id="aa020-125">You can purchase 1, 2, or 4 messaging units for each Service Bus Premium namespace.</span><span class="sxs-lookup"><span data-stu-id="aa020-125">You can purchase 1, 2, or 4 messaging units for each Service Bus Premium namespace.</span></span> <span data-ttu-id="aa020-126">A single workload or entity can span multiple messaging units and the number of messaging units can be changed at will, although billing is in 24-hour or daily rate charges.</span><span class="sxs-lookup"><span data-stu-id="aa020-126">A single workload or entity can span multiple messaging units and the number of messaging units can be changed at will, although billing is in 24-hour or daily rate charges.</span></span> <span data-ttu-id="aa020-127">The result is predictable and repeatable performance for your Service Bus-based solution.</span><span class="sxs-lookup"><span data-stu-id="aa020-127">The result is predictable and repeatable performance for your Service Bus-based solution.</span></span>

<span data-ttu-id="aa020-128">Not only is this performance more predictable and available, but it is also faster.</span><span class="sxs-lookup"><span data-stu-id="aa020-128">Not only is this performance more predictable and available, but it is also faster.</span></span> <span data-ttu-id="aa020-129">Service Bus Premium Messaging builds on the storage engine introduced in [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="aa020-129">Service Bus Premium Messaging builds on the storage engine introduced in [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).</span></span> <span data-ttu-id="aa020-130">With Premium Messaging, peak performance is much faster than with the Standard tier.</span><span class="sxs-lookup"><span data-stu-id="aa020-130">With Premium Messaging, peak performance is much faster than with the Standard tier.</span></span>

## <a name="premium-messaging-technical-differences"></a><span data-ttu-id="aa020-131">Premium Messaging technical differences</span><span class="sxs-lookup"><span data-stu-id="aa020-131">Premium Messaging technical differences</span></span>

<span data-ttu-id="aa020-132">The following sections discuss a few differences between Premium and Standard messaging tiers.</span><span class="sxs-lookup"><span data-stu-id="aa020-132">The following sections discuss a few differences between Premium and Standard messaging tiers.</span></span>

### <a name="partitioned-queues-and-topics"></a><span data-ttu-id="aa020-133">Partitioned queues and topics</span><span class="sxs-lookup"><span data-stu-id="aa020-133">Partitioned queues and topics</span></span>

<span data-ttu-id="aa020-134">Partitioned queues and topics are not supported in Premium Messaging.</span><span class="sxs-lookup"><span data-stu-id="aa020-134">Partitioned queues and topics are not supported in Premium Messaging.</span></span> <span data-ttu-id="aa020-135">For more information about partitioning, see [Partitioned queues and topics](service-bus-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="aa020-135">For more information about partitioning, see [Partitioned queues and topics](service-bus-partitioning.md).</span></span>

### <a name="express-entities"></a><span data-ttu-id="aa020-136">Express entities</span><span class="sxs-lookup"><span data-stu-id="aa020-136">Express entities</span></span>

<span data-ttu-id="aa020-137">Because Premium messaging runs in a completely isolated run-time environment, express entities are not supported in Premium namespaces.</span><span class="sxs-lookup"><span data-stu-id="aa020-137">Because Premium messaging runs in a completely isolated run-time environment, express entities are not supported in Premium namespaces.</span></span> <span data-ttu-id="aa020-138">For more information about the express feature, see the [QueueDescription.EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress) property.</span><span class="sxs-lookup"><span data-stu-id="aa020-138">For more information about the express feature, see the [QueueDescription.EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress) property.</span></span>

<span data-ttu-id="aa020-139">If you have code running under Standard messaging and want to port it to the Premium tier, make sure the [EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress) property is set to **false** (the default value).</span><span class="sxs-lookup"><span data-stu-id="aa020-139">If you have code running under Standard messaging and want to port it to the Premium tier, make sure the [EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress) property is set to **false** (the default value).</span></span>

## <a name="get-started-with-premium-messaging"></a><span data-ttu-id="aa020-140">Get started with Premium Messaging</span><span class="sxs-lookup"><span data-stu-id="aa020-140">Get started with Premium Messaging</span></span>

<span data-ttu-id="aa020-141">Getting started with Premium Messaging is straightforward and the process is similar to that of Standard Messaging.</span><span class="sxs-lookup"><span data-stu-id="aa020-141">Getting started with Premium Messaging is straightforward and the process is similar to that of Standard Messaging.</span></span> <span data-ttu-id="aa020-142">Begin by [creating a namespace](service-bus-create-namespace-portal.md) in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="aa020-142">Begin by [creating a namespace](service-bus-create-namespace-portal.md) in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="aa020-143">Make sure you select **Premium** under **Pricing tier**.</span><span class="sxs-lookup"><span data-stu-id="aa020-143">Make sure you select **Premium** under **Pricing tier**.</span></span> <span data-ttu-id="aa020-144">Click **View full pricing details** to see more information about each tier.</span><span class="sxs-lookup"><span data-stu-id="aa020-144">Click **View full pricing details** to see more information about each tier.</span></span>

![create-premium-namespace][create-premium-namespace]

<span data-ttu-id="aa020-146">You can also create [Premium namespaces using Azure Resource Manager templates](https://azure.microsoft.com/resources/templates/101-servicebus-pn-ar/).</span><span class="sxs-lookup"><span data-stu-id="aa020-146">You can also create [Premium namespaces using Azure Resource Manager templates](https://azure.microsoft.com/resources/templates/101-servicebus-pn-ar/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa020-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="aa020-147">Next steps</span></span>

<span data-ttu-id="aa020-148">To learn more about Service Bus Messaging, see the following links:</span><span class="sxs-lookup"><span data-stu-id="aa020-148">To learn more about Service Bus Messaging, see the following links:</span></span>

* [<span data-ttu-id="aa020-149">Introducing Azure Service Bus Premium Messaging (blog post)</span><span class="sxs-lookup"><span data-stu-id="aa020-149">Introducing Azure Service Bus Premium Messaging (blog post)</span></span>](http://azure.microsoft.com/blog/introducing-azure-service-bus-premium-messaging/)
* [<span data-ttu-id="aa020-150">Introducing Azure Service Bus Premium Messaging (Channel9)</span><span class="sxs-lookup"><span data-stu-id="aa020-150">Introducing Azure Service Bus Premium Messaging (Channel9)</span></span>](https://channel9.msdn.com/Blogs/Subscribe/Introducing-Azure-Service-Bus-Premium-Messaging)
* [<span data-ttu-id="aa020-151">Service Bus Messaging overview</span><span class="sxs-lookup"><span data-stu-id="aa020-151">Service Bus Messaging overview</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="aa020-152">Get started with Service Bus queues</span><span class="sxs-lookup"><span data-stu-id="aa020-152">Get started with Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)

<!--Image references-->

[create-premium-namespace]: ./media/service-bus-premium-messaging/select-premium-tier.png
