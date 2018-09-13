---
title: Azure Event Hubs best practices for managing performance and scale | Microsoft Docs
description: Azure Event Hubs performance and scale best practices
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: ''
ms.assetid: ''
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/09/2017
ms.author: sethm
ms.openlocfilehash: 920378e21985ae6bb63914e6c065314aaf979214
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553615"
---
# <a name="-event-hubs-best-practices-for-managing-performance-and-scale"></a><span data-ttu-id="ae537-103">🔧 Event Hubs best practices for managing performance and scale</span><span class="sxs-lookup"><span data-stu-id="ae537-103">🔧 Event Hubs best practices for managing performance and scale</span></span>

> [!NOTE]
> 
> <span data-ttu-id="ae537-104">This topic hasn’t been written yet!</span><span class="sxs-lookup"><span data-stu-id="ae537-104">This topic hasn’t been written yet!</span></span> 
>
> <span data-ttu-id="ae537-105">We welcome your input to help shape the scope and approach of this content.</span><span class="sxs-lookup"><span data-stu-id="ae537-105">We welcome your input to help shape the scope and approach of this content.</span></span> <span data-ttu-id="ae537-106">You can track the status and provide input on this [issue in GitHub](https://github.com/Azure/azure-event-hubs/issues/306).</span><span class="sxs-lookup"><span data-stu-id="ae537-106">You can track the status and provide input on this [issue in GitHub](https://github.com/Azure/azure-event-hubs/issues/306).</span></span>
> 
> <span data-ttu-id="ae537-107">Learn more about how you can contribute on [GitHub](https://github.com/Microsoft/azure-docs/blob/master/contributor-guide/contributor-guide-index.md).</span><span class="sxs-lookup"><span data-stu-id="ae537-107">Learn more about how you can contribute on [GitHub](https://github.com/Microsoft/azure-docs/blob/master/contributor-guide/contributor-guide-index.md).</span></span>

<span data-ttu-id="ae537-108">This article will cover:</span><span class="sxs-lookup"><span data-stu-id="ae537-108">This article will cover:</span></span>

- <span data-ttu-id="ae537-109">Partitioning</span><span class="sxs-lookup"><span data-stu-id="ae537-109">Partitioning</span></span>
- <span data-ttu-id="ae537-110">Throughput units</span><span class="sxs-lookup"><span data-stu-id="ae537-110">Throughput units</span></span>
- <span data-ttu-id="ae537-111">Parallelism</span><span class="sxs-lookup"><span data-stu-id="ae537-111">Parallelism</span></span>
- <span data-ttu-id="ae537-112">Common bottlenecks</span><span class="sxs-lookup"><span data-stu-id="ae537-112">Common bottlenecks</span></span>

