---
title: Service Bus Premium and Standard Messaging pricing tiers overview | Microsoft Docs
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
ms.date: 04/19/2017
ms.author: darosa;sethm;jotaub
ms.openlocfilehash: f65fb616fc7bd190df35377249300a317bd6bcc3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662614"
---
# <a name="service-bus-premium-and-standard-messaging-tiers"></a><span data-ttu-id="e02a7-103">Service Bus Premium and Standard messaging tiers</span><span class="sxs-lookup"><span data-stu-id="e02a7-103">Service Bus Premium and Standard messaging tiers</span></span>

<span data-ttu-id="e02a7-104">Service Bus Messaging, which includes entities such as queues and topics, combines enterprise messaging capabilities with rich publish-subscribe semantics at cloud scale.</span><span class="sxs-lookup"><span data-stu-id="e02a7-104">Service Bus Messaging, which includes entities such as queues and topics, combines enterprise messaging capabilities with rich publish-subscribe semantics at cloud scale.</span></span> <span data-ttu-id="e02a7-105">Service Bus Messaging is used as the communication backbone for many sophisticated cloud solutions.</span><span class="sxs-lookup"><span data-stu-id="e02a7-105">Service Bus Messaging is used as the communication backbone for many sophisticated cloud solutions.</span></span>

<span data-ttu-id="e02a7-106">The *Premium* tier of Service Bus Messaging addresses common customer requests around scale, performance, and availability for mission-critical applications.</span><span class="sxs-lookup"><span data-stu-id="e02a7-106">The *Premium* tier of Service Bus Messaging addresses common customer requests around scale, performance, and availability for mission-critical applications.</span></span> <span data-ttu-id="e02a7-107">Although the feature sets are nearly identical, these two tiers of Service Bus Messaging are designed to serve different use cases.</span><span class="sxs-lookup"><span data-stu-id="e02a7-107">Although the feature sets are nearly identical, these two tiers of Service Bus Messaging are designed to serve different use cases.</span></span>

<span data-ttu-id="e02a7-108">Some high-level differences are highlighted in the following table.</span><span class="sxs-lookup"><span data-stu-id="e02a7-108">Some high-level differences are highlighted in the following table.</span></span>

| <span data-ttu-id="e02a7-109">Premium</span><span class="sxs-lookup"><span data-stu-id="e02a7-109">Premium</span></span> | <span data-ttu-id="e02a7-110">Standard</span><span class="sxs-lookup"><span data-stu-id="e02a7-110">Standard</span></span> |
| --- | --- |
| <span data-ttu-id="e02a7-111">High throughput</span><span class="sxs-lookup"><span data-stu-id="e02a7-111">High throughput</span></span> |<span data-ttu-id="e02a7-112">Variable throughput</span><span class="sxs-lookup"><span data-stu-id="e02a7-112">Variable throughput</span></span> |
| <span data-ttu-id="e02a7-113">Predictable performance</span><span class="sxs-lookup"><span data-stu-id="e02a7-113">Predictable performance</span></span> |<span data-ttu-id="e02a7-114">Variable latency</span><span class="sxs-lookup"><span data-stu-id="e02a7-114">Variable latency</span></span> |
| <span data-ttu-id="e02a7-115">Fixed pricing</span><span class="sxs-lookup"><span data-stu-id="e02a7-115">Fixed pricing</span></span> |<span data-ttu-id="e02a7-116">Pay as you go variable pricing</span><span class="sxs-lookup"><span data-stu-id="e02a7-116">Pay as you go variable pricing</span></span> |
| <span data-ttu-id="e02a7-117">Ability to scale workload up and down</span><span class="sxs-lookup"><span data-stu-id="e02a7-117">Ability to scale workload up and down</span></span> |<span data-ttu-id="e02a7-118">N/A</span><span class="sxs-lookup"><span data-stu-id="e02a7-118">N/A</span></span> |
| <span data-ttu-id="e02a7-119">Message size up to 1 MB</span><span class="sxs-lookup"><span data-stu-id="e02a7-119">Message size up to 1 MB</span></span> |<span data-ttu-id="e02a7-120">Message size up to 256 KB</span><span class="sxs-lookup"><span data-stu-id="e02a7-120">Message size up to 256 KB</span></span> |

<span data-ttu-id="e02a7-121">**Service Bus Premium Messaging** provides resource isolation at the CPU and memory level so that each customer workload runs in isolation.</span><span class="sxs-lookup"><span data-stu-id="e02a7-121">**Service Bus Premium Messaging** provides resource isolation at the CPU and memory level so that each customer workload runs in isolation.</span></span> <span data-ttu-id="e02a7-122">This resource container is called a *messaging unit*.</span><span class="sxs-lookup"><span data-stu-id="e02a7-122">This resource container is called a *messaging unit*.</span></span> <span data-ttu-id="e02a7-123">Each premium namespace is allocated at least one messaging unit.</span><span class="sxs-lookup"><span data-stu-id="e02a7-123">Each premium namespace is allocated at least one messaging unit.</span></span> <span data-ttu-id="e02a7-124">You can purchase 1, 2, or 4 messaging units for each Service Bus Premium namespace.</span><span class="sxs-lookup"><span data-stu-id="e02a7-124">You can purchase 1, 2, or 4 messaging units for each Service Bus Premium namespace.</span></span> <span data-ttu-id="e02a7-125">A single workload or entity can span multiple messaging units and the number of messaging units can be changed at will, although billing is in 24-hour or daily rate charges.</span><span class="sxs-lookup"><span data-stu-id="e02a7-125">A single workload or entity can span multiple messaging units and the number of messaging units can be changed at will, although billing is in 24-hour or daily rate charges.</span></span> <span data-ttu-id="e02a7-126">The result is predictable and repeatable performance for your Service Bus-based solution.</span><span class="sxs-lookup"><span data-stu-id="e02a7-126">The result is predictable and repeatable performance for your Service Bus-based solution.</span></span>

<span data-ttu-id="e02a7-127">Not only is this performance more predictable and available, but it is also faster.</span><span class="sxs-lookup"><span data-stu-id="e02a7-127">Not only is this performance more predictable and available, but it is also faster.</span></span> <span data-ttu-id="e02a7-128">Service Bus Premium Messaging builds on the storage engine introduced in [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="e02a7-128">Service Bus Premium Messaging builds on the storage engine introduced in [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).</span></span> <span data-ttu-id="e02a7-129">With Premium Messaging, peak performance is much faster than with the Standard tier.</span><span class="sxs-lookup"><span data-stu-id="e02a7-129">With Premium Messaging, peak performance is much faster than with the Standard tier.</span></span>

## <a name="premium-messaging-technical-differences"></a><span data-ttu-id="e02a7-130">Premium Messaging technical differences</span><span class="sxs-lookup"><span data-stu-id="e02a7-130">Premium Messaging technical differences</span></span>

<span data-ttu-id="e02a7-131">The following sections discuss a few differences between Premium and Standard messaging tiers.</span><span class="sxs-lookup"><span data-stu-id="e02a7-131">The following sections discuss a few differences between Premium and Standard messaging tiers.</span></span>

### <a name="partitioned-queues-and-topics"></a><span data-ttu-id="e02a7-132">Partitioned queues and topics</span><span class="sxs-lookup"><span data-stu-id="e02a7-132">Partitioned queues and topics</span></span>

<span data-ttu-id="e02a7-133">Partitioned queues and topics are supported in Premium Messaging, but they do not function the same way as in the Standard and Basic tiers of Service Bus Messaging.</span><span class="sxs-lookup"><span data-stu-id="e02a7-133">Partitioned queues and topics are supported in Premium Messaging, but they do not function the same way as in the Standard and Basic tiers of Service Bus Messaging.</span></span> <span data-ttu-id="e02a7-134">Premium Messaging does not use SQL as a data store and no longer has the possible resource competition associated with a shared platform.</span><span class="sxs-lookup"><span data-stu-id="e02a7-134">Premium Messaging does not use SQL as a data store and no longer has the possible resource competition associated with a shared platform.</span></span> <span data-ttu-id="e02a7-135">As a result, partitioning is not necessary for performance.</span><span class="sxs-lookup"><span data-stu-id="e02a7-135">As a result, partitioning is not necessary for performance.</span></span> <span data-ttu-id="e02a7-136">Additionally, the partition count has been changed from 16 partitions in Standard Messaging to 2 partitions in Premium.</span><span class="sxs-lookup"><span data-stu-id="e02a7-136">Additionally, the partition count has been changed from 16 partitions in Standard Messaging to 2 partitions in Premium.</span></span> <span data-ttu-id="e02a7-137">Having two partitions ensures availability and is a more appropriate number for the Premium runtime environment.</span><span class="sxs-lookup"><span data-stu-id="e02a7-137">Having two partitions ensures availability and is a more appropriate number for the Premium runtime environment.</span></span> <span data-ttu-id="e02a7-138">For more information about partitioning, see [Partitioned queues and topics](service-bus-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="e02a7-138">For more information about partitioning, see [Partitioned queues and topics](service-bus-partitioning.md).</span></span>

### <a name="express-entities"></a><span data-ttu-id="e02a7-139">Express entities</span><span class="sxs-lookup"><span data-stu-id="e02a7-139">Express entities</span></span>

<span data-ttu-id="e02a7-140">Because Premium Messaging runs in a completely isolated run-time environment, express entities are not supported in Premium namespaces.</span><span class="sxs-lookup"><span data-stu-id="e02a7-140">Because Premium Messaging runs in a completely isolated run-time environment, express entities are not supported in Premium namespaces.</span></span> <span data-ttu-id="e02a7-141">For more information about the express feature, see the [QueueDescription.EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress) property.</span><span class="sxs-lookup"><span data-stu-id="e02a7-141">For more information about the express feature, see the [QueueDescription.EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress) property.</span></span>

## <a name="get-started-with-premium-messaging"></a><span data-ttu-id="e02a7-142">Get started with Premium Messaging</span><span class="sxs-lookup"><span data-stu-id="e02a7-142">Get started with Premium Messaging</span></span>

<span data-ttu-id="e02a7-143">Getting started with Premium Messaging is straightforward and the process is similar to that of Standard Messaging.</span><span class="sxs-lookup"><span data-stu-id="e02a7-143">Getting started with Premium Messaging is straightforward and the process is similar to that of Standard Messaging.</span></span> <span data-ttu-id="e02a7-144">Begin by [creating a namespace](service-bus-create-namespace-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e02a7-144">Begin by [creating a namespace](service-bus-create-namespace-portal.md).</span></span> <span data-ttu-id="e02a7-145">Make sure you select **Premium** under **Pricing tier**.</span><span class="sxs-lookup"><span data-stu-id="e02a7-145">Make sure you select **Premium** under **Pricing tier**.</span></span>

![create-premium-namespace][create-premium-namespace]

<span data-ttu-id="e02a7-147">You can also create [Premium namespaces using Azure Resource Manager templates](https://azure.microsoft.com/en-us/resources/templates/101-servicebus-pn-ar/).</span><span class="sxs-lookup"><span data-stu-id="e02a7-147">You can also create [Premium namespaces using Azure Resource Manager templates](https://azure.microsoft.com/en-us/resources/templates/101-servicebus-pn-ar/).</span></span>


## <a name="next-steps"></a><span data-ttu-id="e02a7-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="e02a7-148">Next steps</span></span>

<span data-ttu-id="e02a7-149">To learn more about Service Bus Messaging, see the following topics.</span><span class="sxs-lookup"><span data-stu-id="e02a7-149">To learn more about Service Bus Messaging, see the following topics.</span></span>

* [<span data-ttu-id="e02a7-150">Introducing Azure Service Bus Premium Messaging (blog post)</span><span class="sxs-lookup"><span data-stu-id="e02a7-150">Introducing Azure Service Bus Premium Messaging (blog post)</span></span>](http://azure.microsoft.com/blog/introducing-azure-service-bus-premium-messaging/)
* [<span data-ttu-id="e02a7-151">Introducing Azure Service Bus Premium Messaging (Channel9)</span><span class="sxs-lookup"><span data-stu-id="e02a7-151">Introducing Azure Service Bus Premium Messaging (Channel9)</span></span>](https://channel9.msdn.com/Blogs/Subscribe/Introducing-Azure-Service-Bus-Premium-Messaging)
* [<span data-ttu-id="e02a7-152">Service Bus Messaging overview</span><span class="sxs-lookup"><span data-stu-id="e02a7-152">Service Bus Messaging overview</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="e02a7-153">How to use Service Bus queues</span><span class="sxs-lookup"><span data-stu-id="e02a7-153">How to use Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)

<!--Image references-->

[create-premium-namespace]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-premium-messaging/select-premium-tier.png

