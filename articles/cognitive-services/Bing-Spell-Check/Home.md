---
title: Bing Spell Check APIs overview | Microsoft Docs
description: The Bing Spell Check APIs use machine learning and statistical machine translation for contextual spell checking and inline suggestions.
services: cognitive-services
author: swhite-msft
manager: ehansen
ms.service: cognitive-services
ms.technology: bing-spell-check
ms.topic: article
ms.date: 06/21/2016
ms.author: scottwhi
ms.openlocfilehash: a51b1eaa220f8a517eb90f2b7cbb6e1bf5e71087
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549449"
---
# <a name="bing-spell-check-api-formerly-spell-check-api"></a>Bing Spell Check API (formerly Spell Check API)

Welcome to Bing Spell Check API which performs contextual spell checking for any text and provides inline suggestions for misspelled words.

## <a name="what-is-special-about-our-3rd-generation-spell-checker"></a>What is special about our 3rd generation spell-checker?

What’s the difference between regular spell-checkers and Bing’s 3rd generation spell-checker? Current spell-checkers rely on verifying spelling and grammar against dictionary-based rule sets which get updated and expanded periodically. In other words, the spell-checker is only as strong as the dictionary that supports it, and the editorial staff who supports the dictionary. You know this type of spell-checker from Microsoft Word and other word processors.

In contrast, the Bing team has developed a web-based spell-checker that leverages machine learning and statistical machine translation to dynamically train a constantly-evolving and highly-contextual algorithm to provide spell checking on-demand for almost any word or phrase that exists on the web.

The OneSpeller team, in partnership with Office Online, has adapted this technology to any number of word processing scenarios, texting, web form entries and search. Our spell-checker is based on a massive corpus of web searches and documents.

This spell-checker can handle any word processing scenario:
*   Recognizes slang and informal language
*   Recognizes common name errors in context
*   Corrects word breaking issues with a single flag
*   Is able to correct homophones* in context, and other difficult to spot errors
*   Supports new brands, digital entertainment and popular expressions as they emerge
*   Words that sound the same but differ in meaning and spelling, for example “see” and “sea”.

To help you get started with this supporting technology for all your word processing needs on PC or mobile apps, a new example application will soon be added. Check back soon. In the meantime, you can read our [Getting Started](https://msdn.microsoft.com/en-US/library/mt712546.aspx) guide, which describes how you can obtain your own subscription keys and start making calls to the API. If you already have a subscription, try our API Testing Console [API Testing Console](https://dev.cognitive.microsoft.com/docs/services/56e73033cf5ff80c2008c679/operations/56e73036cf5ff81048ee6727/console) where you can easily craft API requests in a sandbox environment.

## <a name="language-support"></a>Language support

Bing Spell Check API currently supports only U.S. English (en-US). Other English locales such as British English (en-GB), Canadian English (en-CA), Australian English (en-AU), New Zealand English (en-NZ), and Indian English (en-IN) plus Chinese and Spanish will be added in the near future. This page will be updated as new languages are added.
