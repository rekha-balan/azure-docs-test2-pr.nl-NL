---
title: Azure Event Hubs best practices for handling errors | Microsoft Docs
description: Azure Event Hubs handling errors and retry
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
ms.openlocfilehash: 200bc0828574bca72739dea5badb22da129cd896
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555820"
---
# <a name="-event-hubs-best-practices-for-handling-errors-and-retry"></a><span data-ttu-id="125cb-103">🔧 Event Hubs best practices for handling errors and retry</span><span class="sxs-lookup"><span data-stu-id="125cb-103">🔧 Event Hubs best practices for handling errors and retry</span></span>

> [!NOTE]
> 
> <span data-ttu-id="125cb-104">This topic hasn’t been written yet!</span><span class="sxs-lookup"><span data-stu-id="125cb-104">This topic hasn’t been written yet!</span></span> 
>
> <span data-ttu-id="125cb-105">We welcome your input to help shape the scope and approach of this content.</span><span class="sxs-lookup"><span data-stu-id="125cb-105">We welcome your input to help shape the scope and approach of this content.</span></span> <span data-ttu-id="125cb-106">You can track the status and provide input on this [issue in GitHub](https://github.com/Azure/azure-event-hubs/issues/305).</span><span class="sxs-lookup"><span data-stu-id="125cb-106">You can track the status and provide input on this [issue in GitHub](https://github.com/Azure/azure-event-hubs/issues/305).</span></span>
> 
> <span data-ttu-id="125cb-107">Learn more about how you can contribute on [GitHub](https://github.com/Microsoft/azure-docs/blob/master/contributor-guide/contributor-guide-index.md).</span><span class="sxs-lookup"><span data-stu-id="125cb-107">Learn more about how you can contribute on [GitHub](https://github.com/Microsoft/azure-docs/blob/master/contributor-guide/contributor-guide-index.md).</span></span>

<span data-ttu-id="125cb-108">This article will cover:</span><span class="sxs-lookup"><span data-stu-id="125cb-108">This article will cover:</span></span>

- <span data-ttu-id="125cb-109">What different kinds of errors are there?</span><span class="sxs-lookup"><span data-stu-id="125cb-109">What different kinds of errors are there?</span></span>
- <span data-ttu-id="125cb-110">What happens when I get an error?</span><span class="sxs-lookup"><span data-stu-id="125cb-110">What happens when I get an error?</span></span>
- <span data-ttu-id="125cb-111">What kinds of errors should be retried?</span><span class="sxs-lookup"><span data-stu-id="125cb-111">What kinds of errors should be retried?</span></span> <span data-ttu-id="125cb-112">Which shouldn't?</span><span class="sxs-lookup"><span data-stu-id="125cb-112">Which shouldn't?</span></span>
- <span data-ttu-id="125cb-113">Custom retry policy</span><span class="sxs-lookup"><span data-stu-id="125cb-113">Custom retry policy</span></span>
