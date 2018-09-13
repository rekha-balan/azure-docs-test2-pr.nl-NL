---
title: Azure CDN rules engine conditional expressions | Microsoft  Docs
description: Reference documentation for Azure CDN rules engine match conditions and features.
services: cdn
documentationcenter: ''
author: Lichard
manager: akucer
editor: ''
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: 57e56c38e003cb83dcf44f455c4451d159db8a59
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44774377"
---
# <a name="azure-cdn-rules-engine-conditional-expressions"></a><span data-ttu-id="28ab6-103">Azure CDN rules engine conditional expressions</span><span class="sxs-lookup"><span data-stu-id="28ab6-103">Azure CDN rules engine conditional expressions</span></span>
<span data-ttu-id="28ab6-104">This topic lists detailed descriptions of the Conditional Expressions for Azure Content Delivery Network (CDN) [Rules Engine](cdn-rules-engine.md).</span><span class="sxs-lookup"><span data-stu-id="28ab6-104">This topic lists detailed descriptions of the Conditional Expressions for Azure Content Delivery Network (CDN) [Rules Engine](cdn-rules-engine.md).</span></span>

<span data-ttu-id="28ab6-105">The first part of a rule is the Conditional Expression.</span><span class="sxs-lookup"><span data-stu-id="28ab6-105">The first part of a rule is the Conditional Expression.</span></span>

<span data-ttu-id="28ab6-106">Conditional Expression</span><span class="sxs-lookup"><span data-stu-id="28ab6-106">Conditional Expression</span></span> | <span data-ttu-id="28ab6-107">Description</span><span class="sxs-lookup"><span data-stu-id="28ab6-107">Description</span></span>
-----------------------|-------------
<span data-ttu-id="28ab6-108">IF</span><span class="sxs-lookup"><span data-stu-id="28ab6-108">IF</span></span> | <span data-ttu-id="28ab6-109">An IF expression is always a part of the first statement in a rule.</span><span class="sxs-lookup"><span data-stu-id="28ab6-109">An IF expression is always a part of the first statement in a rule.</span></span> <span data-ttu-id="28ab6-110">Like all other conditional expressions, this IF statement must be associated with a match.</span><span class="sxs-lookup"><span data-stu-id="28ab6-110">Like all other conditional expressions, this IF statement must be associated with a match.</span></span> <span data-ttu-id="28ab6-111">If no additional conditional expressions are defined, then this match determines the criterion that must be met before a set of features may be applied to a request.</span><span class="sxs-lookup"><span data-stu-id="28ab6-111">If no additional conditional expressions are defined, then this match determines the criterion that must be met before a set of features may be applied to a request.</span></span>
<span data-ttu-id="28ab6-112">AND IF</span><span class="sxs-lookup"><span data-stu-id="28ab6-112">AND IF</span></span> | <span data-ttu-id="28ab6-113">An AND IF expression may only be added after the following types of conditional expressions:IF,AND IF.</span><span class="sxs-lookup"><span data-stu-id="28ab6-113">An AND IF expression may only be added after the following types of conditional expressions:IF,AND IF.</span></span> <span data-ttu-id="28ab6-114">It indicates that there is another condition that must be met for the initial IF statement.</span><span class="sxs-lookup"><span data-stu-id="28ab6-114">It indicates that there is another condition that must be met for the initial IF statement.</span></span>
<span data-ttu-id="28ab6-115">ELSE IF</span><span class="sxs-lookup"><span data-stu-id="28ab6-115">ELSE IF</span></span>| <span data-ttu-id="28ab6-116">An ELSE IF expression specifies an alternative condition that must be met before a set of features specific to this ELSE IF statement takes place.</span><span class="sxs-lookup"><span data-stu-id="28ab6-116">An ELSE IF expression specifies an alternative condition that must be met before a set of features specific to this ELSE IF statement takes place.</span></span> <span data-ttu-id="28ab6-117">The presence of an ELSE IF statement indicates the end of the previous statement.</span><span class="sxs-lookup"><span data-stu-id="28ab6-117">The presence of an ELSE IF statement indicates the end of the previous statement.</span></span> <span data-ttu-id="28ab6-118">The only conditional expression that may be placed after an ELSE IF statement is another ELSE IF statement.</span><span class="sxs-lookup"><span data-stu-id="28ab6-118">The only conditional expression that may be placed after an ELSE IF statement is another ELSE IF statement.</span></span> <span data-ttu-id="28ab6-119">This means that an ELSE IF statement may only be used to specify a single additional condition that has to be met.</span><span class="sxs-lookup"><span data-stu-id="28ab6-119">This means that an ELSE IF statement may only be used to specify a single additional condition that has to be met.</span></span>

<span data-ttu-id="28ab6-120">**Example**: ![CDN match condition](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span><span class="sxs-lookup"><span data-stu-id="28ab6-120">**Example**: ![CDN match condition](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span></span>

 > [!TIP]
   > <span data-ttu-id="28ab6-121">A subsequent rule may override the actions specified by a previous rule.</span><span class="sxs-lookup"><span data-stu-id="28ab6-121">A subsequent rule may override the actions specified by a previous rule.</span></span> <span data-ttu-id="28ab6-122">Example: A catch-all rule secures all requests via Token-Based Authentication.</span><span class="sxs-lookup"><span data-stu-id="28ab6-122">Example: A catch-all rule secures all requests via Token-Based Authentication.</span></span> <span data-ttu-id="28ab6-123">Another rule may be created directly below it to make an exception for certain types of requests.</span><span class="sxs-lookup"><span data-stu-id="28ab6-123">Another rule may be created directly below it to make an exception for certain types of requests.</span></span>

### <a name="next-steps"></a><span data-ttu-id="28ab6-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="28ab6-124">Next steps</span></span>
* [<span data-ttu-id="28ab6-125">Azure CDN Overview</span><span class="sxs-lookup"><span data-stu-id="28ab6-125">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="28ab6-126">Rules Engine Reference</span><span class="sxs-lookup"><span data-stu-id="28ab6-126">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="28ab6-127">Rules Engine Match Conditions</span><span class="sxs-lookup"><span data-stu-id="28ab6-127">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="28ab6-128">Rules Engine Features</span><span class="sxs-lookup"><span data-stu-id="28ab6-128">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="28ab6-129">Overriding default HTTP behavior using the rules engine</span><span class="sxs-lookup"><span data-stu-id="28ab6-129">Overriding default HTTP behavior using the rules engine</span></span>](cdn-rules-engine.md)
