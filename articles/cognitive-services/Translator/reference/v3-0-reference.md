---
title: Microsoft Translator Text API V3.0 Reference | Microsoft Docs
description: Reference documentation for the V3.0 Microsoft Translator Text API.
services: cognitive-services
author: Jann-Skotdal
manager: chriswendt1
ms.service: cognitive-services
ms.technology: microsoft translator
ms.topic: article
ms.date: 03/29/2018
ms.author: v-jansko
ms.openlocfilehash: cfaa9584e833b137b417d9074fbfcf606eb21388
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966597"
---
#<a name="translator-text-api-v30"></a><span data-ttu-id="74f69-103">Translator Text API v3.0</span><span class="sxs-lookup"><span data-stu-id="74f69-103">Translator Text API v3.0</span></span>

## <a name="whats-new"></a><span data-ttu-id="74f69-104">What's new?</span><span class="sxs-lookup"><span data-stu-id="74f69-104">What's new?</span></span>

<span data-ttu-id="74f69-105">Version 3 of the Microsoft Translator Text API provides a modern JSON-based Web API.</span><span class="sxs-lookup"><span data-stu-id="74f69-105">Version 3 of the Microsoft Translator Text API provides a modern JSON-based Web API.</span></span> <span data-ttu-id="74f69-106">It improves usability and performance by consolidating existing features into fewer operations and it provides new features.</span><span class="sxs-lookup"><span data-stu-id="74f69-106">It improves usability and performance by consolidating existing features into fewer operations and it provides new features.</span></span>

 * <span data-ttu-id="74f69-107">Transliteration to convert text in one language from one script to another script.</span><span class="sxs-lookup"><span data-stu-id="74f69-107">Transliteration to convert text in one language from one script to another script.</span></span>
 * <span data-ttu-id="74f69-108">Translation to multiple languages in one request.</span><span class="sxs-lookup"><span data-stu-id="74f69-108">Translation to multiple languages in one request.</span></span>
 * <span data-ttu-id="74f69-109">Language detection, translation, and transliteration in one request.</span><span class="sxs-lookup"><span data-stu-id="74f69-109">Language detection, translation, and transliteration in one request.</span></span>
 * <span data-ttu-id="74f69-110">Dictionary to lookup alternative translations of a term, to find back-translations and examples showing terms used in context.</span><span class="sxs-lookup"><span data-stu-id="74f69-110">Dictionary to lookup alternative translations of a term, to find back-translations and examples showing terms used in context.</span></span>
 * <span data-ttu-id="74f69-111">More informative language detection results.</span><span class="sxs-lookup"><span data-stu-id="74f69-111">More informative language detection results.</span></span>

## <a name="base-urls"></a><span data-ttu-id="74f69-112">Base URLs</span><span class="sxs-lookup"><span data-stu-id="74f69-112">Base URLs</span></span>

<span data-ttu-id="74f69-113">Text API v3.0 is available in the following cloud:</span><span class="sxs-lookup"><span data-stu-id="74f69-113">Text API v3.0 is available in the following cloud:</span></span>

| <span data-ttu-id="74f69-114">Description</span><span class="sxs-lookup"><span data-stu-id="74f69-114">Description</span></span> | <span data-ttu-id="74f69-115">Region</span><span class="sxs-lookup"><span data-stu-id="74f69-115">Region</span></span> | <span data-ttu-id="74f69-116">Base URL</span><span class="sxs-lookup"><span data-stu-id="74f69-116">Base URL</span></span>                                        |
|-------------|--------|-------------------------------------------------|
| <span data-ttu-id="74f69-117">Azure</span><span class="sxs-lookup"><span data-stu-id="74f69-117">Azure</span></span>       | <span data-ttu-id="74f69-118">Global</span><span class="sxs-lookup"><span data-stu-id="74f69-118">Global</span></span> | <span data-ttu-id="74f69-119">api.cognitive.microsofttranslator.com</span><span class="sxs-lookup"><span data-stu-id="74f69-119">api.cognitive.microsofttranslator.com</span></span>           |


## <a name="authentication"></a><span data-ttu-id="74f69-120">Authentication</span><span class="sxs-lookup"><span data-stu-id="74f69-120">Authentication</span></span>

<span data-ttu-id="74f69-121">Subscribe to Translator Text API in Microsoft Cognitive Services and use your subscription key (available in the Azure portal) to authenticate.</span><span class="sxs-lookup"><span data-stu-id="74f69-121">Subscribe to Translator Text API in Microsoft Cognitive Services and use your subscription key (available in the Azure portal) to authenticate.</span></span> 

<span data-ttu-id="74f69-122">The simplest way is to pass your Azure secret key to the Translator service using request header `Ocp-Apim-Subscription-Key`.</span><span class="sxs-lookup"><span data-stu-id="74f69-122">The simplest way is to pass your Azure secret key to the Translator service using request header `Ocp-Apim-Subscription-Key`.</span></span>

<span data-ttu-id="74f69-123">An alternative is to use your secret key to obtain an authorization token from the token service.</span><span class="sxs-lookup"><span data-stu-id="74f69-123">An alternative is to use your secret key to obtain an authorization token from the token service.</span></span> <span data-ttu-id="74f69-124">Then, you pass the authorization token to the Translator service using the `Authorization` request header.</span><span class="sxs-lookup"><span data-stu-id="74f69-124">Then, you pass the authorization token to the Translator service using the `Authorization` request header.</span></span> <span data-ttu-id="74f69-125">To obtain an authorization token, make a `POST` request to the following URL:</span><span class="sxs-lookup"><span data-stu-id="74f69-125">To obtain an authorization token, make a `POST` request to the following URL:</span></span>

| <span data-ttu-id="74f69-126">Environment</span><span class="sxs-lookup"><span data-stu-id="74f69-126">Environment</span></span>     | <span data-ttu-id="74f69-127">Authentication service URL</span><span class="sxs-lookup"><span data-stu-id="74f69-127">Authentication service URL</span></span>                                |
|-----------------|-----------------------------------------------------------|
| <span data-ttu-id="74f69-128">Azure</span><span class="sxs-lookup"><span data-stu-id="74f69-128">Azure</span></span>           | `https://api.cognitive.microsoft.com/sts/v1.0/issueToken` |

<span data-ttu-id="74f69-129">Here are example requests to obtain a token given a secret key:</span><span class="sxs-lookup"><span data-stu-id="74f69-129">Here are example requests to obtain a token given a secret key:</span></span>

```
// Pass secret key using header
curl --header 'Ocp-Apim-Subscription-Key: <your-key>' --data "" 'https://api.cognitive.microsoft.com/sts/v1.0/issueToken'
// Pass secret key using query string parameter
curl --data "" 'https://api.cognitive.microsoft.com/sts/v1.0/issueToken?Subscription-Key=<your-key>'
```

<span data-ttu-id="74f69-130">A successful request returns the encoded access token as plain text in the response body.</span><span class="sxs-lookup"><span data-stu-id="74f69-130">A successful request returns the encoded access token as plain text in the response body.</span></span> <span data-ttu-id="74f69-131">The valid token is passed to the Translator service as a bearer token in the Authorization.</span><span class="sxs-lookup"><span data-stu-id="74f69-131">The valid token is passed to the Translator service as a bearer token in the Authorization.</span></span>

```
Authorization: Bearer <Base64-access_token>
```

<span data-ttu-id="74f69-132">An authentication token is valid for 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="74f69-132">An authentication token is valid for 10 minutes.</span></span> <span data-ttu-id="74f69-133">The token should be re-used when making multiple calls to the Translator APIs.</span><span class="sxs-lookup"><span data-stu-id="74f69-133">The token should be re-used when making multiple calls to the Translator APIs.</span></span> <span data-ttu-id="74f69-134">However, if your program makes requests to the Translator API over an extended period of time, then your program must request a new access token at regular intervals (e.g. every 8 minutes).</span><span class="sxs-lookup"><span data-stu-id="74f69-134">However, if your program makes requests to the Translator API over an extended period of time, then your program must request a new access token at regular intervals (e.g. every 8 minutes).</span></span>

<span data-ttu-id="74f69-135">To summarize, a client request to the Translator API will include one authorization header taken from the following table:</span><span class="sxs-lookup"><span data-stu-id="74f69-135">To summarize, a client request to the Translator API will include one authorization header taken from the following table:</span></span>

<table width="100%">
  <th width="30%"><span data-ttu-id="74f69-136">Headers</span><span class="sxs-lookup"><span data-stu-id="74f69-136">Headers</span></span></th>
  <th><span data-ttu-id="74f69-137">Description</span><span class="sxs-lookup"><span data-stu-id="74f69-137">Description</span></span></th>
  <tr>
    <td><span data-ttu-id="74f69-138">Ocp-Apim-Subscription-Key</span><span class="sxs-lookup"><span data-stu-id="74f69-138">Ocp-Apim-Subscription-Key</span></span></td>
    <td><span data-ttu-id="74f69-139">*Use with Cognitive Services subscription if you are passing your secret key*.</span><span class="sxs-lookup"><span data-stu-id="74f69-139">*Use with Cognitive Services subscription if you are passing your secret key*.</span></span><br/><span data-ttu-id="74f69-140">The value is the Azure secret key for your subscription to Translator Text API.</span><span class="sxs-lookup"><span data-stu-id="74f69-140">The value is the Azure secret key for your subscription to Translator Text API.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="74f69-141">Authorization</span><span class="sxs-lookup"><span data-stu-id="74f69-141">Authorization</span></span></td>
    <td><span data-ttu-id="74f69-142">*Use with Cognitive Services subscription if you are passing an authentication token.*</span><span class="sxs-lookup"><span data-stu-id="74f69-142">*Use with Cognitive Services subscription if you are passing an authentication token.*</span></span><br/><span data-ttu-id="74f69-143">The value is the Bearer token: `Bearer <token>`.</span><span class="sxs-lookup"><span data-stu-id="74f69-143">The value is the Bearer token: `Bearer <token>`.</span></span></td>
  </tr>
</table> 

## <a name="errors"></a><span data-ttu-id="74f69-144">Errors</span><span class="sxs-lookup"><span data-stu-id="74f69-144">Errors</span></span>

<span data-ttu-id="74f69-145">A standard error response is a JSON object with name/value pair named `error`.</span><span class="sxs-lookup"><span data-stu-id="74f69-145">A standard error response is a JSON object with name/value pair named `error`.</span></span> <span data-ttu-id="74f69-146">The value is also a JSON object with properties:</span><span class="sxs-lookup"><span data-stu-id="74f69-146">The value is also a JSON object with properties:</span></span>

  * <span data-ttu-id="74f69-147">`code`: A server-defined error code.</span><span class="sxs-lookup"><span data-stu-id="74f69-147">`code`: A server-defined error code.</span></span>

  * <span data-ttu-id="74f69-148">`message`: A string giving a human-readable representation of the error.</span><span class="sxs-lookup"><span data-stu-id="74f69-148">`message`: A string giving a human-readable representation of the error.</span></span>

<span data-ttu-id="74f69-149">For example, a customer with a free trial subscription would receive the following error once the free quota is exhausted:</span><span class="sxs-lookup"><span data-stu-id="74f69-149">For example, a customer with a free trial subscription would receive the following error once the free quota is exhausted:</span></span>

```
{
  "error": {
    "code":403000,
    "message":"The subscription has exceeded its free quota."
    }
}
```
