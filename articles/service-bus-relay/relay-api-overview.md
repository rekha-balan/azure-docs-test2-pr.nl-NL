---
title: Azure Relay API overview | Microsoft Docs
description: Overview of available Azure Relay APIs
services: event-hubs
documentationcenter: na
author: jtaubensee
manager: timlt
editor: ''
ms.assetid: fdaa1d2b-bd80-4e75-abb9-0c3d0773af2d
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: jotaub
ms.openlocfilehash: edc730aa383b07dc308da8a160203faf3636208b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554363"
---
# <a name="available-relay-apis"></a><span data-ttu-id="18b7f-103">Available Relay APIs</span><span class="sxs-lookup"><span data-stu-id="18b7f-103">Available Relay APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="18b7f-104">Runtime APIs</span><span class="sxs-lookup"><span data-stu-id="18b7f-104">Runtime APIs</span></span>

<span data-ttu-id="18b7f-105">The following is a listing of all currently available Relay runtime clients.</span><span class="sxs-lookup"><span data-stu-id="18b7f-105">The following is a listing of all currently available Relay runtime clients.</span></span>

<span data-ttu-id="18b7f-106">See [additional information](#additional-information) for more details on the status of each runtime library.</span><span class="sxs-lookup"><span data-stu-id="18b7f-106">See [additional information](#additional-information) for more details on the status of each runtime library.</span></span>

| <span data-ttu-id="18b7f-107">Language/Platform</span><span class="sxs-lookup"><span data-stu-id="18b7f-107">Language/Platform</span></span> | <span data-ttu-id="18b7f-108">Available feature</span><span class="sxs-lookup"><span data-stu-id="18b7f-108">Available feature</span></span> | <span data-ttu-id="18b7f-109">Client package</span><span class="sxs-lookup"><span data-stu-id="18b7f-109">Client package</span></span> | <span data-ttu-id="18b7f-110">Repository</span><span class="sxs-lookup"><span data-stu-id="18b7f-110">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="18b7f-111">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="18b7f-111">.NET Standard</span></span> | <span data-ttu-id="18b7f-112">Hybrid Connections</span><span class="sxs-lookup"><span data-stu-id="18b7f-112">Hybrid Connections</span></span> | [<span data-ttu-id="18b7f-113">Microsoft.Azure.Relay</span><span class="sxs-lookup"><span data-stu-id="18b7f-113">Microsoft.Azure.Relay</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Relay/) | [<span data-ttu-id="18b7f-114">GitHub</span><span class="sxs-lookup"><span data-stu-id="18b7f-114">GitHub</span></span>](https://github.com/azure/azure-relay-dotnet) |
| <span data-ttu-id="18b7f-115">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="18b7f-115">.NET Framework</span></span> | <span data-ttu-id="18b7f-116">WCF Relay</span><span class="sxs-lookup"><span data-stu-id="18b7f-116">WCF Relay</span></span> | [<span data-ttu-id="18b7f-117">WindowsAzure.ServiceBus</span><span class="sxs-lookup"><span data-stu-id="18b7f-117">WindowsAzure.ServiceBus</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | <span data-ttu-id="18b7f-118">N/A</span><span class="sxs-lookup"><span data-stu-id="18b7f-118">N/A</span></span> |
| <span data-ttu-id="18b7f-119">Node</span><span class="sxs-lookup"><span data-stu-id="18b7f-119">Node</span></span> | <span data-ttu-id="18b7f-120">Hybrid Connections</span><span class="sxs-lookup"><span data-stu-id="18b7f-120">Hybrid Connections</span></span> | [<span data-ttu-id="18b7f-121">hyco-ws</span><span class="sxs-lookup"><span data-stu-id="18b7f-121">hyco-ws</span></span>](https://www.npmjs.com/package/hyco-ws)<br/>[<span data-ttu-id="18b7f-122">hyco-websocket</span><span class="sxs-lookup"><span data-stu-id="18b7f-122">hyco-websocket</span></span>](https://www.npmjs.com/package/hyco-websocket) | [<span data-ttu-id="18b7f-123">GitHub</span><span class="sxs-lookup"><span data-stu-id="18b7f-123">GitHub</span></span>](https://github.com/Azure/azure-relay-node) |

### <a name="additional-information"></a><span data-ttu-id="18b7f-124">Additional information</span><span class="sxs-lookup"><span data-stu-id="18b7f-124">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="18b7f-125">.NET</span><span class="sxs-lookup"><span data-stu-id="18b7f-125">.NET</span></span>
<span data-ttu-id="18b7f-126">The .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="18b7f-126">The .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="18b7f-127">The .NET Standard library can be run using either .NET Core or the .NET Framework, while the .NET Framework library can only be run in a .NET Framework environment.</span><span class="sxs-lookup"><span data-stu-id="18b7f-127">The .NET Standard library can be run using either .NET Core or the .NET Framework, while the .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="18b7f-128">For more information on .NET Frameworks, see [framework versions](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span><span class="sxs-lookup"><span data-stu-id="18b7f-128">For more information on .NET Frameworks, see [framework versions](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="18b7f-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="18b7f-129">Next steps</span></span>
<span data-ttu-id="18b7f-130">To learn more about Azure Relay, visit these links:</span><span class="sxs-lookup"><span data-stu-id="18b7f-130">To learn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="18b7f-131">What is Azure Relay?</span><span class="sxs-lookup"><span data-stu-id="18b7f-131">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="18b7f-132">Relay FAQ</span><span class="sxs-lookup"><span data-stu-id="18b7f-132">Relay FAQ</span></span>](relay-faq.md)