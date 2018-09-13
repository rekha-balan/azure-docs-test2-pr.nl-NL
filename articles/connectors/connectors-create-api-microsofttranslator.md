---
title: Add the Microsoft Translator in logic apps| Microsoft Docs
description: Overview of the Microsoft Translator connector with REST API parameters
services: ''
suite: ''
documentationcenter: ''
author: MandiOhlinger
manager: anneta
editor: ''
tags: connectors
ms.assetid: da782baf-8bf8-4973-8238-e469865f5328
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: fd501f9ef8a8883dc03a9d590b1d465a2c97dd96
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549885"
---
# <a name="get-started-with-the-microsoft-translator-connector"></a><span data-ttu-id="8613c-103">Get started with the Microsoft Translator connector</span><span class="sxs-lookup"><span data-stu-id="8613c-103">Get started with the Microsoft Translator connector</span></span>
<span data-ttu-id="8613c-104">Connect to Microsoft Translator to translate text, detect a language, and more.</span><span class="sxs-lookup"><span data-stu-id="8613c-104">Connect to Microsoft Translator to translate text, detect a language, and more.</span></span> <span data-ttu-id="8613c-105">With Microsoft Translator, you can:</span><span class="sxs-lookup"><span data-stu-id="8613c-105">With Microsoft Translator, you can:</span></span> 

* <span data-ttu-id="8613c-106">Build your business flow based on the data you get from Microsoft Translator.</span><span class="sxs-lookup"><span data-stu-id="8613c-106">Build your business flow based on the data you get from Microsoft Translator.</span></span> 
* <span data-ttu-id="8613c-107">Use actions to translate text, detect a language, and more.</span><span class="sxs-lookup"><span data-stu-id="8613c-107">Use actions to translate text, detect a language, and more.</span></span> <span data-ttu-id="8613c-108">These actions get a response, and then make the output available for other actions.</span><span class="sxs-lookup"><span data-stu-id="8613c-108">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="8613c-109">For example, when a new file is created in Dropbox, you can translate the text in the file to another language using Microsoft Translator.</span><span class="sxs-lookup"><span data-stu-id="8613c-109">For example, when a new file is created in Dropbox, you can translate the text in the file to another language using Microsoft Translator.</span></span>

<span data-ttu-id="8613c-110">To add an operation in logic apps, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="8613c-110">To add an operation in logic apps, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="triggers-and-actions"></a><span data-ttu-id="8613c-111">Triggers and actions</span><span class="sxs-lookup"><span data-stu-id="8613c-111">Triggers and actions</span></span>
<span data-ttu-id="8613c-112">Microsoft Translator includes the following actions.</span><span class="sxs-lookup"><span data-stu-id="8613c-112">Microsoft Translator includes the following actions.</span></span> <span data-ttu-id="8613c-113">There are no triggers.</span><span class="sxs-lookup"><span data-stu-id="8613c-113">There are no triggers.</span></span>

| <span data-ttu-id="8613c-114">Triggers</span><span class="sxs-lookup"><span data-stu-id="8613c-114">Triggers</span></span> | <span data-ttu-id="8613c-115">Actions</span><span class="sxs-lookup"><span data-stu-id="8613c-115">Actions</span></span> |
| --- | --- |
| <span data-ttu-id="8613c-116">None</span><span class="sxs-lookup"><span data-stu-id="8613c-116">None</span></span> |<ul><li><span data-ttu-id="8613c-117">Detect language</span><span class="sxs-lookup"><span data-stu-id="8613c-117">Detect language</span></span></li><li><span data-ttu-id="8613c-118">Text to speech</span><span class="sxs-lookup"><span data-stu-id="8613c-118">Text to speech</span></span></li><li><span data-ttu-id="8613c-119">Translate text</span><span class="sxs-lookup"><span data-stu-id="8613c-119">Translate text</span></span></li><li><span data-ttu-id="8613c-120">Get languages</span><span class="sxs-lookup"><span data-stu-id="8613c-120">Get languages</span></span></li><li><span data-ttu-id="8613c-121">Get speech languages</span><span class="sxs-lookup"><span data-stu-id="8613c-121">Get speech languages</span></span></li></ul> |

<span data-ttu-id="8613c-122">All connectors support data in JSON and XML formats.</span><span class="sxs-lookup"><span data-stu-id="8613c-122">All connectors support data in JSON and XML formats.</span></span>

## <a name="create-a-connection-to-microsoft-translator"></a><span data-ttu-id="8613c-123">Create a connection to Microsoft Translator</span><span class="sxs-lookup"><span data-stu-id="8613c-123">Create a connection to Microsoft Translator</span></span>
> [!INCLUDE [Steps to create a connection to Microsoft Translator](../../includes/connectors-create-api-microsofttranslator.md)]
> 
> 

## <a name="swagger-rest-api-reference"></a><span data-ttu-id="8613c-124">Swagger REST API reference</span><span class="sxs-lookup"><span data-stu-id="8613c-124">Swagger REST API reference</span></span>
<span data-ttu-id="8613c-125">Applies to version: 1.0.</span><span class="sxs-lookup"><span data-stu-id="8613c-125">Applies to version: 1.0.</span></span>

### <a name="detect-language"></a><span data-ttu-id="8613c-126">Detect language</span><span class="sxs-lookup"><span data-stu-id="8613c-126">Detect language</span></span>
<span data-ttu-id="8613c-127">Detects source language of given text.</span><span class="sxs-lookup"><span data-stu-id="8613c-127">Detects source language of given text.</span></span>  
```GET: /Detect```

| <span data-ttu-id="8613c-128">Name</span><span class="sxs-lookup"><span data-stu-id="8613c-128">Name</span></span> | <span data-ttu-id="8613c-129">Data Type</span><span class="sxs-lookup"><span data-stu-id="8613c-129">Data Type</span></span> | <span data-ttu-id="8613c-130">Required</span><span class="sxs-lookup"><span data-stu-id="8613c-130">Required</span></span> | <span data-ttu-id="8613c-131">Located In</span><span class="sxs-lookup"><span data-stu-id="8613c-131">Located In</span></span> | <span data-ttu-id="8613c-132">Default Value</span><span class="sxs-lookup"><span data-stu-id="8613c-132">Default Value</span></span> | <span data-ttu-id="8613c-133">Description</span><span class="sxs-lookup"><span data-stu-id="8613c-133">Description</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="8613c-134">query</span><span class="sxs-lookup"><span data-stu-id="8613c-134">query</span></span> |<span data-ttu-id="8613c-135">string</span><span class="sxs-lookup"><span data-stu-id="8613c-135">string</span></span> |<span data-ttu-id="8613c-136">yes</span><span class="sxs-lookup"><span data-stu-id="8613c-136">yes</span></span> |<span data-ttu-id="8613c-137">query</span><span class="sxs-lookup"><span data-stu-id="8613c-137">query</span></span> |<span data-ttu-id="8613c-138">none</span><span class="sxs-lookup"><span data-stu-id="8613c-138">none</span></span> |<span data-ttu-id="8613c-139">Text whose language will be identified</span><span class="sxs-lookup"><span data-stu-id="8613c-139">Text whose language will be identified</span></span> |

#### <a name="response"></a><span data-ttu-id="8613c-140">Response</span><span class="sxs-lookup"><span data-stu-id="8613c-140">Response</span></span>
| <span data-ttu-id="8613c-141">Name</span><span class="sxs-lookup"><span data-stu-id="8613c-141">Name</span></span> | <span data-ttu-id="8613c-142">Description</span><span class="sxs-lookup"><span data-stu-id="8613c-142">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8613c-143">200</span><span class="sxs-lookup"><span data-stu-id="8613c-143">200</span></span> |<span data-ttu-id="8613c-144">OK</span><span class="sxs-lookup"><span data-stu-id="8613c-144">OK</span></span> |
| <span data-ttu-id="8613c-145">default</span><span class="sxs-lookup"><span data-stu-id="8613c-145">default</span></span> |<span data-ttu-id="8613c-146">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="8613c-146">Operation Failed.</span></span> |

### <a name="text-to-speech"></a><span data-ttu-id="8613c-147">Text to speech</span><span class="sxs-lookup"><span data-stu-id="8613c-147">Text to speech</span></span>
<span data-ttu-id="8613c-148">Converts a given text into speech as an audio stream in wave format.</span><span class="sxs-lookup"><span data-stu-id="8613c-148">Converts a given text into speech as an audio stream in wave format.</span></span>  
```GET: /Speak```

| <span data-ttu-id="8613c-149">Name</span><span class="sxs-lookup"><span data-stu-id="8613c-149">Name</span></span> | <span data-ttu-id="8613c-150">Data Type</span><span class="sxs-lookup"><span data-stu-id="8613c-150">Data Type</span></span> | <span data-ttu-id="8613c-151">Required</span><span class="sxs-lookup"><span data-stu-id="8613c-151">Required</span></span> | <span data-ttu-id="8613c-152">Located In</span><span class="sxs-lookup"><span data-stu-id="8613c-152">Located In</span></span> | <span data-ttu-id="8613c-153">Default Value</span><span class="sxs-lookup"><span data-stu-id="8613c-153">Default Value</span></span> | <span data-ttu-id="8613c-154">Description</span><span class="sxs-lookup"><span data-stu-id="8613c-154">Description</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="8613c-155">query</span><span class="sxs-lookup"><span data-stu-id="8613c-155">query</span></span> |<span data-ttu-id="8613c-156">string</span><span class="sxs-lookup"><span data-stu-id="8613c-156">string</span></span> |<span data-ttu-id="8613c-157">yes</span><span class="sxs-lookup"><span data-stu-id="8613c-157">yes</span></span> |<span data-ttu-id="8613c-158">query</span><span class="sxs-lookup"><span data-stu-id="8613c-158">query</span></span> |<span data-ttu-id="8613c-159">none</span><span class="sxs-lookup"><span data-stu-id="8613c-159">none</span></span> |<span data-ttu-id="8613c-160">Text to convert</span><span class="sxs-lookup"><span data-stu-id="8613c-160">Text to convert</span></span> |
| <span data-ttu-id="8613c-161">language</span><span class="sxs-lookup"><span data-stu-id="8613c-161">language</span></span> |<span data-ttu-id="8613c-162">string</span><span class="sxs-lookup"><span data-stu-id="8613c-162">string</span></span> |<span data-ttu-id="8613c-163">yes</span><span class="sxs-lookup"><span data-stu-id="8613c-163">yes</span></span> |<span data-ttu-id="8613c-164">query</span><span class="sxs-lookup"><span data-stu-id="8613c-164">query</span></span> |<span data-ttu-id="8613c-165">none</span><span class="sxs-lookup"><span data-stu-id="8613c-165">none</span></span> |<span data-ttu-id="8613c-166">Language code to generate speech (example: 'en-us')</span><span class="sxs-lookup"><span data-stu-id="8613c-166">Language code to generate speech (example: 'en-us')</span></span> |

#### <a name="response"></a><span data-ttu-id="8613c-167">Response</span><span class="sxs-lookup"><span data-stu-id="8613c-167">Response</span></span>
| <span data-ttu-id="8613c-168">Name</span><span class="sxs-lookup"><span data-stu-id="8613c-168">Name</span></span> | <span data-ttu-id="8613c-169">Description</span><span class="sxs-lookup"><span data-stu-id="8613c-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8613c-170">200</span><span class="sxs-lookup"><span data-stu-id="8613c-170">200</span></span> |<span data-ttu-id="8613c-171">OK</span><span class="sxs-lookup"><span data-stu-id="8613c-171">OK</span></span> |
| <span data-ttu-id="8613c-172">default</span><span class="sxs-lookup"><span data-stu-id="8613c-172">default</span></span> |<span data-ttu-id="8613c-173">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="8613c-173">Operation Failed.</span></span> |

### <a name="translate-text"></a><span data-ttu-id="8613c-174">Translate text</span><span class="sxs-lookup"><span data-stu-id="8613c-174">Translate text</span></span>
<span data-ttu-id="8613c-175">Translates text to a specified language using Microsoft Translator.</span><span class="sxs-lookup"><span data-stu-id="8613c-175">Translates text to a specified language using Microsoft Translator.</span></span>  
```GET: /Translate```

| <span data-ttu-id="8613c-176">Name</span><span class="sxs-lookup"><span data-stu-id="8613c-176">Name</span></span> | <span data-ttu-id="8613c-177">Data Type</span><span class="sxs-lookup"><span data-stu-id="8613c-177">Data Type</span></span> | <span data-ttu-id="8613c-178">Required</span><span class="sxs-lookup"><span data-stu-id="8613c-178">Required</span></span> | <span data-ttu-id="8613c-179">Located In</span><span class="sxs-lookup"><span data-stu-id="8613c-179">Located In</span></span> | <span data-ttu-id="8613c-180">Default Value</span><span class="sxs-lookup"><span data-stu-id="8613c-180">Default Value</span></span> | <span data-ttu-id="8613c-181">Description</span><span class="sxs-lookup"><span data-stu-id="8613c-181">Description</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="8613c-182">query</span><span class="sxs-lookup"><span data-stu-id="8613c-182">query</span></span> |<span data-ttu-id="8613c-183">string</span><span class="sxs-lookup"><span data-stu-id="8613c-183">string</span></span> |<span data-ttu-id="8613c-184">yes</span><span class="sxs-lookup"><span data-stu-id="8613c-184">yes</span></span> |<span data-ttu-id="8613c-185">query</span><span class="sxs-lookup"><span data-stu-id="8613c-185">query</span></span> |<span data-ttu-id="8613c-186">none</span><span class="sxs-lookup"><span data-stu-id="8613c-186">none</span></span> |<span data-ttu-id="8613c-187">Text to translate</span><span class="sxs-lookup"><span data-stu-id="8613c-187">Text to translate</span></span> |
| <span data-ttu-id="8613c-188">languageTo</span><span class="sxs-lookup"><span data-stu-id="8613c-188">languageTo</span></span> |<span data-ttu-id="8613c-189">string</span><span class="sxs-lookup"><span data-stu-id="8613c-189">string</span></span> |<span data-ttu-id="8613c-190">yes</span><span class="sxs-lookup"><span data-stu-id="8613c-190">yes</span></span> |<span data-ttu-id="8613c-191">query</span><span class="sxs-lookup"><span data-stu-id="8613c-191">query</span></span> |<span data-ttu-id="8613c-192">none</span><span class="sxs-lookup"><span data-stu-id="8613c-192">none</span></span> |<span data-ttu-id="8613c-193">Target language code (example: 'fr')</span><span class="sxs-lookup"><span data-stu-id="8613c-193">Target language code (example: 'fr')</span></span> |
| <span data-ttu-id="8613c-194">languageFrom</span><span class="sxs-lookup"><span data-stu-id="8613c-194">languageFrom</span></span> |<span data-ttu-id="8613c-195">string</span><span class="sxs-lookup"><span data-stu-id="8613c-195">string</span></span> |<span data-ttu-id="8613c-196">no</span><span class="sxs-lookup"><span data-stu-id="8613c-196">no</span></span> |<span data-ttu-id="8613c-197">query</span><span class="sxs-lookup"><span data-stu-id="8613c-197">query</span></span> |<span data-ttu-id="8613c-198">none</span><span class="sxs-lookup"><span data-stu-id="8613c-198">none</span></span> |<span data-ttu-id="8613c-199">Source language; if not provided, Microsoft Translator will try to auto-detect.</span><span class="sxs-lookup"><span data-stu-id="8613c-199">Source language; if not provided, Microsoft Translator will try to auto-detect.</span></span> <span data-ttu-id="8613c-200">(example: en)</span><span class="sxs-lookup"><span data-stu-id="8613c-200">(example: en)</span></span> |
| <span data-ttu-id="8613c-201">category</span><span class="sxs-lookup"><span data-stu-id="8613c-201">category</span></span> |<span data-ttu-id="8613c-202">string</span><span class="sxs-lookup"><span data-stu-id="8613c-202">string</span></span> |<span data-ttu-id="8613c-203">no</span><span class="sxs-lookup"><span data-stu-id="8613c-203">no</span></span> |<span data-ttu-id="8613c-204">query</span><span class="sxs-lookup"><span data-stu-id="8613c-204">query</span></span> |<span data-ttu-id="8613c-205">general</span><span class="sxs-lookup"><span data-stu-id="8613c-205">general</span></span> |<span data-ttu-id="8613c-206">Translation category (default: 'general')</span><span class="sxs-lookup"><span data-stu-id="8613c-206">Translation category (default: 'general')</span></span> |

#### <a name="response"></a><span data-ttu-id="8613c-207">Response</span><span class="sxs-lookup"><span data-stu-id="8613c-207">Response</span></span>
| <span data-ttu-id="8613c-208">Name</span><span class="sxs-lookup"><span data-stu-id="8613c-208">Name</span></span> | <span data-ttu-id="8613c-209">Description</span><span class="sxs-lookup"><span data-stu-id="8613c-209">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8613c-210">200</span><span class="sxs-lookup"><span data-stu-id="8613c-210">200</span></span> |<span data-ttu-id="8613c-211">OK</span><span class="sxs-lookup"><span data-stu-id="8613c-211">OK</span></span> |
| <span data-ttu-id="8613c-212">default</span><span class="sxs-lookup"><span data-stu-id="8613c-212">default</span></span> |<span data-ttu-id="8613c-213">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="8613c-213">Operation Failed.</span></span> |

### <a name="get-languages"></a><span data-ttu-id="8613c-214">Get languages</span><span class="sxs-lookup"><span data-stu-id="8613c-214">Get languages</span></span>
<span data-ttu-id="8613c-215">Retrieves all languages that Microsoft Translator supports.</span><span class="sxs-lookup"><span data-stu-id="8613c-215">Retrieves all languages that Microsoft Translator supports.</span></span>  
```GET: /TranslatableLanguages```

<span data-ttu-id="8613c-216">There are no parameters for this call.</span><span class="sxs-lookup"><span data-stu-id="8613c-216">There are no parameters for this call.</span></span> 

#### <a name="response"></a><span data-ttu-id="8613c-217">Response</span><span class="sxs-lookup"><span data-stu-id="8613c-217">Response</span></span>
| <span data-ttu-id="8613c-218">Name</span><span class="sxs-lookup"><span data-stu-id="8613c-218">Name</span></span> | <span data-ttu-id="8613c-219">Description</span><span class="sxs-lookup"><span data-stu-id="8613c-219">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8613c-220">200</span><span class="sxs-lookup"><span data-stu-id="8613c-220">200</span></span> |<span data-ttu-id="8613c-221">OK</span><span class="sxs-lookup"><span data-stu-id="8613c-221">OK</span></span> |
| <span data-ttu-id="8613c-222">default</span><span class="sxs-lookup"><span data-stu-id="8613c-222">default</span></span> |<span data-ttu-id="8613c-223">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="8613c-223">Operation Failed.</span></span> |

### <a name="get-speech-languages"></a><span data-ttu-id="8613c-224">Get speech languages</span><span class="sxs-lookup"><span data-stu-id="8613c-224">Get speech languages</span></span>
<span data-ttu-id="8613c-225">Retrieves the languages available for speech synthesis.</span><span class="sxs-lookup"><span data-stu-id="8613c-225">Retrieves the languages available for speech synthesis.</span></span>  
```GET: /SpeakLanguages``` 

<span data-ttu-id="8613c-226">There are no parameters for this call.</span><span class="sxs-lookup"><span data-stu-id="8613c-226">There are no parameters for this call.</span></span>

#### <a name="response"></a><span data-ttu-id="8613c-227">Response</span><span class="sxs-lookup"><span data-stu-id="8613c-227">Response</span></span>
| <span data-ttu-id="8613c-228">Name</span><span class="sxs-lookup"><span data-stu-id="8613c-228">Name</span></span> | <span data-ttu-id="8613c-229">Description</span><span class="sxs-lookup"><span data-stu-id="8613c-229">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8613c-230">200</span><span class="sxs-lookup"><span data-stu-id="8613c-230">200</span></span> |<span data-ttu-id="8613c-231">OK</span><span class="sxs-lookup"><span data-stu-id="8613c-231">OK</span></span> |
| <span data-ttu-id="8613c-232">default</span><span class="sxs-lookup"><span data-stu-id="8613c-232">default</span></span> |<span data-ttu-id="8613c-233">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="8613c-233">Operation Failed.</span></span> |

## <a name="object-definitions"></a><span data-ttu-id="8613c-234">Object definitions</span><span class="sxs-lookup"><span data-stu-id="8613c-234">Object definitions</span></span>
#### <a name="language-language-model-for-microsoft-translator-translatable-languages"></a><span data-ttu-id="8613c-235">Language: language model for Microsoft Translator translatable languages</span><span class="sxs-lookup"><span data-stu-id="8613c-235">Language: language model for Microsoft Translator translatable languages</span></span>
| <span data-ttu-id="8613c-236">Property Name</span><span class="sxs-lookup"><span data-stu-id="8613c-236">Property Name</span></span> | <span data-ttu-id="8613c-237">Data Type</span><span class="sxs-lookup"><span data-stu-id="8613c-237">Data Type</span></span> | <span data-ttu-id="8613c-238">Required</span><span class="sxs-lookup"><span data-stu-id="8613c-238">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8613c-239">Code</span><span class="sxs-lookup"><span data-stu-id="8613c-239">Code</span></span> |<span data-ttu-id="8613c-240">string</span><span class="sxs-lookup"><span data-stu-id="8613c-240">string</span></span> |<span data-ttu-id="8613c-241">no</span><span class="sxs-lookup"><span data-stu-id="8613c-241">no</span></span> |
| <span data-ttu-id="8613c-242">Name</span><span class="sxs-lookup"><span data-stu-id="8613c-242">Name</span></span> |<span data-ttu-id="8613c-243">string</span><span class="sxs-lookup"><span data-stu-id="8613c-243">string</span></span> |<span data-ttu-id="8613c-244">no</span><span class="sxs-lookup"><span data-stu-id="8613c-244">no</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8613c-245">Next steps</span><span class="sxs-lookup"><span data-stu-id="8613c-245">Next steps</span></span>
<span data-ttu-id="8613c-246">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="8613c-246">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<span data-ttu-id="8613c-247">Go back to the [APIs list](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="8613c-247">Go back to the [APIs list](apis-list.md).</span></span>

<!--References-->
[5]: https://datamarket.azure.com/developer/applications/
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-microsofttranslator/register-your-application.png

