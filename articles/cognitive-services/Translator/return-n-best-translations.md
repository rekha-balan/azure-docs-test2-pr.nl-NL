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
# <a name="how-to-return-n-best-translations"></a>How to return N-Best translations

> [!NOTE]
> This method is deprecated. It is not available in V3.0 of the Translator Text API.

The GetTranslations() and GetTranslationsArray() methods of the Microsoft Translator API include an optional Boolean flag "IncludeMultipleMTAlternatives".
The method will return up to maxTranslations alternatives where the delta is supplied from the N-Best list of the translator engine.

The signature is:

**Syntax**

| C# |
|:---|
| GetTranslationsResponse Microsoft.Translator.GetTranslations(appId, text, from, to, maxTranslations, options); |

**Parameters**

| Parameter | Description |
|:---|:---|
| appId | **Required** If the Authorization header is used, leave the appid field empty else specify a string containing "Bearer" + " " + access token.|
| text | **Required** A string representing the text to translate. The size of the text must not exceed 10000 characters.|
| from | **Required** A string representing the language code of the text to translate. |
| to | **Required** A string representing the language code to translate the text into. |
| maxTranslations | **Required** An int representing the maximum number of translations to return. |
| options | **Optional** A TranslateOptions object that contains the values listed below. They are all optional and default to the most common settings.

* Category: The only supported, and the default, option is "general".
* ContentType: The only supported, and the default, option is "text/plain".
* State: User state to help correlate request and response. The same contents will be returned in the response.
* IncludeMultipleMTAlternatives: flag to determine whether to return more than one alternatives from the MT engine. Default is false and includes only 1 alternative.

## <a name="ratings"></a>Ratings
The ratings are applied as follows: The best automatic translation has a rating of 5.
The automatically generated (N-Best) translation alternatives have a rating of 0, and have a match degree of 100.

## <a name="number-of-alternatives"></a>Number of alternatives
The number of returned alternatives is up to maxTranslations, but may be less.

## <a name="language-pairs"></a>Language pairs
This functionality is not available for translations between Simplified and Traditional Chinese, both directions. It is available for all other Microsoft Translator supported language pairs.
