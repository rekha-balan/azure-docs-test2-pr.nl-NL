---
title: Translate speech by using the Speech SDK for C#
titleSuffix: Microsoft Cognitive Services
description: Shows how to translate speech using the Speech SDK for C#.
services: cognitive-services
author: wolfma61
ms.service: cognitive-services
ms.technology: Speech
ms.topic: article
ms.date: 07/16/2018
ms.author: wolfma
ms.openlocfilehash: 078d2902997f7981f42976e7ce8ee5a15dab404d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870989"
---
# <a name="translate-speech-with-the-cognitive-services-speech-sdk-for-c"></a>Translate speech with the Cognitive Services Speech SDK for C#

[!INCLUDE [Selector](../../../includes/cognitive-services-speech-service-how-to-translate-speech-selector.md)]

[!INCLUDE [Introduction](../../../includes/cognitive-services-speech-service-how-to-translate-speech-intro.md)]

[!INCLUDE [Introduction to top-level declarations](../../../includes/cognitive-services-speech-service-how-to-toplevel-declarations.md)]

[!code-csharp[Top-level declarations](~/samples-cognitive-services-speech-sdk/samples/csharp/sharedcontent/console/translation_samples.cs#toplevel)]

[!INCLUDE [Introduction to using a microphone](../../../includes/cognitive-services-speech-service-how-to-translate-speech-microphone.md)]

[!code-csharp[Translation from a microphone](~/samples-cognitive-services-speech-sdk/samples/csharp/sharedcontent/console/translation_samples.cs#TranslationWithMicrophoneAsync)]

[!INCLUDE [Introduction to using a file](../../../includes/cognitive-services-speech-service-how-to-translate-speech-file.md)]

[!code-csharp[Translation from file input](~/samples-cognitive-services-speech-sdk/samples/csharp/sharedcontent/console/translation_samples.cs#TranslationWithFileAsync)]

[!INCLUDE [Download the sample](../../../includes/cognitive-services-speech-service-speech-sdk-sample-download-h2.md)]
Look for the code that's used in this article in the samples/csharp/sharedcontent/console folder.

## <a name="next-steps"></a>Next steps

- [How to recognize speech](how-to-recognize-speech-csharp.md)
- [How to recognize intents from speech](how-to-recognize-intents-from-speech-csharp.md)
