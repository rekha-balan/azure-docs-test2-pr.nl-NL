---
title: Key management - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: How to manage your QnA Maker keys
services: cognitive-services
author: nstulasi
manager: sangitap
ms.service: cognitive-services
ms.component: QnAMaker
ms.topic: article
ms.date: 05/07/2018
ms.author: saneppal
ms.openlocfilehash: b402187f4949dac34fa476648c81b980ba3efc96
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869383"
---
# <a name="key-management"></a>Key Management

Your QnA Maker service deals with two kinds of keys, **subscription keys** and **endpoint keys**.

![key management](../media/qnamaker-how-to-key-management/key-management.png)

1. **Subscription Keys**: These keys are used to access the [QnA Maker management service APIs](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75ff). These APIs let you perform various CRUD operations on your knowledge base.  

2. **Endpoint Keys**: These keys are used to access the knowledge base endpoint to get a response for a user question. You would typically use this endpoint in your chat bot/App code that consumes the QnA Maker service.
 
## <a name="subscription-keys"></a>Subscription Keys
You can view and reset your subscription keys from the Azure portal where you created the QnA Maker resource. 
1. Go to the QnA Maker resource in the Azure portal.

    ![QnA Maker resource list](../media/qnamaker-how-to-key-management/qnamaker-resource-list.png)

2. Go to **Keys**.

    ![subscription key](../media/qnamaker-how-to-key-management/subscription-key.PNG)

## <a name="endpoint-keys"></a>Endpoint Keys

Endpoint keys can be managed from the [QnA Maker portal](https://qnamaker.ai).

1. Log in to the [QnA Maker portal](https://qnamaker.ai), and go to **Manage keys**.

    ![endpoint key](../media/qnamaker-how-to-key-management/Endpoint-keys.png)

2. View or reset your keys.

    ![endpoint key manager](../media/qnamaker-how-to-key-management/Endpoint-keys1.png)

    >[!NOTE]
    >Refresh your keys if you feel they have been compromised. This may require corresponding changes to your App/Bot code.

## <a name="next-steps"></a>Next steps

> [!div class="nextstepaction"]
> [Create a knowledge base in a different language](./language-knowledge-base.md)