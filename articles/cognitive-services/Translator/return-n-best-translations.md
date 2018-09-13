---
title: Return N-Best Translations with the Microsoft Translator Text API | Microsoft Docs
description: Return N-Best translations using the Microsoft Translator Text API.
services: cognitive-services
author: Jann-Skotdal
manager: chriswendt1
ms.service: cognitive-services
ms.component: translator-text
ms.topic: article
ms.date: 12/14/2017
ms.author: v-jansko
ms.openlocfilehash: 9377f4bc812bc1496875450ffd9d3574c85f1802
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855569"
---
# <a name="how-to-return-n-best-translations"></a><span data-ttu-id="59f9d-103">How to return N-Best translations</span><span class="sxs-lookup"><span data-stu-id="59f9d-103">How to return N-Best translations</span></span>

> [!NOTE]
> <span data-ttu-id="59f9d-104">This method is deprecated.</span><span class="sxs-lookup"><span data-stu-id="59f9d-104">This method is deprecated.</span></span> <span data-ttu-id="59f9d-105">It is not available in V3.0 of the Translator Text API.</span><span class="sxs-lookup"><span data-stu-id="59f9d-105">It is not available in V3.0 of the Translator Text API.</span></span>

<span data-ttu-id="59f9d-106">The GetTranslations() and GetTranslationsArray() methods of the Microsoft Translator API include an optional Boolean flag "IncludeMultipleMTAlternatives".</span><span class="sxs-lookup"><span data-stu-id="59f9d-106">The GetTranslations() and GetTranslationsArray() methods of the Microsoft Translator API include an optional Boolean flag "IncludeMultipleMTAlternatives".</span></span>
<span data-ttu-id="59f9d-107">The method will return up to maxTranslations alternatives where the delta is supplied from the N-Best list of the translator engine.</span><span class="sxs-lookup"><span data-stu-id="59f9d-107">The method will return up to maxTranslations alternatives where the delta is supplied from the N-Best list of the translator engine.</span></span>

<span data-ttu-id="59f9d-108">The signature is:</span><span class="sxs-lookup"><span data-stu-id="59f9d-108">The signature is:</span></span>

<span data-ttu-id="59f9d-109">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="59f9d-109">**Syntax**</span></span>

| <span data-ttu-id="59f9d-110">C#</span><span class="sxs-lookup"><span data-stu-id="59f9d-110">C#</span></span> |
|:---|
| <span data-ttu-id="59f9d-111">GetTranslationsResponse Microsoft.Translator.GetTranslations(appId, text, from, to, maxTranslations, options);</span><span class="sxs-lookup"><span data-stu-id="59f9d-111">GetTranslationsResponse Microsoft.Translator.GetTranslations(appId, text, from, to, maxTranslations, options);</span></span> |

<span data-ttu-id="59f9d-112">**Parameters**</span><span class="sxs-lookup"><span data-stu-id="59f9d-112">**Parameters**</span></span>

| <span data-ttu-id="59f9d-113">Parameter</span><span class="sxs-lookup"><span data-stu-id="59f9d-113">Parameter</span></span> | <span data-ttu-id="59f9d-114">Description</span><span class="sxs-lookup"><span data-stu-id="59f9d-114">Description</span></span> |
|:---|:---|
| <span data-ttu-id="59f9d-115">appId</span><span class="sxs-lookup"><span data-stu-id="59f9d-115">appId</span></span> | <span data-ttu-id="59f9d-116">**Required** If the Authorization header is used, leave the appid field empty else specify a string containing "Bearer" + " " + access token.</span><span class="sxs-lookup"><span data-stu-id="59f9d-116">**Required** If the Authorization header is used, leave the appid field empty else specify a string containing "Bearer" + " " + access token.</span></span>|
| <span data-ttu-id="59f9d-117">text</span><span class="sxs-lookup"><span data-stu-id="59f9d-117">text</span></span> | <span data-ttu-id="59f9d-118">**Required** A string representing the text to translate.</span><span class="sxs-lookup"><span data-stu-id="59f9d-118">**Required** A string representing the text to translate.</span></span> <span data-ttu-id="59f9d-119">The size of the text must not exceed 10000 characters.</span><span class="sxs-lookup"><span data-stu-id="59f9d-119">The size of the text must not exceed 10000 characters.</span></span>|
| <span data-ttu-id="59f9d-120">from</span><span class="sxs-lookup"><span data-stu-id="59f9d-120">from</span></span> | <span data-ttu-id="59f9d-121">**Required** A string representing the language code of the text to translate.</span><span class="sxs-lookup"><span data-stu-id="59f9d-121">**Required** A string representing the language code of the text to translate.</span></span> |
| <span data-ttu-id="59f9d-122">to</span><span class="sxs-lookup"><span data-stu-id="59f9d-122">to</span></span> | <span data-ttu-id="59f9d-123">**Required** A string representing the language code to translate the text into.</span><span class="sxs-lookup"><span data-stu-id="59f9d-123">**Required** A string representing the language code to translate the text into.</span></span> |
| <span data-ttu-id="59f9d-124">maxTranslations</span><span class="sxs-lookup"><span data-stu-id="59f9d-124">maxTranslations</span></span> | <span data-ttu-id="59f9d-125">**Required** An int representing the maximum number of translations to return.</span><span class="sxs-lookup"><span data-stu-id="59f9d-125">**Required** An int representing the maximum number of translations to return.</span></span> |
| <span data-ttu-id="59f9d-126">options</span><span class="sxs-lookup"><span data-stu-id="59f9d-126">options</span></span> | <span data-ttu-id="59f9d-127">**Optional** A TranslateOptions object that contains the values listed below.</span><span class="sxs-lookup"><span data-stu-id="59f9d-127">**Optional** A TranslateOptions object that contains the values listed below.</span></span> <span data-ttu-id="59f9d-128">They are all optional and default to the most common settings.</span><span class="sxs-lookup"><span data-stu-id="59f9d-128">They are all optional and default to the most common settings.</span></span>

* <span data-ttu-id="59f9d-129">Category: The only supported, and the default, option is "general".</span><span class="sxs-lookup"><span data-stu-id="59f9d-129">Category: The only supported, and the default, option is "general".</span></span>
* <span data-ttu-id="59f9d-130">ContentType: The only supported, and the default, option is "text/plain".</span><span class="sxs-lookup"><span data-stu-id="59f9d-130">ContentType: The only supported, and the default, option is "text/plain".</span></span>
* <span data-ttu-id="59f9d-131">State: User state to help correlate request and response.</span><span class="sxs-lookup"><span data-stu-id="59f9d-131">State: User state to help correlate request and response.</span></span> <span data-ttu-id="59f9d-132">The same contents will be returned in the response.</span><span class="sxs-lookup"><span data-stu-id="59f9d-132">The same contents will be returned in the response.</span></span>
* <span data-ttu-id="59f9d-133">IncludeMultipleMTAlternatives: flag to determine whether to return more than one alternatives from the MT engine.</span><span class="sxs-lookup"><span data-stu-id="59f9d-133">IncludeMultipleMTAlternatives: flag to determine whether to return more than one alternatives from the MT engine.</span></span> <span data-ttu-id="59f9d-134">Default is false and includes only 1 alternative.</span><span class="sxs-lookup"><span data-stu-id="59f9d-134">Default is false and includes only 1 alternative.</span></span>

## <a name="ratings"></a><span data-ttu-id="59f9d-135">Ratings</span><span class="sxs-lookup"><span data-stu-id="59f9d-135">Ratings</span></span>
<span data-ttu-id="59f9d-136">The ratings are applied as follows: The best automatic translation has a rating of 5.</span><span class="sxs-lookup"><span data-stu-id="59f9d-136">The ratings are applied as follows: The best automatic translation has a rating of 5.</span></span>
<span data-ttu-id="59f9d-137">The automatically generated (N-Best) translation alternatives have a rating of 0, and have a match degree of 100.</span><span class="sxs-lookup"><span data-stu-id="59f9d-137">The automatically generated (N-Best) translation alternatives have a rating of 0, and have a match degree of 100.</span></span>

## <a name="number-of-alternatives"></a><span data-ttu-id="59f9d-138">Number of alternatives</span><span class="sxs-lookup"><span data-stu-id="59f9d-138">Number of alternatives</span></span>
<span data-ttu-id="59f9d-139">The number of returned alternatives is up to maxTranslations, but may be less.</span><span class="sxs-lookup"><span data-stu-id="59f9d-139">The number of returned alternatives is up to maxTranslations, but may be less.</span></span>

## <a name="language-pairs"></a><span data-ttu-id="59f9d-140">Language pairs</span><span class="sxs-lookup"><span data-stu-id="59f9d-140">Language pairs</span></span>
<span data-ttu-id="59f9d-141">This functionality is not available for translations between Simplified and Traditional Chinese, both directions.</span><span class="sxs-lookup"><span data-stu-id="59f9d-141">This functionality is not available for translations between Simplified and Traditional Chinese, both directions.</span></span> <span data-ttu-id="59f9d-142">It is available for all other Microsoft Translator supported language pairs.</span><span class="sxs-lookup"><span data-stu-id="59f9d-142">It is available for all other Microsoft Translator supported language pairs.</span></span>
