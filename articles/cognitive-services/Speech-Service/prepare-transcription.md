---
title: Transcription guidelines for the Speech Service training
description: Learn how to prepare text to customize acoustic and language models and voice fonts for the Speech Service.
titleSuffix: Microsoft Cognitive Services
services: cognitive-services
author: PanosPeriorellis
ms.service: cognitive-services
ms.component: speech-service
ms.topic: article
ms.date: 07/01/2018
ms.author: panosper
ms.openlocfilehash: f9cb205b5111e981ee70adca715139402c9e31a4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868879"
---
# <a name="transcription-guidelines-for-using-the-speech-service"></a><span data-ttu-id="04781-103">Transcription guidelines for using the Speech Service</span><span class="sxs-lookup"><span data-stu-id="04781-103">Transcription guidelines for using the Speech Service</span></span>

<span data-ttu-id="04781-104">To customize **Speech to Text** or **Text to Speech**, you must provide text along with speech.</span><span class="sxs-lookup"><span data-stu-id="04781-104">To customize **Speech to Text** or **Text to Speech**, you must provide text along with speech.</span></span> <span data-ttu-id="04781-105">Each line in the text corresponds to a single utterance.</span><span class="sxs-lookup"><span data-stu-id="04781-105">Each line in the text corresponds to a single utterance.</span></span> <span data-ttu-id="04781-106">The text should match the speech as closely as possible.</span><span class="sxs-lookup"><span data-stu-id="04781-106">The text should match the speech as closely as possible.</span></span> <span data-ttu-id="04781-107">The text is called a *transcript*, and you must create it in a specific format.</span><span class="sxs-lookup"><span data-stu-id="04781-107">The text is called a *transcript*, and you must create it in a specific format.</span></span>

<span data-ttu-id="04781-108">The Speech Service normalizes the input to keep text consistent.</span><span class="sxs-lookup"><span data-stu-id="04781-108">The Speech Service normalizes the input to keep text consistent.</span></span> 

<span data-ttu-id="04781-109">This article describes both types of normalizations.</span><span class="sxs-lookup"><span data-stu-id="04781-109">This article describes both types of normalizations.</span></span> <span data-ttu-id="04781-110">The guidelines vary slightly for various languages.</span><span class="sxs-lookup"><span data-stu-id="04781-110">The guidelines vary slightly for various languages.</span></span>

## <a name="us-english-en-us"></a><span data-ttu-id="04781-111">US English (en-us)</span><span class="sxs-lookup"><span data-stu-id="04781-111">US English (en-us)</span></span>

<span data-ttu-id="04781-112">Text data should be written one utterance per line, in plain text, using only the ASCII character set.</span><span class="sxs-lookup"><span data-stu-id="04781-112">Text data should be written one utterance per line, in plain text, using only the ASCII character set.</span></span>

<span data-ttu-id="04781-113">Avoid the use of extended (Latin-1) or Unicode punctuation characters.</span><span class="sxs-lookup"><span data-stu-id="04781-113">Avoid the use of extended (Latin-1) or Unicode punctuation characters.</span></span> <span data-ttu-id="04781-114">These characters can be included inadvertently when you prepare the data in a word-processing program or scrape data from webpages.</span><span class="sxs-lookup"><span data-stu-id="04781-114">These characters can be included inadvertently when you prepare the data in a word-processing program or scrape data from webpages.</span></span> <span data-ttu-id="04781-115">Replace the characters with appropriate ASCII substitutions.</span><span class="sxs-lookup"><span data-stu-id="04781-115">Replace the characters with appropriate ASCII substitutions.</span></span> <span data-ttu-id="04781-116">For example:</span><span class="sxs-lookup"><span data-stu-id="04781-116">For example:</span></span>

| <span data-ttu-id="04781-117">Characters to avoid</span><span class="sxs-lookup"><span data-stu-id="04781-117">Characters to avoid</span></span> | <span data-ttu-id="04781-118">Substitution</span><span class="sxs-lookup"><span data-stu-id="04781-118">Substitution</span></span> |
|----- | ----- |
| <span data-ttu-id="04781-119">“Hello world” (opening and closing double quotation marks)</span><span class="sxs-lookup"><span data-stu-id="04781-119">“Hello world” (opening and closing double quotation marks)</span></span> | <span data-ttu-id="04781-120">"Hello world" (double quotation marks)</span><span class="sxs-lookup"><span data-stu-id="04781-120">"Hello world" (double quotation marks)</span></span> |
| <span data-ttu-id="04781-121">John’s day (right single quotation mark)</span><span class="sxs-lookup"><span data-stu-id="04781-121">John’s day (right single quotation mark)</span></span> | <span data-ttu-id="04781-122">John's day (apostrophe)</span><span class="sxs-lookup"><span data-stu-id="04781-122">John's day (apostrophe)</span></span> |
| <span data-ttu-id="04781-123">it was good—no, it was great!</span><span class="sxs-lookup"><span data-stu-id="04781-123">it was good—no, it was great!</span></span> <span data-ttu-id="04781-124">(em dash)</span><span class="sxs-lookup"><span data-stu-id="04781-124">(em dash)</span></span> | <span data-ttu-id="04781-125">it was good--no, it was great!</span><span class="sxs-lookup"><span data-stu-id="04781-125">it was good--no, it was great!</span></span> <span data-ttu-id="04781-126">(hyphens)</span><span class="sxs-lookup"><span data-stu-id="04781-126">(hyphens)</span></span> |

### <a name="text-normalization-rules-for-english"></a><span data-ttu-id="04781-127">Text normalization rules for English</span><span class="sxs-lookup"><span data-stu-id="04781-127">Text normalization rules for English</span></span>

<span data-ttu-id="04781-128">The Speech Service carries out the following normalization rules:</span><span class="sxs-lookup"><span data-stu-id="04781-128">The Speech Service carries out the following normalization rules:</span></span>

* <span data-ttu-id="04781-129">Using lowercase letters for all text</span><span class="sxs-lookup"><span data-stu-id="04781-129">Using lowercase letters for all text</span></span>
* <span data-ttu-id="04781-130">Removing all punctuation except word-internal apostrophes</span><span class="sxs-lookup"><span data-stu-id="04781-130">Removing all punctuation except word-internal apostrophes</span></span>
* <span data-ttu-id="04781-131">Expanding numbers to spoken form, including dollar amounts</span><span class="sxs-lookup"><span data-stu-id="04781-131">Expanding numbers to spoken form, including dollar amounts</span></span>

<span data-ttu-id="04781-132">Here are some examples:</span><span class="sxs-lookup"><span data-stu-id="04781-132">Here are some examples:</span></span>

| <span data-ttu-id="04781-133">Original text</span><span class="sxs-lookup"><span data-stu-id="04781-133">Original text</span></span> | <span data-ttu-id="04781-134">After normalization</span><span class="sxs-lookup"><span data-stu-id="04781-134">After normalization</span></span> |
|----- | ----- |
| <span data-ttu-id="04781-135">"Holy cow!"</span><span class="sxs-lookup"><span data-stu-id="04781-135">"Holy cow!"</span></span> <span data-ttu-id="04781-136">said Batman.</span><span class="sxs-lookup"><span data-stu-id="04781-136">said Batman.</span></span> | <span data-ttu-id="04781-137">holy cow said batman</span><span class="sxs-lookup"><span data-stu-id="04781-137">holy cow said batman</span></span> |
| <span data-ttu-id="04781-138">"What?"</span><span class="sxs-lookup"><span data-stu-id="04781-138">"What?"</span></span> <span data-ttu-id="04781-139">said Batman's sidekick, Robin.</span><span class="sxs-lookup"><span data-stu-id="04781-139">said Batman's sidekick, Robin.</span></span> | <span data-ttu-id="04781-140">what said batman's sidekick robin</span><span class="sxs-lookup"><span data-stu-id="04781-140">what said batman's sidekick robin</span></span> |
| <span data-ttu-id="04781-141">Go get -em!</span><span class="sxs-lookup"><span data-stu-id="04781-141">Go get -em!</span></span> | <span data-ttu-id="04781-142">go get em</span><span class="sxs-lookup"><span data-stu-id="04781-142">go get em</span></span> |
| <span data-ttu-id="04781-143">I'm double-jointed</span><span class="sxs-lookup"><span data-stu-id="04781-143">I'm double-jointed</span></span> | <span data-ttu-id="04781-144">I'm double jointed</span><span class="sxs-lookup"><span data-stu-id="04781-144">I'm double jointed</span></span> |
| <span data-ttu-id="04781-145">104 Elm Street</span><span class="sxs-lookup"><span data-stu-id="04781-145">104 Elm Street</span></span> | <span data-ttu-id="04781-146">one oh four Elm street</span><span class="sxs-lookup"><span data-stu-id="04781-146">one oh four Elm street</span></span> |
| <span data-ttu-id="04781-147">Tune to 102.7</span><span class="sxs-lookup"><span data-stu-id="04781-147">Tune to 102.7</span></span> | <span data-ttu-id="04781-148">tune to one oh two seven</span><span class="sxs-lookup"><span data-stu-id="04781-148">tune to one oh two seven</span></span> |
| <span data-ttu-id="04781-149">Pi is about 3.14</span><span class="sxs-lookup"><span data-stu-id="04781-149">Pi is about 3.14</span></span> | <span data-ttu-id="04781-150">pi is about three point one four</span><span class="sxs-lookup"><span data-stu-id="04781-150">pi is about three point one four</span></span> |
| <span data-ttu-id="04781-151">It costs $3.14</span><span class="sxs-lookup"><span data-stu-id="04781-151">It costs $3.14</span></span> | <span data-ttu-id="04781-152">it costs three fourteen</span><span class="sxs-lookup"><span data-stu-id="04781-152">it costs three fourteen</span></span> |

<span data-ttu-id="04781-153">Apply the following normalization to your text transcripts:</span><span class="sxs-lookup"><span data-stu-id="04781-153">Apply the following normalization to your text transcripts:</span></span>

* <span data-ttu-id="04781-154">Abbreviations should be written out in words.</span><span class="sxs-lookup"><span data-stu-id="04781-154">Abbreviations should be written out in words.</span></span>
* <span data-ttu-id="04781-155">Non-standard numeric strings (such as some date or accounting forms) should be written out in words.</span><span class="sxs-lookup"><span data-stu-id="04781-155">Non-standard numeric strings (such as some date or accounting forms) should be written out in words.</span></span>
* <span data-ttu-id="04781-156">Words with non-alphabetic characters or mixed alphanumeric characters should be transcribed as pronounced.</span><span class="sxs-lookup"><span data-stu-id="04781-156">Words with non-alphabetic characters or mixed alphanumeric characters should be transcribed as pronounced.</span></span>
* <span data-ttu-id="04781-157">Leave abbreviations that are pronounced as words untouched (for example, "radar," "laser," "RAM," or "NATO").</span><span class="sxs-lookup"><span data-stu-id="04781-157">Leave abbreviations that are pronounced as words untouched (for example, "radar," "laser," "RAM," or "NATO").</span></span>
* <span data-ttu-id="04781-158">Write abbreviations that are pronounced as separate letters, with letters separated by spaces (for example, "IBM," "CPU," "FBI," "TBD," or "NaN").</span><span class="sxs-lookup"><span data-stu-id="04781-158">Write abbreviations that are pronounced as separate letters, with letters separated by spaces (for example, "IBM," "CPU," "FBI," "TBD," or "NaN").</span></span> 

<span data-ttu-id="04781-159">Here are some examples:</span><span class="sxs-lookup"><span data-stu-id="04781-159">Here are some examples:</span></span>

| <span data-ttu-id="04781-160">Original text</span><span class="sxs-lookup"><span data-stu-id="04781-160">Original text</span></span> | <span data-ttu-id="04781-161">After normalization</span><span class="sxs-lookup"><span data-stu-id="04781-161">After normalization</span></span> |
|----- | ----- |
| <span data-ttu-id="04781-162">14 NE 3rd Dr.</span><span class="sxs-lookup"><span data-stu-id="04781-162">14 NE 3rd Dr.</span></span> | <span data-ttu-id="04781-163">fourteen northeast third drive</span><span class="sxs-lookup"><span data-stu-id="04781-163">fourteen northeast third drive</span></span> |
| <span data-ttu-id="04781-164">Dr. Bruce Banner</span><span class="sxs-lookup"><span data-stu-id="04781-164">Dr. Bruce Banner</span></span> | <span data-ttu-id="04781-165">Doctor Bruce Banner</span><span class="sxs-lookup"><span data-stu-id="04781-165">Doctor Bruce Banner</span></span> |
| <span data-ttu-id="04781-166">James Bond, 007</span><span class="sxs-lookup"><span data-stu-id="04781-166">James Bond, 007</span></span> | <span data-ttu-id="04781-167">James Bond, double oh seven</span><span class="sxs-lookup"><span data-stu-id="04781-167">James Bond, double oh seven</span></span> |
| <span data-ttu-id="04781-168">Ke$ha</span><span class="sxs-lookup"><span data-stu-id="04781-168">Ke$ha</span></span> | <span data-ttu-id="04781-169">Kesha</span><span class="sxs-lookup"><span data-stu-id="04781-169">Kesha</span></span> |
| <span data-ttu-id="04781-170">How long is the 2x4</span><span class="sxs-lookup"><span data-stu-id="04781-170">How long is the 2x4</span></span> | <span data-ttu-id="04781-171">How long is the two by four</span><span class="sxs-lookup"><span data-stu-id="04781-171">How long is the two by four</span></span> |
| <span data-ttu-id="04781-172">The meeting goes from 1-3pm</span><span class="sxs-lookup"><span data-stu-id="04781-172">The meeting goes from 1-3pm</span></span> | <span data-ttu-id="04781-173">The meeting goes from one to three pm</span><span class="sxs-lookup"><span data-stu-id="04781-173">The meeting goes from one to three pm</span></span> |
| <span data-ttu-id="04781-174">my blood type is O+</span><span class="sxs-lookup"><span data-stu-id="04781-174">my blood type is O+</span></span> | <span data-ttu-id="04781-175">My blood type is O positive</span><span class="sxs-lookup"><span data-stu-id="04781-175">My blood type is O positive</span></span> |
| <span data-ttu-id="04781-176">water is H20</span><span class="sxs-lookup"><span data-stu-id="04781-176">water is H20</span></span> | <span data-ttu-id="04781-177">water is H 2 O</span><span class="sxs-lookup"><span data-stu-id="04781-177">water is H 2 O</span></span> |
| <span data-ttu-id="04781-178">play OU812 by Van Halen</span><span class="sxs-lookup"><span data-stu-id="04781-178">play OU812 by Van Halen</span></span> | <span data-ttu-id="04781-179">play O U 8 1 2 by Van Halen</span><span class="sxs-lookup"><span data-stu-id="04781-179">play O U 8 1 2 by Van Halen</span></span> |
| <span data-ttu-id="04781-180">UTF-8 with BOM</span><span class="sxs-lookup"><span data-stu-id="04781-180">UTF-8 with BOM</span></span> | <span data-ttu-id="04781-181">U T F 8 with BOM</span><span class="sxs-lookup"><span data-stu-id="04781-181">U T F 8 with BOM</span></span> |

## <a name="chinese-zh-cn"></a><span data-ttu-id="04781-182">Chinese (zh-cn)</span><span class="sxs-lookup"><span data-stu-id="04781-182">Chinese (zh-cn)</span></span>

<span data-ttu-id="04781-183">Text data that's uploaded to the Custom Speech Service should use UTF-8 encoding with a byte-order marker.</span><span class="sxs-lookup"><span data-stu-id="04781-183">Text data that's uploaded to the Custom Speech Service should use UTF-8 encoding with a byte-order marker.</span></span> <span data-ttu-id="04781-184">The file should be written one utterance per line.</span><span class="sxs-lookup"><span data-stu-id="04781-184">The file should be written one utterance per line.</span></span>

<span data-ttu-id="04781-185">Avoid the use of half-width punctuation characters.</span><span class="sxs-lookup"><span data-stu-id="04781-185">Avoid the use of half-width punctuation characters.</span></span> <span data-ttu-id="04781-186">These characters can be included inadvertently when you prepare the data in a word-processing program or scrape data from webpages.</span><span class="sxs-lookup"><span data-stu-id="04781-186">These characters can be included inadvertently when you prepare the data in a word-processing program or scrape data from webpages.</span></span> <span data-ttu-id="04781-187">Replace them with appropriate full-width substitutions.</span><span class="sxs-lookup"><span data-stu-id="04781-187">Replace them with appropriate full-width substitutions.</span></span> <span data-ttu-id="04781-188">For example:</span><span class="sxs-lookup"><span data-stu-id="04781-188">For example:</span></span>

| <span data-ttu-id="04781-189">Characters to avoid</span><span class="sxs-lookup"><span data-stu-id="04781-189">Characters to avoid</span></span> | <span data-ttu-id="04781-190">Substitution</span><span class="sxs-lookup"><span data-stu-id="04781-190">Substitution</span></span> |
|----- | ----- |
| <span data-ttu-id="04781-191">"你好" (opening and closing double quotation marks)</span><span class="sxs-lookup"><span data-stu-id="04781-191">"你好" (opening and closing double quotation marks)</span></span> | <span data-ttu-id="04781-192">"你好" (double quotation marks)</span><span class="sxs-lookup"><span data-stu-id="04781-192">"你好" (double quotation marks)</span></span> |
| <span data-ttu-id="04781-193">需要什么帮助?</span><span class="sxs-lookup"><span data-stu-id="04781-193">需要什么帮助?</span></span> <span data-ttu-id="04781-194">(question mark)</span><span class="sxs-lookup"><span data-stu-id="04781-194">(question mark)</span></span> | <span data-ttu-id="04781-195">需要什么帮助？</span><span class="sxs-lookup"><span data-stu-id="04781-195">需要什么帮助？</span></span> |

### <a name="text-normalization-rules-for-chinese"></a><span data-ttu-id="04781-196">Text normalization rules for Chinese</span><span class="sxs-lookup"><span data-stu-id="04781-196">Text normalization rules for Chinese</span></span>

<span data-ttu-id="04781-197">The Speech Service carries out the following normalization rules:</span><span class="sxs-lookup"><span data-stu-id="04781-197">The Speech Service carries out the following normalization rules:</span></span>

* <span data-ttu-id="04781-198">Removing all punctuation</span><span class="sxs-lookup"><span data-stu-id="04781-198">Removing all punctuation</span></span>
* <span data-ttu-id="04781-199">Expanding numbers to spoken form</span><span class="sxs-lookup"><span data-stu-id="04781-199">Expanding numbers to spoken form</span></span>
* <span data-ttu-id="04781-200">Converting full-width letters to half-width letters</span><span class="sxs-lookup"><span data-stu-id="04781-200">Converting full-width letters to half-width letters</span></span>
* <span data-ttu-id="04781-201">Using uppercase letters for all English words</span><span class="sxs-lookup"><span data-stu-id="04781-201">Using uppercase letters for all English words</span></span>

<span data-ttu-id="04781-202">Here are some examples:</span><span class="sxs-lookup"><span data-stu-id="04781-202">Here are some examples:</span></span>

| <span data-ttu-id="04781-203">Original text</span><span class="sxs-lookup"><span data-stu-id="04781-203">Original text</span></span> | <span data-ttu-id="04781-204">After normalization</span><span class="sxs-lookup"><span data-stu-id="04781-204">After normalization</span></span> |
|----- | ----- |
| <span data-ttu-id="04781-205">3.1415</span><span class="sxs-lookup"><span data-stu-id="04781-205">3.1415</span></span> | <span data-ttu-id="04781-206">三 点 一 四 一 五</span><span class="sxs-lookup"><span data-stu-id="04781-206">三 点 一 四 一 五</span></span> |
| <span data-ttu-id="04781-207">￥3.5</span><span class="sxs-lookup"><span data-stu-id="04781-207">￥3.5</span></span> | <span data-ttu-id="04781-208">三 元 五 角</span><span class="sxs-lookup"><span data-stu-id="04781-208">三 元 五 角</span></span> |
| <span data-ttu-id="04781-209">w f y z</span><span class="sxs-lookup"><span data-stu-id="04781-209">w f y z</span></span> | <span data-ttu-id="04781-210">W F Y Z</span><span class="sxs-lookup"><span data-stu-id="04781-210">W F Y Z</span></span> |
| <span data-ttu-id="04781-211">1992年8月8日</span><span class="sxs-lookup"><span data-stu-id="04781-211">1992年8月8日</span></span> | <span data-ttu-id="04781-212">一 九 九 二 年 八 月 八 日</span><span class="sxs-lookup"><span data-stu-id="04781-212">一 九 九 二 年 八 月 八 日</span></span> |
| <span data-ttu-id="04781-213">你吃饭了吗?</span><span class="sxs-lookup"><span data-stu-id="04781-213">你吃饭了吗?</span></span> | <span data-ttu-id="04781-214">你 吃饭 了 吗</span><span class="sxs-lookup"><span data-stu-id="04781-214">你 吃饭 了 吗</span></span> |
| <span data-ttu-id="04781-215">下午5:00的航班</span><span class="sxs-lookup"><span data-stu-id="04781-215">下午5:00的航班</span></span> | <span data-ttu-id="04781-216">下午 五点 的 航班</span><span class="sxs-lookup"><span data-stu-id="04781-216">下午 五点 的 航班</span></span> |
| <span data-ttu-id="04781-217">我今年21岁</span><span class="sxs-lookup"><span data-stu-id="04781-217">我今年21岁</span></span> | <span data-ttu-id="04781-218">我 今年 二十 一 岁</span><span class="sxs-lookup"><span data-stu-id="04781-218">我 今年 二十 一 岁</span></span> |

<span data-ttu-id="04781-219">Before you import your text, apply the following normalization to it:</span><span class="sxs-lookup"><span data-stu-id="04781-219">Before you import your text, apply the following normalization to it:</span></span>

* <span data-ttu-id="04781-220">Abbreviations should be written out in words (as in spoken form).</span><span class="sxs-lookup"><span data-stu-id="04781-220">Abbreviations should be written out in words (as in spoken form).</span></span>
* <span data-ttu-id="04781-221">Write out numeric strings in spoken form.</span><span class="sxs-lookup"><span data-stu-id="04781-221">Write out numeric strings in spoken form.</span></span>

<span data-ttu-id="04781-222">Here are some examples:</span><span class="sxs-lookup"><span data-stu-id="04781-222">Here are some examples:</span></span>

| <span data-ttu-id="04781-223">Original text</span><span class="sxs-lookup"><span data-stu-id="04781-223">Original text</span></span> | <span data-ttu-id="04781-224">After normalization</span><span class="sxs-lookup"><span data-stu-id="04781-224">After normalization</span></span> |
|----- | ----- |
| <span data-ttu-id="04781-225">我今年21</span><span class="sxs-lookup"><span data-stu-id="04781-225">我今年21</span></span> | <span data-ttu-id="04781-226">我今年二十一</span><span class="sxs-lookup"><span data-stu-id="04781-226">我今年二十一</span></span> |
| <span data-ttu-id="04781-227">3号楼504</span><span class="sxs-lookup"><span data-stu-id="04781-227">3号楼504</span></span> | <span data-ttu-id="04781-228">三号 楼 五 零 四</span><span class="sxs-lookup"><span data-stu-id="04781-228">三号 楼 五 零 四</span></span> |

## <a name="other-languages"></a><span data-ttu-id="04781-229">Other languages</span><span class="sxs-lookup"><span data-stu-id="04781-229">Other languages</span></span>

<span data-ttu-id="04781-230">Text data uploaded to the **Speech to Text** service must use UTF-8 encoding with a byte-order marker.</span><span class="sxs-lookup"><span data-stu-id="04781-230">Text data uploaded to the **Speech to Text** service must use UTF-8 encoding with a byte-order marker.</span></span> <span data-ttu-id="04781-231">The file should be written one utterance per line.</span><span class="sxs-lookup"><span data-stu-id="04781-231">The file should be written one utterance per line.</span></span>

> [!NOTE]
> <span data-ttu-id="04781-232">The following examples use German.</span><span class="sxs-lookup"><span data-stu-id="04781-232">The following examples use German.</span></span> <span data-ttu-id="04781-233">However, the guidelines apply to all languages that are not US English or Chinese.</span><span class="sxs-lookup"><span data-stu-id="04781-233">However, the guidelines apply to all languages that are not US English or Chinese.</span></span>

### <a name="text-normalization-rules-for-german"></a><span data-ttu-id="04781-234">Text normalization rules for German</span><span class="sxs-lookup"><span data-stu-id="04781-234">Text normalization rules for German</span></span>

<span data-ttu-id="04781-235">The Speech Service carries out the following normalization rules:</span><span class="sxs-lookup"><span data-stu-id="04781-235">The Speech Service carries out the following normalization rules:</span></span>

* <span data-ttu-id="04781-236">Using lowercase letters for all text</span><span class="sxs-lookup"><span data-stu-id="04781-236">Using lowercase letters for all text</span></span>
* <span data-ttu-id="04781-237">Removing all punctuation, including various types of quotation marks ("test", 'test', "test„ and «test» are OK)</span><span class="sxs-lookup"><span data-stu-id="04781-237">Removing all punctuation, including various types of quotation marks ("test", 'test', "test„ and «test» are OK)</span></span>
* <span data-ttu-id="04781-238">Discarding rows with any special character from the set  ¢ ¤ ¥ ¦ § © ª ¬ ® ° ± ² µ × ÿ Ø¬¬</span><span class="sxs-lookup"><span data-stu-id="04781-238">Discarding rows with any special character from the set  ¢ ¤ ¥ ¦ § © ª ¬ ® ° ± ² µ × ÿ Ø¬¬</span></span>
* <span data-ttu-id="04781-239">Expanding numbers to word form, including dollar or Euro amounts</span><span class="sxs-lookup"><span data-stu-id="04781-239">Expanding numbers to word form, including dollar or Euro amounts</span></span>
* <span data-ttu-id="04781-240">Accepting umlauts only for a, o, and u; others will be replaced by "th" or be discarded</span><span class="sxs-lookup"><span data-stu-id="04781-240">Accepting umlauts only for a, o, and u; others will be replaced by "th" or be discarded</span></span>

<span data-ttu-id="04781-241">Here are some examples:</span><span class="sxs-lookup"><span data-stu-id="04781-241">Here are some examples:</span></span>

| <span data-ttu-id="04781-242">Original text</span><span class="sxs-lookup"><span data-stu-id="04781-242">Original text</span></span> | <span data-ttu-id="04781-243">After normalization</span><span class="sxs-lookup"><span data-stu-id="04781-243">After normalization</span></span> |
|----- | ----- |
| <span data-ttu-id="04781-244">Frankfurter Ring</span><span class="sxs-lookup"><span data-stu-id="04781-244">Frankfurter Ring</span></span> | <span data-ttu-id="04781-245">frankfurter ring</span><span class="sxs-lookup"><span data-stu-id="04781-245">frankfurter ring</span></span> |
| <span data-ttu-id="04781-246">¡Eine Frage!</span><span class="sxs-lookup"><span data-stu-id="04781-246">¡Eine Frage!</span></span> | <span data-ttu-id="04781-247">eine frage</span><span class="sxs-lookup"><span data-stu-id="04781-247">eine frage</span></span> |
| <span data-ttu-id="04781-248">wir, haben</span><span class="sxs-lookup"><span data-stu-id="04781-248">wir, haben</span></span> | <span data-ttu-id="04781-249">wir haben</span><span class="sxs-lookup"><span data-stu-id="04781-249">wir haben</span></span> |

<span data-ttu-id="04781-250">Before you import your text, apply the following normalization to it:</span><span class="sxs-lookup"><span data-stu-id="04781-250">Before you import your text, apply the following normalization to it:</span></span>

* <span data-ttu-id="04781-251">Decimal points should be "," and not ".".</span><span class="sxs-lookup"><span data-stu-id="04781-251">Decimal points should be "," and not ".".</span></span>
* <span data-ttu-id="04781-252">Time separators between hours and minutes should be ":" and not "." (for example, 12:00 Uhr).</span><span class="sxs-lookup"><span data-stu-id="04781-252">Time separators between hours and minutes should be ":" and not "." (for example, 12:00 Uhr).</span></span>
* <span data-ttu-id="04781-253">Abbreviations such as "ca."</span><span class="sxs-lookup"><span data-stu-id="04781-253">Abbreviations such as "ca."</span></span> <span data-ttu-id="04781-254">aren't replaced.</span><span class="sxs-lookup"><span data-stu-id="04781-254">aren't replaced.</span></span> <span data-ttu-id="04781-255">We recommend that you use the full form.</span><span class="sxs-lookup"><span data-stu-id="04781-255">We recommend that you use the full form.</span></span>
* <span data-ttu-id="04781-256">The four main mathematical operators (+, -, \*, and /) are removed.</span><span class="sxs-lookup"><span data-stu-id="04781-256">The four main mathematical operators (+, -, \*, and /) are removed.</span></span> <span data-ttu-id="04781-257">We recommend replacing them with their literal form: "plus," "minus," "mal," and "geteilt."</span><span class="sxs-lookup"><span data-stu-id="04781-257">We recommend replacing them with their literal form: "plus," "minus," "mal," and "geteilt."</span></span>
* <span data-ttu-id="04781-258">The same rule applies to comparison operators (=, <, and >).</span><span class="sxs-lookup"><span data-stu-id="04781-258">The same rule applies to comparison operators (=, <, and >).</span></span> <span data-ttu-id="04781-259">We recommend replacing them with "gleich," "kleiner als," and "grösser als."</span><span class="sxs-lookup"><span data-stu-id="04781-259">We recommend replacing them with "gleich," "kleiner als," and "grösser als."</span></span>
* <span data-ttu-id="04781-260">Use fractions, such as 3/4, in word form (for example, "drei viertel" instead of ¾).</span><span class="sxs-lookup"><span data-stu-id="04781-260">Use fractions, such as 3/4, in word form (for example, "drei viertel" instead of ¾).</span></span>
* <span data-ttu-id="04781-261">Replace the € symbol with the word form "Euro."</span><span class="sxs-lookup"><span data-stu-id="04781-261">Replace the € symbol with the word form "Euro."</span></span>

<span data-ttu-id="04781-262">Here are some examples:</span><span class="sxs-lookup"><span data-stu-id="04781-262">Here are some examples:</span></span>

| <span data-ttu-id="04781-263">Original text</span><span class="sxs-lookup"><span data-stu-id="04781-263">Original text</span></span> | <span data-ttu-id="04781-264">After user's normalization</span><span class="sxs-lookup"><span data-stu-id="04781-264">After user's normalization</span></span> | <span data-ttu-id="04781-265">After system normalization</span><span class="sxs-lookup"><span data-stu-id="04781-265">After system normalization</span></span>
|--------  | ----- | -------- |
| <span data-ttu-id="04781-266">Es ist 12.23 Uhr</span><span class="sxs-lookup"><span data-stu-id="04781-266">Es ist 12.23 Uhr</span></span> | <span data-ttu-id="04781-267">Es ist 12:23 Uhr</span><span class="sxs-lookup"><span data-stu-id="04781-267">Es ist 12:23 Uhr</span></span> | <span data-ttu-id="04781-268">es ist zwölf uhr drei und zwanzig uhr</span><span class="sxs-lookup"><span data-stu-id="04781-268">es ist zwölf uhr drei und zwanzig uhr</span></span> |
| <span data-ttu-id="04781-269">{12.45}</span><span class="sxs-lookup"><span data-stu-id="04781-269">{12.45}</span></span> | {12,45} | <span data-ttu-id="04781-270">zwölf komma vier fünf</span><span class="sxs-lookup"><span data-stu-id="04781-270">zwölf komma vier fünf</span></span> ||
| <span data-ttu-id="04781-271">2 + 3 - 4</span><span class="sxs-lookup"><span data-stu-id="04781-271">2 + 3 - 4</span></span> | <span data-ttu-id="04781-272">2 plus 3 minus 4</span><span class="sxs-lookup"><span data-stu-id="04781-272">2 plus 3 minus 4</span></span> | <span data-ttu-id="04781-273">zwei plus drei minus vier</span><span class="sxs-lookup"><span data-stu-id="04781-273">zwei plus drei minus vier</span></span>|

## <a name="next-steps"></a><span data-ttu-id="04781-274">Next steps</span><span class="sxs-lookup"><span data-stu-id="04781-274">Next steps</span></span>

- [<span data-ttu-id="04781-275">Get your Speech Service trial subscription</span><span class="sxs-lookup"><span data-stu-id="04781-275">Get your Speech Service trial subscription</span></span>](https://azure.microsoft.com/try/cognitive-services/)
- [<span data-ttu-id="04781-276">Recognize speech in C#</span><span class="sxs-lookup"><span data-stu-id="04781-276">Recognize speech in C#</span></span>](quickstart-csharp-dotnet-windows.md)
