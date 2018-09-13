---
title: Create Apache Kafka enabled Azure Event Hubs | Microsoft Docs
description: Create a Kafka enabled Azure Event Hubs namespace using the Azure portal
services: event-hubs
documentationcenter: .net
author: basilhariri
manager: timlt
ms.service: event-hubs
ms.devlang: dotnet
ms.topic: article
ms.date: 08/16/2018
ms.author: bahariri
ms.openlocfilehash: 7ce12f9dcaa15ade95274419f99c13d5915dbaaa
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870190"
---
# <a name="create-apache-kafka-enabled-event-hubs"></a><span data-ttu-id="e0895-103">Create Apache Kafka enabled event hubs</span><span class="sxs-lookup"><span data-stu-id="e0895-103">Create Apache Kafka enabled event hubs</span></span>

<span data-ttu-id="e0895-104">Azure Event Hubs is a Big Data streaming Platform as a Service (PaaS) that ingests millions of events per second, and provides low latency and high throughput for real-time analytics and visualization.</span><span class="sxs-lookup"><span data-stu-id="e0895-104">Azure Event Hubs is a Big Data streaming Platform as a Service (PaaS) that ingests millions of events per second, and provides low latency and high throughput for real-time analytics and visualization.</span></span>

<span data-ttu-id="e0895-105">Azure Event Hubs provides you with a Kafka endpoint.</span><span class="sxs-lookup"><span data-stu-id="e0895-105">Azure Event Hubs provides you with a Kafka endpoint.</span></span> <span data-ttu-id="e0895-106">This endpoint enables your Event Hubs namespace to natively understand [Apache Kafka](https://kafka.apache.org/intro) message protocol and APIs.</span><span class="sxs-lookup"><span data-stu-id="e0895-106">This endpoint enables your Event Hubs namespace to natively understand [Apache Kafka](https://kafka.apache.org/intro) message protocol and APIs.</span></span> <span data-ttu-id="e0895-107">With this capability, you can communicate with your event hubs as you would with Kafka topics without changing your protocol clients or running your own clusters.</span><span class="sxs-lookup"><span data-stu-id="e0895-107">With this capability, you can communicate with your event hubs as you would with Kafka topics without changing your protocol clients or running your own clusters.</span></span> <span data-ttu-id="e0895-108">Event Hubs supports [Apache Kafka versions 1.0](https://kafka.apache.org/10/documentation.html) and later.</span><span class="sxs-lookup"><span data-stu-id="e0895-108">Event Hubs supports [Apache Kafka versions 1.0](https://kafka.apache.org/10/documentation.html) and later.</span></span>

<span data-ttu-id="e0895-109">This article describes how to create an Event Hubs namespace and get the connection string required to connect Kafka applications to Kafka-enabled event hubs.</span><span class="sxs-lookup"><span data-stu-id="e0895-109">This article describes how to create an Event Hubs namespace and get the connection string required to connect Kafka applications to Kafka-enabled event hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0895-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e0895-110">Prerequisites</span></span>

<span data-ttu-id="e0895-111">If you do not have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) before you begin.</span><span class="sxs-lookup"><span data-stu-id="e0895-111">If you do not have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) before you begin.</span></span>

## <a name="create-a-kafka-enabled-event-hubs-namespace"></a><span data-ttu-id="e0895-112">Create a Kafka enabled Event Hubs namespace</span><span class="sxs-lookup"><span data-stu-id="e0895-112">Create a Kafka enabled Event Hubs namespace</span></span>

1. <span data-ttu-id="e0895-113">Sign in to the [Azure portal][Azure portal], and click **Create a resource** at the top left of the screen.</span><span class="sxs-lookup"><span data-stu-id="e0895-113">Sign in to the [Azure portal][Azure portal], and click **Create a resource** at the top left of the screen.</span></span>

2. <span data-ttu-id="e0895-114">Search for Event Hubs and select the options shown here:</span><span class="sxs-lookup"><span data-stu-id="e0895-114">Search for Event Hubs and select the options shown here:</span></span>
    
    ![Search for Event Hubs in the portal](./media/event-hubs-create-kafka-enabled/event-hubs-create-event-hubs.png)
 
3. <span data-ttu-id="e0895-116">Provide a unique name and enable Kafka on the namespace.</span><span class="sxs-lookup"><span data-stu-id="e0895-116">Provide a unique name and enable Kafka on the namespace.</span></span> <span data-ttu-id="e0895-117">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="e0895-117">Click **Create**.</span></span>
    
    ![Create a namespace](./media/event-hubs-create-kafka-enabled/create-kafka-namespace.png)
 
4. <span data-ttu-id="e0895-119">Once the namespace is created, on the **Settings** tab click **Shared access policies** to get the connection string.</span><span class="sxs-lookup"><span data-stu-id="e0895-119">Once the namespace is created, on the **Settings** tab click **Shared access policies** to get the connection string.</span></span>

    ![Click Shared access policies](./media/event-hubs-create/create-event-hub7.png)

5. <span data-ttu-id="e0895-121">You can choose the default **RootManageSharedAccessKey**, or add a new policy.</span><span class="sxs-lookup"><span data-stu-id="e0895-121">You can choose the default **RootManageSharedAccessKey**, or add a new policy.</span></span> <span data-ttu-id="e0895-122">Click the policy name and copy the connection string.</span><span class="sxs-lookup"><span data-stu-id="e0895-122">Click the policy name and copy the connection string.</span></span> 
    
    ![Select a policy](./media/event-hubs-create/create-event-hub8.png)
 
6. <span data-ttu-id="e0895-124">Add this connection string to your Kafka application configuration.</span><span class="sxs-lookup"><span data-stu-id="e0895-124">Add this connection string to your Kafka application configuration.</span></span>

<span data-ttu-id="e0895-125">You can now stream events from your applications that use the Kafka protocol into Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="e0895-125">You can now stream events from your applications that use the Kafka protocol into Event Hubs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0895-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="e0895-126">Next steps</span></span>

<span data-ttu-id="e0895-127">To learn more about Event Hubs, visit these links:</span><span class="sxs-lookup"><span data-stu-id="e0895-127">To learn more about Event Hubs, visit these links:</span></span>

* [<span data-ttu-id="e0895-128">Stream into Event Hubs from your Kafka applications</span><span class="sxs-lookup"><span data-stu-id="e0895-128">Stream into Event Hubs from your Kafka applications</span></span>](event-hubs-quickstart-kafka-enabled-event-hubs.md)
* [<span data-ttu-id="e0895-129">Learn about Event Hubs for Kafka</span><span class="sxs-lookup"><span data-stu-id="e0895-129">Learn about Event Hubs for Kafka</span></span>](event-hubs-for-kafka-ecosystem-overview.md)
* [<span data-ttu-id="e0895-130">Learn about Event Hubs</span><span class="sxs-lookup"><span data-stu-id="e0895-130">Learn about Event Hubs</span></span>](event-hubs-what-is-event-hubs.md)


[Azure portal]: https://portal.azure.com/
