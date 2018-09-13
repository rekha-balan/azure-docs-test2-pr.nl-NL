---
title: Azure Video Indexer concepts | Microsoft Docs
description: This topic describes some concepts of the Video Indexer service.
services: cognitive services
documentationcenter: ''
author: juliako
manager: erikre
ms.service: cognitive-services
ms.topic: article
ms.date: 07/31/2018
ms.author: juliako
ms.openlocfilehash: 224c8b05027f51fb99c8d58be34c3604032c0f77
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868074"
---
# <a name="video-indexer-concepts"></a>Video Indexer concepts
 
This topic describes some concepts of the Video Indexer service.
    
## <a name="summarized-insights"></a>Summarized insights

Summarized insights contain an aggregated view of the data: faces, keywords, sentiments. For example, instead of going over each of the thousands of time ranges and checking which faces are in it, the summarized insights contains all the faces and for each one, the time ranges it appears in and the % of the time it is shown.

## <a name="topicskeywords"></a>Topics/keywords

Topics/keywords are in the list of key phrases that Video Indexer extracts from the text. For example, a Scott Guthrie video might contain the following topics/keywords: Security, Azure, Microsoft Cloud, Revenue.

## <a name="sentiments"></a>Sentiments

When Video Indexer analyzes transcripts, it detects sentiments as well. For example, "this is a very exciting event" is a positive sentiment.

## <a name="time-range-vs-adjusted-time-range"></a>time range vs. adjusted time range

TimeRange is the time range in the original video. AdjustedTimeRange is the time range relative to the current playlist. Since you can create a playlist from different lines of different videos, you can take a 1-hour video and use just 1 line from it, for example, 10:00-10:15. In that case, you will have a playlist with 1 line, where the time range is 10:00-10:15 but the adjustedTimeRange is 00:00-00:15.
 
## <a name="blocks"></a>Blocks

Blocks are meant to make it easier to go through the data. For example, block might be broken down based on when speakers change or there is a long pause.

## <a name="next-steps"></a>Next steps

For information about how to get started, see [How to sign up and upload your first video](video-indexer-get-started.md).

## <a name="see-also"></a>See also

[Video Indexer overview](video-indexer-overview.md)
