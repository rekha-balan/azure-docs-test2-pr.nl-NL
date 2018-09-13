---
title: Microsoft Translator Text API Languages Method | Microsoft Docs
description: Use the Microsoft Translator Text API Languages method.
services: cognitive-services
author: Jann-Skotdal
manager: chriswendt1
ms.service: cognitive-services
ms.technology: microsoft translator
ms.topic: article
ms.date: 03/29/2018
ms.author: v-jansko
ms.openlocfilehash: 93c06218a560faf439f05903438d021b372ce257
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867001"
---
# <a name="text-api-30-languages"></a><span data-ttu-id="e9d4c-103">Text API 3.0: Languages</span><span class="sxs-lookup"><span data-stu-id="e9d4c-103">Text API 3.0: Languages</span></span>

<span data-ttu-id="e9d4c-104">Gets the set of languages currently supported by other operations of the Text API.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-104">Gets the set of languages currently supported by other operations of the Text API.</span></span> 

## <a name="request-url"></a><span data-ttu-id="e9d4c-105">Request URL</span><span class="sxs-lookup"><span data-stu-id="e9d4c-105">Request URL</span></span>

<span data-ttu-id="e9d4c-106">Send a `GET` request to:</span><span class="sxs-lookup"><span data-stu-id="e9d4c-106">Send a `GET` request to:</span></span>
```HTTP
https://api.cognitive.microsofttranslator.com/languages?api-version=3.0
```

## <a name="request-parameters"></a><span data-ttu-id="e9d4c-107">Request parameters</span><span class="sxs-lookup"><span data-stu-id="e9d4c-107">Request parameters</span></span>

<span data-ttu-id="e9d4c-108">Request parameters passed on the query string are:</span><span class="sxs-lookup"><span data-stu-id="e9d4c-108">Request parameters passed on the query string are:</span></span>

<table width="100%">
  <th width="20%"><span data-ttu-id="e9d4c-109">Query parameter</span><span class="sxs-lookup"><span data-stu-id="e9d4c-109">Query parameter</span></span></th>
  <th><span data-ttu-id="e9d4c-110">Description</span><span class="sxs-lookup"><span data-stu-id="e9d4c-110">Description</span></span></th>
  <tr>
    <td><span data-ttu-id="e9d4c-111">api-version</span><span class="sxs-lookup"><span data-stu-id="e9d4c-111">api-version</span></span></td>
    <td><span data-ttu-id="e9d4c-112">*Required parameter*.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-112">*Required parameter*.</span></span><br/><span data-ttu-id="e9d4c-113">Version of the API requested by the client.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-113">Version of the API requested by the client.</span></span> <span data-ttu-id="e9d4c-114">Value must be `3.0`.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-114">Value must be `3.0`.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="e9d4c-115">scope</span><span class="sxs-lookup"><span data-stu-id="e9d4c-115">scope</span></span></td>
    <td><span data-ttu-id="e9d4c-116">*Optional parameter*.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-116">*Optional parameter*.</span></span><br/><span data-ttu-id="e9d4c-117">A comma-separated list of names defining the group of languages to return.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-117">A comma-separated list of names defining the group of languages to return.</span></span> <span data-ttu-id="e9d4c-118">Allowed group names are: `translation`, `transliteration` and `dictionary`.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-118">Allowed group names are: `translation`, `transliteration` and `dictionary`.</span></span> <span data-ttu-id="e9d4c-119">If no scope is given, then all groups are returned, which is equivalent to passing `scope=translation,transliteration,dictionary`.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-119">If no scope is given, then all groups are returned, which is equivalent to passing `scope=translation,transliteration,dictionary`.</span></span> <span data-ttu-id="e9d4c-120">To decide which set of supported languages is appropriate for your scenario, see the description of the [response object](#response-body).</span><span class="sxs-lookup"><span data-stu-id="e9d4c-120">To decide which set of supported languages is appropriate for your scenario, see the description of the [response object](#response-body).</span></span></td>
  </tr>
</table> 

<span data-ttu-id="e9d4c-121">Request headers are:</span><span class="sxs-lookup"><span data-stu-id="e9d4c-121">Request headers are:</span></span>

<table width="100%">
  <th width="20%"><span data-ttu-id="e9d4c-122">Headers</span><span class="sxs-lookup"><span data-stu-id="e9d4c-122">Headers</span></span></th>
  <th><span data-ttu-id="e9d4c-123">Description</span><span class="sxs-lookup"><span data-stu-id="e9d4c-123">Description</span></span></th>
  <tr>
    <td><span data-ttu-id="e9d4c-124">Accept-Language</span><span class="sxs-lookup"><span data-stu-id="e9d4c-124">Accept-Language</span></span></td>
    <td><span data-ttu-id="e9d4c-125">*Optional request header*.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-125">*Optional request header*.</span></span><br/><span data-ttu-id="e9d4c-126">The language to use for user interface strings.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-126">The language to use for user interface strings.</span></span> <span data-ttu-id="e9d4c-127">Some of the fields in the response are names of languages or names of regions.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-127">Some of the fields in the response are names of languages or names of regions.</span></span> <span data-ttu-id="e9d4c-128">Use this parameter to define the language in which these names are returned.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-128">Use this parameter to define the language in which these names are returned.</span></span> <span data-ttu-id="e9d4c-129">The language is specified by providing a well-formed BCP 47 language tag.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-129">The language is specified by providing a well-formed BCP 47 language tag.</span></span> <span data-ttu-id="e9d4c-130">For instance, use the value `fr` to request names in French or use the value `zh-Hant` to request names in Chinese Traditional.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-130">For instance, use the value `fr` to request names in French or use the value `zh-Hant` to request names in Chinese Traditional.</span></span><br/><span data-ttu-id="e9d4c-131">Names are provided in the English language when a target language is not specified or when localization is not available.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-131">Names are provided in the English language when a target language is not specified or when localization is not available.</span></span>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="e9d4c-132">X-ClientTraceId</span><span class="sxs-lookup"><span data-stu-id="e9d4c-132">X-ClientTraceId</span></span></td>
    <td><span data-ttu-id="e9d4c-133">*Optional request header*.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-133">*Optional request header*.</span></span><br/><span data-ttu-id="e9d4c-134">A client-generated GUID to uniquely identify the request.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-134">A client-generated GUID to uniquely identify the request.</span></span></td>
  </tr>
</table> 

<span data-ttu-id="e9d4c-135">Authentication isn't required to get language resources.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-135">Authentication isn't required to get language resources.</span></span>

## <a name="response-body"></a><span data-ttu-id="e9d4c-136">Response body</span><span class="sxs-lookup"><span data-stu-id="e9d4c-136">Response body</span></span>

<span data-ttu-id="e9d4c-137">A client uses the `scope` query parameter to define which groups of languages it's interested in.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-137">A client uses the `scope` query parameter to define which groups of languages it's interested in.</span></span>

* <span data-ttu-id="e9d4c-138">`scope=translation` provides languages supported to translate text from one language to another language;</span><span class="sxs-lookup"><span data-stu-id="e9d4c-138">`scope=translation` provides languages supported to translate text from one language to another language;</span></span>

* <span data-ttu-id="e9d4c-139">`scope=transliteration` provides capabilities for converting text in one language from one script to another script;</span><span class="sxs-lookup"><span data-stu-id="e9d4c-139">`scope=transliteration` provides capabilities for converting text in one language from one script to another script;</span></span>

* <span data-ttu-id="e9d4c-140">`scope=dictionary` provides language pairs for which `Dictionary` operations return data.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-140">`scope=dictionary` provides language pairs for which `Dictionary` operations return data.</span></span>

<span data-ttu-id="e9d4c-141">A client may retrieve several groups simultaneously by specifying a comma-separated list of names.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-141">A client may retrieve several groups simultaneously by specifying a comma-separated list of names.</span></span> <span data-ttu-id="e9d4c-142">For example, `scope=translation,transliteration,dictionary` would return supported languages for all groups.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-142">For example, `scope=translation,transliteration,dictionary` would return supported languages for all groups.</span></span>

<span data-ttu-id="e9d4c-143">A successful response is a JSON object with one property for each requested group:</span><span class="sxs-lookup"><span data-stu-id="e9d4c-143">A successful response is a JSON object with one property for each requested group:</span></span>

```json
{
    "translation": {
        //... set of languages supported to translate text (scope=translation)
    },
    "transliteration": {
        //... set of languages supported to convert between scripts (scope=transliteration)
    },
    "dictionary": {
        //... set of languages supported for alternative translations and examples (scope=dictionary)
    }
}
```

<span data-ttu-id="e9d4c-144">The value for each property is as follows.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-144">The value for each property is as follows.</span></span>

* <span data-ttu-id="e9d4c-145">`translation` property</span><span class="sxs-lookup"><span data-stu-id="e9d4c-145">`translation` property</span></span>

  <span data-ttu-id="e9d4c-146">The value of the `translation` property is a dictionary of (key, value) pairs.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-146">The value of the `translation` property is a dictionary of (key, value) pairs.</span></span> <span data-ttu-id="e9d4c-147">Each key is a BCP 47 language tag.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-147">Each key is a BCP 47 language tag.</span></span> <span data-ttu-id="e9d4c-148">A key identifies a language for which text can be translated to or translated from.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-148">A key identifies a language for which text can be translated to or translated from.</span></span> <span data-ttu-id="e9d4c-149">The value associated with the key is a JSON object with properties that describe the language:</span><span class="sxs-lookup"><span data-stu-id="e9d4c-149">The value associated with the key is a JSON object with properties that describe the language:</span></span>

  * <span data-ttu-id="e9d4c-150">`name`: Display name of the language in the locale requested via `Accept-Language` header.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-150">`name`: Display name of the language in the locale requested via `Accept-Language` header.</span></span>

  * <span data-ttu-id="e9d4c-151">`nativeName`: Display name of the language in the locale native for this language.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-151">`nativeName`: Display name of the language in the locale native for this language.</span></span>

  * <span data-ttu-id="e9d4c-152">`dir`: Directionality, which is `rtl` for right-to-left languages or `ltr` for left-to-right languages.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-152">`dir`: Directionality, which is `rtl` for right-to-left languages or `ltr` for left-to-right languages.</span></span>

  <span data-ttu-id="e9d4c-153">An example is:</span><span class="sxs-lookup"><span data-stu-id="e9d4c-153">An example is:</span></span>
          
  ```json
  {
    "translation": {
      ...
      "fr": {
        "name": "French",
        "nativeName": "Français",
        "dir": "ltr"
      },
      ...
    }
  }
  ```

* <span data-ttu-id="e9d4c-154">`transliteration` property</span><span class="sxs-lookup"><span data-stu-id="e9d4c-154">`transliteration` property</span></span>

  <span data-ttu-id="e9d4c-155">The value of the `transliteration` property is a dictionary of (key, value) pairs.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-155">The value of the `transliteration` property is a dictionary of (key, value) pairs.</span></span> <span data-ttu-id="e9d4c-156">Each key is a BCP 47 language tag.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-156">Each key is a BCP 47 language tag.</span></span> <span data-ttu-id="e9d4c-157">A key identifies a language for which text can be converted from one script to another script.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-157">A key identifies a language for which text can be converted from one script to another script.</span></span> <span data-ttu-id="e9d4c-158">The value associated with the key is a JSON object with properties that describe the language and its supported scripts:</span><span class="sxs-lookup"><span data-stu-id="e9d4c-158">The value associated with the key is a JSON object with properties that describe the language and its supported scripts:</span></span>

  * <span data-ttu-id="e9d4c-159">`name`: Display name of the language in the locale requested via `Accept-Language` header.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-159">`name`: Display name of the language in the locale requested via `Accept-Language` header.</span></span>

  * <span data-ttu-id="e9d4c-160">`nativeName`: Display name of the language in the locale native for this language.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-160">`nativeName`: Display name of the language in the locale native for this language.</span></span>

  * <span data-ttu-id="e9d4c-161">`scripts`: List of scripts to convert from.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-161">`scripts`: List of scripts to convert from.</span></span> <span data-ttu-id="e9d4c-162">Each element of the `scripts` list has properties:</span><span class="sxs-lookup"><span data-stu-id="e9d4c-162">Each element of the `scripts` list has properties:</span></span>

    * <span data-ttu-id="e9d4c-163">`code`: Code identifying the script.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-163">`code`: Code identifying the script.</span></span>

    * <span data-ttu-id="e9d4c-164">`name`: Display name of the script in the locale requested via `Accept-Language` header.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-164">`name`: Display name of the script in the locale requested via `Accept-Language` header.</span></span>

    * <span data-ttu-id="e9d4c-165">`nativeName`: Display name of the language in the locale native for the language.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-165">`nativeName`: Display name of the language in the locale native for the language.</span></span>

    * <span data-ttu-id="e9d4c-166">`dir`: Directionality, which is `rtl` for right-to-left languages or `ltr` for left-to-right languages.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-166">`dir`: Directionality, which is `rtl` for right-to-left languages or `ltr` for left-to-right languages.</span></span>

    * <span data-ttu-id="e9d4c-167">`toScripts`: List of scripts available to convert text to.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-167">`toScripts`: List of scripts available to convert text to.</span></span> <span data-ttu-id="e9d4c-168">Each element of the `toScripts` list has properties `code`, `name`, `nativeName`, and `dir` as described earlier.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-168">Each element of the `toScripts` list has properties `code`, `name`, `nativeName`, and `dir` as described earlier.</span></span>

  <span data-ttu-id="e9d4c-169">An example is:</span><span class="sxs-lookup"><span data-stu-id="e9d4c-169">An example is:</span></span>

  ```json
  {
    "transliteration": {
      ...
      "ja": {
        "name": "Japanese",
        "nativeName": "日本語",
        "scripts": [
          {
            "code": "Jpan",
            "name": "Japanese",
            "nativeName": "日本語",
            "dir": "ltr",
            "toScripts": [
              {
                "code": "Latn",
                "name": "Latin",
                "nativeName": "ラテン語",
                "dir": "ltr"
              }
            ]
          },
          {
            "code": "Latn",
            "name": "Latin",
            "nativeName": "ラテン語",
            "dir": "ltr",
            "toScripts": [
              {
                "code": "Jpan",
                "name": "Japanese",
                "nativeName": "日本語",
                "dir": "ltr"
              }
            ]
          }
        ]
      },
      ...
    }
  }
  ```

* <span data-ttu-id="e9d4c-170">`dictionary` property</span><span class="sxs-lookup"><span data-stu-id="e9d4c-170">`dictionary` property</span></span>

  <span data-ttu-id="e9d4c-171">The value of the `dictionary` property is a dictionary of (key, value) pairs.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-171">The value of the `dictionary` property is a dictionary of (key, value) pairs.</span></span> <span data-ttu-id="e9d4c-172">Each key is a BCP 47 language tag.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-172">Each key is a BCP 47 language tag.</span></span> <span data-ttu-id="e9d4c-173">The key identifies a language for which alternative translations and back-translations are available.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-173">The key identifies a language for which alternative translations and back-translations are available.</span></span> <span data-ttu-id="e9d4c-174">The value is a JSON object that describes the source language and the target languages with available translations:</span><span class="sxs-lookup"><span data-stu-id="e9d4c-174">The value is a JSON object that describes the source language and the target languages with available translations:</span></span>

  * <span data-ttu-id="e9d4c-175">`name`: Display name of the source language in the locale requested via `Accept-Language` header.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-175">`name`: Display name of the source language in the locale requested via `Accept-Language` header.</span></span>

  * <span data-ttu-id="e9d4c-176">`nativeName`: Display name of the language in the locale native for this language.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-176">`nativeName`: Display name of the language in the locale native for this language.</span></span>

  * <span data-ttu-id="e9d4c-177">`dir`: Directionality, which is `rtl` for right-to-left languages or `ltr` for left-to-right languages.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-177">`dir`: Directionality, which is `rtl` for right-to-left languages or `ltr` for left-to-right languages.</span></span>

  * <span data-ttu-id="e9d4c-178">`translations`: List of languages with alterative translations and examples for the query expressed in the source language.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-178">`translations`: List of languages with alterative translations and examples for the query expressed in the source language.</span></span> <span data-ttu-id="e9d4c-179">Each element of the `translations` list has properties:</span><span class="sxs-lookup"><span data-stu-id="e9d4c-179">Each element of the `translations` list has properties:</span></span>

    * <span data-ttu-id="e9d4c-180">`name`: Display name of the target language in the locale requested via `Accept-Language` header.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-180">`name`: Display name of the target language in the locale requested via `Accept-Language` header.</span></span>

    * <span data-ttu-id="e9d4c-181">`nativeName`: Display name of the target language in the locale native for the target language.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-181">`nativeName`: Display name of the target language in the locale native for the target language.</span></span>

    * <span data-ttu-id="e9d4c-182">`dir`: Directionality, which is `rtl` for right-to-left languages or `ltr` for left-to-right languages.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-182">`dir`: Directionality, which is `rtl` for right-to-left languages or `ltr` for left-to-right languages.</span></span>
    
    * <span data-ttu-id="e9d4c-183">`code`: Language code identifying the target language.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-183">`code`: Language code identifying the target language.</span></span>

  <span data-ttu-id="e9d4c-184">An example is:</span><span class="sxs-lookup"><span data-stu-id="e9d4c-184">An example is:</span></span>

  ```json
  "es": {
    "name": "Spanish",
    "nativeName": "Español",
    "dir": "ltr",
    "translations": [
      {
        "name": "English",
        "nativeName": "English",
        "dir": "ltr",
        "code": "en"
      }
    ]
  },
  ```

<span data-ttu-id="e9d4c-185">The structure of the response object will not change without a change in the version of the API.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-185">The structure of the response object will not change without a change in the version of the API.</span></span> <span data-ttu-id="e9d4c-186">For the same version of the API, the list of available languages may change over time because Microsoft Translator continually extends the list of languages supported by its services.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-186">For the same version of the API, the list of available languages may change over time because Microsoft Translator continually extends the list of languages supported by its services.</span></span>

<span data-ttu-id="e9d4c-187">The list of supported languages will not change frequently.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-187">The list of supported languages will not change frequently.</span></span> <span data-ttu-id="e9d4c-188">To save network bandwidth and improve responsiveness, a client application should consider caching language resources and the corresponding entity tag (`ETag`).</span><span class="sxs-lookup"><span data-stu-id="e9d4c-188">To save network bandwidth and improve responsiveness, a client application should consider caching language resources and the corresponding entity tag (`ETag`).</span></span> <span data-ttu-id="e9d4c-189">Then, the client application can periodically (for example, once every 24 hours) query the service to fetch the latest set of supported languages.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-189">Then, the client application can periodically (for example, once every 24 hours) query the service to fetch the latest set of supported languages.</span></span> <span data-ttu-id="e9d4c-190">Passing the current `ETag` value in an `If-None-Match` header field will allow the service to optimize the response.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-190">Passing the current `ETag` value in an `If-None-Match` header field will allow the service to optimize the response.</span></span> <span data-ttu-id="e9d4c-191">If the resource has not been modified, the service will return status code 304 and an empty response body.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-191">If the resource has not been modified, the service will return status code 304 and an empty response body.</span></span>

## <a name="response-headers"></a><span data-ttu-id="e9d4c-192">Response headers</span><span class="sxs-lookup"><span data-stu-id="e9d4c-192">Response headers</span></span>

<table width="100%">
  <th width="20%"><span data-ttu-id="e9d4c-193">Headers</span><span class="sxs-lookup"><span data-stu-id="e9d4c-193">Headers</span></span></th>
  <th><span data-ttu-id="e9d4c-194">Description</span><span class="sxs-lookup"><span data-stu-id="e9d4c-194">Description</span></span></th>
  <tr>
    <td><span data-ttu-id="e9d4c-195">ETag</span><span class="sxs-lookup"><span data-stu-id="e9d4c-195">ETag</span></span></td>
    <td><span data-ttu-id="e9d4c-196">Current value of the entity tag for the requested groups of supported languages.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-196">Current value of the entity tag for the requested groups of supported languages.</span></span> <span data-ttu-id="e9d4c-197">To make subsequent requests more efficient, the client may send the `ETag` value in an `If-None-Match` header field.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-197">To make subsequent requests more efficient, the client may send the `ETag` value in an `If-None-Match` header field.</span></span>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="e9d4c-198">X-RequestId</span><span class="sxs-lookup"><span data-stu-id="e9d4c-198">X-RequestId</span></span></td>
    <td><span data-ttu-id="e9d4c-199">Value generated by the service to identify the request.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-199">Value generated by the service to identify the request.</span></span> <span data-ttu-id="e9d4c-200">It is used for troubleshooting purposes.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-200">It is used for troubleshooting purposes.</span></span></td>
  </tr>
</table> 

## <a name="response-status-codes"></a><span data-ttu-id="e9d4c-201">Response status codes</span><span class="sxs-lookup"><span data-stu-id="e9d4c-201">Response status codes</span></span>

<span data-ttu-id="e9d4c-202">The following are the possible HTTP status codes that a request returns.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-202">The following are the possible HTTP status codes that a request returns.</span></span> 

<table width="100%">
  <th width="20%"><span data-ttu-id="e9d4c-203">Status Code</span><span class="sxs-lookup"><span data-stu-id="e9d4c-203">Status Code</span></span></th>
  <th><span data-ttu-id="e9d4c-204">Description</span><span class="sxs-lookup"><span data-stu-id="e9d4c-204">Description</span></span></th>
  <tr>
    <td><span data-ttu-id="e9d4c-205">200</span><span class="sxs-lookup"><span data-stu-id="e9d4c-205">200</span></span></td>
    <td><span data-ttu-id="e9d4c-206">Success.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-206">Success.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="e9d4c-207">304</span><span class="sxs-lookup"><span data-stu-id="e9d4c-207">304</span></span></td>
    <td><span data-ttu-id="e9d4c-208">The resource has not been modified since the version specified by request headers `If-None-Match`.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-208">The resource has not been modified since the version specified by request headers `If-None-Match`.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="e9d4c-209">400</span><span class="sxs-lookup"><span data-stu-id="e9d4c-209">400</span></span></td>
    <td><span data-ttu-id="e9d4c-210">One of the query parameters is missing or not valid.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-210">One of the query parameters is missing or not valid.</span></span> <span data-ttu-id="e9d4c-211">Correct request parameters before retrying.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-211">Correct request parameters before retrying.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="e9d4c-212">429</span><span class="sxs-lookup"><span data-stu-id="e9d4c-212">429</span></span></td>
    <td><span data-ttu-id="e9d4c-213">The caller is sending too many requests.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-213">The caller is sending too many requests.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="e9d4c-214">500</span><span class="sxs-lookup"><span data-stu-id="e9d4c-214">500</span></span></td>
    <td><span data-ttu-id="e9d4c-215">An unexpected error occurred.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-215">An unexpected error occurred.</span></span> <span data-ttu-id="e9d4c-216">If the error persists, report it with: date and time of the failure, request identifier from response header `X-RequestId`, and client identifier from request header `X-ClientTraceId`.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-216">If the error persists, report it with: date and time of the failure, request identifier from response header `X-RequestId`, and client identifier from request header `X-ClientTraceId`.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="e9d4c-217">503</span><span class="sxs-lookup"><span data-stu-id="e9d4c-217">503</span></span></td>
    <td><span data-ttu-id="e9d4c-218">Server temporarily unavailable.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-218">Server temporarily unavailable.</span></span> <span data-ttu-id="e9d4c-219">Retry the request.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-219">Retry the request.</span></span> <span data-ttu-id="e9d4c-220">If the error persists, report it with: date and time of the failure, request identifier from response header `X-RequestId`, and client identifier from request header `X-ClientTraceId`.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-220">If the error persists, report it with: date and time of the failure, request identifier from response header `X-RequestId`, and client identifier from request header `X-ClientTraceId`.</span></span></td>
  </tr>
</table> 

## <a name="examples"></a><span data-ttu-id="e9d4c-221">Examples</span><span class="sxs-lookup"><span data-stu-id="e9d4c-221">Examples</span></span>

<span data-ttu-id="e9d4c-222">The following example shows how to retrieve languages supported for text translation.</span><span class="sxs-lookup"><span data-stu-id="e9d4c-222">The following example shows how to retrieve languages supported for text translation.</span></span>

# <a name="curltabcurl"></a>[<span data-ttu-id="e9d4c-223">curl</span><span class="sxs-lookup"><span data-stu-id="e9d4c-223">curl</span></span>](#tab/curl)

```
curl "https://api.cognitive.microsofttranslator.com/languages?api-version=3.0&scope=translation"
```

---
