---
title: Text Moderation API in Content Moderator | Microsoft Docs
description: The Text Moderation API moderates text for profanity, reports malware and phishing URLs, and matches against lists specific to a business.
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.technology: content-moderator
ms.topic: article
ms.date: 12/01/2016
ms.author: sajagtap
ms.openlocfilehash: 78aebc9ab20900a5d516b24240116ebd1acfbb3f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549429"
---
# <a name="text-moderation-api"></a><span data-ttu-id="543f8-103">Text Moderation API</span><span class="sxs-lookup"><span data-stu-id="543f8-103">Text Moderation API</span></span>

<span data-ttu-id="543f8-104">Use Content Moderator’s text moderation API [(see API reference)](api-reference.md "Content Moderator API Reference") to moderate text for profanity in more than 100 languages, and match against custom and shared lists that are specific to your business and users.</span><span class="sxs-lookup"><span data-stu-id="543f8-104">Use Content Moderator’s text moderation API [(see API reference)](api-reference.md "Content Moderator API Reference") to moderate text for profanity in more than 100 languages, and match against custom and shared lists that are specific to your business and users.</span></span>

## <a name="language-detection"></a><span data-ttu-id="543f8-105">Language detection</span><span class="sxs-lookup"><span data-stu-id="543f8-105">Language detection</span></span>

<span data-ttu-id="543f8-106">The first step to using the text moderation API is to have the algorithm detect the language of the content to be moderated.</span><span class="sxs-lookup"><span data-stu-id="543f8-106">The first step to using the text moderation API is to have the algorithm detect the language of the content to be moderated.</span></span> <span data-ttu-id="543f8-107">The API supports more than [100 languages](Text-Moderation-API-Languages.md).</span><span class="sxs-lookup"><span data-stu-id="543f8-107">The API supports more than [100 languages](Text-Moderation-API-Languages.md).</span></span> <span data-ttu-id="543f8-108">The **Detect Language** operation returns language codes for the predominant language comprising the submitted text in the following format: {"DetectedLanguage": "eng"}</span><span class="sxs-lookup"><span data-stu-id="543f8-108">The **Detect Language** operation returns language codes for the predominant language comprising the submitted text in the following format: {"DetectedLanguage": "eng"}</span></span>

## <a name="screening-for-profanity"></a><span data-ttu-id="543f8-109">Screening for profanity</span><span class="sxs-lookup"><span data-stu-id="543f8-109">Screening for profanity</span></span>

<span data-ttu-id="543f8-110">The text moderation API’s **Screen** operation does it all – screen the incoming text (maximum 1024 characters) for profanity and PII, while matching against custom lists of terms.</span><span class="sxs-lookup"><span data-stu-id="543f8-110">The text moderation API’s **Screen** operation does it all – screen the incoming text (maximum 1024 characters) for profanity and PII, while matching against custom lists of terms.</span></span>

<span data-ttu-id="543f8-111">The response may include:</span><span class="sxs-lookup"><span data-stu-id="543f8-111">The response may include:</span></span>

- <span data-ttu-id="543f8-112">Auto-corrected text</span><span class="sxs-lookup"><span data-stu-id="543f8-112">Auto-corrected text</span></span>
- <span data-ttu-id="543f8-113">Original text</span><span class="sxs-lookup"><span data-stu-id="543f8-113">Original text</span></span>
- <span data-ttu-id="543f8-114">Language</span><span class="sxs-lookup"><span data-stu-id="543f8-114">Language</span></span>
- <span data-ttu-id="543f8-115">PII</span><span class="sxs-lookup"><span data-stu-id="543f8-115">PII</span></span>
- <span data-ttu-id="543f8-116">Location of detected terms within the submitted text</span><span class="sxs-lookup"><span data-stu-id="543f8-116">Location of detected terms within the submitted text</span></span>
- <span data-ttu-id="543f8-117">Terms: detected profanity content</span><span class="sxs-lookup"><span data-stu-id="543f8-117">Terms: detected profanity content</span></span>

<span data-ttu-id="543f8-118">Let’s look at these fields in greater detail.</span><span class="sxs-lookup"><span data-stu-id="543f8-118">Let’s look at these fields in greater detail.</span></span>

## <a name="auto-correction"></a><span data-ttu-id="543f8-119">Auto-correction</span><span class="sxs-lookup"><span data-stu-id="543f8-119">Auto-correction</span></span>

<span data-ttu-id="543f8-120">Let’s assume that the input text is: (the ‘lzay’ is intentional.)</span><span class="sxs-lookup"><span data-stu-id="543f8-120">Let’s assume that the input text is: (the ‘lzay’ is intentional.)</span></span>

    The <a href="www.bunnies.com">qu!ck</a> brown  <a href="b.suspiciousdomain.com">f0x</a> jumps over the lzay dog www.benign.net.

<span data-ttu-id="543f8-121">If you ask for auto-correction, the response will contain the corrected version of the text as in:</span><span class="sxs-lookup"><span data-stu-id="543f8-121">If you ask for auto-correction, the response will contain the corrected version of the text as in:</span></span>

    “The quick brown fox jumps over the lazy dog."

## <a name="profanity-terms"></a><span data-ttu-id="543f8-122">Profanity terms</span><span class="sxs-lookup"><span data-stu-id="543f8-122">Profanity terms</span></span>

<span data-ttu-id="543f8-123">If any terms are detected, those terms are included in the response, along with their starting index (location) within the original text.</span><span class="sxs-lookup"><span data-stu-id="543f8-123">If any terms are detected, those terms are included in the response, along with their starting index (location) within the original text.</span></span>

## <a name="creating-and-managing-your-custom-lists-of-terms"></a><span data-ttu-id="543f8-124">Creating and managing your custom lists of terms</span><span class="sxs-lookup"><span data-stu-id="543f8-124">Creating and managing your custom lists of terms</span></span>

<span data-ttu-id="543f8-125">While the default, global list of terms works great for most cases, you may want to screen against terms that are specific to your business needs.</span><span class="sxs-lookup"><span data-stu-id="543f8-125">While the default, global list of terms works great for most cases, you may want to screen against terms that are specific to your business needs.</span></span> <span data-ttu-id="543f8-126">For example, you may want to filter out any competitive brand names from posts by users.</span><span class="sxs-lookup"><span data-stu-id="543f8-126">For example, you may want to filter out any competitive brand names from posts by users.</span></span> <span data-ttu-id="543f8-127">Your threshold of permitted text content may be different from the default list.</span><span class="sxs-lookup"><span data-stu-id="543f8-127">Your threshold of permitted text content may be different from the default list.</span></span>

<span data-ttu-id="543f8-128">The Content Moderator provides a complete [terms list API](https://westus.dev.cognitive.microsoft.com/docs/services/57cf755e3f9b070c105bd2c2/operations/57cf755e3f9b070868a1f675 "Content Moderator Terms List API") with operations for creating and deleting lists of terms, and for adding and removing text terms from those lists.</span><span class="sxs-lookup"><span data-stu-id="543f8-128">The Content Moderator provides a complete [terms list API](https://westus.dev.cognitive.microsoft.com/docs/services/57cf755e3f9b070c105bd2c2/operations/57cf755e3f9b070868a1f675 "Content Moderator Terms List API") with operations for creating and deleting lists of terms, and for adding and removing text terms from those lists.</span></span>

<span data-ttu-id="543f8-129">A typical sequence of operations would be to:</span><span class="sxs-lookup"><span data-stu-id="543f8-129">A typical sequence of operations would be to:</span></span>

1. <span data-ttu-id="543f8-130">Create a list.</span><span class="sxs-lookup"><span data-stu-id="543f8-130">Create a list.</span></span>
1. <span data-ttu-id="543f8-131">Add terms to your list.</span><span class="sxs-lookup"><span data-stu-id="543f8-131">Add terms to your list.</span></span>
1. <span data-ttu-id="543f8-132">Screen terms against the ones in the list.</span><span class="sxs-lookup"><span data-stu-id="543f8-132">Screen terms against the ones in the list.</span></span>
1. <span data-ttu-id="543f8-133">Delete term or terms from the list.</span><span class="sxs-lookup"><span data-stu-id="543f8-133">Delete term or terms from the list.</span></span>
1. <span data-ttu-id="543f8-134">Delete the list.</span><span class="sxs-lookup"><span data-stu-id="543f8-134">Delete the list.</span></span>
