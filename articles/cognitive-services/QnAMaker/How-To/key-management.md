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
# <a name="key-management"></a><span data-ttu-id="4657b-103">Key Management</span><span class="sxs-lookup"><span data-stu-id="4657b-103">Key Management</span></span>

<span data-ttu-id="4657b-104">Your QnA Maker service deals with two kinds of keys, **subscription keys** and **endpoint keys**.</span><span class="sxs-lookup"><span data-stu-id="4657b-104">Your QnA Maker service deals with two kinds of keys, **subscription keys** and **endpoint keys**.</span></span>

![key management](../media/qnamaker-how-to-key-management/key-management.png)

1. <span data-ttu-id="4657b-106">**Subscription Keys**: These keys are used to access the [QnA Maker management service APIs](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75ff).</span><span class="sxs-lookup"><span data-stu-id="4657b-106">**Subscription Keys**: These keys are used to access the [QnA Maker management service APIs](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75ff).</span></span> <span data-ttu-id="4657b-107">These APIs let you perform various CRUD operations on your knowledge base.</span><span class="sxs-lookup"><span data-stu-id="4657b-107">These APIs let you perform various CRUD operations on your knowledge base.</span></span>  

2. <span data-ttu-id="4657b-108">**Endpoint Keys**: These keys are used to access the knowledge base endpoint to get a response for a user question.</span><span class="sxs-lookup"><span data-stu-id="4657b-108">**Endpoint Keys**: These keys are used to access the knowledge base endpoint to get a response for a user question.</span></span> <span data-ttu-id="4657b-109">You would typically use this endpoint in your chat bot/App code that consumes the QnA Maker service.</span><span class="sxs-lookup"><span data-stu-id="4657b-109">You would typically use this endpoint in your chat bot/App code that consumes the QnA Maker service.</span></span>
 
## <a name="subscription-keys"></a><span data-ttu-id="4657b-110">Subscription Keys</span><span class="sxs-lookup"><span data-stu-id="4657b-110">Subscription Keys</span></span>
<span data-ttu-id="4657b-111">You can view and reset your subscription keys from the Azure portal where you created the QnA Maker resource.</span><span class="sxs-lookup"><span data-stu-id="4657b-111">You can view and reset your subscription keys from the Azure portal where you created the QnA Maker resource.</span></span> 
1. <span data-ttu-id="4657b-112">Go to the QnA Maker resource in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4657b-112">Go to the QnA Maker resource in the Azure portal.</span></span>

    ![QnA Maker resource list](../media/qnamaker-how-to-key-management/qnamaker-resource-list.png)

2. <span data-ttu-id="4657b-114">Go to **Keys**.</span><span class="sxs-lookup"><span data-stu-id="4657b-114">Go to **Keys**.</span></span>

    ![subscription key](../media/qnamaker-how-to-key-management/subscription-key.PNG)

## <a name="endpoint-keys"></a><span data-ttu-id="4657b-116">Endpoint Keys</span><span class="sxs-lookup"><span data-stu-id="4657b-116">Endpoint Keys</span></span>

<span data-ttu-id="4657b-117">Endpoint keys can be managed from the [QnA Maker portal](https://qnamaker.ai).</span><span class="sxs-lookup"><span data-stu-id="4657b-117">Endpoint keys can be managed from the [QnA Maker portal](https://qnamaker.ai).</span></span>

1. <span data-ttu-id="4657b-118">Log in to the [QnA Maker portal](https://qnamaker.ai), and go to **Manage keys**.</span><span class="sxs-lookup"><span data-stu-id="4657b-118">Log in to the [QnA Maker portal](https://qnamaker.ai), and go to **Manage keys**.</span></span>

    ![endpoint key](../media/qnamaker-how-to-key-management/Endpoint-keys.png)

2. <span data-ttu-id="4657b-120">View or reset your keys.</span><span class="sxs-lookup"><span data-stu-id="4657b-120">View or reset your keys.</span></span>

    ![endpoint key manager](../media/qnamaker-how-to-key-management/Endpoint-keys1.png)

    >[!NOTE]
    ><span data-ttu-id="4657b-122">Refresh your keys if you feel they have been compromised.</span><span class="sxs-lookup"><span data-stu-id="4657b-122">Refresh your keys if you feel they have been compromised.</span></span> <span data-ttu-id="4657b-123">This may require corresponding changes to your App/Bot code.</span><span class="sxs-lookup"><span data-stu-id="4657b-123">This may require corresponding changes to your App/Bot code.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4657b-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="4657b-124">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4657b-125">Create a knowledge base in a different language</span><span class="sxs-lookup"><span data-stu-id="4657b-125">Create a knowledge base in a different language</span></span>](./language-knowledge-base.md)
