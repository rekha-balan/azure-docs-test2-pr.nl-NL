---
title: Test and train with QnA Maker | Microsoft Docs
description: Use QnA Maker to evaluate the correctness of the responses and correct them and re-train the knowledge base.
services: cognitive-services
author: pchoudhari
manager: rsrikan
ms.service: cognitive-services
ms.technology: qnamaker
ms.topic: article
ms.date: 12/08/2016
ms.author: pchoudh
ms.openlocfilehash: ba25decedf833c2a43daf3d1b52418008f13477c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563167"
---
# <a name="test-and-train"></a>Test and train
The relevance of the responses is the most important part of your QnA service. The train feature lets you evaluate the correctness of the responses and correct them and re-train the knowledge base.

There are two ways you can improve the relevance of the responses.

## <a name="chat-with-your-kb"></a>Chat with your KB
Chat with your knowledge base, to see the relevance of the responses. You can add a variation to an existing question as well as choose a different answer for a question

![alt text](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/QnAMaker/Images/kbTest.png)

To bulk upload questions (so you don't need to type every time), click on Upload chat logs. It expects one question per line.

Once uploaded, you can play the questions in order by clicking Show next question.

>[!WARNING]
>Only one file can be uploaded at a time. Uploading multiple file will overwrite the previous one.

![alt text](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/QnAMaker/Images/uploadChatLogs.png)

Make sure you press Save and retrain, to reflect any changes/inputs you have provided.

![alt text](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/QnAMaker/Images/kbSaveRetrain.png)

## <a name="replay-live-chat-logs"></a>Replay live chat logs
A very useful feature is to see what responses the service returns for live traffic, and then train it appropriately.

You can download the live chat traffic hitting your published end-point by clicking on Download chat logs. This downloads all the questions hitting your end-point in descending order of frequency.

Looking at the chat logs, you can decide which questions you want to test and train your knowledge base on, as described in the above section.

![alt text](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/QnAMaker/Images/downloadChatLogs.png)




