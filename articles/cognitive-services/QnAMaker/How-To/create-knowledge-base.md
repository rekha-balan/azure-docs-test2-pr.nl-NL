---
title: How to create a knowledge base - QnA Maker - Azure Cognitive Services | Microsoft Docs
description: How to create a knowledge base
services: cognitive-services
author: nstulasi
manager: sangitap
ms.service: cognitive-services
ms.component: QnAMaker
ms.topic: article
ms.date: 05/07/2018
ms.author: saneppal
ms.openlocfilehash: 93b64948ecc52feeb0f862f2b76ea898dce2333a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870174"
---
# <a name="create-a-knowledge-base"></a><span data-ttu-id="466cc-103">Create a knowledge base</span><span class="sxs-lookup"><span data-stu-id="466cc-103">Create a knowledge base</span></span>

<span data-ttu-id="466cc-104">QnA Maker makes it very simple to onboard your existing data sources to create a knowledge base.</span><span class="sxs-lookup"><span data-stu-id="466cc-104">QnA Maker makes it very simple to onboard your existing data sources to create a knowledge base.</span></span> <span data-ttu-id="466cc-105">You can create a new QnA Maker knowledge base from FAQ pages, products manuals, structured documents or add them editorially.</span><span class="sxs-lookup"><span data-stu-id="466cc-105">You can create a new QnA Maker knowledge base from FAQ pages, products manuals, structured documents or add them editorially.</span></span>

## <a name="steps"></a><span data-ttu-id="466cc-106">Steps</span><span class="sxs-lookup"><span data-stu-id="466cc-106">Steps</span></span>

1. <span data-ttu-id="466cc-107">To get started, sign into to the [QnA Maker portal](https://qnamaker.ai) with your azure credentials and click on **Create new service**.</span><span class="sxs-lookup"><span data-stu-id="466cc-107">To get started, sign into to the [QnA Maker portal](https://qnamaker.ai) with your azure credentials and click on **Create new service**.</span></span>

    ![<span data-ttu-id="466cc-108">Create KB</span><span class="sxs-lookup"><span data-stu-id="466cc-108">Create KB</span></span> ](../media/qnamaker-how-to-create-kb/create-new-service.png)

2. <span data-ttu-id="466cc-109">If you have not already created a QnA Maker service, select **Create a QnA service**.</span><span class="sxs-lookup"><span data-stu-id="466cc-109">If you have not already created a QnA Maker service, select **Create a QnA service**.</span></span> <span data-ttu-id="466cc-110">Otherwise, choose a QnA Maker service from the drop-downs in Step 2.</span><span class="sxs-lookup"><span data-stu-id="466cc-110">Otherwise, choose a QnA Maker service from the drop-downs in Step 2.</span></span> <span data-ttu-id="466cc-111">Select the QnA Maker service that will host the Knowledge Base.</span><span class="sxs-lookup"><span data-stu-id="466cc-111">Select the QnA Maker service that will host the Knowledge Base.</span></span>

    ![Setup QnA service](../media/qnamaker-how-to-create-kb/setup-qna-resource.png)

3. <span data-ttu-id="466cc-113">Enter the following information in order to create the knowledge base.</span><span class="sxs-lookup"><span data-stu-id="466cc-113">Enter the following information in order to create the knowledge base.</span></span>

    ![Set data sources](../media/qnamaker-how-to-create-kb/set-data-sources.png)

    - <span data-ttu-id="466cc-115">Give your service a **name.**</span><span class="sxs-lookup"><span data-stu-id="466cc-115">Give your service a **name.**</span></span> <span data-ttu-id="466cc-116">Duplicate names are supported and special characters are supported as well.</span><span class="sxs-lookup"><span data-stu-id="466cc-116">Duplicate names are supported and special characters are supported as well.</span></span>
    - <span data-ttu-id="466cc-117">Paste in URLs which will be extracted from.</span><span class="sxs-lookup"><span data-stu-id="466cc-117">Paste in URLs which will be extracted from.</span></span> <span data-ttu-id="466cc-118">See more information on the types of sources supported [here](../Concepts/data-sources-supported.md).</span><span class="sxs-lookup"><span data-stu-id="466cc-118">See more information on the types of sources supported [here](../Concepts/data-sources-supported.md).</span></span>
    - <span data-ttu-id="466cc-119">Alternately, upload files from which data is extracted.</span><span class="sxs-lookup"><span data-stu-id="466cc-119">Alternately, upload files from which data is extracted.</span></span> <span data-ttu-id="466cc-120">See the [pricing information](https://aka.ms/qnamaker-pricing
) to see how many documents you can add.</span><span class="sxs-lookup"><span data-stu-id="466cc-120">See the [pricing information](https://aka.ms/qnamaker-pricing
) to see how many documents you can add.</span></span>
    - <span data-ttu-id="466cc-121">If you want to manually add QnAs, you can skip linking files.</span><span class="sxs-lookup"><span data-stu-id="466cc-121">If you want to manually add QnAs, you can skip linking files.</span></span>

4. <span data-ttu-id="466cc-122">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="466cc-122">Select **Create**.</span></span>

    ![Create KB](../media/qnamaker-how-to-create-kb/create-kb.png)

5. <span data-ttu-id="466cc-124">It takes a few minutes for data to be extracted.</span><span class="sxs-lookup"><span data-stu-id="466cc-124">It takes a few minutes for data to be extracted.</span></span>

    ![Extraction](../media/qnamaker-how-to-create-kb/hang-tight-extraction.png)

6. <span data-ttu-id="466cc-126">If your Knowledge Base has been successfully created, you will be redirected to the **Knowledge base** page.</span><span class="sxs-lookup"><span data-stu-id="466cc-126">If your Knowledge Base has been successfully created, you will be redirected to the **Knowledge base** page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="466cc-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="466cc-127">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="466cc-128">Import a knowledge base</span><span class="sxs-lookup"><span data-stu-id="466cc-128">Import a knowledge base</span></span>](../Tutorials/migrate-knowledge-base.md)
