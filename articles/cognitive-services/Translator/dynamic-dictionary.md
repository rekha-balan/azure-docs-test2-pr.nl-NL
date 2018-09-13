---
title: Microsoft Translator Text API Dynamic Dictionary | Microsoft Docs
description: How to use the dynamic dictionary feature of the Microsoft Translator Text API.
services: cognitive-services
author: Jann-Skotdal
manager: chriswendt1
ms.service: cognitive-services
ms.component: translator-text
ms.topic: article
ms.date: 12/14/2017
ms.author: v-jansko
ms.openlocfilehash: 8259fe56a6475f1ab4faca28e41675195cd58b6c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857529"
---
# <a name="how-to-use-the-dynamic-dictionary-feature-of-the-microsoft-translator-text-api"></a><span data-ttu-id="52539-103">How to use the dynamic dictionary feature of the Microsoft Translator Text API</span><span class="sxs-lookup"><span data-stu-id="52539-103">How to use the dynamic dictionary feature of the Microsoft Translator Text API</span></span>

<span data-ttu-id="52539-104">If you already know the translation you want to apply to a word or a phrase, you can supply it as markup within the request.</span><span class="sxs-lookup"><span data-stu-id="52539-104">If you already know the translation you want to apply to a word or a phrase, you can supply it as markup within the request.</span></span> <span data-ttu-id="52539-105">The dynamic dictionary is only safe for compound nouns like proper names and product names.</span><span class="sxs-lookup"><span data-stu-id="52539-105">The dynamic dictionary is only safe for compound nouns like proper names and product names.</span></span> 

<span data-ttu-id="52539-106">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="52539-106">**Syntax:**</span></span> 

<span data-ttu-id="52539-107"><mstrans:dictionary translation=”translation of phrase”>phrase</mstrans:dictionary></span><span class="sxs-lookup"><span data-stu-id="52539-107"><mstrans:dictionary translation=”translation of phrase”>phrase</mstrans:dictionary></span></span>

<span data-ttu-id="52539-108">**Example: en-de:**</span><span class="sxs-lookup"><span data-stu-id="52539-108">**Example: en-de:**</span></span>

<span data-ttu-id="52539-109">Source input: The word <mstrans:dictionary translation=\"wordomatic\">word or phrase</mstrans:dictionary> is a dictionary entry.</span><span class="sxs-lookup"><span data-stu-id="52539-109">Source input: The word <mstrans:dictionary translation=\"wordomatic\">word or phrase</mstrans:dictionary> is a dictionary entry.</span></span>

<span data-ttu-id="52539-110">Target output: Das Wort "wordomatic" ist ein Wörterbucheintrag.</span><span class="sxs-lookup"><span data-stu-id="52539-110">Target output: Das Wort "wordomatic" ist ein Wörterbucheintrag.</span></span>

<span data-ttu-id="52539-111">This feature works the same way with and without HTML mode.</span><span class="sxs-lookup"><span data-stu-id="52539-111">This feature works the same way with and without HTML mode.</span></span> 

<span data-ttu-id="52539-112">The feature should be used sparingly.</span><span class="sxs-lookup"><span data-stu-id="52539-112">The feature should be used sparingly.</span></span> <span data-ttu-id="52539-113">The appropriate and far better way of customizing translation is by using Custom Translator.</span><span class="sxs-lookup"><span data-stu-id="52539-113">The appropriate and far better way of customizing translation is by using Custom Translator.</span></span> <span data-ttu-id="52539-114">Custom Translator makes full use of context and statistical probabilities.</span><span class="sxs-lookup"><span data-stu-id="52539-114">Custom Translator makes full use of context and statistical probabilities.</span></span> <span data-ttu-id="52539-115">If you have or can create training data that shows your work or phrase in context, you get much better results.</span><span class="sxs-lookup"><span data-stu-id="52539-115">If you have or can create training data that shows your work or phrase in context, you get much better results.</span></span> <span data-ttu-id="52539-116">You can find more information about Custom Translator at [http://aka.ms/CustomTranslator](http://aka.ms/CustomTranslator).</span><span class="sxs-lookup"><span data-stu-id="52539-116">You can find more information about Custom Translator at [http://aka.ms/CustomTranslator](http://aka.ms/CustomTranslator).</span></span>

