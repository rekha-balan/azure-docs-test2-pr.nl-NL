---
title: What is Conversation Learner? - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: Learn about Conversation Learner and how it works.
services: cognitive-services
author: v-jaswel
manager: nolachar
ms.service: cognitive-services
ms.component: conversation-learner
ms.topic: article
ms.date: 04/30/2018
ms.author: v-jaswel
ms.openlocfilehash: 9cbf0e60382ef17d68aab47cf5f24ea9b8434f13
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864558"
---
# <a name="what-is-conversation-learner"></a><span data-ttu-id="523df-104">What is Conversation Learner?</span><span class="sxs-lookup"><span data-stu-id="523df-104">What is Conversation Learner?</span></span>

<span data-ttu-id="523df-105">Conversation Learner enables you to build and teach conversational interfaces that learn from example interactions.</span><span class="sxs-lookup"><span data-stu-id="523df-105">Conversation Learner enables you to build and teach conversational interfaces that learn from example interactions.</span></span> 

<span data-ttu-id="523df-106">Unlike traditional approaches, Conversation Learner considers the end-to-end context of a dialogue to improve responses and deliver more compelling user experiences.</span><span class="sxs-lookup"><span data-stu-id="523df-106">Unlike traditional approaches, Conversation Learner considers the end-to-end context of a dialogue to improve responses and deliver more compelling user experiences.</span></span> <span data-ttu-id="523df-107">Spanning a broad set of task-oriented use cases, Conversation Learner applies machine learning behind the scenes to make bots and intelligent agents less likely to frustrate users, incur additional customer service costs, and more intuitive to interact with.</span><span class="sxs-lookup"><span data-stu-id="523df-107">Spanning a broad set of task-oriented use cases, Conversation Learner applies machine learning behind the scenes to make bots and intelligent agents less likely to frustrate users, incur additional customer service costs, and more intuitive to interact with.</span></span>

<span data-ttu-id="523df-108">To get started, the developer enters prototypical dialogs they want to imitate.</span><span class="sxs-lookup"><span data-stu-id="523df-108">To get started, the developer enters prototypical dialogs they want to imitate.</span></span> <span data-ttu-id="523df-109">As more dialogs are entered, the model is continuously updated, and developer can see how well the model is generalizing.</span><span class="sxs-lookup"><span data-stu-id="523df-109">As more dialogs are entered, the model is continuously updated, and developer can see how well the model is generalizing.</span></span> <span data-ttu-id="523df-110">Once the model is working well, the bot can be deployed to end users.</span><span class="sxs-lookup"><span data-stu-id="523df-110">Once the model is working well, the bot can be deployed to end users.</span></span> <span data-ttu-id="523df-111">Conversation Learner logs conversations with users, and the developer can review them.</span><span class="sxs-lookup"><span data-stu-id="523df-111">Conversation Learner logs conversations with users, and the developer can review them.</span></span> <span data-ttu-id="523df-112">If mistakes are spotted, the developer can make an on-the-spot correction, and the model is retrained and available for use immediately.</span><span class="sxs-lookup"><span data-stu-id="523df-112">If mistakes are spotted, the developer can make an on-the-spot correction, and the model is retrained and available for use immediately.</span></span>

<span data-ttu-id="523df-113">This approach reduces manual coding of dialogue control logic and enables business owners or domain experts to contribute to a conversational interface without prior machine learning knowledge.</span><span class="sxs-lookup"><span data-stu-id="523df-113">This approach reduces manual coding of dialogue control logic and enables business owners or domain experts to contribute to a conversational interface without prior machine learning knowledge.</span></span> <span data-ttu-id="523df-114">Whether it’s deployed as part of a bot, smart device, or intelligent agent, Conversation Learner can rapidly iterate new skills, behaviors, or competencies and quickly improve their quality.</span><span class="sxs-lookup"><span data-stu-id="523df-114">Whether it’s deployed as part of a bot, smart device, or intelligent agent, Conversation Learner can rapidly iterate new skills, behaviors, or competencies and quickly improve their quality.</span></span> 

<span data-ttu-id="523df-115">Conversation Learner empowers developers to increase speed-to-market and drive successful dialogues across multiple conversational channels through the Microsoft Bot Framework, or standalone using their own infrastructure.</span><span class="sxs-lookup"><span data-stu-id="523df-115">Conversation Learner empowers developers to increase speed-to-market and drive successful dialogues across multiple conversational channels through the Microsoft Bot Framework, or standalone using their own infrastructure.</span></span>

<span data-ttu-id="523df-116">Summary and highlights:</span><span class="sxs-lookup"><span data-stu-id="523df-116">Summary and highlights:</span></span>

- <span data-ttu-id="523df-117">Conversation Learner is an AI-first way of building task-oriented bots.</span><span class="sxs-lookup"><span data-stu-id="523df-117">Conversation Learner is an AI-first way of building task-oriented bots.</span></span>

- <span data-ttu-id="523df-118">It relies on an end-to-end recurrent neural network (LSTM), and learns directly from multi-turn examples of conversations.</span><span class="sxs-lookup"><span data-stu-id="523df-118">It relies on an end-to-end recurrent neural network (LSTM), and learns directly from multi-turn examples of conversations.</span></span> 

- <span data-ttu-id="523df-119">Enables designers, developers, business users, and call center workers to build and maintain bots.</span><span class="sxs-lookup"><span data-stu-id="523df-119">Enables designers, developers, business users, and call center workers to build and maintain bots.</span></span> 

- <span data-ttu-id="523df-120">Provides the ability to express business rules and common sense in code.</span><span class="sxs-lookup"><span data-stu-id="523df-120">Provides the ability to express business rules and common sense in code.</span></span>

- <span data-ttu-id="523df-121">During teaching sessions, the neural network model is used to score the next set of expected actions in the conversation.</span><span class="sxs-lookup"><span data-stu-id="523df-121">During teaching sessions, the neural network model is used to score the next set of expected actions in the conversation.</span></span> <span data-ttu-id="523df-122">The bot developer can then select the correct action, and train the network to provide the proper response.</span><span class="sxs-lookup"><span data-stu-id="523df-122">The bot developer can then select the correct action, and train the network to provide the proper response.</span></span>
 
- <span data-ttu-id="523df-123">After training is complete, the developer can use the log dialogs from the user interactions to make corrections to bot responses and retrain the model.</span><span class="sxs-lookup"><span data-stu-id="523df-123">After training is complete, the developer can use the log dialogs from the user interactions to make corrections to bot responses and retrain the model.</span></span> 

- <span data-ttu-id="523df-124">Can call domain-specific and third-party APIs to complete tasks.</span><span class="sxs-lookup"><span data-stu-id="523df-124">Can call domain-specific and third-party APIs to complete tasks.</span></span>

