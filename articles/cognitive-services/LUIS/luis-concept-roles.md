---
title: Understanding how roles are used in pattern-based entities - Azure| Microsoft Docs
description: Learn how a role is used in an pattern-based entity to give a name to a contextual entity subtype.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.technology: luis
ms.topic: article
ms.date: 06/08/2018
ms.author: diberry
ms.openlocfilehash: d2692cdce9da7428bd7b30c4feaf7347792618f5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857645"
---
# <a name="entity-roles-in-patterns-are-contextual-subtypes"></a><span data-ttu-id="c3bf6-103">Entity roles in Patterns are contextual subtypes</span><span class="sxs-lookup"><span data-stu-id="c3bf6-103">Entity roles in Patterns are contextual subtypes</span></span>
<span data-ttu-id="c3bf6-104">Roles are named, contextual subtypes of an entity used only in [patterns](luis-concept-patterns.md).</span><span class="sxs-lookup"><span data-stu-id="c3bf6-104">Roles are named, contextual subtypes of an entity used only in [patterns](luis-concept-patterns.md).</span></span>

<span data-ttu-id="c3bf6-105">For example, in the utterance `buy a ticket from New York to London`, both New York and London are cities but each has a different meaning in the sentence.</span><span class="sxs-lookup"><span data-stu-id="c3bf6-105">For example, in the utterance `buy a ticket from New York to London`, both New York and London are cities but each has a different meaning in the sentence.</span></span> <span data-ttu-id="c3bf6-106">New York is the origin city and London is the destination city.</span><span class="sxs-lookup"><span data-stu-id="c3bf6-106">New York is the origin city and London is the destination city.</span></span> 

<span data-ttu-id="c3bf6-107">Roles give a name to those differences:</span><span class="sxs-lookup"><span data-stu-id="c3bf6-107">Roles give a name to those differences:</span></span>

|<span data-ttu-id="c3bf6-108">Entity</span><span class="sxs-lookup"><span data-stu-id="c3bf6-108">Entity</span></span>|<span data-ttu-id="c3bf6-109">Role</span><span class="sxs-lookup"><span data-stu-id="c3bf6-109">Role</span></span>|<span data-ttu-id="c3bf6-110">Purpose</span><span class="sxs-lookup"><span data-stu-id="c3bf6-110">Purpose</span></span>|
|--|--|--|
|<span data-ttu-id="c3bf6-111">Location</span><span class="sxs-lookup"><span data-stu-id="c3bf6-111">Location</span></span>|<span data-ttu-id="c3bf6-112">origin</span><span class="sxs-lookup"><span data-stu-id="c3bf6-112">origin</span></span>|<span data-ttu-id="c3bf6-113">where the plane leaves from</span><span class="sxs-lookup"><span data-stu-id="c3bf6-113">where the plane leaves from</span></span>|
|<span data-ttu-id="c3bf6-114">Location</span><span class="sxs-lookup"><span data-stu-id="c3bf6-114">Location</span></span>|<span data-ttu-id="c3bf6-115">destination</span><span class="sxs-lookup"><span data-stu-id="c3bf6-115">destination</span></span>|<span data-ttu-id="c3bf6-116">where the plane lands</span><span class="sxs-lookup"><span data-stu-id="c3bf6-116">where the plane lands</span></span>|

## <a name="how-are-roles-used-in-patterns"></a><span data-ttu-id="c3bf6-117">How are roles used in patterns?</span><span class="sxs-lookup"><span data-stu-id="c3bf6-117">How are roles used in patterns?</span></span>
<span data-ttu-id="c3bf6-118">In a pattern's template utterance, roles are used within the utterance:</span><span class="sxs-lookup"><span data-stu-id="c3bf6-118">In a pattern's template utterance, roles are used within the utterance:</span></span> 

```
buy a ticket from {Location:origin} to {Location:destination}
```

## <a name="role-syntax-in-patterns"></a><span data-ttu-id="c3bf6-119">Role syntax in patterns</span><span class="sxs-lookup"><span data-stu-id="c3bf6-119">Role syntax in patterns</span></span>
<span data-ttu-id="c3bf6-120">The entity and role are surrounded in parentheses, `{}`.</span><span class="sxs-lookup"><span data-stu-id="c3bf6-120">The entity and role are surrounded in parentheses, `{}`.</span></span> <span data-ttu-id="c3bf6-121">The entity and the role are separated by a colon.</span><span class="sxs-lookup"><span data-stu-id="c3bf6-121">The entity and the role are separated by a colon.</span></span> 

## <a name="roles-versus-hierarchical-entities"></a><span data-ttu-id="c3bf6-122">Roles versus Hierarchical entities</span><span class="sxs-lookup"><span data-stu-id="c3bf6-122">Roles versus Hierarchical entities</span></span>
<span data-ttu-id="c3bf6-123">Hierarchical entities provide the same contextual information as roles but only to utterances in **intents**.</span><span class="sxs-lookup"><span data-stu-id="c3bf6-123">Hierarchical entities provide the same contextual information as roles but only to utterances in **intents**.</span></span> <span data-ttu-id="c3bf6-124">Similarly, roles provide the same contextual information as hierarchical entities but only in **patterns**.</span><span class="sxs-lookup"><span data-stu-id="c3bf6-124">Similarly, roles provide the same contextual information as hierarchical entities but only in **patterns**.</span></span>

|<span data-ttu-id="c3bf6-125">Contextual learning</span><span class="sxs-lookup"><span data-stu-id="c3bf6-125">Contextual learning</span></span>|<span data-ttu-id="c3bf6-126">Used in</span><span class="sxs-lookup"><span data-stu-id="c3bf6-126">Used in</span></span>|
|--|--|
|<span data-ttu-id="c3bf6-127">hierarchical entities</span><span class="sxs-lookup"><span data-stu-id="c3bf6-127">hierarchical entities</span></span>|<span data-ttu-id="c3bf6-128">intents</span><span class="sxs-lookup"><span data-stu-id="c3bf6-128">intents</span></span>|
|<span data-ttu-id="c3bf6-129">roles</span><span class="sxs-lookup"><span data-stu-id="c3bf6-129">roles</span></span>|<span data-ttu-id="c3bf6-130">patterns</span><span class="sxs-lookup"><span data-stu-id="c3bf6-130">patterns</span></span>|

## <a name="next-steps"></a><span data-ttu-id="c3bf6-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="c3bf6-131">Next steps</span></span>

* <span data-ttu-id="c3bf6-132">Learn how to add [roles](luis-how-to-add-entities.md#add-role-to-pattern-based-entity)</span><span class="sxs-lookup"><span data-stu-id="c3bf6-132">Learn how to add [roles](luis-how-to-add-entities.md#add-role-to-pattern-based-entity)</span></span>
