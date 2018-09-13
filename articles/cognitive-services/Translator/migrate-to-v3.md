---
title: Microsoft Translator Text API - Migrate to V3 | Microsoft Docs
description: Learn how to migrate from V2 to V3 of the Translator Text API.
services: cognitive-services
author: Jann-Skotdal
manager: chriswendt1
ms.service: cognitive-services
ms.technology: translator
ms.topic: article
ms.date: 03/27/2018
ms.author: v-jansko
ms.openlocfilehash: 16fec351af5b5b3875657ee244c18f305311d965
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965932"
---
# <a name="microsoft-translator-text-api-v2-to-v3-migration"></a><span data-ttu-id="6a56a-103">Microsoft Translator Text API V2 to V3 Migration</span><span class="sxs-lookup"><span data-stu-id="6a56a-103">Microsoft Translator Text API V2 to V3 Migration</span></span>

<span data-ttu-id="6a56a-104">The Microsoft Translator team has released Version 3 (V3) of the Text Translation API.</span><span class="sxs-lookup"><span data-stu-id="6a56a-104">The Microsoft Translator team has released Version 3 (V3) of the Text Translation API.</span></span> <span data-ttu-id="6a56a-105">This release includes new features, deprecated methods and a new format for sending to, and receiving data from the Microsoft Translator Service.</span><span class="sxs-lookup"><span data-stu-id="6a56a-105">This release includes new features, deprecated methods and a new format for sending to, and receiving data from the Microsoft Translator Service.</span></span> <span data-ttu-id="6a56a-106">This document provides information for changing applications to use V3.</span><span class="sxs-lookup"><span data-stu-id="6a56a-106">This document provides information for changing applications to use V3.</span></span> <span data-ttu-id="6a56a-107">V2 will be deprecated on April 30, 2018 and will be discontinued on April 30, 2019.</span><span class="sxs-lookup"><span data-stu-id="6a56a-107">V2 will be deprecated on April 30, 2018 and will be discontinued on April 30, 2019.</span></span>

<span data-ttu-id="6a56a-108">The end of this document contains helpful links for you to learn more.</span><span class="sxs-lookup"><span data-stu-id="6a56a-108">The end of this document contains helpful links for you to learn more.</span></span>

## <a name="summary-of-features"></a><span data-ttu-id="6a56a-109">Summary of features</span><span class="sxs-lookup"><span data-stu-id="6a56a-109">Summary of features</span></span>

* <span data-ttu-id="6a56a-110">No Trace - In V3 No-Trace applies to all pricing tiers in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6a56a-110">No Trace - In V3 No-Trace applies to all pricing tiers in the Azure portal.</span></span> <span data-ttu-id="6a56a-111">This means that no text submitted to the V3 API, will be saved by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6a56a-111">This means that no text submitted to the V3 API, will be saved by Microsoft.</span></span>
* <span data-ttu-id="6a56a-112">JSON - XML is replaced by JSON.</span><span class="sxs-lookup"><span data-stu-id="6a56a-112">JSON - XML is replaced by JSON.</span></span> <span data-ttu-id="6a56a-113">All data sent to the service and received from the service is in JSON format.</span><span class="sxs-lookup"><span data-stu-id="6a56a-113">All data sent to the service and received from the service is in JSON format.</span></span>
* <span data-ttu-id="6a56a-114">Multiple target languages in a single request - The Translate method accepts multiple ‘to’ languages for translation in a single request.</span><span class="sxs-lookup"><span data-stu-id="6a56a-114">Multiple target languages in a single request - The Translate method accepts multiple ‘to’ languages for translation in a single request.</span></span> <span data-ttu-id="6a56a-115">For example, a single request can be ‘from’ English and ‘to’ German, Spanish and Japanese, or any other group of languages.</span><span class="sxs-lookup"><span data-stu-id="6a56a-115">For example, a single request can be ‘from’ English and ‘to’ German, Spanish and Japanese, or any other group of languages.</span></span>
* <span data-ttu-id="6a56a-116">Bilingual dictionary - A bilingual dictionary method has been added to the API.</span><span class="sxs-lookup"><span data-stu-id="6a56a-116">Bilingual dictionary - A bilingual dictionary method has been added to the API.</span></span> <span data-ttu-id="6a56a-117">This method includes ‘lookup’ and ‘examples’.</span><span class="sxs-lookup"><span data-stu-id="6a56a-117">This method includes ‘lookup’ and ‘examples’.</span></span>
* <span data-ttu-id="6a56a-118">Transliterate - A transliterate method has been added to the API.</span><span class="sxs-lookup"><span data-stu-id="6a56a-118">Transliterate - A transliterate method has been added to the API.</span></span> <span data-ttu-id="6a56a-119">This method will convert words and sentences in one script (E.g.</span><span class="sxs-lookup"><span data-stu-id="6a56a-119">This method will convert words and sentences in one script (E.g.</span></span> <span data-ttu-id="6a56a-120">Arabic) into another script (E.g.</span><span class="sxs-lookup"><span data-stu-id="6a56a-120">Arabic) into another script (E.g.</span></span> <span data-ttu-id="6a56a-121">Latin).</span><span class="sxs-lookup"><span data-stu-id="6a56a-121">Latin).</span></span>
* <span data-ttu-id="6a56a-122">Languages - A new ‘languages’ method delivers language information, in JSON format, for use with the ‘translate’, ‘dictionary’, and ‘transliterate’ methods.</span><span class="sxs-lookup"><span data-stu-id="6a56a-122">Languages - A new ‘languages’ method delivers language information, in JSON format, for use with the ‘translate’, ‘dictionary’, and ‘transliterate’ methods.</span></span>
* <span data-ttu-id="6a56a-123">New to Translate - New capabilities have been added to the ‘translate’ method to support some of the features that were in the V2 API as separate methods.</span><span class="sxs-lookup"><span data-stu-id="6a56a-123">New to Translate - New capabilities have been added to the ‘translate’ method to support some of the features that were in the V2 API as separate methods.</span></span> <span data-ttu-id="6a56a-124">An example is TranslateArray.</span><span class="sxs-lookup"><span data-stu-id="6a56a-124">An example is TranslateArray.</span></span>
* <span data-ttu-id="6a56a-125">Speak method - Text to speech functionality is no longer supported in the Microsoft Translator API.</span><span class="sxs-lookup"><span data-stu-id="6a56a-125">Speak method - Text to speech functionality is no longer supported in the Microsoft Translator API.</span></span> <span data-ttu-id="6a56a-126">Text to speech functionality is available in the Microsoft Azure Cognitive services Bing Speech API.</span><span class="sxs-lookup"><span data-stu-id="6a56a-126">Text to speech functionality is available in the Microsoft Azure Cognitive services Bing Speech API.</span></span>

<span data-ttu-id="6a56a-127">The following list of V2 and V3 methods identifies the V3 methods and APIs that will provide the functionality that came with V2.</span><span class="sxs-lookup"><span data-stu-id="6a56a-127">The following list of V2 and V3 methods identifies the V3 methods and APIs that will provide the functionality that came with V2.</span></span>

| <span data-ttu-id="6a56a-128">V2 API Method</span><span class="sxs-lookup"><span data-stu-id="6a56a-128">V2 API Method</span></span>   | <span data-ttu-id="6a56a-129">V3 API Compatibility</span><span class="sxs-lookup"><span data-stu-id="6a56a-129">V3 API Compatibility</span></span> |
|:----------- |:-------------|
| <span data-ttu-id="6a56a-130">Translate</span><span class="sxs-lookup"><span data-stu-id="6a56a-130">Translate</span></span>     | <span data-ttu-id="6a56a-131">Translate</span><span class="sxs-lookup"><span data-stu-id="6a56a-131">Translate</span></span>          |
| <span data-ttu-id="6a56a-132">TranslateArray</span><span class="sxs-lookup"><span data-stu-id="6a56a-132">TranslateArray</span></span>      | <span data-ttu-id="6a56a-133">Translate</span><span class="sxs-lookup"><span data-stu-id="6a56a-133">Translate</span></span>          |
| <span data-ttu-id="6a56a-134">GetLanguageNames</span><span class="sxs-lookup"><span data-stu-id="6a56a-134">GetLanguageNames</span></span>      | <span data-ttu-id="6a56a-135">Languages</span><span class="sxs-lookup"><span data-stu-id="6a56a-135">Languages</span></span>          |
| <span data-ttu-id="6a56a-136">GetLanguagesForTranslate</span><span class="sxs-lookup"><span data-stu-id="6a56a-136">GetLanguagesForTranslate</span></span>     | <span data-ttu-id="6a56a-137">Languages</span><span class="sxs-lookup"><span data-stu-id="6a56a-137">Languages</span></span>        |
| <span data-ttu-id="6a56a-138">GetLanguagesForSpeak</span><span class="sxs-lookup"><span data-stu-id="6a56a-138">GetLanguagesForSpeak</span></span>      | <span data-ttu-id="6a56a-139">Cognitive Services Speech API</span><span class="sxs-lookup"><span data-stu-id="6a56a-139">Cognitive Services Speech API</span></span>         |
| <span data-ttu-id="6a56a-140">Speak</span><span class="sxs-lookup"><span data-stu-id="6a56a-140">Speak</span></span>     | <span data-ttu-id="6a56a-141">Cognitive Services Speech API</span><span class="sxs-lookup"><span data-stu-id="6a56a-141">Cognitive Services Speech API</span></span>          |
| <span data-ttu-id="6a56a-142">Detect</span><span class="sxs-lookup"><span data-stu-id="6a56a-142">Detect</span></span>     | <span data-ttu-id="6a56a-143">Detect</span><span class="sxs-lookup"><span data-stu-id="6a56a-143">Detect</span></span>         |
| <span data-ttu-id="6a56a-144">DetectArray</span><span class="sxs-lookup"><span data-stu-id="6a56a-144">DetectArray</span></span>     | <span data-ttu-id="6a56a-145">Detect</span><span class="sxs-lookup"><span data-stu-id="6a56a-145">Detect</span></span>         |
| <span data-ttu-id="6a56a-146">AddTranslation</span><span class="sxs-lookup"><span data-stu-id="6a56a-146">AddTranslation</span></span>     | <span data-ttu-id="6a56a-147">Microsoft Translator HUB API</span><span class="sxs-lookup"><span data-stu-id="6a56a-147">Microsoft Translator HUB API</span></span>         |
| <span data-ttu-id="6a56a-148">AddTranslationArray</span><span class="sxs-lookup"><span data-stu-id="6a56a-148">AddTranslationArray</span></span>    | <span data-ttu-id="6a56a-149">Microsoft Translator HUB API</span><span class="sxs-lookup"><span data-stu-id="6a56a-149">Microsoft Translator HUB API</span></span>          |
| <span data-ttu-id="6a56a-150">BreakSentences</span><span class="sxs-lookup"><span data-stu-id="6a56a-150">BreakSentences</span></span>      | <span data-ttu-id="6a56a-151">BreakSentence</span><span class="sxs-lookup"><span data-stu-id="6a56a-151">BreakSentence</span></span>         |
| <span data-ttu-id="6a56a-152">GetTranslations</span><span class="sxs-lookup"><span data-stu-id="6a56a-152">GetTranslations</span></span>      | <span data-ttu-id="6a56a-153">Feature is no longer supported</span><span class="sxs-lookup"><span data-stu-id="6a56a-153">Feature is no longer supported</span></span>         |
| <span data-ttu-id="6a56a-154">GetTranslationsArray</span><span class="sxs-lookup"><span data-stu-id="6a56a-154">GetTranslationsArray</span></span>      | <span data-ttu-id="6a56a-155">Feature is no longer supported</span><span class="sxs-lookup"><span data-stu-id="6a56a-155">Feature is no longer supported</span></span>         |

## <a name="move-to-json-format"></a><span data-ttu-id="6a56a-156">Move to JSON format</span><span class="sxs-lookup"><span data-stu-id="6a56a-156">Move to JSON format</span></span>

<span data-ttu-id="6a56a-157">Microsoft Translator Text Translation V2 accepted and returned data in XML format.</span><span class="sxs-lookup"><span data-stu-id="6a56a-157">Microsoft Translator Text Translation V2 accepted and returned data in XML format.</span></span> <span data-ttu-id="6a56a-158">In V3 all data sent and received using the API is in JSON format.</span><span class="sxs-lookup"><span data-stu-id="6a56a-158">In V3 all data sent and received using the API is in JSON format.</span></span> <span data-ttu-id="6a56a-159">XML will no longer be accepted or returned in V3.</span><span class="sxs-lookup"><span data-stu-id="6a56a-159">XML will no longer be accepted or returned in V3.</span></span> 

<span data-ttu-id="6a56a-160">This change will affect several aspects of an application written for the V2 Text Translation API.</span><span class="sxs-lookup"><span data-stu-id="6a56a-160">This change will affect several aspects of an application written for the V2 Text Translation API.</span></span> <span data-ttu-id="6a56a-161">As an example: The Languages API returns language information for text translation, transliteration and the two dictionary methods.</span><span class="sxs-lookup"><span data-stu-id="6a56a-161">As an example: The Languages API returns language information for text translation, transliteration and the two dictionary methods.</span></span> <span data-ttu-id="6a56a-162">You can request all language information for all methods in one call or request them individually.</span><span class="sxs-lookup"><span data-stu-id="6a56a-162">You can request all language information for all methods in one call or request them individually.</span></span>

<span data-ttu-id="6a56a-163">The languages method does not require authentication; by clicking on the following link you can see all the language information for V3 in JSON:</span><span class="sxs-lookup"><span data-stu-id="6a56a-163">The languages method does not require authentication; by clicking on the following link you can see all the language information for V3 in JSON:</span></span>

[<span data-ttu-id="6a56a-164">https://api.cognitive.microsofttranslator.com/languages?api-version=3.0&scope=translation,dictionary,transliteration</span><span class="sxs-lookup"><span data-stu-id="6a56a-164">https://api.cognitive.microsofttranslator.com/languages?api-version=3.0&scope=translation,dictionary,transliteration</span></span>](https://api.cognitive.microsofttranslator.com/languages?api-version=3.0&scope=translation,dictionary,transliteration)

## <a name="authentication-key"></a><span data-ttu-id="6a56a-165">Authentication Key</span><span class="sxs-lookup"><span data-stu-id="6a56a-165">Authentication Key</span></span>

<span data-ttu-id="6a56a-166">The authentication key you are using for V2 will be accepted for V3.</span><span class="sxs-lookup"><span data-stu-id="6a56a-166">The authentication key you are using for V2 will be accepted for V3.</span></span> <span data-ttu-id="6a56a-167">You will not need to get a new subscription.</span><span class="sxs-lookup"><span data-stu-id="6a56a-167">You will not need to get a new subscription.</span></span> <span data-ttu-id="6a56a-168">You will be able to mix V2 and V3 in your apps during the yearlong migration period, making it easier for you to release new versions while you are still migrating from V2-XML to V3-JSON.</span><span class="sxs-lookup"><span data-stu-id="6a56a-168">You will be able to mix V2 and V3 in your apps during the yearlong migration period, making it easier for you to release new versions while you are still migrating from V2-XML to V3-JSON.</span></span>

## <a name="pricing-model"></a><span data-ttu-id="6a56a-169">Pricing Model</span><span class="sxs-lookup"><span data-stu-id="6a56a-169">Pricing Model</span></span>

<span data-ttu-id="6a56a-170">Microsoft Translator V3 is priced in the same way V2 was priced; per character, including spaces.</span><span class="sxs-lookup"><span data-stu-id="6a56a-170">Microsoft Translator V3 is priced in the same way V2 was priced; per character, including spaces.</span></span> <span data-ttu-id="6a56a-171">The new features in V3 make some changes in what characters are counted for billing.</span><span class="sxs-lookup"><span data-stu-id="6a56a-171">The new features in V3 make some changes in what characters are counted for billing.</span></span>

| <span data-ttu-id="6a56a-172">V3 Method</span><span class="sxs-lookup"><span data-stu-id="6a56a-172">V3 Method</span></span>   | <span data-ttu-id="6a56a-173">Characters Counted for Billing</span><span class="sxs-lookup"><span data-stu-id="6a56a-173">Characters Counted for Billing</span></span> |
|:----------- |:-------------|
| <span data-ttu-id="6a56a-174">Languages</span><span class="sxs-lookup"><span data-stu-id="6a56a-174">Languages</span></span>     | <span data-ttu-id="6a56a-175">No characters submitted, none counted, no charge.</span><span class="sxs-lookup"><span data-stu-id="6a56a-175">No characters submitted, none counted, no charge.</span></span>          |
| <span data-ttu-id="6a56a-176">Translate</span><span class="sxs-lookup"><span data-stu-id="6a56a-176">Translate</span></span>     | <span data-ttu-id="6a56a-177">Count is based on how many characters are submitted for translation, and how many languages the characters are translated into.</span><span class="sxs-lookup"><span data-stu-id="6a56a-177">Count is based on how many characters are submitted for translation, and how many languages the characters are translated into.</span></span> <span data-ttu-id="6a56a-178">50 characters submitted, and 5 languages requested will be 50x5.</span><span class="sxs-lookup"><span data-stu-id="6a56a-178">50 characters submitted, and 5 languages requested will be 50x5.</span></span>           |
| <span data-ttu-id="6a56a-179">Transliterate</span><span class="sxs-lookup"><span data-stu-id="6a56a-179">Transliterate</span></span>     | <span data-ttu-id="6a56a-180">Number of characters submitted for transliteration are counted.</span><span class="sxs-lookup"><span data-stu-id="6a56a-180">Number of characters submitted for transliteration are counted.</span></span>         |
| <span data-ttu-id="6a56a-181">Dictionary lookup & example</span><span class="sxs-lookup"><span data-stu-id="6a56a-181">Dictionary lookup & example</span></span>     | <span data-ttu-id="6a56a-182">Number of characters submitted for Dictionary lookup and examples are counted.</span><span class="sxs-lookup"><span data-stu-id="6a56a-182">Number of characters submitted for Dictionary lookup and examples are counted.</span></span>         |
| <span data-ttu-id="6a56a-183">BreakSentence</span><span class="sxs-lookup"><span data-stu-id="6a56a-183">BreakSentence</span></span>     | <span data-ttu-id="6a56a-184">No Charge.</span><span class="sxs-lookup"><span data-stu-id="6a56a-184">No Charge.</span></span>       |
| <span data-ttu-id="6a56a-185">Detect</span><span class="sxs-lookup"><span data-stu-id="6a56a-185">Detect</span></span>     | <span data-ttu-id="6a56a-186">No Charge.</span><span class="sxs-lookup"><span data-stu-id="6a56a-186">No Charge.</span></span>      |

## <a name="v3-end-points"></a><span data-ttu-id="6a56a-187">V3 End Points</span><span class="sxs-lookup"><span data-stu-id="6a56a-187">V3 End Points</span></span>

<span data-ttu-id="6a56a-188">Global</span><span class="sxs-lookup"><span data-stu-id="6a56a-188">Global</span></span>

* <span data-ttu-id="6a56a-189">api.cognitive.microsofttranslator.com</span><span class="sxs-lookup"><span data-stu-id="6a56a-189">api.cognitive.microsofttranslator.com</span></span>


## <a name="v3-api-text-translations-methods"></a><span data-ttu-id="6a56a-190">V3 API text translations methods</span><span class="sxs-lookup"><span data-stu-id="6a56a-190">V3 API text translations methods</span></span>

[<span data-ttu-id="6a56a-191">Languages</span><span class="sxs-lookup"><span data-stu-id="6a56a-191">Languages</span></span>](reference/v3-0-languages.md)

[<span data-ttu-id="6a56a-192">Translate</span><span class="sxs-lookup"><span data-stu-id="6a56a-192">Translate</span></span>](reference/v3-0-translate.md)

[<span data-ttu-id="6a56a-193">Transliterate</span><span class="sxs-lookup"><span data-stu-id="6a56a-193">Transliterate</span></span>](reference/v3-0-transliterate.md)

[<span data-ttu-id="6a56a-194">BreakSentence</span><span class="sxs-lookup"><span data-stu-id="6a56a-194">BreakSentence</span></span>](reference/v3-0-break-sentence.md)

[<span data-ttu-id="6a56a-195">Detect</span><span class="sxs-lookup"><span data-stu-id="6a56a-195">Detect</span></span>](reference/v3-0-detect.md)

[<span data-ttu-id="6a56a-196">Dictionary/lookup</span><span class="sxs-lookup"><span data-stu-id="6a56a-196">Dictionary/lookup</span></span>](reference/v3-0-dictionary-lookup.md)

[<span data-ttu-id="6a56a-197">Dictionary/example</span><span class="sxs-lookup"><span data-stu-id="6a56a-197">Dictionary/example</span></span>](reference/v3-0-dictionary-examples.md)

## <a name="customization"></a><span data-ttu-id="6a56a-198">Customization</span><span class="sxs-lookup"><span data-stu-id="6a56a-198">Customization</span></span>

<span data-ttu-id="6a56a-199">Microsoft Translator V3 uses neural machine translation by default.</span><span class="sxs-lookup"><span data-stu-id="6a56a-199">Microsoft Translator V3 uses neural machine translation by default.</span></span> <span data-ttu-id="6a56a-200">As such, it cannot be used with the Microsoft Translator Hub which only supports legacy statistical machine translation.</span><span class="sxs-lookup"><span data-stu-id="6a56a-200">As such, it cannot be used with the Microsoft Translator Hub which only supports legacy statistical machine translation.</span></span> <span data-ttu-id="6a56a-201">Customization for neural translation is now available using the Custom Translator.</span><span class="sxs-lookup"><span data-stu-id="6a56a-201">Customization for neural translation is now available using the Custom Translator.</span></span> [<span data-ttu-id="6a56a-202">Learn more about customizing neural machine translation</span><span class="sxs-lookup"><span data-stu-id="6a56a-202">Learn more about customizing neural machine translation</span></span>](customization.md)

<span data-ttu-id="6a56a-203">Neural translation with the V3 text API does not support the use of standard categories (smt, speech, text, generalnn).</span><span class="sxs-lookup"><span data-stu-id="6a56a-203">Neural translation with the V3 text API does not support the use of standard categories (smt, speech, text, generalnn).</span></span>


## <a name="links"></a><span data-ttu-id="6a56a-204">Links</span><span class="sxs-lookup"><span data-stu-id="6a56a-204">Links</span></span>

* [<span data-ttu-id="6a56a-205">Microsoft Privacy Policy</span><span class="sxs-lookup"><span data-stu-id="6a56a-205">Microsoft Privacy Policy</span></span>](https://privacy.microsoft.com/privacystatement)
* [<span data-ttu-id="6a56a-206">Microsoft Azure Legal Information</span><span class="sxs-lookup"><span data-stu-id="6a56a-206">Microsoft Azure Legal Information</span></span>](https://azure.microsoft.com/support/legal)
* [<span data-ttu-id="6a56a-207">Online Services Terms</span><span class="sxs-lookup"><span data-stu-id="6a56a-207">Online Services Terms</span></span>](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)

## <a name="next-steps"></a><span data-ttu-id="6a56a-208">Next steps</span><span class="sxs-lookup"><span data-stu-id="6a56a-208">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6a56a-209">View V3.0 Documentation</span><span class="sxs-lookup"><span data-stu-id="6a56a-209">View V3.0 Documentation</span></span>](reference/v3-0-reference.md)
