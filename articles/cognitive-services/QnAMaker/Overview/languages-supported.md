---
title: Supported languages - QnA Maker - Azure Cognitive Services | Microsoft Docs
description: Learn what languages are supported for QnA Maker.
services: cognitive-services
author: nstulasi
manager: sangitap
ms.service: cognitive-services
ms.component: QnAMaker
ms.topic: article
ms.date: 05/07/2018
ms.author: saneppal
ms.openlocfilehash: b210f59129a962046787b27d003c2872a54f6c8e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866343"
---
# <a name="supported-languages"></a><span data-ttu-id="b20cf-103">Supported languages</span><span class="sxs-lookup"><span data-stu-id="b20cf-103">Supported languages</span></span>

<span data-ttu-id="b20cf-104">The language of a knowledge base affects QnA Maker's ability to auto-extract questions and answers from [sources](../Concepts/data-sources-supported.md), as well as the relevance of the results QnA Maker provides in response to user queries.</span><span class="sxs-lookup"><span data-stu-id="b20cf-104">The language of a knowledge base affects QnA Maker's ability to auto-extract questions and answers from [sources](../Concepts/data-sources-supported.md), as well as the relevance of the results QnA Maker provides in response to user queries.</span></span>

## <a name="auto-extraction"></a><span data-ttu-id="b20cf-105">Auto extraction</span><span class="sxs-lookup"><span data-stu-id="b20cf-105">Auto extraction</span></span>
<span data-ttu-id="b20cf-106">QnA Maker supports question/answer extraction in any language page, but the effectiveness of the extraction is much higher for the following languages, as QnA Maker uses keywords to identify questions.</span><span class="sxs-lookup"><span data-stu-id="b20cf-106">QnA Maker supports question/answer extraction in any language page, but the effectiveness of the extraction is much higher for the following languages, as QnA Maker uses keywords to identify questions.</span></span>

|<span data-ttu-id="b20cf-107">Languages supported</span><span class="sxs-lookup"><span data-stu-id="b20cf-107">Languages supported</span></span>| <span data-ttu-id="b20cf-108">Locale</span><span class="sxs-lookup"><span data-stu-id="b20cf-108">Locale</span></span>|
|-----|----|
|<span data-ttu-id="b20cf-109">English</span><span class="sxs-lookup"><span data-stu-id="b20cf-109">English</span></span>|<span data-ttu-id="b20cf-110">en-\*</span><span class="sxs-lookup"><span data-stu-id="b20cf-110">en-\*</span></span>|
|<span data-ttu-id="b20cf-111">French</span><span class="sxs-lookup"><span data-stu-id="b20cf-111">French</span></span>|<span data-ttu-id="b20cf-112">fr-\*</span><span class="sxs-lookup"><span data-stu-id="b20cf-112">fr-\*</span></span>|
|<span data-ttu-id="b20cf-113">Italian</span><span class="sxs-lookup"><span data-stu-id="b20cf-113">Italian</span></span>|<span data-ttu-id="b20cf-114">it-\*</span><span class="sxs-lookup"><span data-stu-id="b20cf-114">it-\*</span></span>|
|<span data-ttu-id="b20cf-115">German</span><span class="sxs-lookup"><span data-stu-id="b20cf-115">German</span></span>|<span data-ttu-id="b20cf-116">de-\*</span><span class="sxs-lookup"><span data-stu-id="b20cf-116">de-\*</span></span>|
|<span data-ttu-id="b20cf-117">Spanish</span><span class="sxs-lookup"><span data-stu-id="b20cf-117">Spanish</span></span>|<span data-ttu-id="b20cf-118">es-\*</span><span class="sxs-lookup"><span data-stu-id="b20cf-118">es-\*</span></span>|

## <a name="query-matching-and-relevance"></a><span data-ttu-id="b20cf-119">Query matching and relevance</span><span class="sxs-lookup"><span data-stu-id="b20cf-119">Query matching and relevance</span></span>
<span data-ttu-id="b20cf-120">QnA Maker depends on [language analyzers](https://docs.microsoft.com/en-us/rest/api/searchservice/language-support) in Azure search for providing results.</span><span class="sxs-lookup"><span data-stu-id="b20cf-120">QnA Maker depends on [language analyzers](https://docs.microsoft.com/en-us/rest/api/searchservice/language-support) in Azure search for providing results.</span></span> <span data-ttu-id="b20cf-121">Special re-ranking features are available for En-\* languages that enable better relevance.</span><span class="sxs-lookup"><span data-stu-id="b20cf-121">Special re-ranking features are available for En-\* languages that enable better relevance.</span></span>

<span data-ttu-id="b20cf-122">QnA Maker auto-detects the language of the knowledge base during creation and sets the analyzer accordingly.</span><span class="sxs-lookup"><span data-stu-id="b20cf-122">QnA Maker auto-detects the language of the knowledge base during creation and sets the analyzer accordingly.</span></span> <span data-ttu-id="b20cf-123">You can create knowledge bases in the following languages.</span><span class="sxs-lookup"><span data-stu-id="b20cf-123">You can create knowledge bases in the following languages.</span></span> <span data-ttu-id="b20cf-124">Read [this](../How-To/language-knowledge-base.md) for more details about how QnA Maker handles languages.</span><span class="sxs-lookup"><span data-stu-id="b20cf-124">Read [this](../How-To/language-knowledge-base.md) for more details about how QnA Maker handles languages.</span></span>


> [!Tip]
> <span data-ttu-id="b20cf-125">Language analyzers, once set, cannot be changed.</span><span class="sxs-lookup"><span data-stu-id="b20cf-125">Language analyzers, once set, cannot be changed.</span></span> <span data-ttu-id="b20cf-126">Also, the language analyzer applies to all the knowledge bases in a [QnA Maker service](../How-To/set-up-qnamaker-service-azure.md).</span><span class="sxs-lookup"><span data-stu-id="b20cf-126">Also, the language analyzer applies to all the knowledge bases in a [QnA Maker service](../How-To/set-up-qnamaker-service-azure.md).</span></span> <span data-ttu-id="b20cf-127">If you plan to have knowledge bases in different language, you should create them under separate QnA Maker services.</span><span class="sxs-lookup"><span data-stu-id="b20cf-127">If you plan to have knowledge bases in different language, you should create them under separate QnA Maker services.</span></span>

|<span data-ttu-id="b20cf-128">Languages supported</span><span class="sxs-lookup"><span data-stu-id="b20cf-128">Languages supported</span></span>|
|-----|
|<span data-ttu-id="b20cf-129">Arabic</span><span class="sxs-lookup"><span data-stu-id="b20cf-129">Arabic</span></span>|
|<span data-ttu-id="b20cf-130">Armenian</span><span class="sxs-lookup"><span data-stu-id="b20cf-130">Armenian</span></span>|<span data-ttu-id="b20cf-131">,</span><span class="sxs-lookup"><span data-stu-id="b20cf-131">,</span></span>
<span data-ttu-id="b20cf-132">Bengali</span><span class="sxs-lookup"><span data-stu-id="b20cf-132">Bengali</span></span>|
|<span data-ttu-id="b20cf-133">Basque</span><span class="sxs-lookup"><span data-stu-id="b20cf-133">Basque</span></span>|
|<span data-ttu-id="b20cf-134">Bulgarian</span><span class="sxs-lookup"><span data-stu-id="b20cf-134">Bulgarian</span></span>|
|<span data-ttu-id="b20cf-135">Catalan</span><span class="sxs-lookup"><span data-stu-id="b20cf-135">Catalan</span></span>|
|<span data-ttu-id="b20cf-136">Chinese_Simplified</span><span class="sxs-lookup"><span data-stu-id="b20cf-136">Chinese_Simplified</span></span>|
|<span data-ttu-id="b20cf-137">Chinese_Traditional</span><span class="sxs-lookup"><span data-stu-id="b20cf-137">Chinese_Traditional</span></span>|
|<span data-ttu-id="b20cf-138">Croatian</span><span class="sxs-lookup"><span data-stu-id="b20cf-138">Croatian</span></span>|
|<span data-ttu-id="b20cf-139">Czech</span><span class="sxs-lookup"><span data-stu-id="b20cf-139">Czech</span></span>|
|<span data-ttu-id="b20cf-140">Danish</span><span class="sxs-lookup"><span data-stu-id="b20cf-140">Danish</span></span>|
|<span data-ttu-id="b20cf-141">Dutch</span><span class="sxs-lookup"><span data-stu-id="b20cf-141">Dutch</span></span>|
|<span data-ttu-id="b20cf-142">English</span><span class="sxs-lookup"><span data-stu-id="b20cf-142">English</span></span>|
|<span data-ttu-id="b20cf-143">Estonian</span><span class="sxs-lookup"><span data-stu-id="b20cf-143">Estonian</span></span>|
|<span data-ttu-id="b20cf-144">Finnish</span><span class="sxs-lookup"><span data-stu-id="b20cf-144">Finnish</span></span>|
|<span data-ttu-id="b20cf-145">French</span><span class="sxs-lookup"><span data-stu-id="b20cf-145">French</span></span>|
|<span data-ttu-id="b20cf-146">Galician</span><span class="sxs-lookup"><span data-stu-id="b20cf-146">Galician</span></span>|
|<span data-ttu-id="b20cf-147">German</span><span class="sxs-lookup"><span data-stu-id="b20cf-147">German</span></span>|
|<span data-ttu-id="b20cf-148">Greek</span><span class="sxs-lookup"><span data-stu-id="b20cf-148">Greek</span></span>|
|<span data-ttu-id="b20cf-149">Gujarati</span><span class="sxs-lookup"><span data-stu-id="b20cf-149">Gujarati</span></span>|
|<span data-ttu-id="b20cf-150">Hebrew</span><span class="sxs-lookup"><span data-stu-id="b20cf-150">Hebrew</span></span>|
|<span data-ttu-id="b20cf-151">Hindi</span><span class="sxs-lookup"><span data-stu-id="b20cf-151">Hindi</span></span>|
|<span data-ttu-id="b20cf-152">Hungarian</span><span class="sxs-lookup"><span data-stu-id="b20cf-152">Hungarian</span></span>|
|<span data-ttu-id="b20cf-153">Icelandic</span><span class="sxs-lookup"><span data-stu-id="b20cf-153">Icelandic</span></span>|
|<span data-ttu-id="b20cf-154">Indonesian</span><span class="sxs-lookup"><span data-stu-id="b20cf-154">Indonesian</span></span>|
|<span data-ttu-id="b20cf-155">Irish</span><span class="sxs-lookup"><span data-stu-id="b20cf-155">Irish</span></span>|
|<span data-ttu-id="b20cf-156">Italian</span><span class="sxs-lookup"><span data-stu-id="b20cf-156">Italian</span></span>|
|<span data-ttu-id="b20cf-157">Japanese</span><span class="sxs-lookup"><span data-stu-id="b20cf-157">Japanese</span></span>|
|<span data-ttu-id="b20cf-158">Kannada</span><span class="sxs-lookup"><span data-stu-id="b20cf-158">Kannada</span></span>|
|<span data-ttu-id="b20cf-159">Korean</span><span class="sxs-lookup"><span data-stu-id="b20cf-159">Korean</span></span>|
|<span data-ttu-id="b20cf-160">Latvian</span><span class="sxs-lookup"><span data-stu-id="b20cf-160">Latvian</span></span>|
|<span data-ttu-id="b20cf-161">Lithuanian</span><span class="sxs-lookup"><span data-stu-id="b20cf-161">Lithuanian</span></span>|
|<span data-ttu-id="b20cf-162">Malayalam</span><span class="sxs-lookup"><span data-stu-id="b20cf-162">Malayalam</span></span>|
|<span data-ttu-id="b20cf-163">Malay</span><span class="sxs-lookup"><span data-stu-id="b20cf-163">Malay</span></span>|
|<span data-ttu-id="b20cf-164">Norwegian</span><span class="sxs-lookup"><span data-stu-id="b20cf-164">Norwegian</span></span>|
|<span data-ttu-id="b20cf-165">Polish</span><span class="sxs-lookup"><span data-stu-id="b20cf-165">Polish</span></span>|
|<span data-ttu-id="b20cf-166">Portuguese</span><span class="sxs-lookup"><span data-stu-id="b20cf-166">Portuguese</span></span>|
|<span data-ttu-id="b20cf-167">Punjabi</span><span class="sxs-lookup"><span data-stu-id="b20cf-167">Punjabi</span></span>|
|<span data-ttu-id="b20cf-168">Romanian</span><span class="sxs-lookup"><span data-stu-id="b20cf-168">Romanian</span></span>|
|<span data-ttu-id="b20cf-169">Russian</span><span class="sxs-lookup"><span data-stu-id="b20cf-169">Russian</span></span>|
|<span data-ttu-id="b20cf-170">Serbian_Cyrillic</span><span class="sxs-lookup"><span data-stu-id="b20cf-170">Serbian_Cyrillic</span></span>|
|<span data-ttu-id="b20cf-171">Serbian_Latin</span><span class="sxs-lookup"><span data-stu-id="b20cf-171">Serbian_Latin</span></span>|
|<span data-ttu-id="b20cf-172">Slovak</span><span class="sxs-lookup"><span data-stu-id="b20cf-172">Slovak</span></span>|
|<span data-ttu-id="b20cf-173">Slovenian</span><span class="sxs-lookup"><span data-stu-id="b20cf-173">Slovenian</span></span>|
|<span data-ttu-id="b20cf-174">Spanish</span><span class="sxs-lookup"><span data-stu-id="b20cf-174">Spanish</span></span>|
|<span data-ttu-id="b20cf-175">Swedish</span><span class="sxs-lookup"><span data-stu-id="b20cf-175">Swedish</span></span>|
|<span data-ttu-id="b20cf-176">Tamil</span><span class="sxs-lookup"><span data-stu-id="b20cf-176">Tamil</span></span>|
|<span data-ttu-id="b20cf-177">Telugu</span><span class="sxs-lookup"><span data-stu-id="b20cf-177">Telugu</span></span>|
|<span data-ttu-id="b20cf-178">Thai</span><span class="sxs-lookup"><span data-stu-id="b20cf-178">Thai</span></span>|
|<span data-ttu-id="b20cf-179">Turkish</span><span class="sxs-lookup"><span data-stu-id="b20cf-179">Turkish</span></span>|
|<span data-ttu-id="b20cf-180">Ukrainian</span><span class="sxs-lookup"><span data-stu-id="b20cf-180">Ukrainian</span></span>|
|<span data-ttu-id="b20cf-181">Urdu</span><span class="sxs-lookup"><span data-stu-id="b20cf-181">Urdu</span></span>|
|<span data-ttu-id="b20cf-182">Vietnamese</span><span class="sxs-lookup"><span data-stu-id="b20cf-182">Vietnamese</span></span>|
