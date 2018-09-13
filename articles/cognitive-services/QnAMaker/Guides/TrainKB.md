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
# <a name="test-and-train"></a><span data-ttu-id="7e358-103">Test and train</span><span class="sxs-lookup"><span data-stu-id="7e358-103">Test and train</span></span>
<span data-ttu-id="7e358-104">The relevance of the responses is the most important part of your QnA service.</span><span class="sxs-lookup"><span data-stu-id="7e358-104">The relevance of the responses is the most important part of your QnA service.</span></span> <span data-ttu-id="7e358-105">The train feature lets you evaluate the correctness of the responses and correct them and re-train the knowledge base.</span><span class="sxs-lookup"><span data-stu-id="7e358-105">The train feature lets you evaluate the correctness of the responses and correct them and re-train the knowledge base.</span></span>

<span data-ttu-id="7e358-106">There are two ways you can improve the relevance of the responses.</span><span class="sxs-lookup"><span data-stu-id="7e358-106">There are two ways you can improve the relevance of the responses.</span></span>

## <a name="chat-with-your-kb"></a><span data-ttu-id="7e358-107">Chat with your KB</span><span class="sxs-lookup"><span data-stu-id="7e358-107">Chat with your KB</span></span>
<span data-ttu-id="7e358-108">Chat with your knowledge base, to see the relevance of the responses.</span><span class="sxs-lookup"><span data-stu-id="7e358-108">Chat with your knowledge base, to see the relevance of the responses.</span></span> <span data-ttu-id="7e358-109">You can add a variation to an existing question as well as choose a different answer for a question</span><span class="sxs-lookup"><span data-stu-id="7e358-109">You can add a variation to an existing question as well as choose a different answer for a question</span></span>

![alt text](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/QnAMaker/Images/kbTest.png)

<span data-ttu-id="7e358-111">To bulk upload questions (so you don't need to type every time), click on Upload chat logs.</span><span class="sxs-lookup"><span data-stu-id="7e358-111">To bulk upload questions (so you don't need to type every time), click on Upload chat logs.</span></span> <span data-ttu-id="7e358-112">It expects one question per line.</span><span class="sxs-lookup"><span data-stu-id="7e358-112">It expects one question per line.</span></span>

<span data-ttu-id="7e358-113">Once uploaded, you can play the questions in order by clicking Show next question.</span><span class="sxs-lookup"><span data-stu-id="7e358-113">Once uploaded, you can play the questions in order by clicking Show next question.</span></span>

>[!WARNING]
><span data-ttu-id="7e358-114">Only one file can be uploaded at a time.</span><span class="sxs-lookup"><span data-stu-id="7e358-114">Only one file can be uploaded at a time.</span></span> <span data-ttu-id="7e358-115">Uploading multiple file will overwrite the previous one.</span><span class="sxs-lookup"><span data-stu-id="7e358-115">Uploading multiple file will overwrite the previous one.</span></span>

![alt text](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/QnAMaker/Images/uploadChatLogs.png)

<span data-ttu-id="7e358-117">Make sure you press Save and retrain, to reflect any changes/inputs you have provided.</span><span class="sxs-lookup"><span data-stu-id="7e358-117">Make sure you press Save and retrain, to reflect any changes/inputs you have provided.</span></span>

![alt text](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/QnAMaker/Images/kbSaveRetrain.png)

## <a name="replay-live-chat-logs"></a><span data-ttu-id="7e358-119">Replay live chat logs</span><span class="sxs-lookup"><span data-stu-id="7e358-119">Replay live chat logs</span></span>
<span data-ttu-id="7e358-120">A very useful feature is to see what responses the service returns for live traffic, and then train it appropriately.</span><span class="sxs-lookup"><span data-stu-id="7e358-120">A very useful feature is to see what responses the service returns for live traffic, and then train it appropriately.</span></span>

<span data-ttu-id="7e358-121">You can download the live chat traffic hitting your published end-point by clicking on Download chat logs.</span><span class="sxs-lookup"><span data-stu-id="7e358-121">You can download the live chat traffic hitting your published end-point by clicking on Download chat logs.</span></span> <span data-ttu-id="7e358-122">This downloads all the questions hitting your end-point in descending order of frequency.</span><span class="sxs-lookup"><span data-stu-id="7e358-122">This downloads all the questions hitting your end-point in descending order of frequency.</span></span>

<span data-ttu-id="7e358-123">Looking at the chat logs, you can decide which questions you want to test and train your knowledge base on, as described in the above section.</span><span class="sxs-lookup"><span data-stu-id="7e358-123">Looking at the chat logs, you can decide which questions you want to test and train your knowledge base on, as described in the above section.</span></span>

![alt text](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/QnAMaker/Images/downloadChatLogs.png)




