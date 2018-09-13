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
# <a name="sentence-separation-and-tokenization"></a>Sentence Separation and Tokenization

## <a name="background-and-motivation"></a>Background and motivation

Given a body of text, the first step of linguistic analysis is to break it into sentences and tokens.

### <a name="sentence-separation"></a>Sentence Separation

On first glance, it seems that breaking text into sentences is simple: just find the end-of-sentence markers and break sentences there.
However, these marks are often complicated and ambiguous.

Consider the following example text:

> What did you say?!? I didn't hear about the director's "new proposal." It's important to Mr. and Mrs. Smith.

This text contains three sentences:

- What did you say?!?
- I didn't hear about the director's "new proposal."
- It's important to Mr. and Mrs. Smith.

Note how the ends of sentences are marked in very different ways.
The first ends in an combination of question marks and exclamation points (sometimes called an interrobang).
The second ends with a period or full stop, but the following quotation mark should be pulled into the prior sentence.
In the third sentence, you can see how that same period character can be used to mark abbreviations as well.
Looking just at punctuation provides a good candidate set, but further work is required to identify the true sentence boundaries.

### <a name="tokenization"></a>Tokenization

The next task is to break these sentences into tokens.
For the most part, English tokens are delimited by white space.
(Finding tokens or words is much easier in English than in Chinese, where spaces are mostly not used between words.
The first sentence might be written as "Whatdidyousay?")

There are a few difficult cases.
First, punctuation often (but not always) should be split away from it surrounding context.
Second, English has *contractions*, like "didn't" or "it's", where words have been compressed and abbreviated into smaller pieces. The goal of the tokenizer is to break the character sequence into words.

Let's return to the example sentences from above.
Now we've placed a "center dot" (&middot;) between each distinct token.

- What &middot; did &middot; you &middot; say &middot; ?!?
- I &middot; did &middot; n't &middot; hear &middot; about &middot; the &middot; director &middot; 's &middot; " &middot; new &middot; proposal &middot; . &middot; "
- It &middot; 's &middot; important &middot; to &middot; Mr. &middot; and &middot; Mrs. &middot; Smith &middot; .

Note how most tokens are words you'd find in the dictionary (e.g., *important*, *director*).
Others solely consist of punctuation.
Finally, there are more unusual tokens to represent contractions like *n't* for *not*, possessives like *'s*, etc. This tokenization allows us to handle the word *didn't* and the phrase *did not* in a more consistent way, for instance.

## <a name="specification"></a>Specification

It is important to make consistent decisions about what comprises a sentence and a token.
We rely on the specification from the [Penn Treebank](https://www.cis.upenn.edu/~treebank/) (some additional details are available  here: [https://www.cis.upenn.edu/~treebank/tokenization.html]).
