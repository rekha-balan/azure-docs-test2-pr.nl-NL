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
# <a name="glossary"></a><span data-ttu-id="76c53-103">Glossary</span><span class="sxs-lookup"><span data-stu-id="76c53-103">Glossary</span></span>

## <a name="qna-maker-service"></a><span data-ttu-id="76c53-104">QnA Maker Service</span><span class="sxs-lookup"><span data-stu-id="76c53-104">QnA Maker Service</span></span>
<span data-ttu-id="76c53-105">A QnA Maker service is a pre-requisite to start using QnA Maker.</span><span class="sxs-lookup"><span data-stu-id="76c53-105">A QnA Maker service is a pre-requisite to start using QnA Maker.</span></span> <span data-ttu-id="76c53-106">Purchasing a QnA Maker tier sets up resources in your Azure subscription for creating and managing your knowledge base.</span><span class="sxs-lookup"><span data-stu-id="76c53-106">Purchasing a QnA Maker tier sets up resources in your Azure subscription for creating and managing your knowledge base.</span></span> <span data-ttu-id="76c53-107">Each QnA Maker user account can create multiple QnA Maker services in their Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="76c53-107">Each QnA Maker user account can create multiple QnA Maker services in their Azure subscription.</span></span>

## <a name="knowledge-base"></a><span data-ttu-id="76c53-108">Knowledge Base</span><span class="sxs-lookup"><span data-stu-id="76c53-108">Knowledge Base</span></span>
<span data-ttu-id="76c53-109">A Knowledge base is the repository of questions and answers created, maintained, and used through QnA Maker.</span><span class="sxs-lookup"><span data-stu-id="76c53-109">A Knowledge base is the repository of questions and answers created, maintained, and used through QnA Maker.</span></span> <span data-ttu-id="76c53-110">Each QnA Maker tier can be used for multiple Knowledge bases.</span><span class="sxs-lookup"><span data-stu-id="76c53-110">Each QnA Maker tier can be used for multiple Knowledge bases.</span></span>

## <a name="endpoint"></a><span data-ttu-id="76c53-111">Endpoint</span><span class="sxs-lookup"><span data-stu-id="76c53-111">Endpoint</span></span>
<span data-ttu-id="76c53-112">A REST-based HTTP endpoint servicing your knowledge base content that can be integrated into your application, commonly a chat bot.</span><span class="sxs-lookup"><span data-stu-id="76c53-112">A REST-based HTTP endpoint servicing your knowledge base content that can be integrated into your application, commonly a chat bot.</span></span> 

## <a name="test-knowledge-base"></a><span data-ttu-id="76c53-113">Test Knowledge Base</span><span class="sxs-lookup"><span data-stu-id="76c53-113">Test Knowledge Base</span></span>
<span data-ttu-id="76c53-114">A knowledge base has two states - Test and published.</span><span class="sxs-lookup"><span data-stu-id="76c53-114">A knowledge base has two states - Test and published.</span></span> <span data-ttu-id="76c53-115">The test knowledge base is the version that is being edited, saved, and tested for accuracy and completeness of responses.</span><span class="sxs-lookup"><span data-stu-id="76c53-115">The test knowledge base is the version that is being edited, saved, and tested for accuracy and completeness of responses.</span></span> <span data-ttu-id="76c53-116">Changes made to the test knowledge base do not affect the end user of your application/chat bot.</span><span class="sxs-lookup"><span data-stu-id="76c53-116">Changes made to the test knowledge base do not affect the end user of your application/chat bot.</span></span>

## <a name="published-knowledge-base"></a><span data-ttu-id="76c53-117">Published Knowledge Base</span><span class="sxs-lookup"><span data-stu-id="76c53-117">Published Knowledge Base</span></span>
<span data-ttu-id="76c53-118">A knowledge base has two states - Test and Published.</span><span class="sxs-lookup"><span data-stu-id="76c53-118">A knowledge base has two states - Test and Published.</span></span>  <span data-ttu-id="76c53-119">The published knowledge base is the version that is used in your chat bot/application.</span><span class="sxs-lookup"><span data-stu-id="76c53-119">The published knowledge base is the version that is used in your chat bot/application.</span></span> <span data-ttu-id="76c53-120">The action of publishing a knowledge base puts the content of the Test knowledge base in the Published version of the knowledge base.</span><span class="sxs-lookup"><span data-stu-id="76c53-120">The action of publishing a knowledge base puts the content of the Test knowledge base in the Published version of the knowledge base.</span></span> <span data-ttu-id="76c53-121">Since the published knowledge base is the version that the application uses through the endpoint, care should be taken to ensure that the content is correct and well-tested.</span><span class="sxs-lookup"><span data-stu-id="76c53-121">Since the published knowledge base is the version that the application uses through the endpoint, care should be taken to ensure that the content is correct and well-tested.</span></span>

## <a name="query"></a><span data-ttu-id="76c53-122">Query</span><span class="sxs-lookup"><span data-stu-id="76c53-122">Query</span></span>
<span data-ttu-id="76c53-123">A user query is the question that the end-user or tester asks of the knowledge base.</span><span class="sxs-lookup"><span data-stu-id="76c53-123">A user query is the question that the end-user or tester asks of the knowledge base.</span></span> <span data-ttu-id="76c53-124">The query is often in a natural language format or a few keywords that represent the question.</span><span class="sxs-lookup"><span data-stu-id="76c53-124">The query is often in a natural language format or a few keywords that represent the question.</span></span>

## <a name="response"></a><span data-ttu-id="76c53-125">Response</span><span class="sxs-lookup"><span data-stu-id="76c53-125">Response</span></span>
<span data-ttu-id="76c53-126">The response is the answer retrieved from the knowledge base, based on the best match for a given user query.</span><span class="sxs-lookup"><span data-stu-id="76c53-126">The response is the answer retrieved from the knowledge base, based on the best match for a given user query.</span></span>

## <a name="confidence-score"></a><span data-ttu-id="76c53-127">Confidence Score</span><span class="sxs-lookup"><span data-stu-id="76c53-127">Confidence Score</span></span>
<span data-ttu-id="76c53-128">The confidence score of the response is a numeric value between 0 and 100, 100 being an exact query match between user query and a question in knowledge base, that the response served is the correct, appropriate response for a given user query.</span><span class="sxs-lookup"><span data-stu-id="76c53-128">The confidence score of the response is a numeric value between 0 and 100, 100 being an exact query match between user query and a question in knowledge base, that the response served is the correct, appropriate response for a given user query.</span></span> <span data-ttu-id="76c53-129">Answers are typically ranked by the confidence score and the one with the higher confidence score is served as the default response.</span><span class="sxs-lookup"><span data-stu-id="76c53-129">Answers are typically ranked by the confidence score and the one with the higher confidence score is served as the default response.</span></span>
