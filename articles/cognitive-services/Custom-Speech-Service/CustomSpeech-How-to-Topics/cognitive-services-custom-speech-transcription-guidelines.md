---
title: Transcription guidelines in Custom Speech Service on Azure  | Microsoft Docs
description: Learn how to prepare your data for Custom Speech Service in Cognitive Services.
services: cognitive-services
author: PanosPeriorellis
manager: onano
ms.service: cognitive-services
ms.component: custom-speech
ms.topic: article
ms.date: 02/08/2017
ms.author: panosper
ms.openlocfilehash: 2785a35ac7583ac3d9503cb721d10078d86aa365
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867452"
---
# <a name="transcription-guidelines"></a><span data-ttu-id="6a641-103">Transcription guidelines</span><span class="sxs-lookup"><span data-stu-id="6a641-103">Transcription guidelines</span></span>
<span data-ttu-id="6a641-104">To ensure the best use of your text data for acoustic and language model customization, the following transcription guidelines should be followed.</span><span class="sxs-lookup"><span data-stu-id="6a641-104">To ensure the best use of your text data for acoustic and language model customization, the following transcription guidelines should be followed.</span></span> <span data-ttu-id="6a641-105">These guidelines are language specific.</span><span class="sxs-lookup"><span data-stu-id="6a641-105">These guidelines are language specific.</span></span>

## <a name="text-normalization"></a><span data-ttu-id="6a641-106">Text normalization</span><span class="sxs-lookup"><span data-stu-id="6a641-106">Text normalization</span></span>

<span data-ttu-id="6a641-107">For optimal use in the acoustic or language model customization, the text data must be normalized, which means transformed into a standard, unambiguous form readable by the system.</span><span class="sxs-lookup"><span data-stu-id="6a641-107">For optimal use in the acoustic or language model customization, the text data must be normalized, which means transformed into a standard, unambiguous form readable by the system.</span></span> <span data-ttu-id="6a641-108">This section describes the text normalization performed by the Custom Speech Service when data is imported and the text normalization that the user must perform prior to data import.</span><span class="sxs-lookup"><span data-stu-id="6a641-108">This section describes the text normalization performed by the Custom Speech Service when data is imported and the text normalization that the user must perform prior to data import.</span></span>

## <a name="inverse-text-normalization"></a><span data-ttu-id="6a641-109">Inverse text normalization</span><span class="sxs-lookup"><span data-stu-id="6a641-109">Inverse text normalization</span></span>

<span data-ttu-id="6a641-110">The process of converting “raw” unformatted text back to formatted text, i.e. with capitalization and punctuation, is called inverse text normalization (ITN).</span><span class="sxs-lookup"><span data-stu-id="6a641-110">The process of converting “raw” unformatted text back to formatted text, i.e. with capitalization and punctuation, is called inverse text normalization (ITN).</span></span> <span data-ttu-id="6a641-111">ITN is performed on results returned by the Microsoft Cognitive Services Speech API.</span><span class="sxs-lookup"><span data-stu-id="6a641-111">ITN is performed on results returned by the Microsoft Cognitive Services Speech API.</span></span> <span data-ttu-id="6a641-112">A custom endpoint deployed using the Custom Speech Service uses the same ITN as the Microsoft Cognitive Services Speech API.</span><span class="sxs-lookup"><span data-stu-id="6a641-112">A custom endpoint deployed using the Custom Speech Service uses the same ITN as the Microsoft Cognitive Services Speech API.</span></span> <span data-ttu-id="6a641-113">However, this service does not currently support custom ITN, so new terms introduced by a custom language model will not be formatted in the recognition results.</span><span class="sxs-lookup"><span data-stu-id="6a641-113">However, this service does not currently support custom ITN, so new terms introduced by a custom language model will not be formatted in the recognition results.</span></span>

## <a name="transcription-guidelines-for-en-us"></a><span data-ttu-id="6a641-114">Transcription guidelines for en-US</span><span class="sxs-lookup"><span data-stu-id="6a641-114">Transcription guidelines for en-US</span></span>

<span data-ttu-id="6a641-115">Text data uploaded to this service should be written in plain text using only the ASCII printable character set.</span><span class="sxs-lookup"><span data-stu-id="6a641-115">Text data uploaded to this service should be written in plain text using only the ASCII printable character set.</span></span> <span data-ttu-id="6a641-116">Each line of the file should contain the text for a single utterance only.</span><span class="sxs-lookup"><span data-stu-id="6a641-116">Each line of the file should contain the text for a single utterance only.</span></span>

<span data-ttu-id="6a641-117">It is important to avoid the use of Unicode punctuation characters.</span><span class="sxs-lookup"><span data-stu-id="6a641-117">It is important to avoid the use of Unicode punctuation characters.</span></span> <span data-ttu-id="6a641-118">This can happen inadvertently if preparing the data in a word processing program or scraping data from web pages.</span><span class="sxs-lookup"><span data-stu-id="6a641-118">This can happen inadvertently if preparing the data in a word processing program or scraping data from web pages.</span></span> <span data-ttu-id="6a641-119">Replace these characters with appropriate ASCII substitutions.</span><span class="sxs-lookup"><span data-stu-id="6a641-119">Replace these characters with appropriate ASCII substitutions.</span></span> <span data-ttu-id="6a641-120">For example:</span><span class="sxs-lookup"><span data-stu-id="6a641-120">For example:</span></span>

| <span data-ttu-id="6a641-121">Unicode to avoid</span><span class="sxs-lookup"><span data-stu-id="6a641-121">Unicode to avoid</span></span> | <span data-ttu-id="6a641-122">ASCII substitution</span><span class="sxs-lookup"><span data-stu-id="6a641-122">ASCII substitution</span></span> |
|----- | ----- |
| <span data-ttu-id="6a641-123">“Hello world” (open and close double quotes)</span><span class="sxs-lookup"><span data-stu-id="6a641-123">“Hello world” (open and close double quotes)</span></span> | <span data-ttu-id="6a641-124">"Hello world" (double quotes)</span><span class="sxs-lookup"><span data-stu-id="6a641-124">"Hello world" (double quotes)</span></span> |
| <span data-ttu-id="6a641-125">John’s day (right single quotation mark)</span><span class="sxs-lookup"><span data-stu-id="6a641-125">John’s day (right single quotation mark)</span></span> | <span data-ttu-id="6a641-126">John's day (apostrophe)</span><span class="sxs-lookup"><span data-stu-id="6a641-126">John's day (apostrophe)</span></span> |

### <a name="text-normalization-performed-by-the-custom-speech-service"></a><span data-ttu-id="6a641-127">Text normalization performed by the Custom Speech Service</span><span class="sxs-lookup"><span data-stu-id="6a641-127">Text normalization performed by the Custom Speech Service</span></span>

<span data-ttu-id="6a641-128">This service will perform the following text normalization on data imported as a language data set or transcriptions for an acoustic data set.</span><span class="sxs-lookup"><span data-stu-id="6a641-128">This service will perform the following text normalization on data imported as a language data set or transcriptions for an acoustic data set.</span></span> <span data-ttu-id="6a641-129">This includes</span><span class="sxs-lookup"><span data-stu-id="6a641-129">This includes</span></span>

*   <span data-ttu-id="6a641-130">Lower-casing all text</span><span class="sxs-lookup"><span data-stu-id="6a641-130">Lower-casing all text</span></span>
*   <span data-ttu-id="6a641-131">Removing all punctuation except word-internal apostrophes</span><span class="sxs-lookup"><span data-stu-id="6a641-131">Removing all punctuation except word-internal apostrophes</span></span>
*   <span data-ttu-id="6a641-132">Expansion of numbers to spoken form, including dollar amounts</span><span class="sxs-lookup"><span data-stu-id="6a641-132">Expansion of numbers to spoken form, including dollar amounts</span></span>

<span data-ttu-id="6a641-133">Here are some examples</span><span class="sxs-lookup"><span data-stu-id="6a641-133">Here are some examples</span></span>

| <span data-ttu-id="6a641-134">Original Text</span><span class="sxs-lookup"><span data-stu-id="6a641-134">Original Text</span></span> | <span data-ttu-id="6a641-135">After Normalization</span><span class="sxs-lookup"><span data-stu-id="6a641-135">After Normalization</span></span> |
|----- | ----- |
| <span data-ttu-id="6a641-136">Starbucks Coffee</span><span class="sxs-lookup"><span data-stu-id="6a641-136">Starbucks Coffee</span></span> | <span data-ttu-id="6a641-137">starbucks coffee</span><span class="sxs-lookup"><span data-stu-id="6a641-137">starbucks coffee</span></span> |
| <span data-ttu-id="6a641-138">“Holy cow!”</span><span class="sxs-lookup"><span data-stu-id="6a641-138">“Holy cow!”</span></span> <span data-ttu-id="6a641-139">said Batman.</span><span class="sxs-lookup"><span data-stu-id="6a641-139">said Batman.</span></span> | <span data-ttu-id="6a641-140">holy cow said batman</span><span class="sxs-lookup"><span data-stu-id="6a641-140">holy cow said batman</span></span> |
| <span data-ttu-id="6a641-141">“What?”</span><span class="sxs-lookup"><span data-stu-id="6a641-141">“What?”</span></span> <span data-ttu-id="6a641-142">said Batman’s sidekick, Robin.</span><span class="sxs-lookup"><span data-stu-id="6a641-142">said Batman’s sidekick, Robin.</span></span> | <span data-ttu-id="6a641-143">what said batman’s sidekick robin</span><span class="sxs-lookup"><span data-stu-id="6a641-143">what said batman’s sidekick robin</span></span> |
| <span data-ttu-id="6a641-144">Go get -em!</span><span class="sxs-lookup"><span data-stu-id="6a641-144">Go get -em!</span></span> | <span data-ttu-id="6a641-145">go get em</span><span class="sxs-lookup"><span data-stu-id="6a641-145">go get em</span></span> |
| <span data-ttu-id="6a641-146">I’m double-jointed</span><span class="sxs-lookup"><span data-stu-id="6a641-146">I’m double-jointed</span></span> | <span data-ttu-id="6a641-147">i’m double jointed</span><span class="sxs-lookup"><span data-stu-id="6a641-147">i’m double jointed</span></span> |
| <span data-ttu-id="6a641-148">104 Main Street</span><span class="sxs-lookup"><span data-stu-id="6a641-148">104 Main Street</span></span> | <span data-ttu-id="6a641-149">one oh four main street</span><span class="sxs-lookup"><span data-stu-id="6a641-149">one oh four main street</span></span> |
| <span data-ttu-id="6a641-150">Tune to 102.7</span><span class="sxs-lookup"><span data-stu-id="6a641-150">Tune to 102.7</span></span> | <span data-ttu-id="6a641-151">tune to one oh two point seven</span><span class="sxs-lookup"><span data-stu-id="6a641-151">tune to one oh two point seven</span></span> |
| <span data-ttu-id="6a641-152">Pi is about 3.14</span><span class="sxs-lookup"><span data-stu-id="6a641-152">Pi is about 3.14</span></span> | <span data-ttu-id="6a641-153">pi is about three point one four</span><span class="sxs-lookup"><span data-stu-id="6a641-153">pi is about three point one four</span></span> |
| <span data-ttu-id="6a641-154">It costs $3.14</span><span class="sxs-lookup"><span data-stu-id="6a641-154">It costs $3.14</span></span> | <span data-ttu-id="6a641-155">it costs three fourteen</span><span class="sxs-lookup"><span data-stu-id="6a641-155">it costs three fourteen</span></span> |

### <a name="text-normalization-required-by-users"></a><span data-ttu-id="6a641-156">Text normalization required by users</span><span class="sxs-lookup"><span data-stu-id="6a641-156">Text normalization required by users</span></span>

<span data-ttu-id="6a641-157">To ensure the best use of your data, the following normalization rules should be applied to your data prior to importing it.</span><span class="sxs-lookup"><span data-stu-id="6a641-157">To ensure the best use of your data, the following normalization rules should be applied to your data prior to importing it.</span></span>

*   <span data-ttu-id="6a641-158">Abbreviations should be written out in words to reflect spoken form</span><span class="sxs-lookup"><span data-stu-id="6a641-158">Abbreviations should be written out in words to reflect spoken form</span></span>
*   <span data-ttu-id="6a641-159">Non-standard numeric strings should be written out in words</span><span class="sxs-lookup"><span data-stu-id="6a641-159">Non-standard numeric strings should be written out in words</span></span>
*   <span data-ttu-id="6a641-160">Words with non-alphabetic characters or mixed alphanumeric characters should be transcribed as pronounced</span><span class="sxs-lookup"><span data-stu-id="6a641-160">Words with non-alphabetic characters or mixed alphanumeric characters should be transcribed as pronounced</span></span>
*   <span data-ttu-id="6a641-161">Common acronyms can be left as a single entity without periods or spaces between the letters, but all other acronyms should be written out in separate letters, with each letter separated by a single space</span><span class="sxs-lookup"><span data-stu-id="6a641-161">Common acronyms can be left as a single entity without periods or spaces between the letters, but all other acronyms should be written out in separate letters, with each letter separated by a single space</span></span>

<span data-ttu-id="6a641-162">Here are some examples</span><span class="sxs-lookup"><span data-stu-id="6a641-162">Here are some examples</span></span>

| <span data-ttu-id="6a641-163">Original Text</span><span class="sxs-lookup"><span data-stu-id="6a641-163">Original Text</span></span> | <span data-ttu-id="6a641-164">After Normalization</span><span class="sxs-lookup"><span data-stu-id="6a641-164">After Normalization</span></span> |
|----- | ----- |
| <span data-ttu-id="6a641-165">14 NE 3rd Dr.</span><span class="sxs-lookup"><span data-stu-id="6a641-165">14 NE 3rd Dr.</span></span> | <span data-ttu-id="6a641-166">fourteen northeast third drive</span><span class="sxs-lookup"><span data-stu-id="6a641-166">fourteen northeast third drive</span></span> |
| <span data-ttu-id="6a641-167">Dr. Strangelove</span><span class="sxs-lookup"><span data-stu-id="6a641-167">Dr. Strangelove</span></span> | <span data-ttu-id="6a641-168">Doctor Strangelove</span><span class="sxs-lookup"><span data-stu-id="6a641-168">Doctor Strangelove</span></span> |
| <span data-ttu-id="6a641-169">James Bond 007</span><span class="sxs-lookup"><span data-stu-id="6a641-169">James Bond 007</span></span> | <span data-ttu-id="6a641-170">james bond double oh seven</span><span class="sxs-lookup"><span data-stu-id="6a641-170">james bond double oh seven</span></span> |
| <span data-ttu-id="6a641-171">Ke$ha</span><span class="sxs-lookup"><span data-stu-id="6a641-171">Ke$ha</span></span> | <span data-ttu-id="6a641-172">Kesha</span><span class="sxs-lookup"><span data-stu-id="6a641-172">Kesha</span></span> |
| <span data-ttu-id="6a641-173">How long is the 2x4</span><span class="sxs-lookup"><span data-stu-id="6a641-173">How long is the 2x4</span></span> | <span data-ttu-id="6a641-174">How long is the two by four</span><span class="sxs-lookup"><span data-stu-id="6a641-174">How long is the two by four</span></span> |
| <span data-ttu-id="6a641-175">The meeting goes from 1-3pm</span><span class="sxs-lookup"><span data-stu-id="6a641-175">The meeting goes from 1-3pm</span></span> | <span data-ttu-id="6a641-176">The meeting goes from one to three pm</span><span class="sxs-lookup"><span data-stu-id="6a641-176">The meeting goes from one to three pm</span></span> |
| <span data-ttu-id="6a641-177">my blood type is O+</span><span class="sxs-lookup"><span data-stu-id="6a641-177">my blood type is O+</span></span> | <span data-ttu-id="6a641-178">My blood type is O positive</span><span class="sxs-lookup"><span data-stu-id="6a641-178">My blood type is O positive</span></span> |
| <span data-ttu-id="6a641-179">water is H20</span><span class="sxs-lookup"><span data-stu-id="6a641-179">water is H20</span></span> | <span data-ttu-id="6a641-180">water is H 2 O</span><span class="sxs-lookup"><span data-stu-id="6a641-180">water is H 2 O</span></span> |
| <span data-ttu-id="6a641-181">play OU812 by Van Halen</span><span class="sxs-lookup"><span data-stu-id="6a641-181">play OU812 by Van Halen</span></span> | <span data-ttu-id="6a641-182">play O U 8 1 2 by Van Halen</span><span class="sxs-lookup"><span data-stu-id="6a641-182">play O U 8 1 2 by Van Halen</span></span> |

## <a name="transcription-guidelines-for-zh-cn"></a><span data-ttu-id="6a641-183">Transcription guidelines for zh-CN</span><span class="sxs-lookup"><span data-stu-id="6a641-183">Transcription guidelines for zh-CN</span></span>

<span data-ttu-id="6a641-184">Text data uploaded to the Custom Speech Service should use **UTF-8 encoding (incl. BOM)**.</span><span class="sxs-lookup"><span data-stu-id="6a641-184">Text data uploaded to the Custom Speech Service should use **UTF-8 encoding (incl. BOM)**.</span></span> <span data-ttu-id="6a641-185">Each line of the file should contain the text for a single utterance only.</span><span class="sxs-lookup"><span data-stu-id="6a641-185">Each line of the file should contain the text for a single utterance only.</span></span>

<span data-ttu-id="6a641-186">It is important to avoid the use of half-width punctuation characters.</span><span class="sxs-lookup"><span data-stu-id="6a641-186">It is important to avoid the use of half-width punctuation characters.</span></span> <span data-ttu-id="6a641-187">This can happen inadvertently if preparing the data in a word processing program or scraping data from web pages.</span><span class="sxs-lookup"><span data-stu-id="6a641-187">This can happen inadvertently if preparing the data in a word processing program or scraping data from web pages.</span></span> <span data-ttu-id="6a641-188">Replace these characters with appropriate full-width substitutions.</span><span class="sxs-lookup"><span data-stu-id="6a641-188">Replace these characters with appropriate full-width substitutions.</span></span> <span data-ttu-id="6a641-189">For example:</span><span class="sxs-lookup"><span data-stu-id="6a641-189">For example:</span></span>

| <span data-ttu-id="6a641-190">Unicode to avoid</span><span class="sxs-lookup"><span data-stu-id="6a641-190">Unicode to avoid</span></span> | <span data-ttu-id="6a641-191">ASCII substitution</span><span class="sxs-lookup"><span data-stu-id="6a641-191">ASCII substitution</span></span> |
|----- | ----- |
| <span data-ttu-id="6a641-192">“你好” (open and close double quotes)</span><span class="sxs-lookup"><span data-stu-id="6a641-192">“你好” (open and close double quotes)</span></span> | <span data-ttu-id="6a641-193">"你好" (double quotes)</span><span class="sxs-lookup"><span data-stu-id="6a641-193">"你好" (double quotes)</span></span> |
| <span data-ttu-id="6a641-194">需要什么帮助?</span><span class="sxs-lookup"><span data-stu-id="6a641-194">需要什么帮助?</span></span> <span data-ttu-id="6a641-195">(question mark)</span><span class="sxs-lookup"><span data-stu-id="6a641-195">(question mark)</span></span> | <span data-ttu-id="6a641-196">需要什么帮助？</span><span class="sxs-lookup"><span data-stu-id="6a641-196">需要什么帮助？</span></span> |

### <a name="text-normalization-performed-by-the-custom-speech-service"></a><span data-ttu-id="6a641-197">Text normalization performed by the Custom Speech Service</span><span class="sxs-lookup"><span data-stu-id="6a641-197">Text normalization performed by the Custom Speech Service</span></span>

<span data-ttu-id="6a641-198">This speech service will perform the following text normalization on data imported as a language data set or transcriptions for an acoustic data set.</span><span class="sxs-lookup"><span data-stu-id="6a641-198">This speech service will perform the following text normalization on data imported as a language data set or transcriptions for an acoustic data set.</span></span> <span data-ttu-id="6a641-199">This includes</span><span class="sxs-lookup"><span data-stu-id="6a641-199">This includes</span></span>

*   <span data-ttu-id="6a641-200">Removing all punctuation</span><span class="sxs-lookup"><span data-stu-id="6a641-200">Removing all punctuation</span></span>
*   <span data-ttu-id="6a641-201">Expansion of numbers to spoken form</span><span class="sxs-lookup"><span data-stu-id="6a641-201">Expansion of numbers to spoken form</span></span>
*   <span data-ttu-id="6a641-202">Convert full-width letters to half-width letters.</span><span class="sxs-lookup"><span data-stu-id="6a641-202">Convert full-width letters to half-width letters.</span></span>
*   <span data-ttu-id="6a641-203">Upper-casing all English words</span><span class="sxs-lookup"><span data-stu-id="6a641-203">Upper-casing all English words</span></span>

<span data-ttu-id="6a641-204">Here are some examples:</span><span class="sxs-lookup"><span data-stu-id="6a641-204">Here are some examples:</span></span>

| <span data-ttu-id="6a641-205">Original Text</span><span class="sxs-lookup"><span data-stu-id="6a641-205">Original Text</span></span> | <span data-ttu-id="6a641-206">After Normalization</span><span class="sxs-lookup"><span data-stu-id="6a641-206">After Normalization</span></span> |
|----- | ----- |
| <span data-ttu-id="6a641-207">3.1415</span><span class="sxs-lookup"><span data-stu-id="6a641-207">3.1415</span></span> | <span data-ttu-id="6a641-208">三 点 一 四 一 五</span><span class="sxs-lookup"><span data-stu-id="6a641-208">三 点 一 四 一 五</span></span> |
| <span data-ttu-id="6a641-209">￥3.5</span><span class="sxs-lookup"><span data-stu-id="6a641-209">￥3.5</span></span> | <span data-ttu-id="6a641-210">三 元 五 角</span><span class="sxs-lookup"><span data-stu-id="6a641-210">三 元 五 角</span></span> |
| <span data-ttu-id="6a641-211">w f y z</span><span class="sxs-lookup"><span data-stu-id="6a641-211">w f y z</span></span> | <span data-ttu-id="6a641-212">W F Y Z</span><span class="sxs-lookup"><span data-stu-id="6a641-212">W F Y Z</span></span> |
| <span data-ttu-id="6a641-213">1992年8月8日</span><span class="sxs-lookup"><span data-stu-id="6a641-213">1992年8月8日</span></span> | <span data-ttu-id="6a641-214">一 九 九 二 年 八 月 八 日</span><span class="sxs-lookup"><span data-stu-id="6a641-214">一 九 九 二 年 八 月 八 日</span></span> |
| <span data-ttu-id="6a641-215">你吃饭了吗 ?</span><span class="sxs-lookup"><span data-stu-id="6a641-215">你吃饭了吗 ?</span></span> | <span data-ttu-id="6a641-216">你 吃饭 了 吗</span><span class="sxs-lookup"><span data-stu-id="6a641-216">你 吃饭 了 吗</span></span> |
| <span data-ttu-id="6a641-217">下午5:00的航班</span><span class="sxs-lookup"><span data-stu-id="6a641-217">下午5:00的航班</span></span> | <span data-ttu-id="6a641-218">下午 五点 的 航班</span><span class="sxs-lookup"><span data-stu-id="6a641-218">下午 五点 的 航班</span></span> |
| <span data-ttu-id="6a641-219">我今年21岁</span><span class="sxs-lookup"><span data-stu-id="6a641-219">我今年21岁</span></span> | <span data-ttu-id="6a641-220">我 今年 二十 一 岁</span><span class="sxs-lookup"><span data-stu-id="6a641-220">我 今年 二十 一 岁</span></span> |

### <a name="text-normalization-required-by-users"></a><span data-ttu-id="6a641-221">Text normalization required by users</span><span class="sxs-lookup"><span data-stu-id="6a641-221">Text normalization required by users</span></span>

<span data-ttu-id="6a641-222">To ensure the best use of your data, the following normalization rules should be applied to your data _prior_ to importing it.</span><span class="sxs-lookup"><span data-stu-id="6a641-222">To ensure the best use of your data, the following normalization rules should be applied to your data _prior_ to importing it.</span></span>

*   <span data-ttu-id="6a641-223">Abbreviations should be written out in words to reflect spoken form</span><span class="sxs-lookup"><span data-stu-id="6a641-223">Abbreviations should be written out in words to reflect spoken form</span></span>
*   <span data-ttu-id="6a641-224">This service doesn’t cover all numeric quantities.</span><span class="sxs-lookup"><span data-stu-id="6a641-224">This service doesn’t cover all numeric quantities.</span></span> <span data-ttu-id="6a641-225">It is more reliable to write numeric strings out in spoken form</span><span class="sxs-lookup"><span data-stu-id="6a641-225">It is more reliable to write numeric strings out in spoken form</span></span>

<span data-ttu-id="6a641-226">Here are some examples</span><span class="sxs-lookup"><span data-stu-id="6a641-226">Here are some examples</span></span>

| <span data-ttu-id="6a641-227">Original Text</span><span class="sxs-lookup"><span data-stu-id="6a641-227">Original Text</span></span> | <span data-ttu-id="6a641-228">After Normalization</span><span class="sxs-lookup"><span data-stu-id="6a641-228">After Normalization</span></span> |
|----- | ----- |
| <span data-ttu-id="6a641-229">我今年21</span><span class="sxs-lookup"><span data-stu-id="6a641-229">我今年21</span></span> | <span data-ttu-id="6a641-230">我今年二十一</span><span class="sxs-lookup"><span data-stu-id="6a641-230">我今年二十一</span></span> |
| <span data-ttu-id="6a641-231">3号楼504</span><span class="sxs-lookup"><span data-stu-id="6a641-231">3号楼504</span></span> | <span data-ttu-id="6a641-232">三号 楼 五 零 四</span><span class="sxs-lookup"><span data-stu-id="6a641-232">三号 楼 五 零 四</span></span> |

## <a name="transcription-guidelines-for-de-de"></a><span data-ttu-id="6a641-233">Transcription guidelines for de-DE</span><span class="sxs-lookup"><span data-stu-id="6a641-233">Transcription guidelines for de-DE</span></span>

<span data-ttu-id="6a641-234">Text data uploaded to the Custom Speech Service should only use **UTF-8 encoding (incl. BOM)**.</span><span class="sxs-lookup"><span data-stu-id="6a641-234">Text data uploaded to the Custom Speech Service should only use **UTF-8 encoding (incl. BOM)**.</span></span> <span data-ttu-id="6a641-235">Each line of the file should contain the text for a single utterance only.</span><span class="sxs-lookup"><span data-stu-id="6a641-235">Each line of the file should contain the text for a single utterance only.</span></span>

### <a name="text-normalization-performed-by-the-custom-speech-service"></a><span data-ttu-id="6a641-236">Text normalization performed by the Custom Speech Service</span><span class="sxs-lookup"><span data-stu-id="6a641-236">Text normalization performed by the Custom Speech Service</span></span>

<span data-ttu-id="6a641-237">This service will perform the following text normalization on data imported as a language data set or transcriptions for an acoustic data set.</span><span class="sxs-lookup"><span data-stu-id="6a641-237">This service will perform the following text normalization on data imported as a language data set or transcriptions for an acoustic data set.</span></span> <span data-ttu-id="6a641-238">This includes</span><span class="sxs-lookup"><span data-stu-id="6a641-238">This includes</span></span>

*   <span data-ttu-id="6a641-239">Lower-casing all text</span><span class="sxs-lookup"><span data-stu-id="6a641-239">Lower-casing all text</span></span>
*   <span data-ttu-id="6a641-240">Removing all punctuation including English or German quotes ("test", 'test', “test„ or «test» are ok)</span><span class="sxs-lookup"><span data-stu-id="6a641-240">Removing all punctuation including English or German quotes ("test", 'test', “test„ or «test» are ok)</span></span>
*   <span data-ttu-id="6a641-241">Discard any row containing any special character including: ^ ¢ £ ¤ ¥ ¦ § © ª ¬ ® ° ± ² µ × ÿ Ø¬¬</span><span class="sxs-lookup"><span data-stu-id="6a641-241">Discard any row containing any special character including: ^ ¢ £ ¤ ¥ ¦ § © ª ¬ ® ° ± ² µ × ÿ Ø¬¬</span></span>
*   <span data-ttu-id="6a641-242">Expansion of numbers to word form, including dollar or euro amounts</span><span class="sxs-lookup"><span data-stu-id="6a641-242">Expansion of numbers to word form, including dollar or euro amounts</span></span>
*   <span data-ttu-id="6a641-243">We accept only umlauts for a, o, u; others will be replaced by "th" or discarded</span><span class="sxs-lookup"><span data-stu-id="6a641-243">We accept only umlauts for a, o, u; others will be replaced by "th" or discarded</span></span>

<span data-ttu-id="6a641-244">Here are some examples</span><span class="sxs-lookup"><span data-stu-id="6a641-244">Here are some examples</span></span>

| <span data-ttu-id="6a641-245">Original Text</span><span class="sxs-lookup"><span data-stu-id="6a641-245">Original Text</span></span> | <span data-ttu-id="6a641-246">After Normalization</span><span class="sxs-lookup"><span data-stu-id="6a641-246">After Normalization</span></span> |
|----- | ----- |
| <span data-ttu-id="6a641-247">Frankfurter Ring</span><span class="sxs-lookup"><span data-stu-id="6a641-247">Frankfurter Ring</span></span> | <span data-ttu-id="6a641-248">frankfurter ring</span><span class="sxs-lookup"><span data-stu-id="6a641-248">frankfurter ring</span></span> |
| <span data-ttu-id="6a641-249">"Hallo, Mama!"</span><span class="sxs-lookup"><span data-stu-id="6a641-249">"Hallo, Mama!"</span></span> <span data-ttu-id="6a641-250">sagt die Tochter.</span><span class="sxs-lookup"><span data-stu-id="6a641-250">sagt die Tochter.</span></span> | <span data-ttu-id="6a641-251">hallo mama sagt die tochter</span><span class="sxs-lookup"><span data-stu-id="6a641-251">hallo mama sagt die tochter</span></span> |
| <span data-ttu-id="6a641-252">¡Eine Frage!</span><span class="sxs-lookup"><span data-stu-id="6a641-252">¡Eine Frage!</span></span> | <span data-ttu-id="6a641-253">eine frage</span><span class="sxs-lookup"><span data-stu-id="6a641-253">eine frage</span></span> |
| <span data-ttu-id="6a641-254">wir, haben</span><span class="sxs-lookup"><span data-stu-id="6a641-254">wir, haben</span></span> | <span data-ttu-id="6a641-255">wir haben</span><span class="sxs-lookup"><span data-stu-id="6a641-255">wir haben</span></span> |
| <span data-ttu-id="6a641-256">Das macht $10</span><span class="sxs-lookup"><span data-stu-id="6a641-256">Das macht $10</span></span> | <span data-ttu-id="6a641-257">das macht zehn dollars</span><span class="sxs-lookup"><span data-stu-id="6a641-257">das macht zehn dollars</span></span> |


### <a name="text-normalization-required-by-users"></a><span data-ttu-id="6a641-258">Text normalization required by users</span><span class="sxs-lookup"><span data-stu-id="6a641-258">Text normalization required by users</span></span>

<span data-ttu-id="6a641-259">To ensure the best use of your data, the following normalization rules should be applied to your data prior to importing it.</span><span class="sxs-lookup"><span data-stu-id="6a641-259">To ensure the best use of your data, the following normalization rules should be applied to your data prior to importing it.</span></span>

*   <span data-ttu-id="6a641-260">Decimal point should be , and not .</span><span class="sxs-lookup"><span data-stu-id="6a641-260">Decimal point should be , and not .</span></span> <span data-ttu-id="6a641-261">e.g., 2,3% and not 2.3%</span><span class="sxs-lookup"><span data-stu-id="6a641-261">e.g., 2,3% and not 2.3%</span></span>
*   <span data-ttu-id="6a641-262">Time separator between hours and minutes should be : and not ., e.g., 12:00 Uhr</span><span class="sxs-lookup"><span data-stu-id="6a641-262">Time separator between hours and minutes should be : and not ., e.g., 12:00 Uhr</span></span>
*   <span data-ttu-id="6a641-263">Abbreviations such as 'ca.', 'bzw.'</span><span class="sxs-lookup"><span data-stu-id="6a641-263">Abbreviations such as 'ca.', 'bzw.'</span></span> <span data-ttu-id="6a641-264">are not replaced.</span><span class="sxs-lookup"><span data-stu-id="6a641-264">are not replaced.</span></span> <span data-ttu-id="6a641-265">We recommend to use the full form in order to have the correct pronunciation.</span><span class="sxs-lookup"><span data-stu-id="6a641-265">We recommend to use the full form in order to have the correct pronunciation.</span></span>
*   <span data-ttu-id="6a641-266">The five main mathematical operators are removed: +, -, \*, /.</span><span class="sxs-lookup"><span data-stu-id="6a641-266">The five main mathematical operators are removed: +, -, \*, /.</span></span>
 <span data-ttu-id="6a641-267">We recommend to replace them by their literal form plus, minus, mal, geteilt.</span><span class="sxs-lookup"><span data-stu-id="6a641-267">We recommend to replace them by their literal form plus, minus, mal, geteilt.</span></span>
*   <span data-ttu-id="6a641-268">Same applies for the comparators (=, <, >) - gleich, kleiner als, grösser als</span><span class="sxs-lookup"><span data-stu-id="6a641-268">Same applies for the comparators (=, <, >) - gleich, kleiner als, grösser als</span></span>
*   <span data-ttu-id="6a641-269">Use fraction such as 3/4 in word form 'drei viertel' instead of ¾</span><span class="sxs-lookup"><span data-stu-id="6a641-269">Use fraction such as 3/4 in word form 'drei viertel' instead of ¾</span></span>
*   <span data-ttu-id="6a641-270">Replace the € symbol with the word form "Euro"</span><span class="sxs-lookup"><span data-stu-id="6a641-270">Replace the € symbol with the word form "Euro"</span></span>


<span data-ttu-id="6a641-271">Here are some examples</span><span class="sxs-lookup"><span data-stu-id="6a641-271">Here are some examples</span></span>

| <span data-ttu-id="6a641-272">Original Text</span><span class="sxs-lookup"><span data-stu-id="6a641-272">Original Text</span></span> | <span data-ttu-id="6a641-273">After user's normalization</span><span class="sxs-lookup"><span data-stu-id="6a641-273">After user's normalization</span></span> | <span data-ttu-id="6a641-274">After system normalization</span><span class="sxs-lookup"><span data-stu-id="6a641-274">After system normalization</span></span>
|--------  | ----- | -------- |
| <span data-ttu-id="6a641-275">Es ist 12.23Uhr</span><span class="sxs-lookup"><span data-stu-id="6a641-275">Es ist 12.23Uhr</span></span> | <span data-ttu-id="6a641-276">Es ist 12:23Uhr</span><span class="sxs-lookup"><span data-stu-id="6a641-276">Es ist 12:23Uhr</span></span> | <span data-ttu-id="6a641-277">es ist zwölf uhr drei und zwanzig uhr</span><span class="sxs-lookup"><span data-stu-id="6a641-277">es ist zwölf uhr drei und zwanzig uhr</span></span> |
| <span data-ttu-id="6a641-278">{12.45}</span><span class="sxs-lookup"><span data-stu-id="6a641-278">{12.45}</span></span> | {12,45} | <span data-ttu-id="6a641-279">zwölf komma vier fünf</span><span class="sxs-lookup"><span data-stu-id="6a641-279">zwölf komma vier fünf</span></span> |
| <span data-ttu-id="6a641-280">3 < 5</span><span class="sxs-lookup"><span data-stu-id="6a641-280">3 < 5</span></span> | <span data-ttu-id="6a641-281">3 kleiner als 5</span><span class="sxs-lookup"><span data-stu-id="6a641-281">3 kleiner als 5</span></span> | <span data-ttu-id="6a641-282">drei kleiner als vier</span><span class="sxs-lookup"><span data-stu-id="6a641-282">drei kleiner als vier</span></span> |
| <span data-ttu-id="6a641-283">2 + 3 - 4</span><span class="sxs-lookup"><span data-stu-id="6a641-283">2 + 3 - 4</span></span> | <span data-ttu-id="6a641-284">2 plus 3 minus 4</span><span class="sxs-lookup"><span data-stu-id="6a641-284">2 plus 3 minus 4</span></span> | <span data-ttu-id="6a641-285">zwei plus drei minus vier</span><span class="sxs-lookup"><span data-stu-id="6a641-285">zwei plus drei minus vier</span></span>|
| <span data-ttu-id="6a641-286">Das macht 12€</span><span class="sxs-lookup"><span data-stu-id="6a641-286">Das macht 12€</span></span> | <span data-ttu-id="6a641-287">Das macht 12 Euros</span><span class="sxs-lookup"><span data-stu-id="6a641-287">Das macht 12 Euros</span></span> | <span data-ttu-id="6a641-288">das macht zwölf euros</span><span class="sxs-lookup"><span data-stu-id="6a641-288">das macht zwölf euros</span></span> |



## <a name="next-steps"></a><span data-ttu-id="6a641-289">Next steps</span><span class="sxs-lookup"><span data-stu-id="6a641-289">Next steps</span></span>
* [<span data-ttu-id="6a641-290">How to use a custom speech-to-text endpoint</span><span class="sxs-lookup"><span data-stu-id="6a641-290">How to use a custom speech-to-text endpoint</span></span>](cognitive-services-custom-speech-create-endpoint.md)
* <span data-ttu-id="6a641-291">Improve accuracy with your [custom acoustic model](cognitive-services-custom-speech-create-acoustic-model.md)</span><span class="sxs-lookup"><span data-stu-id="6a641-291">Improve accuracy with your [custom acoustic model](cognitive-services-custom-speech-create-acoustic-model.md)</span></span>
* <span data-ttu-id="6a641-292">Improve accuracy with a [custom language model](cognitive-services-custom-speech-create-language-model.md)</span><span class="sxs-lookup"><span data-stu-id="6a641-292">Improve accuracy with a [custom language model](cognitive-services-custom-speech-create-language-model.md)</span></span>
