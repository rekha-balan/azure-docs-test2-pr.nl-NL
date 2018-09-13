---
title: Azure Event Hubs API overview | Microsoft Docs
description: Overview of available Azure Event Hubs APIs
services: event-hubs
documentationcenter: na
author: jtaubensee
manager: timlt
editor: ''
ms.assetid: 3f221a0c-182d-4e39-9f3d-3a3c16c5c6ed
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/31/2017
ms.author: jotaub
ms.openlocfilehash: a10ab3cf10826c63785d6427c27712573e82457a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564187"
---
# <a name="available-event-hubs-apis"></a><span data-ttu-id="deca1-103">Available Event Hubs APIs</span><span class="sxs-lookup"><span data-stu-id="deca1-103">Available Event Hubs APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="deca1-104">Runtime APIs</span><span class="sxs-lookup"><span data-stu-id="deca1-104">Runtime APIs</span></span>

<span data-ttu-id="deca1-105">The following is a listing of all currently available Azure Event Hubs runtime clients.</span><span class="sxs-lookup"><span data-stu-id="deca1-105">The following is a listing of all currently available Azure Event Hubs runtime clients.</span></span> <span data-ttu-id="deca1-106">While some of these libraries also include limited management functionality, there are also [specific libraries](#management-apis) dedicated to management operations.</span><span class="sxs-lookup"><span data-stu-id="deca1-106">While some of these libraries also include limited management functionality, there are also [specific libraries](#management-apis) dedicated to management operations.</span></span> <span data-ttu-id="deca1-107">The core focus of these libraries is to send and receive messages from an event hub.</span><span class="sxs-lookup"><span data-stu-id="deca1-107">The core focus of these libraries is to send and receive messages from an event hub.</span></span>

<span data-ttu-id="deca1-108">See [additional information](#additional-information) for more details on the current status of each runtime library.</span><span class="sxs-lookup"><span data-stu-id="deca1-108">See [additional information](#additional-information) for more details on the current status of each runtime library.</span></span>

| <span data-ttu-id="deca1-109">Language/Platform</span><span class="sxs-lookup"><span data-stu-id="deca1-109">Language/Platform</span></span> | <span data-ttu-id="deca1-110">Client package</span><span class="sxs-lookup"><span data-stu-id="deca1-110">Client package</span></span> | <span data-ttu-id="deca1-111">EventProcessorHost package</span><span class="sxs-lookup"><span data-stu-id="deca1-111">EventProcessorHost package</span></span> | <span data-ttu-id="deca1-112">Repository</span><span class="sxs-lookup"><span data-stu-id="deca1-112">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="deca1-113">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="deca1-113">.NET Standard</span></span> | [<span data-ttu-id="deca1-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="deca1-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) | [<span data-ttu-id="deca1-115">NuGet</span><span class="sxs-lookup"><span data-stu-id="deca1-115">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) | [<span data-ttu-id="deca1-116">GitHub</span><span class="sxs-lookup"><span data-stu-id="deca1-116">GitHub</span></span>](https://github.com/azure/azure-event-hubs-dotnet) |
| <span data-ttu-id="deca1-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="deca1-117">.NET Framework</span></span> | [<span data-ttu-id="deca1-118">NuGet</span><span class="sxs-lookup"><span data-stu-id="deca1-118">NuGet</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | [<span data-ttu-id="deca1-119">NuGet</span><span class="sxs-lookup"><span data-stu-id="deca1-119">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) | <span data-ttu-id="deca1-120">N/A</span><span class="sxs-lookup"><span data-stu-id="deca1-120">N/A</span></span> |
| <span data-ttu-id="deca1-121">Java</span><span class="sxs-lookup"><span data-stu-id="deca1-121">Java</span></span> | [<span data-ttu-id="deca1-122">Maven</span><span class="sxs-lookup"><span data-stu-id="deca1-122">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22) | [<span data-ttu-id="deca1-123">Maven</span><span class="sxs-lookup"><span data-stu-id="deca1-123">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22) | [<span data-ttu-id="deca1-124">GitHub</span><span class="sxs-lookup"><span data-stu-id="deca1-124">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-java) |
| <span data-ttu-id="deca1-125">Node</span><span class="sxs-lookup"><span data-stu-id="deca1-125">Node</span></span> | [<span data-ttu-id="deca1-126">NPM</span><span class="sxs-lookup"><span data-stu-id="deca1-126">NPM</span></span>](https://www.npmjs.com/package/azure-event-hubs) | <span data-ttu-id="deca1-127">N/A</span><span class="sxs-lookup"><span data-stu-id="deca1-127">N/A</span></span> | [<span data-ttu-id="deca1-128">GitHub</span><span class="sxs-lookup"><span data-stu-id="deca1-128">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-node) |
| <span data-ttu-id="deca1-129">C</span><span class="sxs-lookup"><span data-stu-id="deca1-129">C</span></span> | <span data-ttu-id="deca1-130">N/A</span><span class="sxs-lookup"><span data-stu-id="deca1-130">N/A</span></span> | <span data-ttu-id="deca1-131">N/A</span><span class="sxs-lookup"><span data-stu-id="deca1-131">N/A</span></span> | [<span data-ttu-id="deca1-132">GitHub</span><span class="sxs-lookup"><span data-stu-id="deca1-132">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-c) |

### <a name="additional-information"></a><span data-ttu-id="deca1-133">Additional information</span><span class="sxs-lookup"><span data-stu-id="deca1-133">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="deca1-134">.NET</span><span class="sxs-lookup"><span data-stu-id="deca1-134">.NET</span></span>
<span data-ttu-id="deca1-135">The .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="deca1-135">The .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="deca1-136">The .NET Standard library can be run using either .NET Core or the .NET Framework, while the .NET Framework library can only be run in a .NET Framework environment.</span><span class="sxs-lookup"><span data-stu-id="deca1-136">The .NET Standard library can be run using either .NET Core or the .NET Framework, while the .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="deca1-137">For more information on .NET Frameworks, see [framework versions.](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions)</span><span class="sxs-lookup"><span data-stu-id="deca1-137">For more information on .NET Frameworks, see [framework versions.](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions)</span></span>

#### <a name="node"></a><span data-ttu-id="deca1-138">Node</span><span class="sxs-lookup"><span data-stu-id="deca1-138">Node</span></span>

<span data-ttu-id="deca1-139">The Node.js library is currently in preview and is maintained as a side project by Microsoft employees and external contributors.</span><span class="sxs-lookup"><span data-stu-id="deca1-139">The Node.js library is currently in preview and is maintained as a side project by Microsoft employees and external contributors.</span></span> <span data-ttu-id="deca1-140">All contributions including source code are welcome and will be reviewed.</span><span class="sxs-lookup"><span data-stu-id="deca1-140">All contributions including source code are welcome and will be reviewed.</span></span>

## <a name="management-apis"></a><span data-ttu-id="deca1-141">Management APIs</span><span class="sxs-lookup"><span data-stu-id="deca1-141">Management APIs</span></span>

<span data-ttu-id="deca1-142">The following is a listing of all currently available management specific libraries.</span><span class="sxs-lookup"><span data-stu-id="deca1-142">The following is a listing of all currently available management specific libraries.</span></span> <span data-ttu-id="deca1-143">None of these libraries contain runtime operations, and are for the sole purpose of managing Event Hubs entities.</span><span class="sxs-lookup"><span data-stu-id="deca1-143">None of these libraries contain runtime operations, and are for the sole purpose of managing Event Hubs entities.</span></span>

| <span data-ttu-id="deca1-144">Language/Platform</span><span class="sxs-lookup"><span data-stu-id="deca1-144">Language/Platform</span></span> | <span data-ttu-id="deca1-145">Management package</span><span class="sxs-lookup"><span data-stu-id="deca1-145">Management package</span></span> | <span data-ttu-id="deca1-146">Repository</span><span class="sxs-lookup"><span data-stu-id="deca1-146">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="deca1-147">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="deca1-147">.NET Standard</span></span> | [<span data-ttu-id="deca1-148">NuGet</span><span class="sxs-lookup"><span data-stu-id="deca1-148">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) | [<span data-ttu-id="deca1-149">GitHub</span><span class="sxs-lookup"><span data-stu-id="deca1-149">GitHub</span></span>](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/ResourceManagement/EventHub) |

## <a name="next-steps"></a><span data-ttu-id="deca1-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="deca1-150">Next steps</span></span>
<span data-ttu-id="deca1-151">You can learn more about Event Hubs by visiting the following links:</span><span class="sxs-lookup"><span data-stu-id="deca1-151">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="deca1-152">Event Hubs overview</span><span class="sxs-lookup"><span data-stu-id="deca1-152">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="deca1-153">Create an event hub</span><span class="sxs-lookup"><span data-stu-id="deca1-153">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="deca1-154">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="deca1-154">Event Hubs FAQ</span></span>](event-hubs-faq.md)