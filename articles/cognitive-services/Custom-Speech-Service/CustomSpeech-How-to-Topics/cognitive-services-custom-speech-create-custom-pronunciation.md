---
title: Use custom pronunciation with Custom Speech Service on Azure | Microsoft Docs
description: Learn how to create a language model with the Custom Speech Service in Cognitive Services.
services: cognitive-services
author: PanosPeriorellis
manager: onano
ms.service: cognitive-services
ms.component: custom-speech
ms.topic: article
ms.date: 11/23/2017
ms.author: panosper
ms.openlocfilehash: a74b69b84cc80809a25f18b580a18abb5721b8b1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855573"
---
# <a name="enable-custom-pronunciation"></a><span data-ttu-id="81cea-103">Enable custom pronunciation</span><span class="sxs-lookup"><span data-stu-id="81cea-103">Enable custom pronunciation</span></span>
<span data-ttu-id="81cea-104">Custom pronunciation enables users to define the phonetic form and display of a word or term.</span><span class="sxs-lookup"><span data-stu-id="81cea-104">Custom pronunciation enables users to define the phonetic form and display of a word or term.</span></span> <span data-ttu-id="81cea-105">It is useful for handling customized terms, such as product names or acronyms.</span><span class="sxs-lookup"><span data-stu-id="81cea-105">It is useful for handling customized terms, such as product names or acronyms.</span></span> <span data-ttu-id="81cea-106">All you need is a pronunciation file (a simple .txt file).</span><span class="sxs-lookup"><span data-stu-id="81cea-106">All you need is a pronunciation file (a simple .txt file).</span></span>

<span data-ttu-id="81cea-107">Here's how it works.</span><span class="sxs-lookup"><span data-stu-id="81cea-107">Here's how it works.</span></span> <span data-ttu-id="81cea-108">In a single .txt file, you can enter several custom pronunciation entries.</span><span class="sxs-lookup"><span data-stu-id="81cea-108">In a single .txt file, you can enter several custom pronunciation entries.</span></span> <span data-ttu-id="81cea-109">The structure is as follows:</span><span class="sxs-lookup"><span data-stu-id="81cea-109">The structure is as follows:</span></span>

```
Display form <Tab> Spoken form <Newline>
```

<span data-ttu-id="81cea-110">*Examples*:</span><span class="sxs-lookup"><span data-stu-id="81cea-110">*Examples*:</span></span>

| <span data-ttu-id="81cea-111">Display form</span><span class="sxs-lookup"><span data-stu-id="81cea-111">Display form</span></span> | <span data-ttu-id="81cea-112">Spoken form</span><span class="sxs-lookup"><span data-stu-id="81cea-112">Spoken form</span></span> |
|----------|-------|
| <span data-ttu-id="81cea-113">C3PO</span><span class="sxs-lookup"><span data-stu-id="81cea-113">C3PO</span></span> | <span data-ttu-id="81cea-114">see three pea o</span><span class="sxs-lookup"><span data-stu-id="81cea-114">see three pea o</span></span> |
| <span data-ttu-id="81cea-115">L8R</span><span class="sxs-lookup"><span data-stu-id="81cea-115">L8R</span></span> | <span data-ttu-id="81cea-116">late are</span><span class="sxs-lookup"><span data-stu-id="81cea-116">late are</span></span> |
| <span data-ttu-id="81cea-117">CNTK</span><span class="sxs-lookup"><span data-stu-id="81cea-117">CNTK</span></span> | <span data-ttu-id="81cea-118">see n tea k</span><span class="sxs-lookup"><span data-stu-id="81cea-118">see n tea k</span></span>|

## <a name="requirements-for-the-spoken-form"></a><span data-ttu-id="81cea-119">Requirements for the spoken form</span><span class="sxs-lookup"><span data-stu-id="81cea-119">Requirements for the spoken form</span></span>
<span data-ttu-id="81cea-120">The spoken form must be lowercase, which can be forced during the import.</span><span class="sxs-lookup"><span data-stu-id="81cea-120">The spoken form must be lowercase, which can be forced during the import.</span></span> <span data-ttu-id="81cea-121">In addition, you must provide checks in the data importer.</span><span class="sxs-lookup"><span data-stu-id="81cea-121">In addition, you must provide checks in the data importer.</span></span> <span data-ttu-id="81cea-122">No tab in either the spoken form or the display form is permitted.</span><span class="sxs-lookup"><span data-stu-id="81cea-122">No tab in either the spoken form or the display form is permitted.</span></span> <span data-ttu-id="81cea-123">There might, however, be more forbidden characters in the display form (for example, ~ and ^).</span><span class="sxs-lookup"><span data-stu-id="81cea-123">There might, however, be more forbidden characters in the display form (for example, ~ and ^).</span></span>

<span data-ttu-id="81cea-124">Each .txt file can have several entries.</span><span class="sxs-lookup"><span data-stu-id="81cea-124">Each .txt file can have several entries.</span></span> <span data-ttu-id="81cea-125">For example, see the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="81cea-125">For example, see the following screenshot:</span></span>

![Screenshot of Notepad with several entries for acronym pronunciation](../../../media/cognitive-services/custom-speech-service/custom-speech-pronunciation-file.png)

<span data-ttu-id="81cea-127">The spoken form is the phonetic sequence of the display form.</span><span class="sxs-lookup"><span data-stu-id="81cea-127">The spoken form is the phonetic sequence of the display form.</span></span> <span data-ttu-id="81cea-128">It is composed of letters, words, or syllables.</span><span class="sxs-lookup"><span data-stu-id="81cea-128">It is composed of letters, words, or syllables.</span></span> <span data-ttu-id="81cea-129">Currently, there is no further guidance or set of standards to help you formulate the spoken form.</span><span class="sxs-lookup"><span data-stu-id="81cea-129">Currently, there is no further guidance or set of standards to help you formulate the spoken form.</span></span> 

## <a name="supported-pronunciation-characters"></a><span data-ttu-id="81cea-130">Supported pronunciation characters</span><span class="sxs-lookup"><span data-stu-id="81cea-130">Supported pronunciation characters</span></span>
<span data-ttu-id="81cea-131">Custom Pronunciation is currently supported for English (en-US) and German (de-de).</span><span class="sxs-lookup"><span data-stu-id="81cea-131">Custom Pronunciation is currently supported for English (en-US) and German (de-de).</span></span> <span data-ttu-id="81cea-132">The character set that can be used to express the spoken form of a term (in the custom pronunciation file) is shown in the following table:</span><span class="sxs-lookup"><span data-stu-id="81cea-132">The character set that can be used to express the spoken form of a term (in the custom pronunciation file) is shown in the following table:</span></span> 

| <span data-ttu-id="81cea-133">Language</span><span class="sxs-lookup"><span data-stu-id="81cea-133">Language</span></span> | <span data-ttu-id="81cea-134">Characters</span><span class="sxs-lookup"><span data-stu-id="81cea-134">Characters</span></span> |
|---------- |----------|
| <span data-ttu-id="81cea-135">English (en-US)</span><span class="sxs-lookup"><span data-stu-id="81cea-135">English (en-US)</span></span> | <span data-ttu-id="81cea-136">a, b, c, d, e, f, g, h, i, j, k, l, o, p, q, r, s, t, u, v, w, x, y, z</span><span class="sxs-lookup"><span data-stu-id="81cea-136">a, b, c, d, e, f, g, h, i, j, k, l, o, p, q, r, s, t, u, v, w, x, y, z</span></span> |
| <span data-ttu-id="81cea-137">German (de-de)</span><span class="sxs-lookup"><span data-stu-id="81cea-137">German (de-de)</span></span> | <span data-ttu-id="81cea-138">ä, ö, ü, ẞ, a, b, c, d, e, f, g, h, i, j, k, l, o, p, q, r, s, t, u, v, w, x, y, z</span><span class="sxs-lookup"><span data-stu-id="81cea-138">ä, ö, ü, ẞ, a, b, c, d, e, f, g, h, i, j, k, l, o, p, q, r, s, t, u, v, w, x, y, z</span></span> |

><span data-ttu-id="81cea-139">[NOTE] A term's display form (in a pronunciation file) should be written the same way in a language adaptation data set.</span><span class="sxs-lookup"><span data-stu-id="81cea-139">[NOTE] A term's display form (in a pronunciation file) should be written the same way in a language adaptation data set.</span></span>

## <a name="requirements-for-the-display-form"></a><span data-ttu-id="81cea-140">Requirements for the display form</span><span class="sxs-lookup"><span data-stu-id="81cea-140">Requirements for the display form</span></span>
<span data-ttu-id="81cea-141">A display form can only be a custom word, term, acronym, or compound words that combine existing words.</span><span class="sxs-lookup"><span data-stu-id="81cea-141">A display form can only be a custom word, term, acronym, or compound words that combine existing words.</span></span> <span data-ttu-id="81cea-142">You can also enter alternative pronunciations for common words.</span><span class="sxs-lookup"><span data-stu-id="81cea-142">You can also enter alternative pronunciations for common words.</span></span> 

>[!NOTE]
<span data-ttu-id="81cea-143">We do not recommend using this feature to reformulate common words or to modify the spoken form.</span><span class="sxs-lookup"><span data-stu-id="81cea-143">We do not recommend using this feature to reformulate common words or to modify the spoken form.</span></span> <span data-ttu-id="81cea-144">It is better to run the decoder to see if some unusual words (such as abbreviations, technical words, and foreign words) are not correctly decoded.</span><span class="sxs-lookup"><span data-stu-id="81cea-144">It is better to run the decoder to see if some unusual words (such as abbreviations, technical words, and foreign words) are not correctly decoded.</span></span> <span data-ttu-id="81cea-145">If they are, add them to the custom pronunciation file.</span><span class="sxs-lookup"><span data-stu-id="81cea-145">If they are, add them to the custom pronunciation file.</span></span> <span data-ttu-id="81cea-146">In the Language Model, you should always and only use the display form of a word.</span><span class="sxs-lookup"><span data-stu-id="81cea-146">In the Language Model, you should always and only use the display form of a word.</span></span> 

## <a name="requirements-for-the-file-size"></a><span data-ttu-id="81cea-147">Requirements for the file size</span><span class="sxs-lookup"><span data-stu-id="81cea-147">Requirements for the file size</span></span>
<span data-ttu-id="81cea-148">The size of the .txt file containing the pronunciation entries is limited to 1 MB.</span><span class="sxs-lookup"><span data-stu-id="81cea-148">The size of the .txt file containing the pronunciation entries is limited to 1 MB.</span></span> <span data-ttu-id="81cea-149">Typically, you do not need to upload large amounts of data through this file.</span><span class="sxs-lookup"><span data-stu-id="81cea-149">Typically, you do not need to upload large amounts of data through this file.</span></span> <span data-ttu-id="81cea-150">Most custom pronunciation files are likely to be just a few KBs in size.</span><span class="sxs-lookup"><span data-stu-id="81cea-150">Most custom pronunciation files are likely to be just a few KBs in size.</span></span> <span data-ttu-id="81cea-151">The encoding of the .txt file for all locales should be UTF-8 BOM.</span><span class="sxs-lookup"><span data-stu-id="81cea-151">The encoding of the .txt file for all locales should be UTF-8 BOM.</span></span> <span data-ttu-id="81cea-152">For the English locale, ANSI is also acceptable.</span><span class="sxs-lookup"><span data-stu-id="81cea-152">For the English locale, ANSI is also acceptable.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81cea-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="81cea-153">Next steps</span></span>
* <span data-ttu-id="81cea-154">Improve recognition accuracy by creating your [custom acoustic model](cognitive-services-custom-speech-create-acoustic-model.md).</span><span class="sxs-lookup"><span data-stu-id="81cea-154">Improve recognition accuracy by creating your [custom acoustic model](cognitive-services-custom-speech-create-acoustic-model.md).</span></span>
* <span data-ttu-id="81cea-155">[Create a custom speech-to-text endpoint](cognitive-services-custom-speech-create-endpoint.md), which you can use from an app.</span><span class="sxs-lookup"><span data-stu-id="81cea-155">[Create a custom speech-to-text endpoint](cognitive-services-custom-speech-create-endpoint.md), which you can use from an app.</span></span>
