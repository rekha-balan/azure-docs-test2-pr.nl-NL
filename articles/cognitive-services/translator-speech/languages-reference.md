---
title: Microsoft Translator Speech API Languages Method | Microsoft Docs
titleSuffix: Cognitive Services
description: Use the Microsoft Translator Speech API Languages method.
services: cognitive-services
author: Jann-Skotdal
manager: chriswendt1
ms.service: cognitive-services
ms.technology: microsoft translator
ms.topic: article
ms.date: 05/18/18
ms.author: v-jansko
ms.openlocfilehash: 6952d0d38ba162c741d47d580f79e89dc5ee57f4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866934"
---
# <a name="speech-api-languages"></a><span data-ttu-id="7c1f8-103">Speech API: Languages</span><span class="sxs-lookup"><span data-stu-id="7c1f8-103">Speech API: Languages</span></span>

<span data-ttu-id="7c1f8-104">Microsoft Translator continually extends the list of languages supported by its services.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-104">Microsoft Translator continually extends the list of languages supported by its services.</span></span> <span data-ttu-id="7c1f8-105">Use this API to discover the set of languages currently available for use with the Speech Translation service.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-105">Use this API to discover the set of languages currently available for use with the Speech Translation service.</span></span>

<span data-ttu-id="7c1f8-106">Code samples demonstrating use of the API to get available languages are available from the [Microsoft Translator Github site](https://github.com/MicrosoftTranslator).</span><span class="sxs-lookup"><span data-stu-id="7c1f8-106">Code samples demonstrating use of the API to get available languages are available from the [Microsoft Translator Github site](https://github.com/MicrosoftTranslator).</span></span>

## <a name="implementation-notes"></a><span data-ttu-id="7c1f8-107">Implementation notes</span><span class="sxs-lookup"><span data-stu-id="7c1f8-107">Implementation notes</span></span>

<span data-ttu-id="7c1f8-108">GET /languages</span><span class="sxs-lookup"><span data-stu-id="7c1f8-108">GET /languages</span></span> 

<span data-ttu-id="7c1f8-109">A wide set of languages is available to transcribe speech, to translate the transcribed text, and to produce synthesized speech of the translation.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-109">A wide set of languages is available to transcribe speech, to translate the transcribed text, and to produce synthesized speech of the translation.</span></span>

<span data-ttu-id="7c1f8-110">A client uses the `scope` query parameter to define which sets of languages it is interested in.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-110">A client uses the `scope` query parameter to define which sets of languages it is interested in.</span></span>

* <span data-ttu-id="7c1f8-111">**Speech-to-text:** Use query parameter `scope=speech` to retrieve the set of languages available to transcribe speech into text.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-111">**Speech-to-text:** Use query parameter `scope=speech` to retrieve the set of languages available to transcribe speech into text.</span></span>
* <span data-ttu-id="7c1f8-112">**Text translation:** Use query parameter `scope=text` to retrieve the set of languages available to translate transcribed text.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-112">**Text translation:** Use query parameter `scope=text` to retrieve the set of languages available to translate transcribed text.</span></span>
* <span data-ttu-id="7c1f8-113">**Text-to-speech:**  Use query parameter `scope=tts` to retrieve the set of languages and voices available to synthesize translated text back into speech.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-113">**Text-to-speech:**  Use query parameter `scope=tts` to retrieve the set of languages and voices available to synthesize translated text back into speech.</span></span>

<span data-ttu-id="7c1f8-114">A client can retrieve multiple sets simultaneously by specifying a comma-separated list of choices.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-114">A client can retrieve multiple sets simultaneously by specifying a comma-separated list of choices.</span></span> <span data-ttu-id="7c1f8-115">For example, `scope=speech,text,tts`.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-115">For example, `scope=speech,text,tts`.</span></span>

<span data-ttu-id="7c1f8-116">A successful response is a JSON object with a property for each requested set.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-116">A successful response is a JSON object with a property for each requested set.</span></span>

```
{
    "speech": {
        //... Set of languages supported for speech-to-text
    },
    "text": {
        //... Set of languages supported for text translation
    },
    "tts": {
        //... Set of languages supported for text-to-speech
    }
}
```

<span data-ttu-id="7c1f8-117">Since a client can use the `scope` query parameter to select which sets of supported languages should be returned, an actual response may only include a subset of all properties shown above.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-117">Since a client can use the `scope` query parameter to select which sets of supported languages should be returned, an actual response may only include a subset of all properties shown above.</span></span>

<span data-ttu-id="7c1f8-118">The value provided with each property is as follows.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-118">The value provided with each property is as follows.</span></span>

### <a name="speech-to-text-speech"></a><span data-ttu-id="7c1f8-119">Speech-to-text (speech)</span><span class="sxs-lookup"><span data-stu-id="7c1f8-119">Speech-to-text (speech)</span></span>

<span data-ttu-id="7c1f8-120">The value associated with the speech-to-text property, `speech`, is a dictionary of (key, value) pairs.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-120">The value associated with the speech-to-text property, `speech`, is a dictionary of (key, value) pairs.</span></span> <span data-ttu-id="7c1f8-121">Each key identifies a language supported for speech-to-text.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-121">Each key identifies a language supported for speech-to-text.</span></span> <span data-ttu-id="7c1f8-122">The key is the identifier that client passes to the API.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-122">The key is the identifier that client passes to the API.</span></span> <span data-ttu-id="7c1f8-123">The value associated with the key is an object with the following properties:</span><span class="sxs-lookup"><span data-stu-id="7c1f8-123">The value associated with the key is an object with the following properties:</span></span>

* <span data-ttu-id="7c1f8-124">`name`: Display name of the language.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-124">`name`: Display name of the language.</span></span>
* <span data-ttu-id="7c1f8-125">`language`: Language tag of the associated written language.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-125">`language`: Language tag of the associated written language.</span></span> <span data-ttu-id="7c1f8-126">See "Text transation" below.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-126">See "Text transation" below.</span></span>
<span data-ttu-id="7c1f8-127">An example is:</span><span class="sxs-lookup"><span data-stu-id="7c1f8-127">An example is:</span></span>

```
{
    "speech": {
        "en-US": { name: "English", language: "en" }
    }
}
```

### <a name="text-translation-text"></a><span data-ttu-id="7c1f8-128">Text translation (text)</span><span class="sxs-lookup"><span data-stu-id="7c1f8-128">Text translation (text)</span></span>

<span data-ttu-id="7c1f8-129">The value associated with the `text` property is also a dictionary where each key identifies a language supported for text translation.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-129">The value associated with the `text` property is also a dictionary where each key identifies a language supported for text translation.</span></span> <span data-ttu-id="7c1f8-130">The value associated with the key describes the language:</span><span class="sxs-lookup"><span data-stu-id="7c1f8-130">The value associated with the key describes the language:</span></span>

* <span data-ttu-id="7c1f8-131">`name`: Display name of the language.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-131">`name`: Display name of the language.</span></span>
* <span data-ttu-id="7c1f8-132">`dir`: Directionality which is `rtl` for right-to-left languages or `ltr` for left-to-right languages.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-132">`dir`: Directionality which is `rtl` for right-to-left languages or `ltr` for left-to-right languages.</span></span>

<span data-ttu-id="7c1f8-133">An example is:</span><span class="sxs-lookup"><span data-stu-id="7c1f8-133">An example is:</span></span>

```
{
    "text": {
        "en": { name: "English", dir: "ltr" }
    }
}
```

### <a name="text-to-speech-tts"></a><span data-ttu-id="7c1f8-134">Text-to-speech (tts)</span><span class="sxs-lookup"><span data-stu-id="7c1f8-134">Text-to-speech (tts)</span></span>

<span data-ttu-id="7c1f8-135">The value associated with the text-to-speech property, tts, is also a dictionary where each key identifies a supported voice.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-135">The value associated with the text-to-speech property, tts, is also a dictionary where each key identifies a supported voice.</span></span> <span data-ttu-id="7c1f8-136">Attributes of a voice object are:</span><span class="sxs-lookup"><span data-stu-id="7c1f8-136">Attributes of a voice object are:</span></span>

* <span data-ttu-id="7c1f8-137">`displayName`: Display name for the voice.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-137">`displayName`: Display name for the voice.</span></span>
* <span data-ttu-id="7c1f8-138">`gender`: Gender of the voice (male or female).</span><span class="sxs-lookup"><span data-stu-id="7c1f8-138">`gender`: Gender of the voice (male or female).</span></span>
* <span data-ttu-id="7c1f8-139">`locale`: Language tag of the voice with primary language subtag and region subtag.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-139">`locale`: Language tag of the voice with primary language subtag and region subtag.</span></span>
* <span data-ttu-id="7c1f8-140">`language`: Language tag of the associated written language.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-140">`language`: Language tag of the associated written language.</span></span>
* <span data-ttu-id="7c1f8-141">`languageName`: Display name of the language.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-141">`languageName`: Display name of the language.</span></span>
* <span data-ttu-id="7c1f8-142">`regionName`: Display name of the region for this language.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-142">`regionName`: Display name of the region for this language.</span></span>

<span data-ttu-id="7c1f8-143">An example is:</span><span class="sxs-lookup"><span data-stu-id="7c1f8-143">An example is:</span></span>

```
{
    "tts": {
        "en-US-Zira": {
            "displayName": "Zira",
            "gender": "female",
            "locale": "en-US",
            "languageName": "English",
            "regionName": "United States",
            "language": "en"
        }
}
```

### <a name="localization"></a><span data-ttu-id="7c1f8-144">Localization</span><span class="sxs-lookup"><span data-stu-id="7c1f8-144">Localization</span></span>
<span data-ttu-id="7c1f8-145">The service returns all names in the language of the 'Accept-Language' header, for all the languages supported in text translation.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-145">The service returns all names in the language of the 'Accept-Language' header, for all the languages supported in text translation.</span></span>

### <a name="response-class-status-200"></a><span data-ttu-id="7c1f8-146">Response class (Status 200)</span><span class="sxs-lookup"><span data-stu-id="7c1f8-146">Response class (Status 200)</span></span>
<span data-ttu-id="7c1f8-147">Object describing the set of supported languages.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-147">Object describing the set of supported languages.</span></span>

<span data-ttu-id="7c1f8-148">ModelExample Value:</span><span class="sxs-lookup"><span data-stu-id="7c1f8-148">ModelExample Value:</span></span> 

<span data-ttu-id="7c1f8-149">Langagues { speech (object, optional), text (object, optional), tts (object, optional) }</span><span class="sxs-lookup"><span data-stu-id="7c1f8-149">Langagues { speech (object, optional), text (object, optional), tts (object, optional) }</span></span>

### <a name="headers"></a><span data-ttu-id="7c1f8-150">Headers</span><span class="sxs-lookup"><span data-stu-id="7c1f8-150">Headers</span></span>

|<span data-ttu-id="7c1f8-151">Header</span><span class="sxs-lookup"><span data-stu-id="7c1f8-151">Header</span></span>|<span data-ttu-id="7c1f8-152">Description</span><span class="sxs-lookup"><span data-stu-id="7c1f8-152">Description</span></span>|<span data-ttu-id="7c1f8-153">Type</span><span class="sxs-lookup"><span data-stu-id="7c1f8-153">Type</span></span>|
:--|:--|:--|
<span data-ttu-id="7c1f8-154">X-RequestId</span><span class="sxs-lookup"><span data-stu-id="7c1f8-154">X-RequestId</span></span>|<span data-ttu-id="7c1f8-155">Value generated by server to identify the request and used for troubleshooting purposes.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-155">Value generated by server to identify the request and used for troubleshooting purposes.</span></span>|<span data-ttu-id="7c1f8-156">string</span><span class="sxs-lookup"><span data-stu-id="7c1f8-156">string</span></span>|

### <a name="parameters"></a><span data-ttu-id="7c1f8-157">Parameters</span><span class="sxs-lookup"><span data-stu-id="7c1f8-157">Parameters</span></span>

|<span data-ttu-id="7c1f8-158">Parameter</span><span class="sxs-lookup"><span data-stu-id="7c1f8-158">Parameter</span></span>|<span data-ttu-id="7c1f8-159">Description</span><span class="sxs-lookup"><span data-stu-id="7c1f8-159">Description</span></span>|<span data-ttu-id="7c1f8-160">Parameter Type</span><span class="sxs-lookup"><span data-stu-id="7c1f8-160">Parameter Type</span></span>|<span data-ttu-id="7c1f8-161">Data Type</span><span class="sxs-lookup"><span data-stu-id="7c1f8-161">Data Type</span></span>|
|:--|:--|:--|:--|
|<span data-ttu-id="7c1f8-162">api-version</span><span class="sxs-lookup"><span data-stu-id="7c1f8-162">api-version</span></span>    |<span data-ttu-id="7c1f8-163">Version of the API requested by the client.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-163">Version of the API requested by the client.</span></span> <span data-ttu-id="7c1f8-164">Allowed values are: `1.0`.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-164">Allowed values are: `1.0`.</span></span>|<span data-ttu-id="7c1f8-165">query</span><span class="sxs-lookup"><span data-stu-id="7c1f8-165">query</span></span>|<span data-ttu-id="7c1f8-166">string</span><span class="sxs-lookup"><span data-stu-id="7c1f8-166">string</span></span>|
|<span data-ttu-id="7c1f8-167">scope</span><span class="sxs-lookup"><span data-stu-id="7c1f8-167">scope</span></span>  |<span data-ttu-id="7c1f8-168">Sets of supported languages or voices to return to the client.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-168">Sets of supported languages or voices to return to the client.</span></span> <span data-ttu-id="7c1f8-169">This parameter is specified as a comma-separated list of keywords.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-169">This parameter is specified as a comma-separated list of keywords.</span></span> <span data-ttu-id="7c1f8-170">The following keywords are available:</span><span class="sxs-lookup"><span data-stu-id="7c1f8-170">The following keywords are available:</span></span><ul><li><span data-ttu-id="7c1f8-171">`speech`: Provides the set of languages supported to transcribe speech.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-171">`speech`: Provides the set of languages supported to transcribe speech.</span></span></li><li><span data-ttu-id="7c1f8-172">`tts`: Provides the set of voices supported for text-speech conversion.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-172">`tts`: Provides the set of voices supported for text-speech conversion.</span></span></li><li><span data-ttu-id="7c1f8-173">`text`: Provides the set of languages supported for translating text.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-173">`text`: Provides the set of languages supported for translating text.</span></span></li></ul><span data-ttu-id="7c1f8-174">If a value is not specified, the value of `scope` defaults to  `text`.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-174">If a value is not specified, the value of `scope` defaults to  `text`.</span></span>|<span data-ttu-id="7c1f8-175">query</span><span class="sxs-lookup"><span data-stu-id="7c1f8-175">query</span></span>|<span data-ttu-id="7c1f8-176">string</span><span class="sxs-lookup"><span data-stu-id="7c1f8-176">string</span></span>|
|<span data-ttu-id="7c1f8-177">X-ClientTraceId</span><span class="sxs-lookup"><span data-stu-id="7c1f8-177">X-ClientTraceId</span></span>    |<span data-ttu-id="7c1f8-178">A client-generated GUID used to trace a request.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-178">A client-generated GUID used to trace a request.</span></span> <span data-ttu-id="7c1f8-179">To facilitate troubleshooting of issues, clients should provide a new value with each request and log it.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-179">To facilitate troubleshooting of issues, clients should provide a new value with each request and log it.</span></span>|<span data-ttu-id="7c1f8-180">header</span><span class="sxs-lookup"><span data-stu-id="7c1f8-180">header</span></span>|<span data-ttu-id="7c1f8-181">string</span><span class="sxs-lookup"><span data-stu-id="7c1f8-181">string</span></span>|
|<span data-ttu-id="7c1f8-182">Accept-Language</span><span class="sxs-lookup"><span data-stu-id="7c1f8-182">Accept-Language</span></span>    |<span data-ttu-id="7c1f8-183">Some of the fields in the response are names of languages or regions.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-183">Some of the fields in the response are names of languages or regions.</span></span> <span data-ttu-id="7c1f8-184">Use this parameter to define the language in which names are returned.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-184">Use this parameter to define the language in which names are returned.</span></span> <span data-ttu-id="7c1f8-185">The language is specified by providing a well-formed BCP 47 language tag.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-185">The language is specified by providing a well-formed BCP 47 language tag.</span></span> <span data-ttu-id="7c1f8-186">Select a tag from the list of language identifiers returned with the `text` scope.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-186">Select a tag from the list of language identifiers returned with the `text` scope.</span></span> <span data-ttu-id="7c1f8-187">For unsupported languages, the names are provided in the English language.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-187">For unsupported languages, the names are provided in the English language.</span></span><br/><span data-ttu-id="7c1f8-188">For instance, use the value `fr` to request names in French or use the value `zh-Hant` to request names in Chinese Traditional.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-188">For instance, use the value `fr` to request names in French or use the value `zh-Hant` to request names in Chinese Traditional.</span></span>|<span data-ttu-id="7c1f8-189">header</span><span class="sxs-lookup"><span data-stu-id="7c1f8-189">header</span></span>|<span data-ttu-id="7c1f8-190">string</span><span class="sxs-lookup"><span data-stu-id="7c1f8-190">string</span></span>|
    
### <a name="response-messages"></a><span data-ttu-id="7c1f8-191">Response messages</span><span class="sxs-lookup"><span data-stu-id="7c1f8-191">Response messages</span></span>

|<span data-ttu-id="7c1f8-192">HTTP Status Code</span><span class="sxs-lookup"><span data-stu-id="7c1f8-192">HTTP Status Code</span></span>|<span data-ttu-id="7c1f8-193">Reason</span><span class="sxs-lookup"><span data-stu-id="7c1f8-193">Reason</span></span>|
|:--|:--|
|<span data-ttu-id="7c1f8-194">400</span><span class="sxs-lookup"><span data-stu-id="7c1f8-194">400</span></span>|<span data-ttu-id="7c1f8-195">Bad request.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-195">Bad request.</span></span> <span data-ttu-id="7c1f8-196">Check input parameters to ensure they are valid.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-196">Check input parameters to ensure they are valid.</span></span> <span data-ttu-id="7c1f8-197">The response object includes a more detailed description of the error.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-197">The response object includes a more detailed description of the error.</span></span>|
|<span data-ttu-id="7c1f8-198">429</span><span class="sxs-lookup"><span data-stu-id="7c1f8-198">429</span></span>|<span data-ttu-id="7c1f8-199">Too many requests.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-199">Too many requests.</span></span>|
|<span data-ttu-id="7c1f8-200">500</span><span class="sxs-lookup"><span data-stu-id="7c1f8-200">500</span></span>|<span data-ttu-id="7c1f8-201">An error occured.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-201">An error occured.</span></span> <span data-ttu-id="7c1f8-202">If the error persists, please report it with client trace identifier (X-ClientTraceId) or request identifier (X-RequestId).</span><span class="sxs-lookup"><span data-stu-id="7c1f8-202">If the error persists, please report it with client trace identifier (X-ClientTraceId) or request identifier (X-RequestId).</span></span>|
|<span data-ttu-id="7c1f8-203">503</span><span class="sxs-lookup"><span data-stu-id="7c1f8-203">503</span></span>|<span data-ttu-id="7c1f8-204">Server temporarily unavailable.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-204">Server temporarily unavailable.</span></span> <span data-ttu-id="7c1f8-205">Please retry the request.</span><span class="sxs-lookup"><span data-stu-id="7c1f8-205">Please retry the request.</span></span> <span data-ttu-id="7c1f8-206">If the error persists, please report it with client trace identifier (X-ClientTraceId) or request identifier (X-RequestId).</span><span class="sxs-lookup"><span data-stu-id="7c1f8-206">If the error persists, please report it with client trace identifier (X-ClientTraceId) or request identifier (X-RequestId).</span></span>|
