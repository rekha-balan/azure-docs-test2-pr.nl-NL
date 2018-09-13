---
title: Conversation Learner control flow - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: Learn about the Conversation Learner control flow.
services: cognitive-services
author: v-jaswel
manager: nolachar
ms.service: cognitive-services
ms.component: conversation-learner
ms.topic: article
ms.date: 04/30/2018
ms.author: v-jaswel
ms.openlocfilehash: 592ca82db7e0ab3ff89d25b61f38f8b226f3bc86
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871131"
---
## <a name="control-flow"></a><span data-ttu-id="97993-103">Control flow</span><span class="sxs-lookup"><span data-stu-id="97993-103">Control flow</span></span>

<span data-ttu-id="97993-104">This document describes the control flow of the Conversation Learner (CL) as displayed in the below diagram.</span><span class="sxs-lookup"><span data-stu-id="97993-104">This document describes the control flow of the Conversation Learner (CL) as displayed in the below diagram.</span></span>

![](media/controlflow.PNG)

1. <span data-ttu-id="97993-105">User enters a term or phrase in the bot, for example, 'what's the weather in Seattle?'</span><span class="sxs-lookup"><span data-stu-id="97993-105">User enters a term or phrase in the bot, for example, 'what's the weather in Seattle?'</span></span>
1. <span data-ttu-id="97993-106">CL passes the user input to a machine learning model that extracts entities</span><span class="sxs-lookup"><span data-stu-id="97993-106">CL passes the user input to a machine learning model that extracts entities</span></span>
    - <span data-ttu-id="97993-107">This model is build by Conversation Learner, and hosted by www.luis.ai</span><span class="sxs-lookup"><span data-stu-id="97993-107">This model is build by Conversation Learner, and hosted by www.luis.ai</span></span>
2. <span data-ttu-id="97993-108">Any extracted entities, and the user's input text, are passed to the Entity Detection Callback method in the bot's code.</span><span class="sxs-lookup"><span data-stu-id="97993-108">Any extracted entities, and the user's input text, are passed to the Entity Detection Callback method in the bot's code.</span></span>
    - <span data-ttu-id="97993-109">This code may set/clear/manipulate entity values</span><span class="sxs-lookup"><span data-stu-id="97993-109">This code may set/clear/manipulate entity values</span></span>
1. <span data-ttu-id="97993-110">CL neural network then takes the output of the entity extraction and the user input, and scores all of the actions defined in the bot</span><span class="sxs-lookup"><span data-stu-id="97993-110">CL neural network then takes the output of the entity extraction and the user input, and scores all of the actions defined in the bot</span></span>
    - <span data-ttu-id="97993-111">In this example, the highest probability action is to provide the weather forecast:</span><span class="sxs-lookup"><span data-stu-id="97993-111">In this example, the highest probability action is to provide the weather forecast:</span></span>

![](media/controlflow_forecast.PNG)

5. <span data-ttu-id="97993-112">The selected action, in this case, requires an API call to retrieve the weather forecast.</span><span class="sxs-lookup"><span data-stu-id="97993-112">The selected action, in this case, requires an API call to retrieve the weather forecast.</span></span> 
6. <span data-ttu-id="97993-113">This API, which had been registered using the CL.AddAPICallback method, is then invoked.</span><span class="sxs-lookup"><span data-stu-id="97993-113">This API, which had been registered using the CL.AddAPICallback method, is then invoked.</span></span>  <span data-ttu-id="97993-114">The result of this API is then returned to the user as a message -- for example, 'Sunny with a high of 67.'</span><span class="sxs-lookup"><span data-stu-id="97993-114">The result of this API is then returned to the user as a message -- for example, 'Sunny with a high of 67.'</span></span>
7. <span data-ttu-id="97993-115">The call is then made to the neural network to determine the next action based on the previous step.</span><span class="sxs-lookup"><span data-stu-id="97993-115">The call is then made to the neural network to determine the next action based on the previous step.</span></span>
8. <span data-ttu-id="97993-116">The neural network then predicts the next set of possible actions, and the selected action is presented to the user, in this case, 'Anything else?'</span><span class="sxs-lookup"><span data-stu-id="97993-116">The neural network then predicts the next set of possible actions, and the selected action is presented to the user, in this case, 'Anything else?'</span></span>

## <a name="next-steps"></a><span data-ttu-id="97993-117">Next steps</span><span class="sxs-lookup"><span data-stu-id="97993-117">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="97993-118">How to teach with Conversation Learner </span><span class="sxs-lookup"><span data-stu-id="97993-118">How to teach with Conversation Learner </span></span>](./how-to-teach-cl.md)
