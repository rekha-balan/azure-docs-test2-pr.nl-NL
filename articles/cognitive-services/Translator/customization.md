---
title: Microsoft Translator Text API Translation Customization | Microsoft Docs
description: Use the Microsoft Translator Hub to build your own machine translation system using your preferred terminology and style.
services: cognitive-services
author: Jann-Skotdal
manager: chriswendt1
ms.service: cognitive-services
ms.component: translator-text
ms.topic: article
ms.date: 05/10/2018
ms.author: v-jansko
ms.openlocfilehash: e049423ce64556f60ca74e9bd9c5130fd61c84eb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857029"
---
# <a name="customize-your-text-translations"></a><span data-ttu-id="473fb-103">Customize your text translations</span><span class="sxs-lookup"><span data-stu-id="473fb-103">Customize your text translations</span></span>

<span data-ttu-id="473fb-104">The Microsoft Custom Translator preview is feature of the Microsoft Translator service, which allows users to customize Microsoft Translator’s advanced neural machine translation when translating text using the Microsoft Translator Text API (version 3 only).</span><span class="sxs-lookup"><span data-stu-id="473fb-104">The Microsoft Custom Translator preview is feature of the Microsoft Translator service, which allows users to customize Microsoft Translator’s advanced neural machine translation when translating text using the Microsoft Translator Text API (version 3 only).</span></span> 

<span data-ttu-id="473fb-105">The feature can also be used to customize speech translation when used with [Cognitive Services Speech preview](https://docs.microsoft.com/en-us/azure/cognitive-services/speech-service/).</span><span class="sxs-lookup"><span data-stu-id="473fb-105">The feature can also be used to customize speech translation when used with [Cognitive Services Speech preview](https://docs.microsoft.com/en-us/azure/cognitive-services/speech-service/).</span></span>

## <a name="custom-translator"></a><span data-ttu-id="473fb-106">Custom Translator</span><span class="sxs-lookup"><span data-stu-id="473fb-106">Custom Translator</span></span>
<span data-ttu-id="473fb-107">With Custom Translator, you can build neural translation systems that understand the terminology used in your own business and industry.</span><span class="sxs-lookup"><span data-stu-id="473fb-107">With Custom Translator, you can build neural translation systems that understand the terminology used in your own business and industry.</span></span> <span data-ttu-id="473fb-108">The customized translation system will then integrate into existing applications, workflows, and websites.</span><span class="sxs-lookup"><span data-stu-id="473fb-108">The customized translation system will then integrate into existing applications, workflows, and websites.</span></span> 

### <a name="how-does-it-work"></a><span data-ttu-id="473fb-109">How does it work?</span><span class="sxs-lookup"><span data-stu-id="473fb-109">How does it work?</span></span>
<span data-ttu-id="473fb-110">Use your previously translated documents (leaflets, webpages, documentation, etc.) to build a translation system that reflects your domain-specific terminology and style, better than a generic translation system.</span><span class="sxs-lookup"><span data-stu-id="473fb-110">Use your previously translated documents (leaflets, webpages, documentation, etc.) to build a translation system that reflects your domain-specific terminology and style, better than a generic translation system.</span></span> <span data-ttu-id="473fb-111">Users can upload TMX, XLIFF, TXT, DOCX, and XLSX documents.</span><span class="sxs-lookup"><span data-stu-id="473fb-111">Users can upload TMX, XLIFF, TXT, DOCX, and XLSX documents.</span></span>  

<span data-ttu-id="473fb-112">The system also accepts data that is parallel at the document level but is not yet aligned at the sentence level.</span><span class="sxs-lookup"><span data-stu-id="473fb-112">The system also accepts data that is parallel at the document level but is not yet aligned at the sentence level.</span></span> <span data-ttu-id="473fb-113">If users have access to versions of the same content in multiple languages but in separate documents Custom Translator will be able to automatically match sentences across documents.</span><span class="sxs-lookup"><span data-stu-id="473fb-113">If users have access to versions of the same content in multiple languages but in separate documents Custom Translator will be able to automatically match sentences across documents.</span></span>  <span data-ttu-id="473fb-114">The system can also use monolingual data in either or both languages to complement the parallel training data to improve the translations.</span><span class="sxs-lookup"><span data-stu-id="473fb-114">The system can also use monolingual data in either or both languages to complement the parallel training data to improve the translations.</span></span> 

<span data-ttu-id="473fb-115">The customized system is then available through a regular call to the Microsoft Translator Text API using the category parameter.</span><span class="sxs-lookup"><span data-stu-id="473fb-115">The customized system is then available through a regular call to the Microsoft Translator Text API using the category parameter.</span></span>

<span data-ttu-id="473fb-116">Given the appropriate type and amount of training data it is not uncommon to expect gains between 5 and 10, or even more BLEU points on translation quality by using Custom Translator.</span><span class="sxs-lookup"><span data-stu-id="473fb-116">Given the appropriate type and amount of training data it is not uncommon to expect gains between 5 and 10, or even more BLEU points on translation quality by using Custom Translator.</span></span>

<span data-ttu-id="473fb-117">More details about the various levels of customization based on available data can be found in the [Custom Translator User Guide](http://aka.ms/CustomTranslatorDocs).</span><span class="sxs-lookup"><span data-stu-id="473fb-117">More details about the various levels of customization based on available data can be found in the [Custom Translator User Guide](http://aka.ms/CustomTranslatorDocs).</span></span>


## <a name="microsoft-translator-hub"></a><span data-ttu-id="473fb-118">Microsoft Translator Hub</span><span class="sxs-lookup"><span data-stu-id="473fb-118">Microsoft Translator Hub</span></span>

<span data-ttu-id="473fb-119">The legacy Microsoft Translator Hub can be used to translate statistical machine translation.</span><span class="sxs-lookup"><span data-stu-id="473fb-119">The legacy Microsoft Translator Hub can be used to translate statistical machine translation.</span></span> [<span data-ttu-id="473fb-120">Learn more</span><span class="sxs-lookup"><span data-stu-id="473fb-120">Learn more</span></span>](https://www.microsoft.com/en-us/translator/hub.aspx) 

## <a name="custom-translator-versus-hub"></a><span data-ttu-id="473fb-121">Custom Translator versus Hub</span><span class="sxs-lookup"><span data-stu-id="473fb-121">Custom Translator versus Hub</span></span>

|   | <span data-ttu-id="473fb-122">**Hub**</span><span class="sxs-lookup"><span data-stu-id="473fb-122">**Hub**</span></span> | <span data-ttu-id="473fb-123">**Custom Translator**</span><span class="sxs-lookup"><span data-stu-id="473fb-123">**Custom Translator**</span></span>|
|:-----|:----:|:----:|
|<span data-ttu-id="473fb-124">Customization Feature Status</span><span class="sxs-lookup"><span data-stu-id="473fb-124">Customization Feature Status</span></span>   | <span data-ttu-id="473fb-125">General Availability</span><span class="sxs-lookup"><span data-stu-id="473fb-125">General Availability</span></span>  | <span data-ttu-id="473fb-126">Preview</span><span class="sxs-lookup"><span data-stu-id="473fb-126">Preview</span></span> |
| <span data-ttu-id="473fb-127">Text API version</span><span class="sxs-lookup"><span data-stu-id="473fb-127">Text API version</span></span>  | <span data-ttu-id="473fb-128">V2 only</span><span class="sxs-lookup"><span data-stu-id="473fb-128">V2 only</span></span>   | <span data-ttu-id="473fb-129">V3 only</span><span class="sxs-lookup"><span data-stu-id="473fb-129">V3 only</span></span> |
| <span data-ttu-id="473fb-130">SMT customization</span><span class="sxs-lookup"><span data-stu-id="473fb-130">SMT customization</span></span> | <span data-ttu-id="473fb-131">Yes</span><span class="sxs-lookup"><span data-stu-id="473fb-131">Yes</span></span>   | <span data-ttu-id="473fb-132">No</span><span class="sxs-lookup"><span data-stu-id="473fb-132">No</span></span> | 
| <span data-ttu-id="473fb-133">NMT customization</span><span class="sxs-lookup"><span data-stu-id="473fb-133">NMT customization</span></span> | <span data-ttu-id="473fb-134">No</span><span class="sxs-lookup"><span data-stu-id="473fb-134">No</span></span>    | <span data-ttu-id="473fb-135">Yes</span><span class="sxs-lookup"><span data-stu-id="473fb-135">Yes</span></span> |
| <span data-ttu-id="473fb-136">New unified Speech services customization</span><span class="sxs-lookup"><span data-stu-id="473fb-136">New unified Speech services customization</span></span> | <span data-ttu-id="473fb-137">No</span><span class="sxs-lookup"><span data-stu-id="473fb-137">No</span></span>    | <span data-ttu-id="473fb-138">Yes</span><span class="sxs-lookup"><span data-stu-id="473fb-138">Yes</span></span> | 
| [<span data-ttu-id="473fb-139">No Trace</span><span class="sxs-lookup"><span data-stu-id="473fb-139">No Trace</span></span>](http://www.aka.ms/notrace) | <span data-ttu-id="473fb-140">Yes</span><span class="sxs-lookup"><span data-stu-id="473fb-140">Yes</span></span>   | <span data-ttu-id="473fb-141">Yes</span><span class="sxs-lookup"><span data-stu-id="473fb-141">Yes</span></span> | 

## <a name="collaborative-translations-framework"></a><span data-ttu-id="473fb-142">Collaborative Translations Framework</span><span class="sxs-lookup"><span data-stu-id="473fb-142">Collaborative Translations Framework</span></span>

> [!NOTE]
> <span data-ttu-id="473fb-143">As of February 1, 2018, AddTranslation() and AddTranslationArray() are no longer available for use with the Translator Text API V2.0.</span><span class="sxs-lookup"><span data-stu-id="473fb-143">As of February 1, 2018, AddTranslation() and AddTranslationArray() are no longer available for use with the Translator Text API V2.0.</span></span> <span data-ttu-id="473fb-144">These methods will fail and nothing will be written.</span><span class="sxs-lookup"><span data-stu-id="473fb-144">These methods will fail and nothing will be written.</span></span> <span data-ttu-id="473fb-145">The Translator Text API V3.0 does not support these methods.</span><span class="sxs-lookup"><span data-stu-id="473fb-145">The Translator Text API V3.0 does not support these methods.</span></span>

><span data-ttu-id="473fb-146">Similar functionality is available in the Translator Hub API.</span><span class="sxs-lookup"><span data-stu-id="473fb-146">Similar functionality is available in the Translator Hub API.</span></span> <span data-ttu-id="473fb-147">See [https://hub.microsofttranslator.com/swagger](https://hub.microsofttranslator.com/swagger).</span><span class="sxs-lookup"><span data-stu-id="473fb-147">See [https://hub.microsofttranslator.com/swagger](https://hub.microsofttranslator.com/swagger).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="473fb-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="473fb-148">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="473fb-149">Set up a customized language system using Custom Translator</span><span class="sxs-lookup"><span data-stu-id="473fb-149">Set up a customized language system using Custom Translator</span></span>](http://aka.ms/CustomTranslatorDocs)
