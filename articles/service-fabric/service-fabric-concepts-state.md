---
title: Definine and manage state in Azure microservices| Microsoft Docs
description: How to define and manage service state in Service Fabric
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: ''
ms.assetid: f5e618a5-3ea3-4404-94af-122278f91652
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/05/2017
ms.author: masnider
ms.openlocfilehash: d03bd6a4c317da67a4e6d0e8cdb0cbd3f07d5a1f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554761"
---
# <a name="service-state"></a><span data-ttu-id="1bc0e-103">Service state</span><span class="sxs-lookup"><span data-stu-id="1bc0e-103">Service state</span></span>
<span data-ttu-id="1bc0e-104">**Service state** refers to the data that the service requires to function.</span><span class="sxs-lookup"><span data-stu-id="1bc0e-104">**Service state** refers to the data that the service requires to function.</span></span> <span data-ttu-id="1bc0e-105">It includes the data structures and variables that the service reads and writes to do work.</span><span class="sxs-lookup"><span data-stu-id="1bc0e-105">It includes the data structures and variables that the service reads and writes to do work.</span></span>

<span data-ttu-id="1bc0e-106">Consider a calculator service, for example.</span><span class="sxs-lookup"><span data-stu-id="1bc0e-106">Consider a calculator service, for example.</span></span> <span data-ttu-id="1bc0e-107">This service takes two numbers and returns their sum.</span><span class="sxs-lookup"><span data-stu-id="1bc0e-107">This service takes two numbers and returns their sum.</span></span> <span data-ttu-id="1bc0e-108">This is a purely stateless service that has no data associated with it.</span><span class="sxs-lookup"><span data-stu-id="1bc0e-108">This is a purely stateless service that has no data associated with it.</span></span>

<span data-ttu-id="1bc0e-109">Now consider the same calculator, but in addition to computing sum, it also has a method for returning the last sum it has computed.</span><span class="sxs-lookup"><span data-stu-id="1bc0e-109">Now consider the same calculator, but in addition to computing sum, it also has a method for returning the last sum it has computed.</span></span> <span data-ttu-id="1bc0e-110">This service is now stateful - it contains some state that it writes to (when it computes a new sum) and reads from (when it returns the last computed sum).</span><span class="sxs-lookup"><span data-stu-id="1bc0e-110">This service is now stateful - it contains some state that it writes to (when it computes a new sum) and reads from (when it returns the last computed sum).</span></span>

<span data-ttu-id="1bc0e-111">In Azure Service Fabric, the first service is called a stateless service.</span><span class="sxs-lookup"><span data-stu-id="1bc0e-111">In Azure Service Fabric, the first service is called a stateless service.</span></span> <span data-ttu-id="1bc0e-112">The second service is called a stateful service.</span><span class="sxs-lookup"><span data-stu-id="1bc0e-112">The second service is called a stateful service.</span></span>

## <a name="storing-service-state"></a><span data-ttu-id="1bc0e-113">Storing service state</span><span class="sxs-lookup"><span data-stu-id="1bc0e-113">Storing service state</span></span>
<span data-ttu-id="1bc0e-114">State can be either externalized or co-located with the code that is manipulating the state.</span><span class="sxs-lookup"><span data-stu-id="1bc0e-114">State can be either externalized or co-located with the code that is manipulating the state.</span></span> <span data-ttu-id="1bc0e-115">Externalization of state is typically done by using an external database or store.</span><span class="sxs-lookup"><span data-stu-id="1bc0e-115">Externalization of state is typically done by using an external database or store.</span></span> <span data-ttu-id="1bc0e-116">In our calculator example, this could be a SQL database in which the current result is stored in a table.</span><span class="sxs-lookup"><span data-stu-id="1bc0e-116">In our calculator example, this could be a SQL database in which the current result is stored in a table.</span></span> <span data-ttu-id="1bc0e-117">Every request to compute the sum performs an update on this row.</span><span class="sxs-lookup"><span data-stu-id="1bc0e-117">Every request to compute the sum performs an update on this row.</span></span>

<span data-ttu-id="1bc0e-118">State can also be co-located with the code that manipulates this code.</span><span class="sxs-lookup"><span data-stu-id="1bc0e-118">State can also be co-located with the code that manipulates this code.</span></span> <span data-ttu-id="1bc0e-119">Stateful services in Service Fabric can be built using this model.</span><span class="sxs-lookup"><span data-stu-id="1bc0e-119">Stateful services in Service Fabric can be built using this model.</span></span> <span data-ttu-id="1bc0e-120">Service Fabric provides the infrastructure to ensure that this state is highly available and fault tolerant in the event of a failure.</span><span class="sxs-lookup"><span data-stu-id="1bc0e-120">Service Fabric provides the infrastructure to ensure that this state is highly available and fault tolerant in the event of a failure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1bc0e-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="1bc0e-121">Next steps</span></span>
<span data-ttu-id="1bc0e-122">For more information on Service Fabric concepts, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="1bc0e-122">For more information on Service Fabric concepts, see the following articles:</span></span>

* [<span data-ttu-id="1bc0e-123">Availability of Service Fabric services</span><span class="sxs-lookup"><span data-stu-id="1bc0e-123">Availability of Service Fabric services</span></span>](service-fabric-availability-services.md)
* [<span data-ttu-id="1bc0e-124">Scalability of Service Fabric services</span><span class="sxs-lookup"><span data-stu-id="1bc0e-124">Scalability of Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
* [<span data-ttu-id="1bc0e-125">Partitioning Service Fabric services</span><span class="sxs-lookup"><span data-stu-id="1bc0e-125">Partitioning Service Fabric services</span></span>](service-fabric-concepts-partitioning.md)
* [<span data-ttu-id="1bc0e-126">Service Fabric Reliable Services</span><span class="sxs-lookup"><span data-stu-id="1bc0e-126">Service Fabric Reliable Services</span></span>](service-fabric-reliable-services-introduction.md)
