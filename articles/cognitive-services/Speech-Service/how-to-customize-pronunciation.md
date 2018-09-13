---
title: Azure Cognitive Services Speech Service
description: Learn how to customize pronunciation with the Speech Service Cognitive Services.
services: cognitive-services
author: PanosPeriorellis
ms.service: cognitive-services
ms.component: custom-speech
ms.topic: article
ms.date: 07/02/2018
ms.author: panosper
ms.openlocfilehash: 93fec1ea78263798588a43b2314ffdea736cdbbc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857924"
---
# <a name="enable-custom-pronunciation"></a><span data-ttu-id="6f50a-103">Enable custom pronunciation</span><span class="sxs-lookup"><span data-stu-id="6f50a-103">Enable custom pronunciation</span></span>
<span data-ttu-id="6f50a-104">By using custom pronunciation, you can define the phonetic form and display of a word or term.</span><span class="sxs-lookup"><span data-stu-id="6f50a-104">By using custom pronunciation, you can define the phonetic form and display of a word or term.</span></span> <span data-ttu-id="6f50a-105">It is useful for handling customized terms, such as product names or acronyms.</span><span class="sxs-lookup"><span data-stu-id="6f50a-105">It is useful for handling customized terms, such as product names or acronyms.</span></span> <span data-ttu-id="6f50a-106">All you need is a pronunciation file (a simple .txt file).</span><span class="sxs-lookup"><span data-stu-id="6f50a-106">All you need is a pronunciation file (a simple .txt file).</span></span>

<span data-ttu-id="6f50a-107">Here's how it works.</span><span class="sxs-lookup"><span data-stu-id="6f50a-107">Here's how it works.</span></span> <span data-ttu-id="6f50a-108">In a single .txt file, you can enter several custom pronunciation entries.</span><span class="sxs-lookup"><span data-stu-id="6f50a-108">In a single .txt file, you can enter several custom pronunciation entries.</span></span> <span data-ttu-id="6f50a-109">The structure is as follows:</span><span class="sxs-lookup"><span data-stu-id="6f50a-109">The structure is as follows:</span></span>

```
Display form <Tab> Spoken form <Newline>
```

<span data-ttu-id="6f50a-110">Several examples are shown in the following table:</span><span class="sxs-lookup"><span data-stu-id="6f50a-110">Several examples are shown in the following table:</span></span>

| <span data-ttu-id="6f50a-111">Display form</span><span class="sxs-lookup"><span data-stu-id="6f50a-111">Display form</span></span> | <span data-ttu-id="6f50a-112">Spoken form</span><span class="sxs-lookup"><span data-stu-id="6f50a-112">Spoken form</span></span> |
|----------|-------|
| <span data-ttu-id="6f50a-113">C3PO</span><span class="sxs-lookup"><span data-stu-id="6f50a-113">C3PO</span></span> | <span data-ttu-id="6f50a-114">see three pea o</span><span class="sxs-lookup"><span data-stu-id="6f50a-114">see three pea o</span></span> |
| <span data-ttu-id="6f50a-115">L8R</span><span class="sxs-lookup"><span data-stu-id="6f50a-115">L8R</span></span> | <span data-ttu-id="6f50a-116">late are</span><span class="sxs-lookup"><span data-stu-id="6f50a-116">late are</span></span> |
| <span data-ttu-id="6f50a-117">CNTK</span><span class="sxs-lookup"><span data-stu-id="6f50a-117">CNTK</span></span> | <span data-ttu-id="6f50a-118">see n tea k</span><span class="sxs-lookup"><span data-stu-id="6f50a-118">see n tea k</span></span>|

## <a name="requirements-for-the-spoken-form"></a><span data-ttu-id="6f50a-119">Requirements for the spoken form</span><span class="sxs-lookup"><span data-stu-id="6f50a-119">Requirements for the spoken form</span></span>
<span data-ttu-id="6f50a-120">The spoken form must be lowercase, which you can force during the import.</span><span class="sxs-lookup"><span data-stu-id="6f50a-120">The spoken form must be lowercase, which you can force during the import.</span></span> <span data-ttu-id="6f50a-121">In addition, you must provide checks in the data importer.</span><span class="sxs-lookup"><span data-stu-id="6f50a-121">In addition, you must provide checks in the data importer.</span></span> <span data-ttu-id="6f50a-122">No tab in either the spoken form or the display form is permitted.</span><span class="sxs-lookup"><span data-stu-id="6f50a-122">No tab in either the spoken form or the display form is permitted.</span></span> <span data-ttu-id="6f50a-123">However, there might be more forbidden characters in the display form (for example, ~ and ^).</span><span class="sxs-lookup"><span data-stu-id="6f50a-123">However, there might be more forbidden characters in the display form (for example, ~ and ^).</span></span>

<span data-ttu-id="6f50a-124">Each .txt file can have several entries, as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="6f50a-124">Each .txt file can have several entries, as shown in the following image:</span></span>

![Examples of acronym pronunciation](media/stt/custom-speech-pronunciation-file.png)

<span data-ttu-id="6f50a-126">The spoken form is the phonetic sequence of the display form.</span><span class="sxs-lookup"><span data-stu-id="6f50a-126">The spoken form is the phonetic sequence of the display form.</span></span> <span data-ttu-id="6f50a-127">It is composed of letters, words, or syllables.</span><span class="sxs-lookup"><span data-stu-id="6f50a-127">It is composed of letters, words, or syllables.</span></span> <span data-ttu-id="6f50a-128">Currently, there is no further guidance or set of standards to help you formulate the spoken form.</span><span class="sxs-lookup"><span data-stu-id="6f50a-128">Currently, there is no further guidance or set of standards to help you formulate the spoken form.</span></span> 

## <a name="supported-pronunciation-characters"></a><span data-ttu-id="6f50a-129">Supported pronunciation characters</span><span class="sxs-lookup"><span data-stu-id="6f50a-129">Supported pronunciation characters</span></span>
<span data-ttu-id="6f50a-130">Custom pronunciation is currently supported for English (en-US) and German (de-de).</span><span class="sxs-lookup"><span data-stu-id="6f50a-130">Custom pronunciation is currently supported for English (en-US) and German (de-de).</span></span> <span data-ttu-id="6f50a-131">The character sets that you can use to express the spoken form of a term (in the custom pronunciation file) are shown in the following table:</span><span class="sxs-lookup"><span data-stu-id="6f50a-131">The character sets that you can use to express the spoken form of a term (in the custom pronunciation file) are shown in the following table:</span></span> 

| <span data-ttu-id="6f50a-132">Language</span><span class="sxs-lookup"><span data-stu-id="6f50a-132">Language</span></span> | <span data-ttu-id="6f50a-133">Characters</span><span class="sxs-lookup"><span data-stu-id="6f50a-133">Characters</span></span> |
|---------- |----------|
| <span data-ttu-id="6f50a-134">English (en-US)</span><span class="sxs-lookup"><span data-stu-id="6f50a-134">English (en-US)</span></span> | <span data-ttu-id="6f50a-135">a, b, c, d, e, f, g, h, i, j, k, l, o, p, q, r, s, t, u, v, w, x, y, z</span><span class="sxs-lookup"><span data-stu-id="6f50a-135">a, b, c, d, e, f, g, h, i, j, k, l, o, p, q, r, s, t, u, v, w, x, y, z</span></span> |
| <span data-ttu-id="6f50a-136">German (de-de)</span><span class="sxs-lookup"><span data-stu-id="6f50a-136">German (de-de)</span></span> | <span data-ttu-id="6f50a-137">ä, ö, ü, ẞ, a, b, c, d, e, f, g, h, i, j, k, l, o, p, q, r, s, t, u, v, w, x, y, z</span><span class="sxs-lookup"><span data-stu-id="6f50a-137">ä, ö, ü, ẞ, a, b, c, d, e, f, g, h, i, j, k, l, o, p, q, r, s, t, u, v, w, x, y, z</span></span> |

> [!NOTE]
> <span data-ttu-id="6f50a-138">A term's display form (in a pronunciation file) should be written the same way in a language adaptation dataset.</span><span class="sxs-lookup"><span data-stu-id="6f50a-138">A term's display form (in a pronunciation file) should be written the same way in a language adaptation dataset.</span></span>

## <a name="requirements-for-the-display-form"></a><span data-ttu-id="6f50a-139">Requirements for the display form</span><span class="sxs-lookup"><span data-stu-id="6f50a-139">Requirements for the display form</span></span>
<span data-ttu-id="6f50a-140">A display form can be only a custom word, a term, an acronym, or compound words that combine existing words.</span><span class="sxs-lookup"><span data-stu-id="6f50a-140">A display form can be only a custom word, a term, an acronym, or compound words that combine existing words.</span></span> <span data-ttu-id="6f50a-141">You can also enter alternative pronunciations for common words.</span><span class="sxs-lookup"><span data-stu-id="6f50a-141">You can also enter alternative pronunciations for common words.</span></span> 

>[!NOTE]
><span data-ttu-id="6f50a-142">We do not recommend using this feature to reformulate common words or to modify the spoken form.</span><span class="sxs-lookup"><span data-stu-id="6f50a-142">We do not recommend using this feature to reformulate common words or to modify the spoken form.</span></span> <span data-ttu-id="6f50a-143">It is better to run the decoder to see whether some unusual words (such as abbreviations, technical words, or foreign words) are incorrectly decoded.</span><span class="sxs-lookup"><span data-stu-id="6f50a-143">It is better to run the decoder to see whether some unusual words (such as abbreviations, technical words, or foreign words) are incorrectly decoded.</span></span> <span data-ttu-id="6f50a-144">If they are, add them to the custom pronunciation file.</span><span class="sxs-lookup"><span data-stu-id="6f50a-144">If they are, add them to the custom pronunciation file.</span></span> <span data-ttu-id="6f50a-145">In the language model, you should always and only use the display form of a word.</span><span class="sxs-lookup"><span data-stu-id="6f50a-145">In the language model, you should always and only use the display form of a word.</span></span> 

## <a name="requirements-for-the-file-size"></a><span data-ttu-id="6f50a-146">Requirements for the file size</span><span class="sxs-lookup"><span data-stu-id="6f50a-146">Requirements for the file size</span></span>
<span data-ttu-id="6f50a-147">The size of the .txt file that contains the pronunciation entries is limited to 1 megabyte (MB).</span><span class="sxs-lookup"><span data-stu-id="6f50a-147">The size of the .txt file that contains the pronunciation entries is limited to 1 megabyte (MB).</span></span> <span data-ttu-id="6f50a-148">Usually, you do not need to upload large amounts of data through this file.</span><span class="sxs-lookup"><span data-stu-id="6f50a-148">Usually, you do not need to upload large amounts of data through this file.</span></span> <span data-ttu-id="6f50a-149">Most custom pronunciation files are likely to be just a few kilobytes (KBs) in size.</span><span class="sxs-lookup"><span data-stu-id="6f50a-149">Most custom pronunciation files are likely to be just a few kilobytes (KBs) in size.</span></span> <span data-ttu-id="6f50a-150">The encoding of the .txt file for all locales should be UTF-8 BOM.</span><span class="sxs-lookup"><span data-stu-id="6f50a-150">The encoding of the .txt file for all locales should be UTF-8 BOM.</span></span> <span data-ttu-id="6f50a-151">For the English locale, ANSI is also acceptable.</span><span class="sxs-lookup"><span data-stu-id="6f50a-151">For the English locale, ANSI is also acceptable.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f50a-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="6f50a-152">Next steps</span></span>
* <span data-ttu-id="6f50a-153">Improve recognition accuracy by creating a [custom acoustic model](how-to-customize-acoustic-models.md).</span><span class="sxs-lookup"><span data-stu-id="6f50a-153">Improve recognition accuracy by creating a [custom acoustic model](how-to-customize-acoustic-models.md).</span></span>
* <span data-ttu-id="6f50a-154">Improve recognition accuracy by creating a [custom language model](how-to-customize-language-model.md).</span><span class="sxs-lookup"><span data-stu-id="6f50a-154">Improve recognition accuracy by creating a [custom language model](how-to-customize-language-model.md).</span></span>
 