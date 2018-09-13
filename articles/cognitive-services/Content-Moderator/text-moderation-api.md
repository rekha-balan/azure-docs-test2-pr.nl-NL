---
title: Azure Content Moderator - Text Moderation | Microsoft Docs
description: Use text moderation for possible unwanted text, PII, and custom lists of terms.
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.component: content-moderator
ms.topic: article
ms.date: 01/30/2018
ms.author: sajagtap
ms.openlocfilehash: b2edaa145650ea3c9fe3c0e9fd5e496ec7d30b99
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44790574"
---
# <a name="text-moderation"></a><span data-ttu-id="98f85-103">Text moderation</span><span class="sxs-lookup"><span data-stu-id="98f85-103">Text moderation</span></span>

<span data-ttu-id="98f85-104">Use Content Moderator’s machine-assisted text moderation and [human review](Review-Tool-User-Guide/human-in-the-loop.md) capabilities to moderate text content.</span><span class="sxs-lookup"><span data-stu-id="98f85-104">Use Content Moderator’s machine-assisted text moderation and [human review](Review-Tool-User-Guide/human-in-the-loop.md) capabilities to moderate text content.</span></span>

<span data-ttu-id="98f85-105">You either block, approve or review the content based on your policies and thresholds.</span><span class="sxs-lookup"><span data-stu-id="98f85-105">You either block, approve or review the content based on your policies and thresholds.</span></span> <span data-ttu-id="98f85-106">Use it to augment human moderation of environments where partners, employees and consumers generate text content.</span><span class="sxs-lookup"><span data-stu-id="98f85-106">Use it to augment human moderation of environments where partners, employees and consumers generate text content.</span></span> <span data-ttu-id="98f85-107">These include chat rooms, discussion boards, chatbots, eCommerce catalogs, and documents.</span><span class="sxs-lookup"><span data-stu-id="98f85-107">These include chat rooms, discussion boards, chatbots, eCommerce catalogs, and documents.</span></span> 

<span data-ttu-id="98f85-108">The service response includes the following information:</span><span class="sxs-lookup"><span data-stu-id="98f85-108">The service response includes the following information:</span></span>

- <span data-ttu-id="98f85-109">Profanity: term-based matching with built-in list of profane terms in various languages</span><span class="sxs-lookup"><span data-stu-id="98f85-109">Profanity: term-based matching with built-in list of profane terms in various languages</span></span>
- <span data-ttu-id="98f85-110">Classification: machine-assisted classification into three categories</span><span class="sxs-lookup"><span data-stu-id="98f85-110">Classification: machine-assisted classification into three categories</span></span>
- <span data-ttu-id="98f85-111">Personally Identifiable Information (PII)</span><span class="sxs-lookup"><span data-stu-id="98f85-111">Personally Identifiable Information (PII)</span></span>
- <span data-ttu-id="98f85-112">Auto-corrected text</span><span class="sxs-lookup"><span data-stu-id="98f85-112">Auto-corrected text</span></span>
- <span data-ttu-id="98f85-113">Original text</span><span class="sxs-lookup"><span data-stu-id="98f85-113">Original text</span></span>
- <span data-ttu-id="98f85-114">Language</span><span class="sxs-lookup"><span data-stu-id="98f85-114">Language</span></span>

## <a name="profanity"></a><span data-ttu-id="98f85-115">Profanity</span><span class="sxs-lookup"><span data-stu-id="98f85-115">Profanity</span></span>

<span data-ttu-id="98f85-116">If the API detects any profane terms in any of the [supported languages](Text-Moderation-API-Languages.md), those terms are included in the response.</span><span class="sxs-lookup"><span data-stu-id="98f85-116">If the API detects any profane terms in any of the [supported languages](Text-Moderation-API-Languages.md), those terms are included in the response.</span></span> <span data-ttu-id="98f85-117">The response also contains their location (`Index`) in the original text.</span><span class="sxs-lookup"><span data-stu-id="98f85-117">The response also contains their location (`Index`) in the original text.</span></span> <span data-ttu-id="98f85-118">The `ListId` in the following sample JSON refers to terms found in [custom term lists](try-terms-list-api.md) if available.</span><span class="sxs-lookup"><span data-stu-id="98f85-118">The `ListId` in the following sample JSON refers to terms found in [custom term lists](try-terms-list-api.md) if available.</span></span>

    "Terms": [
    {
        "Index": 118,
        "OriginalIndex": 118,
        "ListId": 0,
        "Term": "crap"
    }

> [!NOTE]
> <span data-ttu-id="98f85-119">For the **language** parameter, assign `eng` or leave it empty to see the machine-assisted **classification** response (preview feature).</span><span class="sxs-lookup"><span data-stu-id="98f85-119">For the **language** parameter, assign `eng` or leave it empty to see the machine-assisted **classification** response (preview feature).</span></span> <span data-ttu-id="98f85-120">**This feature supports English only**.</span><span class="sxs-lookup"><span data-stu-id="98f85-120">**This feature supports English only**.</span></span>
>
> <span data-ttu-id="98f85-121">For **profanity terms** detection, use the [ISO 639-3 code](http://www-01.sil.org/iso639-3/codes.asp) of the supported languages listed in this article, or leave it empty.</span><span class="sxs-lookup"><span data-stu-id="98f85-121">For **profanity terms** detection, use the [ISO 639-3 code](http://www-01.sil.org/iso639-3/codes.asp) of the supported languages listed in this article, or leave it empty.</span></span>

## <a name="classification"></a><span data-ttu-id="98f85-122">Classification</span><span class="sxs-lookup"><span data-stu-id="98f85-122">Classification</span></span>

<span data-ttu-id="98f85-123">Content Moderator’s machine-assisted **text classification feature** supports **English only**, and helps detect potentially undesired content.</span><span class="sxs-lookup"><span data-stu-id="98f85-123">Content Moderator’s machine-assisted **text classification feature** supports **English only**, and helps detect potentially undesired content.</span></span> <span data-ttu-id="98f85-124">The flagged content may be assessed as inappropriate depending on context.</span><span class="sxs-lookup"><span data-stu-id="98f85-124">The flagged content may be assessed as inappropriate depending on context.</span></span> <span data-ttu-id="98f85-125">It conveys the likelihood of each category and may recommend a human review.</span><span class="sxs-lookup"><span data-stu-id="98f85-125">It conveys the likelihood of each category and may recommend a human review.</span></span> <span data-ttu-id="98f85-126">The feature uses a trained model to identify possible abusive, derogatory or discriminatory language.</span><span class="sxs-lookup"><span data-stu-id="98f85-126">The feature uses a trained model to identify possible abusive, derogatory or discriminatory language.</span></span> <span data-ttu-id="98f85-127">This includes slang, abbreviated words, offensive, and intentionally misspelled words for review.</span><span class="sxs-lookup"><span data-stu-id="98f85-127">This includes slang, abbreviated words, offensive, and intentionally misspelled words for review.</span></span> 

<span data-ttu-id="98f85-128">The following extract in the JSON extract shows an example output:</span><span class="sxs-lookup"><span data-stu-id="98f85-128">The following extract in the JSON extract shows an example output:</span></span>

    "Classification": {
        "ReviewRecommended": true,
        "Category1": {
            "Score": 1.5113095059859916E-06
            },
        "Category2": {
            "Score": 0.12747249007225037
            },
        "Category3": {
            "Score": 0.98799997568130493
        }
    }

### <a name="explanation"></a><span data-ttu-id="98f85-129">Explanation</span><span class="sxs-lookup"><span data-stu-id="98f85-129">Explanation</span></span>

- <span data-ttu-id="98f85-130">`Category1` refers to potential presence of language that may be considered sexually explicit or adult in certain situations.</span><span class="sxs-lookup"><span data-stu-id="98f85-130">`Category1` refers to potential presence of language that may be considered sexually explicit or adult in certain situations.</span></span>
- <span data-ttu-id="98f85-131">`Category2` refers to potential presence of language that may be considered sexually suggestive or mature in certain situations.</span><span class="sxs-lookup"><span data-stu-id="98f85-131">`Category2` refers to potential presence of language that may be considered sexually suggestive or mature in certain situations.</span></span>
- <span data-ttu-id="98f85-132">`Category3` refers to potential presence of language that may be considered offensive in certain situations.</span><span class="sxs-lookup"><span data-stu-id="98f85-132">`Category3` refers to potential presence of language that may be considered offensive in certain situations.</span></span>
- <span data-ttu-id="98f85-133">`Score` is between 0 and 1.</span><span class="sxs-lookup"><span data-stu-id="98f85-133">`Score` is between 0 and 1.</span></span> <span data-ttu-id="98f85-134">The higher the score, the higher the model is predicting that the category may be applicable.</span><span class="sxs-lookup"><span data-stu-id="98f85-134">The higher the score, the higher the model is predicting that the category may be applicable.</span></span> <span data-ttu-id="98f85-135">This feature relies on a statistical model rather than manually coded outcomes.</span><span class="sxs-lookup"><span data-stu-id="98f85-135">This feature relies on a statistical model rather than manually coded outcomes.</span></span> <span data-ttu-id="98f85-136">We recommend testing with your own content to determine how each category aligns to your requirements.</span><span class="sxs-lookup"><span data-stu-id="98f85-136">We recommend testing with your own content to determine how each category aligns to your requirements.</span></span>
- <span data-ttu-id="98f85-137">`ReviewRecommended` is either true or false depending on the internal score thresholds.</span><span class="sxs-lookup"><span data-stu-id="98f85-137">`ReviewRecommended` is either true or false depending on the internal score thresholds.</span></span> <span data-ttu-id="98f85-138">Customers should assess whether to use this value or decide on custom thresholds based on their content policies.</span><span class="sxs-lookup"><span data-stu-id="98f85-138">Customers should assess whether to use this value or decide on custom thresholds based on their content policies.</span></span>

## <a name="personally-identifiable-information-pii"></a><span data-ttu-id="98f85-139">Personally Identifiable Information (PII)</span><span class="sxs-lookup"><span data-stu-id="98f85-139">Personally Identifiable Information (PII)</span></span>

<span data-ttu-id="98f85-140">The PII feature detects the potential presence of this information:</span><span class="sxs-lookup"><span data-stu-id="98f85-140">The PII feature detects the potential presence of this information:</span></span>

- <span data-ttu-id="98f85-141">Email address</span><span class="sxs-lookup"><span data-stu-id="98f85-141">Email address</span></span>
- <span data-ttu-id="98f85-142">US Mailing address</span><span class="sxs-lookup"><span data-stu-id="98f85-142">US Mailing address</span></span>
- <span data-ttu-id="98f85-143">IP address</span><span class="sxs-lookup"><span data-stu-id="98f85-143">IP address</span></span>
- <span data-ttu-id="98f85-144">US Phone number</span><span class="sxs-lookup"><span data-stu-id="98f85-144">US Phone number</span></span>
- <span data-ttu-id="98f85-145">UK Phone number</span><span class="sxs-lookup"><span data-stu-id="98f85-145">UK Phone number</span></span>
- <span data-ttu-id="98f85-146">Social Security Number (SSN)</span><span class="sxs-lookup"><span data-stu-id="98f85-146">Social Security Number (SSN)</span></span>

<span data-ttu-id="98f85-147">The following example shows a sample response:</span><span class="sxs-lookup"><span data-stu-id="98f85-147">The following example shows a sample response:</span></span>

    "PII": {
        "Email": [{
            "Detected": "abcdef@abcd.com",
            "SubType": "Regular",
            "Text": "abcdef@abcd.com",
            "Index": 32
            }],
        "IPA": [{
            "SubType": "IPV4",
            "Text": "255.255.255.255",
            "Index": 72
            }],
        "Phone": [{
            "CountryCode": "US",
            "Text": "6657789887",
            "Index": 56
            }, {
            "CountryCode": "US",
            "Text": "870 608 4000",
            "Index": 212
            }, {
            "CountryCode": "UK",
            "Text": "+44 870 608 4000",
            "Index": 208
            }, {
            "CountryCode": "UK",
            "Text": "0344 800 2400",
            "Index": 228
            }, {
            "CountryCode": "UK",
            "Text": "0800 820 3300",
            "Index": 245
            }],
        "Address": [{
            "Text": "1 Microsoft Way, Redmond, WA 98052",
            "Index": 89
            }],
        "SSN": [{
            "Text": "999999999",
            "Index": 56
            }, {
            "Text": "999-99-9999",
            "Index": 267
            }]
        }

## <a name="auto-correction"></a><span data-ttu-id="98f85-148">Auto-correction</span><span class="sxs-lookup"><span data-stu-id="98f85-148">Auto-correction</span></span>

<span data-ttu-id="98f85-149">Suppose the input text is (the ‘lzay’ and 'f0x' are intentional):</span><span class="sxs-lookup"><span data-stu-id="98f85-149">Suppose the input text is (the ‘lzay’ and 'f0x' are intentional):</span></span>

    The qu!ck brown f0x jumps over the lzay dog.

<span data-ttu-id="98f85-150">If you ask for auto-correction, the response contains the corrected version of the text:</span><span class="sxs-lookup"><span data-stu-id="98f85-150">If you ask for auto-correction, the response contains the corrected version of the text:</span></span>

    The quick brown fox jumps over the lazy dog.

## <a name="creating-and-managing-your-custom-lists-of-terms"></a><span data-ttu-id="98f85-151">Creating and managing your custom lists of terms</span><span class="sxs-lookup"><span data-stu-id="98f85-151">Creating and managing your custom lists of terms</span></span>

<span data-ttu-id="98f85-152">While the default, global list of terms works great for most cases, you may want to screen against terms that are specific to your business needs.</span><span class="sxs-lookup"><span data-stu-id="98f85-152">While the default, global list of terms works great for most cases, you may want to screen against terms that are specific to your business needs.</span></span> <span data-ttu-id="98f85-153">For example, you may want to filter out any competitive brand names from posts by users.</span><span class="sxs-lookup"><span data-stu-id="98f85-153">For example, you may want to filter out any competitive brand names from posts by users.</span></span>

> [!NOTE]
> <span data-ttu-id="98f85-154">There is a maximum limit of **5 term lists** with each list to **not exceed 10,000 terms**.</span><span class="sxs-lookup"><span data-stu-id="98f85-154">There is a maximum limit of **5 term lists** with each list to **not exceed 10,000 terms**.</span></span>
>

<span data-ttu-id="98f85-155">The following example shows the matching List ID:</span><span class="sxs-lookup"><span data-stu-id="98f85-155">The following example shows the matching List ID:</span></span>

    "Terms": [
    {
        "Index": 118,
        "OriginalIndex": 118,
        "ListId": 231.
        "Term": "crap"
    }

<span data-ttu-id="98f85-156">The Content Moderator provides a [Term List API](https://westus.dev.cognitive.microsoft.com/docs/services/57cf755e3f9b070c105bd2c2/operations/57cf755e3f9b070868a1f67f) with operations for managing custom term lists.</span><span class="sxs-lookup"><span data-stu-id="98f85-156">The Content Moderator provides a [Term List API](https://westus.dev.cognitive.microsoft.com/docs/services/57cf755e3f9b070c105bd2c2/operations/57cf755e3f9b070868a1f67f) with operations for managing custom term lists.</span></span> <span data-ttu-id="98f85-157">Start with the [Term Lists API Console](try-terms-list-api.md) and use the REST API code samples.</span><span class="sxs-lookup"><span data-stu-id="98f85-157">Start with the [Term Lists API Console](try-terms-list-api.md) and use the REST API code samples.</span></span> <span data-ttu-id="98f85-158">Also check out the [Term Lists .NET quickstart](term-lists-quickstart-dotnet.md) if you are familiar with Visual Studio and C#.</span><span class="sxs-lookup"><span data-stu-id="98f85-158">Also check out the [Term Lists .NET quickstart](term-lists-quickstart-dotnet.md) if you are familiar with Visual Studio and C#.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98f85-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="98f85-159">Next steps</span></span>

<span data-ttu-id="98f85-160">Test drive the [Text moderation API console](try-text-api.md) and use the REST API code samples.</span><span class="sxs-lookup"><span data-stu-id="98f85-160">Test drive the [Text moderation API console](try-text-api.md) and use the REST API code samples.</span></span> <span data-ttu-id="98f85-161">Also check out the [Text moderation .NET quickstart](text-moderation-quickstart-dotnet.md) if you're familiar with Visual Studio and C#.</span><span class="sxs-lookup"><span data-stu-id="98f85-161">Also check out the [Text moderation .NET quickstart](text-moderation-quickstart-dotnet.md) if you're familiar with Visual Studio and C#.</span></span>
