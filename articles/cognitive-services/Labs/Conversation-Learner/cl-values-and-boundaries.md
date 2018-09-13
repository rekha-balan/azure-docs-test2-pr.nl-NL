---
title: Conversation Learner default configuration - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: Learn about the default Conversation Learner configuration.
services: cognitive-services
author: v-jaswel
manager: nolachar
ms.service: cognitive-services
ms.component: conversation-learner
ms.topic: article
ms.date: 04/30/2018
ms.author: v-jaswel
ms.openlocfilehash: c0ad9f71665e503fe794c68200b90a8474750823
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865058"
---
# <a name="default-values-and-boundaries"></a>Default values and boundaries

This document describes the default configuration of Conversation Learner, and key service boundaries.

## <a name="default-configuration"></a>Default configuration

Parameter | Default value
--- | --- 
Default session timeout | 30 minutes

## <a name="boundaries"></a>Boundaries

Parameter | Limit
--- | --- 
Authoring API, max HTTP calls per month | 5M
Authoring API, max HTTP calls per second | 25
Session API, max HTTP calls per month | 500K
Session API, max HTTP calls per second | 10
Max number of custom (non-programmatic) entities per model | See [LUIS boundaries doc](https://docs.microsoft.com/en-us/azure/cognitive-services/luis/luis-boundaries); in practice, actual number may be slightly smaller
Max number of pre-built entities per model | See [LUIS boundaries doc](https://docs.microsoft.com/en-us/azure/cognitive-services/luis/luis-boundaries)
Max number of entities (in total) per model | 100
Max number of actions per model | 32
Max number of train dialogs per model | 1000
Max number of user turns per train dialog | 100
Max number of log dialogs per model | No pre-set limit, but log dialogs are only retained for a fixed period before being discarded.  Also, the Conversation Learner UI will show 100 log dialogs at a time. 
Max number of models per user | No pre-set limit
Max number of sequential non-wait actions | 5 (*)

(*) After 5 sequential non-wait actions, all non-wait actions are masked, and Conversation Learner will choose amongst available wait actions.

## <a name="next-steps"></a>Next steps

> [!div class="nextstepaction"]
> [Get started with Conversation Learner](./quickstart.md)
