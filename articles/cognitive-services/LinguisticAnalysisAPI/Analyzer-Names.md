---
title: Analyzer naming structure in the Linguistic Analysis API | Microsoft Docs
description: Learn how the Linguistic Analysis API uses its naming structure for analyzers to allow both flexibility and precision.
services: cognitive-services
author: RichardSunMS
manager: wkwok
ms.service: cognitive-services
ms.technology: linguistic-analysis-api
ms.topic: article
ms.date: 03/23/2016
ms.author: lesun
ms.openlocfilehash: c5bd0580e3b0362693a30a2b1b51c2ad6c8d23db
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552092"
---
# <a name="analyzer-names"></a><span data-ttu-id="ee64d-103">Analyzer Names</span><span class="sxs-lookup"><span data-stu-id="ee64d-103">Analyzer Names</span></span>

<span data-ttu-id="ee64d-104">We use a somewhat complicated naming structure for analyzers to allow both flexibility on analyzers and precision in understanding what a name means.</span><span class="sxs-lookup"><span data-stu-id="ee64d-104">We use a somewhat complicated naming structure for analyzers to allow both flexibility on analyzers and precision in understanding what a name means.</span></span>
<span data-ttu-id="ee64d-105">Analyzer names consist of four parts: an ID, a Kind, a Specification, and an Implementation.</span><span class="sxs-lookup"><span data-stu-id="ee64d-105">Analyzer names consist of four parts: an ID, a Kind, a Specification, and an Implementation.</span></span>
<span data-ttu-id="ee64d-106">The role of each component is defined below.</span><span class="sxs-lookup"><span data-stu-id="ee64d-106">The role of each component is defined below.</span></span>

## <a name="id"></a><span data-ttu-id="ee64d-107">ID</span><span class="sxs-lookup"><span data-stu-id="ee64d-107">ID</span></span>
<span data-ttu-id="ee64d-108">First, an analyzer has a unique ID; a GUID.</span><span class="sxs-lookup"><span data-stu-id="ee64d-108">First, an analyzer has a unique ID; a GUID.</span></span>
<span data-ttu-id="ee64d-109">These GUIDs should change relatively rarely, but are the only way to uniquely describe a particular analyzer.</span><span class="sxs-lookup"><span data-stu-id="ee64d-109">These GUIDs should change relatively rarely, but are the only way to uniquely describe a particular analyzer.</span></span>

## <a name="kind"></a><span data-ttu-id="ee64d-110">Kind</span><span class="sxs-lookup"><span data-stu-id="ee64d-110">Kind</span></span>
<span data-ttu-id="ee64d-111">Next, each analyzer is a **kind**.</span><span class="sxs-lookup"><span data-stu-id="ee64d-111">Next, each analyzer is a **kind**.</span></span>
<span data-ttu-id="ee64d-112">This defines in very broad terms the type of analysis returned, and should uniquely define the data structure used to represent that analysis.</span><span class="sxs-lookup"><span data-stu-id="ee64d-112">This defines in very broad terms the type of analysis returned, and should uniquely define the data structure used to represent that analysis.</span></span>
<span data-ttu-id="ee64d-113">Currently, there are three distinct kinds:</span><span class="sxs-lookup"><span data-stu-id="ee64d-113">Currently, there are three distinct kinds:</span></span>
 - [<span data-ttu-id="ee64d-114">Tokens</span><span class="sxs-lookup"><span data-stu-id="ee64d-114">Tokens</span></span>](Sentences-and-Tokens.md)
 - [<span data-ttu-id="ee64d-115">POS Tags</span><span class="sxs-lookup"><span data-stu-id="ee64d-115">POS Tags</span></span>](Pos-Tagging.md)
 - [<span data-ttu-id="ee64d-116">Constituency Tree</span><span class="sxs-lookup"><span data-stu-id="ee64d-116">Constituency Tree</span></span>](constituency-parsing.md)

## <a name="specification"></a><span data-ttu-id="ee64d-117">Specification</span><span class="sxs-lookup"><span data-stu-id="ee64d-117">Specification</span></span>
<span data-ttu-id="ee64d-118">Within a given kind, however, different experts might disagree on how a particular phenomenon should be analyzed.</span><span class="sxs-lookup"><span data-stu-id="ee64d-118">Within a given kind, however, different experts might disagree on how a particular phenomenon should be analyzed.</span></span>
<span data-ttu-id="ee64d-119">Unlike programming languages, there's no clear and exact definition of how this should be done.</span><span class="sxs-lookup"><span data-stu-id="ee64d-119">Unlike programming languages, there's no clear and exact definition of how this should be done.</span></span>

<span data-ttu-id="ee64d-120">For instance, imagine we were trying to find the tokens in the English sentence "He didn't go."</span><span class="sxs-lookup"><span data-stu-id="ee64d-120">For instance, imagine we were trying to find the tokens in the English sentence "He didn't go."</span></span>
<span data-ttu-id="ee64d-121">In particular, consider the string "didn't".</span><span class="sxs-lookup"><span data-stu-id="ee64d-121">In particular, consider the string "didn't".</span></span>
<span data-ttu-id="ee64d-122">One possible interpretation is that this should be split into two tokens: "did" and "not".</span><span class="sxs-lookup"><span data-stu-id="ee64d-122">One possible interpretation is that this should be split into two tokens: "did" and "not".</span></span>
<span data-ttu-id="ee64d-123">Then the alternative sentence "He did not go" would have the same set of tokens.</span><span class="sxs-lookup"><span data-stu-id="ee64d-123">Then the alternative sentence "He did not go" would have the same set of tokens.</span></span>
<span data-ttu-id="ee64d-124">Another possibility is to say that it should be split into the tokens "did" and "n't".</span><span class="sxs-lookup"><span data-stu-id="ee64d-124">Another possibility is to say that it should be split into the tokens "did" and "n't".</span></span>
<span data-ttu-id="ee64d-125">The latter token would not normally be considered a word, but this approach retains more information about the surface string, which can sometimes be useful.</span><span class="sxs-lookup"><span data-stu-id="ee64d-125">The latter token would not normally be considered a word, but this approach retains more information about the surface string, which can sometimes be useful.</span></span>
<span data-ttu-id="ee64d-126">Or perhaps that contraction should be considered a single word.</span><span class="sxs-lookup"><span data-stu-id="ee64d-126">Or perhaps that contraction should be considered a single word.</span></span>

<span data-ttu-id="ee64d-127">Regardless which choice is made, that choice should be made consistently.</span><span class="sxs-lookup"><span data-stu-id="ee64d-127">Regardless which choice is made, that choice should be made consistently.</span></span>
<span data-ttu-id="ee64d-128">This is precisely the role of a **specification**: to decide what a correct representation should be.</span><span class="sxs-lookup"><span data-stu-id="ee64d-128">This is precisely the role of a **specification**: to decide what a correct representation should be.</span></span>

<span data-ttu-id="ee64d-129">Analyzer outputs can only be fairly compared to data that conforms to the same specification.</span><span class="sxs-lookup"><span data-stu-id="ee64d-129">Analyzer outputs can only be fairly compared to data that conforms to the same specification.</span></span>

## <a name="implementation"></a><span data-ttu-id="ee64d-130">Implementation</span><span class="sxs-lookup"><span data-stu-id="ee64d-130">Implementation</span></span>

<span data-ttu-id="ee64d-131">Often there are multiple models that attempt to achieve the same results, but with different performance characteristics.</span><span class="sxs-lookup"><span data-stu-id="ee64d-131">Often there are multiple models that attempt to achieve the same results, but with different performance characteristics.</span></span>
<span data-ttu-id="ee64d-132">One model might be faster though less accurate; another might make a different trade-off.</span><span class="sxs-lookup"><span data-stu-id="ee64d-132">One model might be faster though less accurate; another might make a different trade-off.</span></span>

<span data-ttu-id="ee64d-133">The **implementation** portion of an analyzer name is used to identify this type of information, so that users can pick the most appropriate analyzer for their needs.</span><span class="sxs-lookup"><span data-stu-id="ee64d-133">The **implementation** portion of an analyzer name is used to identify this type of information, so that users can pick the most appropriate analyzer for their needs.</span></span>
