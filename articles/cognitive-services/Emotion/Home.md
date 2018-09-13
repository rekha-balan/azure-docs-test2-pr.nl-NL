---
title: Emotion API overview | Microsoft Docs
description: Use the Microsoft cutting-edge, cloud-based emotion recognition algorithm to build more personalized apps, with the Emotion API in Cognitive Services.
services: cognitive-services
author: v-royhar
manager: yutkuo
ms.service: cognitive-services
ms.technology: emotion
ms.topic: article
ms.date: 02/06/2017
ms.author: anroth
ms.openlocfilehash: 2f756ecd61fa7092645dab46c1db14bc3e323080
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549454"
---
# <a name="emotion-api"></a>Emotion API

Welcome to the Microsoft Emotion API, which allows you to build more personalized apps with Microsoft’s cutting edge cloud-based emotion recognition algorithm.

### <a name="emotion-recognition"></a>Emotion Recognition

The Emotion API beta takes an image as an input, and returns the confidence across a set of emotions for each face in the image, as well as bounding box for the face, from the Face API. The emotions detected are happiness, sadness, surprise, anger, fear, contempt, disgust or neutral. These emotions are communicated cross-culturally and universally via the same basic facial expressions, where are identified by Emotion API. 

**Interpreting Results:** 

In interpreting results from the Emotion API, the emotion detected should be interpreted as the emotion with the highest score, as scores are normalized to sum to one. Users may choose to set a higher confidence threshold within their application, depending on their needs. 

For more details about emotion detection, please refer to the API Reference: 
  * Basic: If a user has already called the Face API, they can submit the face rectangle as an input and use the basic tier. [API Reference](https://westus.dev.cognitive.microsoft.com/docs/services/5639d931ca73072154c1ce89/operations/56f23eb019845524ec61c4d7)
  * Standard: If a user does not submit a face rectangle, they should use standard mode.  [API Reference](https://westus.dev.cognitive.microsoft.com/docs/services/5639d931ca73072154c1ce89/operations/563b31ea778daf121cc3a5fa)

### <a name="emotion-in-video"></a>Emotion in Video

The Emotion API for Video takes a video as an input, and returns the confidence across a set of emotions for the group of faces in the image over a period of time. The emotions detected are happiness, sadness, surprise, anger, fear, contempt, disgust or neutral. These emotions are communicated cross-culturally and universally via the same basic facial expressions, where are identified by Emotion API.

**Interpreting Results:**

Emotion API for Video provides two types of aggregate results for the emotions of faces in a frame. The API first calculates emotion scores for each face in a video, smoothing the results over time for higher accuracy. It returns two types of aggregates: *windowMeanScores* gives a mean score for all of the faces detected in a frame for each emotion. The emotion detected should be interpreted as the emotion with the highest score, as scores are normalized to sum to one. Users may choose to set a higher confidence threshold within their application, depending on their needs. *windowFaceDistribution* gives the distribution of faces with each emotion as the dominant emotion for that face. Dominant emotions for each face have been determined based on the emotion with the highest score for that face. 

Because emotions are smoothed over time, if you ever build a visualization to overlay your results on top of the original video, subtract 250 milliseconds from the provided timestamps. 

For more detail on how to parse the format of Emotion for Video API results, you may also want to view  <link to Glossary from Video API> For more details about emotion detection in video, please refer to the [API Reference](https://westus.dev.cognitive.microsoft.com/docs/services/5639d931ca73072154c1ce89).

