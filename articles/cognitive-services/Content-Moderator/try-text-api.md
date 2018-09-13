---
title: Moderate text by using the Text Moderation API in Azure Content Moderator | Microsoft Docs
description: Test-drive text moderation by using the Text Moderation API in the online console.
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.component: content-moderator
ms.topic: article
ms.date: 08/05/2017
ms.author: sajagtap
ms.openlocfilehash: ed696c31a886626819414c45eb7995edaf161fff
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969259"
---
# <a name="moderate-text-from-the-api-console"></a><span data-ttu-id="1d1d2-103">Moderate text from the API console</span><span class="sxs-lookup"><span data-stu-id="1d1d2-103">Moderate text from the API console</span></span>

<span data-ttu-id="1d1d2-104">Use the [Text Moderation API](https://westus.dev.cognitive.microsoft.com/docs/services/57cf753a3f9b070c105bd2c1/operations/57cf753a3f9b070868a1f66f) in Azure Content Moderator to scan your text content.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-104">Use the [Text Moderation API](https://westus.dev.cognitive.microsoft.com/docs/services/57cf753a3f9b070c105bd2c1/operations/57cf753a3f9b070868a1f66f) in Azure Content Moderator to scan your text content.</span></span> <span data-ttu-id="1d1d2-105">The operation scans your content for profanity, and compares the content against custom and shared blacklists.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-105">The operation scans your content for profanity, and compares the content against custom and shared blacklists.</span></span>


## <a name="get-your-api-key"></a><span data-ttu-id="1d1d2-106">Get your API key</span><span class="sxs-lookup"><span data-stu-id="1d1d2-106">Get your API key</span></span>
<span data-ttu-id="1d1d2-107">Before you can test-drive the API in the online console, you need your subscription key.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-107">Before you can test-drive the API in the online console, you need your subscription key.</span></span> <span data-ttu-id="1d1d2-108">This is located on the **Settings** tab, in the **Ocp-Apim-Subscription-Key** box.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-108">This is located on the **Settings** tab, in the **Ocp-Apim-Subscription-Key** box.</span></span> <span data-ttu-id="1d1d2-109">For more information, see [Overview](overview.md).</span><span class="sxs-lookup"><span data-stu-id="1d1d2-109">For more information, see [Overview](overview.md).</span></span>

## <a name="navigate-to-the-api-reference"></a><span data-ttu-id="1d1d2-110">Navigate to the API reference</span><span class="sxs-lookup"><span data-stu-id="1d1d2-110">Navigate to the API reference</span></span>
<span data-ttu-id="1d1d2-111">Go to the [Text Moderation API reference](https://westus.dev.cognitive.microsoft.com/docs/services/57cf753a3f9b070c105bd2c1/operations/57cf753a3f9b070868a1f66f).</span><span class="sxs-lookup"><span data-stu-id="1d1d2-111">Go to the [Text Moderation API reference](https://westus.dev.cognitive.microsoft.com/docs/services/57cf753a3f9b070c105bd2c1/operations/57cf753a3f9b070868a1f66f).</span></span> 

  <span data-ttu-id="1d1d2-112">The **Text - Screen** page opens.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-112">The **Text - Screen** page opens.</span></span>

## <a name="open-the-api-console"></a><span data-ttu-id="1d1d2-113">Open the API console</span><span class="sxs-lookup"><span data-stu-id="1d1d2-113">Open the API console</span></span>
<span data-ttu-id="1d1d2-114">For **Open API testing console**, select the region that most closely describes your location.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-114">For **Open API testing console**, select the region that most closely describes your location.</span></span> 

  ![Text - Screen page region selection](images/test-drive-region.png)

  <span data-ttu-id="1d1d2-116">The **Text - Screen** API console opens.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-116">The **Text - Screen** API console opens.</span></span>

## <a name="select-the-inputs"></a><span data-ttu-id="1d1d2-117">Select the inputs</span><span class="sxs-lookup"><span data-stu-id="1d1d2-117">Select the inputs</span></span>

### <a name="parameters"></a><span data-ttu-id="1d1d2-118">Parameters</span><span class="sxs-lookup"><span data-stu-id="1d1d2-118">Parameters</span></span>
<span data-ttu-id="1d1d2-119">Select the query parameters that you want to use in your text screen.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-119">Select the query parameters that you want to use in your text screen.</span></span> <span data-ttu-id="1d1d2-120">For this example, use the default value for **language**.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-120">For this example, use the default value for **language**.</span></span> <span data-ttu-id="1d1d2-121">You can also leave it blank because the operation will automatically detect the likely language as part of its execution.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-121">You can also leave it blank because the operation will automatically detect the likely language as part of its execution.</span></span>

> [!NOTE]
> <span data-ttu-id="1d1d2-122">For the **language** parameter, assign `eng` or leave it empty to see the machine-assisted **classification** response (preview feature).</span><span class="sxs-lookup"><span data-stu-id="1d1d2-122">For the **language** parameter, assign `eng` or leave it empty to see the machine-assisted **classification** response (preview feature).</span></span> <span data-ttu-id="1d1d2-123">**This feature supports English only**.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-123">**This feature supports English only**.</span></span>
>
> <span data-ttu-id="1d1d2-124">For **profanity terms** detection, use the [ISO 639-3 code](http://www-01.sil.org/iso639-3/codes.asp) of the supported languages listed in this article, or leave it empty.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-124">For **profanity terms** detection, use the [ISO 639-3 code](http://www-01.sil.org/iso639-3/codes.asp) of the supported languages listed in this article, or leave it empty.</span></span>

<span data-ttu-id="1d1d2-125">For **autocorrect**, **PII**, and **classify (preview)**, select **true**.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-125">For **autocorrect**, **PII**, and **classify (preview)**, select **true**.</span></span> <span data-ttu-id="1d1d2-126">Leave the **ListId** field empty.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-126">Leave the **ListId** field empty.</span></span>

  ![Text - Screen console query parameters](images/text-api-console-inputs.PNG)

### <a name="content-type"></a><span data-ttu-id="1d1d2-128">Content type</span><span class="sxs-lookup"><span data-stu-id="1d1d2-128">Content type</span></span>
<span data-ttu-id="1d1d2-129">For **Content-Type**, select the type of content you want to screen.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-129">For **Content-Type**, select the type of content you want to screen.</span></span> <span data-ttu-id="1d1d2-130">For this example, use the default **text/plain** content type.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-130">For this example, use the default **text/plain** content type.</span></span> <span data-ttu-id="1d1d2-131">In the **Ocp-Apim-Subscription-Key** box, enter your subscription key.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-131">In the **Ocp-Apim-Subscription-Key** box, enter your subscription key.</span></span>

### <a name="sample-text-to-scan"></a><span data-ttu-id="1d1d2-132">Sample text to scan</span><span class="sxs-lookup"><span data-stu-id="1d1d2-132">Sample text to scan</span></span>
<span data-ttu-id="1d1d2-133">In the **Request body** box, enter some text.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-133">In the **Request body** box, enter some text.</span></span> <span data-ttu-id="1d1d2-134">The following example shows an intentional typo in the text.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-134">The following example shows an intentional typo in the text.</span></span>

> [!NOTE]
> <span data-ttu-id="1d1d2-135">The invalid social security number in the following sample text is intentional.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-135">The invalid social security number in the following sample text is intentional.</span></span> <span data-ttu-id="1d1d2-136">The purpose is to convey the sample input and output format.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-136">The purpose is to convey the sample input and output format.</span></span>

```
    Is this a grabage or crap email abcdef@abcd.com, phone: 6657789887, IP: 255.255.255.255, 1 Microsoft Way, Redmond, WA 98052.
    These are all UK phone numbers, the last two being Microsoft UK support numbers: +44 870 608 4000 or 0344 800 2400 or 0800 820 3300.
    Also, 999-99-9999 looks like a social security number (SSN).
```

### <a name="text-classification-feature"></a><span data-ttu-id="1d1d2-137">Text classification feature</span><span class="sxs-lookup"><span data-stu-id="1d1d2-137">Text classification feature</span></span>

<span data-ttu-id="1d1d2-138">In the following example, you see Content Moderator’s machine-assisted text classification response.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-138">In the following example, you see Content Moderator’s machine-assisted text classification response.</span></span> <span data-ttu-id="1d1d2-139">It helps detect potentially undesired content.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-139">It helps detect potentially undesired content.</span></span> <span data-ttu-id="1d1d2-140">The flagged content may be deemed as inappropriate depending on context.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-140">The flagged content may be deemed as inappropriate depending on context.</span></span> <span data-ttu-id="1d1d2-141">In addition to conveying the likelihood of each category, it may recommend a human review of the content.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-141">In addition to conveying the likelihood of each category, it may recommend a human review of the content.</span></span> <span data-ttu-id="1d1d2-142">The feature uses a trained model to identify possible abusive, derogatory or discriminatory language.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-142">The feature uses a trained model to identify possible abusive, derogatory or discriminatory language.</span></span> <span data-ttu-id="1d1d2-143">This includes slang, abbreviated words, offensive, and intentionally misspelled words for review.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-143">This includes slang, abbreviated words, offensive, and intentionally misspelled words for review.</span></span> 

#### <a name="explanation"></a><span data-ttu-id="1d1d2-144">Explanation</span><span class="sxs-lookup"><span data-stu-id="1d1d2-144">Explanation</span></span>

- <span data-ttu-id="1d1d2-145">`Category1` represents the potential presence of language that may be considered sexually explicit or adult in certain situations.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-145">`Category1` represents the potential presence of language that may be considered sexually explicit or adult in certain situations.</span></span>
- <span data-ttu-id="1d1d2-146">`Category2` represents the potential presence of language that may be considered sexually suggestive or mature in certain situations.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-146">`Category2` represents the potential presence of language that may be considered sexually suggestive or mature in certain situations.</span></span>
- <span data-ttu-id="1d1d2-147">`Category3` represents the potential presence of language that may be considered offensive in certain situations.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-147">`Category3` represents the potential presence of language that may be considered offensive in certain situations.</span></span>
- <span data-ttu-id="1d1d2-148">`Score` is between 0 and 1.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-148">`Score` is between 0 and 1.</span></span> <span data-ttu-id="1d1d2-149">The higher the score, the higher the model is predicting that the category may be applicable.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-149">The higher the score, the higher the model is predicting that the category may be applicable.</span></span> <span data-ttu-id="1d1d2-150">This preview relies on a statistical model rather than manually coded outcomes.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-150">This preview relies on a statistical model rather than manually coded outcomes.</span></span> <span data-ttu-id="1d1d2-151">We recommend testing with your own content to determine how each category aligns to your requirements.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-151">We recommend testing with your own content to determine how each category aligns to your requirements.</span></span>
- <span data-ttu-id="1d1d2-152">`ReviewRecommended` is either true or false depending on the internal score thresholds.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-152">`ReviewRecommended` is either true or false depending on the internal score thresholds.</span></span> <span data-ttu-id="1d1d2-153">Customers should assess whether to use this value or decide on custom thresholds based on their content policies.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-153">Customers should assess whether to use this value or decide on custom thresholds based on their content policies.</span></span>

### <a name="analyze-the-response"></a><span data-ttu-id="1d1d2-154">Analyze the response</span><span class="sxs-lookup"><span data-stu-id="1d1d2-154">Analyze the response</span></span>
<span data-ttu-id="1d1d2-155">The following response shows the various insights from the API.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-155">The following response shows the various insights from the API.</span></span> <span data-ttu-id="1d1d2-156">It contains potential profanity, PII, classification (preview), and the auto-corrected version.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-156">It contains potential profanity, PII, classification (preview), and the auto-corrected version.</span></span>

> [!NOTE]
> <span data-ttu-id="1d1d2-157">The machine-assisted 'Classification' feature is in preview and supports English only.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-157">The machine-assisted 'Classification' feature is in preview and supports English only.</span></span>

```
{
    "OriginalText": "Is this a grabage or crap email abcdef@abcd.com, phone: 6657789887, IP: 255.255.255.255, 1 Microsoft Way, Redmond, WA 98052.\r\nThese are all UK phone numbers, the last two being Microsoft UK support numbers: +44 870 608 4000 or 0344 800 2400 or 0800 820 3300.\r\nAlso, 544-56-7788 looks like a social security number (SSN).",
    "NormalizedText": "Is this a grabage or crap email abcdef@ abcd. com, phone: 6657789887, IP: 255. 255. 255. 255, 1 Microsoft Way, Redmond, WA 98052. \r\nThese are all UK phone numbers, the last two being Microsoft UK support numbers: +44 870 608 4000 or 0344 800 2400 or 0800 820 3300. \r\nAlso, 544- 56- 7788 looks like a social security number ( SSN) .",
"Misrepresentation": null,
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
                "Index": 211
                }, {
                "CountryCode": "UK",
                "Text": "+44 870 608 4000",
                "Index": 207
                }, {
                "CountryCode": "UK",
                "Text": "0344 800 2400",
                "Index": 227
                }, {
                "CountryCode": "UK",
                "Text": "0800 820 3300",
                "Index": 244
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
                "Index": 266
            }]
        },
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
        },
    "Language": "eng",
    "Terms": [{
            "Index": 21,
            "OriginalIndex": 21,
            "ListId": 0,
         "Term": "crap"
        }],
    "Status": {
            "Code": 3000,
            "Description": "OK",
            "Exception": null
        },
     "TrackingId": "2eaa012f-1604-4e36-a8d7-cc34b14ebcb4"
}
```

<span data-ttu-id="1d1d2-158">For a detailed explanation of all sections in the JSON response, refer to the [text moderation API overview](text-moderation-api.md).</span><span class="sxs-lookup"><span data-stu-id="1d1d2-158">For a detailed explanation of all sections in the JSON response, refer to the [text moderation API overview](text-moderation-api.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d1d2-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="1d1d2-159">Next steps</span></span>

<span data-ttu-id="1d1d2-160">Use the REST API in your code or start with the [text moderation .NET quickstart](text-moderation-quickstart-dotnet.md) to integrate with your application.</span><span class="sxs-lookup"><span data-stu-id="1d1d2-160">Use the REST API in your code or start with the [text moderation .NET quickstart](text-moderation-quickstart-dotnet.md) to integrate with your application.</span></span>
