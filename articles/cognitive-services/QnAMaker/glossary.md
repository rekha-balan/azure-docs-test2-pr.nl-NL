---
title: Glossary - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: Glossary
services: cognitive-services
author: nstulasi
manager: sangitap
ms.service: cognitive-services
ms.component: QnAMaker
ms.topic: article
ms.date: 04/21/2018
ms.author: saneppal
ms.openlocfilehash: e28cddec005cb6ba99b9f60d8b03a11f1bc97062
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865261"
---
# <a name="glossary"></a>Glossary

## <a name="qna-maker-service"></a>QnA Maker Service
A QnA Maker service is a pre-requisite to start using QnA Maker. Purchasing a QnA Maker tier sets up resources in your Azure subscription for creating and managing your knowledge base. Each QnA Maker user account can create multiple QnA Maker services in their Azure subscription.

## <a name="knowledge-base"></a>Knowledge Base
A Knowledge base is the repository of questions and answers created, maintained, and used through QnA Maker. Each QnA Maker tier can be used for multiple Knowledge bases.

## <a name="endpoint"></a>Endpoint
A REST-based HTTP endpoint servicing your knowledge base content that can be integrated into your application, commonly a chat bot. 

## <a name="test-knowledge-base"></a>Test Knowledge Base
A knowledge base has two states - Test and published. The test knowledge base is the version that is being edited, saved, and tested for accuracy and completeness of responses. Changes made to the test knowledge base do not affect the end user of your application/chat bot.

## <a name="published-knowledge-base"></a>Published Knowledge Base
A knowledge base has two states - Test and Published.  The published knowledge base is the version that is used in your chat bot/application. The action of publishing a knowledge base puts the content of the Test knowledge base in the Published version of the knowledge base. Since the published knowledge base is the version that the application uses through the endpoint, care should be taken to ensure that the content is correct and well-tested.

## <a name="query"></a>Query
A user query is the question that the end-user or tester asks of the knowledge base. The query is often in a natural language format or a few keywords that represent the question.

## <a name="response"></a>Response
The response is the answer retrieved from the knowledge base, based on the best match for a given user query.

## <a name="confidence-score"></a>Confidence Score
The confidence score of the response is a numeric value between 0 and 100, 100 being an exact query match between user query and a question in knowledge base, that the response served is the correct, appropriate response for a given user query. Answers are typically ranked by the confidence score and the one with the higher confidence score is served as the default response.
