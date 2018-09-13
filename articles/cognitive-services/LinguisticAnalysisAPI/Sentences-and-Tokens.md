---
title: Sentences and tokens in the Linguistic Analysis API | Microsoft Docs
description: Learn about sentence separation and tokenization in the Linguistic Analysis API in Cognitive Services.
services: cognitive-services
author: DavidLiCIG
manager: wkwok
ms.service: cognitive-services
ms.technology: linguisticanalysisapi
ms.topic: article
ms.date: 03/21/2016
ms.author: davl
ms.openlocfilehash: d302fe7b2f6bd25d5a3348118ac197264784e00a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563178"
---
# <a name="sentence-separation-and-tokenization"></a><span data-ttu-id="0e0a2-103">Sentence Separation and Tokenization</span><span class="sxs-lookup"><span data-stu-id="0e0a2-103">Sentence Separation and Tokenization</span></span>

## <a name="background-and-motivation"></a><span data-ttu-id="0e0a2-104">Background and motivation</span><span class="sxs-lookup"><span data-stu-id="0e0a2-104">Background and motivation</span></span>

<span data-ttu-id="0e0a2-105">Given a body of text, the first step of linguistic analysis is to break it into sentences and tokens.</span><span class="sxs-lookup"><span data-stu-id="0e0a2-105">Given a body of text, the first step of linguistic analysis is to break it into sentences and tokens.</span></span>

### <a name="sentence-separation"></a><span data-ttu-id="0e0a2-106">Sentence Separation</span><span class="sxs-lookup"><span data-stu-id="0e0a2-106">Sentence Separation</span></span>

<span data-ttu-id="0e0a2-107">On first glance, it seems that breaking text into sentences is simple: just find the end-of-sentence markers and break sentences there.</span><span class="sxs-lookup"><span data-stu-id="0e0a2-107">On first glance, it seems that breaking text into sentences is simple: just find the end-of-sentence markers and break sentences there.</span></span>
<span data-ttu-id="0e0a2-108">However, these marks are often complicated and ambiguous.</span><span class="sxs-lookup"><span data-stu-id="0e0a2-108">However, these marks are often complicated and ambiguous.</span></span>

<span data-ttu-id="0e0a2-109">Consider the following example text:</span><span class="sxs-lookup"><span data-stu-id="0e0a2-109">Consider the following example text:</span></span>

> <span data-ttu-id="0e0a2-110">What did you say?!?</span><span class="sxs-lookup"><span data-stu-id="0e0a2-110">What did you say?!?</span></span> <span data-ttu-id="0e0a2-111">I didn't hear about the director's "new proposal."</span><span class="sxs-lookup"><span data-stu-id="0e0a2-111">I didn't hear about the director's "new proposal."</span></span> <span data-ttu-id="0e0a2-112">It's important to Mr. and Mrs. Smith.</span><span class="sxs-lookup"><span data-stu-id="0e0a2-112">It's important to Mr. and Mrs. Smith.</span></span>

<span data-ttu-id="0e0a2-113">This text contains three sentences:</span><span class="sxs-lookup"><span data-stu-id="0e0a2-113">This text contains three sentences:</span></span>

- <span data-ttu-id="0e0a2-114">What did you say?!?</span><span class="sxs-lookup"><span data-stu-id="0e0a2-114">What did you say?!?</span></span>
- <span data-ttu-id="0e0a2-115">I didn't hear about the director's "new proposal."</span><span class="sxs-lookup"><span data-stu-id="0e0a2-115">I didn't hear about the director's "new proposal."</span></span>
- <span data-ttu-id="0e0a2-116">It's important to Mr. and Mrs. Smith.</span><span class="sxs-lookup"><span data-stu-id="0e0a2-116">It's important to Mr. and Mrs. Smith.</span></span>

<span data-ttu-id="0e0a2-117">Note how the ends of sentences are marked in very different ways.</span><span class="sxs-lookup"><span data-stu-id="0e0a2-117">Note how the ends of sentences are marked in very different ways.</span></span>
<span data-ttu-id="0e0a2-118">The first ends in an combination of question marks and exclamation points (sometimes called an interrobang).</span><span class="sxs-lookup"><span data-stu-id="0e0a2-118">The first ends in an combination of question marks and exclamation points (sometimes called an interrobang).</span></span>
<span data-ttu-id="0e0a2-119">The second ends with a period or full stop, but the following quotation mark should be pulled into the prior sentence.</span><span class="sxs-lookup"><span data-stu-id="0e0a2-119">The second ends with a period or full stop, but the following quotation mark should be pulled into the prior sentence.</span></span>
<span data-ttu-id="0e0a2-120">In the third sentence, you can see how that same period character can be used to mark abbreviations as well.</span><span class="sxs-lookup"><span data-stu-id="0e0a2-120">In the third sentence, you can see how that same period character can be used to mark abbreviations as well.</span></span>
<span data-ttu-id="0e0a2-121">Looking just at punctuation provides a good candidate set, but further work is required to identify the true sentence boundaries.</span><span class="sxs-lookup"><span data-stu-id="0e0a2-121">Looking just at punctuation provides a good candidate set, but further work is required to identify the true sentence boundaries.</span></span>

### <a name="tokenization"></a><span data-ttu-id="0e0a2-122">Tokenization</span><span class="sxs-lookup"><span data-stu-id="0e0a2-122">Tokenization</span></span>

<span data-ttu-id="0e0a2-123">The next task is to break these sentences into tokens.</span><span class="sxs-lookup"><span data-stu-id="0e0a2-123">The next task is to break these sentences into tokens.</span></span>
<span data-ttu-id="0e0a2-124">For the most part, English tokens are delimited by white space.</span><span class="sxs-lookup"><span data-stu-id="0e0a2-124">For the most part, English tokens are delimited by white space.</span></span>
<span data-ttu-id="0e0a2-125">(Finding tokens or words is much easier in English than in Chinese, where spaces are mostly not used between words.</span><span class="sxs-lookup"><span data-stu-id="0e0a2-125">(Finding tokens or words is much easier in English than in Chinese, where spaces are mostly not used between words.</span></span>
<span data-ttu-id="0e0a2-126">The first sentence might be written as "Whatdidyousay?")</span><span class="sxs-lookup"><span data-stu-id="0e0a2-126">The first sentence might be written as "Whatdidyousay?")</span></span>

<span data-ttu-id="0e0a2-127">There are a few difficult cases.</span><span class="sxs-lookup"><span data-stu-id="0e0a2-127">There are a few difficult cases.</span></span>
<span data-ttu-id="0e0a2-128">First, punctuation often (but not always) should be split away from it surrounding context.</span><span class="sxs-lookup"><span data-stu-id="0e0a2-128">First, punctuation often (but not always) should be split away from it surrounding context.</span></span>
<span data-ttu-id="0e0a2-129">Second, English has *contractions*, like "didn't" or "it's", where words have been compressed and abbreviated into smaller pieces.</span><span class="sxs-lookup"><span data-stu-id="0e0a2-129">Second, English has *contractions*, like "didn't" or "it's", where words have been compressed and abbreviated into smaller pieces.</span></span> <span data-ttu-id="0e0a2-130">The goal of the tokenizer is to break the character sequence into words.</span><span class="sxs-lookup"><span data-stu-id="0e0a2-130">The goal of the tokenizer is to break the character sequence into words.</span></span>

<span data-ttu-id="0e0a2-131">Let's return to the example sentences from above.</span><span class="sxs-lookup"><span data-stu-id="0e0a2-131">Let's return to the example sentences from above.</span></span>
<span data-ttu-id="0e0a2-132">Now we've placed a "center dot" (&middot;) between each distinct token.</span><span class="sxs-lookup"><span data-stu-id="0e0a2-132">Now we've placed a "center dot" (&middot;) between each distinct token.</span></span>

- <span data-ttu-id="0e0a2-133">What &middot; did &middot; you &middot; say &middot; ?!?</span><span class="sxs-lookup"><span data-stu-id="0e0a2-133">What &middot; did &middot; you &middot; say &middot; ?!?</span></span>
- <span data-ttu-id="0e0a2-134">I &middot; did &middot; n't &middot; hear &middot; about &middot; the &middot; director &middot; 's &middot; " &middot; new &middot; proposal &middot; .</span><span class="sxs-lookup"><span data-stu-id="0e0a2-134">I &middot; did &middot; n't &middot; hear &middot; about &middot; the &middot; director &middot; 's &middot; " &middot; new &middot; proposal &middot; .</span></span> <span data-ttu-id="0e0a2-135">&middot; "</span><span class="sxs-lookup"><span data-stu-id="0e0a2-135">&middot; "</span></span>
- <span data-ttu-id="0e0a2-136">It &middot; 's &middot; important &middot; to &middot; Mr. &middot; and &middot; Mrs. &middot; Smith &middot; .</span><span class="sxs-lookup"><span data-stu-id="0e0a2-136">It &middot; 's &middot; important &middot; to &middot; Mr. &middot; and &middot; Mrs. &middot; Smith &middot; .</span></span>

<span data-ttu-id="0e0a2-137">Note how most tokens are words you'd find in the dictionary (e.g., *important*, *director*).</span><span class="sxs-lookup"><span data-stu-id="0e0a2-137">Note how most tokens are words you'd find in the dictionary (e.g., *important*, *director*).</span></span>
<span data-ttu-id="0e0a2-138">Others solely consist of punctuation.</span><span class="sxs-lookup"><span data-stu-id="0e0a2-138">Others solely consist of punctuation.</span></span>
<span data-ttu-id="0e0a2-139">Finally, there are more unusual tokens to represent contractions like *n't* for *not*, possessives like *'s*, etc. This tokenization allows us to handle the word *didn't* and the phrase *did not* in a more consistent way, for instance.</span><span class="sxs-lookup"><span data-stu-id="0e0a2-139">Finally, there are more unusual tokens to represent contractions like *n't* for *not*, possessives like *'s*, etc. This tokenization allows us to handle the word *didn't* and the phrase *did not* in a more consistent way, for instance.</span></span>

## <a name="specification"></a><span data-ttu-id="0e0a2-140">Specification</span><span class="sxs-lookup"><span data-stu-id="0e0a2-140">Specification</span></span>

<span data-ttu-id="0e0a2-141">It is important to make consistent decisions about what comprises a sentence and a token.</span><span class="sxs-lookup"><span data-stu-id="0e0a2-141">It is important to make consistent decisions about what comprises a sentence and a token.</span></span>
<span data-ttu-id="0e0a2-142">We rely on the specification from the [Penn Treebank](https://www.cis.upenn.edu/~treebank/) (some additional details are available  here: [https://www.cis.upenn.edu/~treebank/tokenization.html]).</span><span class="sxs-lookup"><span data-stu-id="0e0a2-142">We rely on the specification from the [Penn Treebank](https://www.cis.upenn.edu/~treebank/) (some additional details are available  here: [https://www.cis.upenn.edu/~treebank/tokenization.html]).</span></span>
