---
title: How to Choose Recognition Mode | Microsoft Docs
description: How to choose the best recognition mode.
services: cognitive-services
author: zhouwangzw
manager: wolfma
ms.service: cognitive-services
ms.component: bing-speech
ms.topic: article
ms.date: 09/15/2017
ms.author: zhouwang
ms.openlocfilehash: 4f02b683dde16b537ae5554e6435c068f0fcb808
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856231"
---
# <a name="speech-recognition-modes"></a>Speech recognition modes

Microsoft's *Speech to Text* APIs support multiple modes of speech recognition. Choose the mode that produces the best recognition results for your application.

| Mode | Description |
|---|---|
| *interactive* | "Command and control" recognition for interactive user application scenarios. Users speak short phrases intended as commands to an application. |
| *dictation* | Continuous recognition for dictation scenarios. Users speak longer sentences that are displayed as text. Users adopt a more formal speaking style. |
| *conversation* | Continuous recognition for transcribing conversations between humans. Users adopt a less formal speaking style and may alternate between longer sentences and shorter phrases.

> [!NOTE]
> These modes are applicable when you use the [REST APIs](../GetStarted/GetStartedREST.md). The [client libraries](../GetStarted/GetStartedClientLibraries.md) use different parameters to specify recognition mode. For more information, see the client library of your choice.

For more information, see the [Recognition Modes](../concepts.md#recognition-modes) page.
