---
title: Collaborating on your knowledge base - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: How to collaborate on your QnA Maker knowledge base
services: cognitive-services
author: nstulasi
manager: sangitap
ms.service: cognitive-services
ms.component: QnAMaker
ms.topic: article
ms.date: 05/07/2018
ms.author: saneppal
ms.openlocfilehash: e18d656236276595fc5186a6656349bf28974ead
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870374"
---
# <a name="collaborate-on-your-knowledge-base"></a><span data-ttu-id="4cff9-103">Collaborate on your knowledge base</span><span class="sxs-lookup"><span data-stu-id="4cff9-103">Collaborate on your knowledge base</span></span>

<span data-ttu-id="4cff9-104">QnA Maker allows multiple people to collaborate on a knowledge base.</span><span class="sxs-lookup"><span data-stu-id="4cff9-104">QnA Maker allows multiple people to collaborate on a knowledge base.</span></span> <span data-ttu-id="4cff9-105">This feature is provided with the Azure [Role-Based Access Control](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-configure).</span><span class="sxs-lookup"><span data-stu-id="4cff9-105">This feature is provided with the Azure [Role-Based Access Control](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-configure).</span></span> 

<span data-ttu-id="4cff9-106">Perform the following steps to share your QnA Maker service with someone:</span><span class="sxs-lookup"><span data-stu-id="4cff9-106">Perform the following steps to share your QnA Maker service with someone:</span></span>

1. <span data-ttu-id="4cff9-107">Log in to the Azure portal, and go to your QnA Maker resource.</span><span class="sxs-lookup"><span data-stu-id="4cff9-107">Log in to the Azure portal, and go to your QnA Maker resource.</span></span>

    ![QnA Maker resource list](../media/qnamaker-how-to-collaborate-knowledge-base/qnamaker-resource-list.PNG)

2. <span data-ttu-id="4cff9-109">Go to the **Access Control (IAM)** tab.</span><span class="sxs-lookup"><span data-stu-id="4cff9-109">Go to the **Access Control (IAM)** tab.</span></span>

    ![QnA Maker IAM](../media/qnamaker-how-to-collaborate-knowledge-base/qnamaker-iam.PNG)

3. <span data-ttu-id="4cff9-111">Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="4cff9-111">Select **Add**.</span></span>

    ![QnA Maker IAM add](../media/qnamaker-how-to-collaborate-knowledge-base/qnamaker-iam-add.PNG)

4. <span data-ttu-id="4cff9-113">Select the **Owner** or the **Contributor** role.</span><span class="sxs-lookup"><span data-stu-id="4cff9-113">Select the **Owner** or the **Contributor** role.</span></span>

    ![QnA Maker IAM add role](../media/qnamaker-how-to-collaborate-knowledge-base/qnamaker-iam-add-role.PNG)

5. <span data-ttu-id="4cff9-115">Enter the email you want to share with, and press save.</span><span class="sxs-lookup"><span data-stu-id="4cff9-115">Enter the email you want to share with, and press save.</span></span>

    ![QnA Maker IAM add email](../media/qnamaker-how-to-collaborate-knowledge-base/qnamaker-iam-add-email.PNG)

<span data-ttu-id="4cff9-117">Now when the person you shared your QnA Maker service with, logs into the [QnA Maker portal](https://qnamaker.ai) they can see all the knowledge bases in that service.</span><span class="sxs-lookup"><span data-stu-id="4cff9-117">Now when the person you shared your QnA Maker service with, logs into the [QnA Maker portal](https://qnamaker.ai) they can see all the knowledge bases in that service.</span></span>

<span data-ttu-id="4cff9-118">Remember, you cannot share a particular knowledge base in a QnA Maker service.</span><span class="sxs-lookup"><span data-stu-id="4cff9-118">Remember, you cannot share a particular knowledge base in a QnA Maker service.</span></span> <span data-ttu-id="4cff9-119">If you want more granular access control, consider distributing your knowledge bases across different QnA Maker services.</span><span class="sxs-lookup"><span data-stu-id="4cff9-119">If you want more granular access control, consider distributing your knowledge bases across different QnA Maker services.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4cff9-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="4cff9-120">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4cff9-121">Test a knowledge base</span><span class="sxs-lookup"><span data-stu-id="4cff9-121">Test a knowledge base</span></span>](./test-knowledge-base.md)
