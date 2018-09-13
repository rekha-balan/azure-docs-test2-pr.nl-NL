---
title: How to create a non-English knowledge base - QnA Maker - Azure Cognitive Services | Microsoft Docs
description: How to create a non-English knowledge base.
services: cognitive-services
author: nstulasi
manager: sangitap
ms.service: cognitive-services
ms.component: QnAMaker
ms.topic: article
ms.date: 05/07/2018
ms.author: saneppal
ms.openlocfilehash: 3fbd590229044af0daa60968fd8d556d539a58c9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870761"
---
# <a name="language-support-of-knowledge-base-content-for-qna-maker"></a><span data-ttu-id="ff00e-103">Language support of knowledge base content for QnA Maker</span><span class="sxs-lookup"><span data-stu-id="ff00e-103">Language support of knowledge base content for QnA Maker</span></span>
<span data-ttu-id="ff00e-104">QnA Maker supports knowledge base content in many languages.</span><span class="sxs-lookup"><span data-stu-id="ff00e-104">QnA Maker supports knowledge base content in many languages.</span></span> <span data-ttu-id="ff00e-105">However, each QnA Maker service should be reserved for a single language.</span><span class="sxs-lookup"><span data-stu-id="ff00e-105">However, each QnA Maker service should be reserved for a single language.</span></span> <span data-ttu-id="ff00e-106">The first knowledge base created targeting a particular QnA Maker service sets the language of that service.</span><span class="sxs-lookup"><span data-stu-id="ff00e-106">The first knowledge base created targeting a particular QnA Maker service sets the language of that service.</span></span> <span data-ttu-id="ff00e-107">See [here](../Overview/languages-supported.md) for the list of supported languages.</span><span class="sxs-lookup"><span data-stu-id="ff00e-107">See [here](../Overview/languages-supported.md) for the list of supported languages.</span></span>

<span data-ttu-id="ff00e-108">The language is automatically recognized from the content of the data sources being extracted.</span><span class="sxs-lookup"><span data-stu-id="ff00e-108">The language is automatically recognized from the content of the data sources being extracted.</span></span> <span data-ttu-id="ff00e-109">Once you create a new QnA Maker Service and a new Knowledge Base in that service, you can verify that the language has been set correctly.</span><span class="sxs-lookup"><span data-stu-id="ff00e-109">Once you create a new QnA Maker Service and a new Knowledge Base in that service, you can verify that the language has been set correctly.</span></span>

1. <span data-ttu-id="ff00e-110">Navigate to the [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ff00e-110">Navigate to the [Azure Portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="ff00e-111">Select **resource groups** and navigate to the resource group where the QnA Maker service is deployed and select the **Azure Search** resource.</span><span class="sxs-lookup"><span data-stu-id="ff00e-111">Select **resource groups** and navigate to the resource group where the QnA Maker service is deployed and select the **Azure Search** resource.</span></span>

    ![Select Azure Search resource](../media/qnamaker-how-to-language-kb/select-azsearch.png)

3. <span data-ttu-id="ff00e-113">Select the **testkb** index.</span><span class="sxs-lookup"><span data-stu-id="ff00e-113">Select the **testkb** index.</span></span> <span data-ttu-id="ff00e-114">This Azure Search index is always the first one created and it contains the saved content of all the knowledge bases in that service.</span><span class="sxs-lookup"><span data-stu-id="ff00e-114">This Azure Search index is always the first one created and it contains the saved content of all the knowledge bases in that service.</span></span> 

    ![Select the Test KB](../media/qnamaker-how-to-language-kb/select-testkb.png)

4. <span data-ttu-id="ff00e-116">Select **Fields** section showing the testkb details.</span><span class="sxs-lookup"><span data-stu-id="ff00e-116">Select **Fields** section showing the testkb details.</span></span>

    ![Select Fields](../media/qnamaker-how-to-language-kb/selectfields.png)

5. <span data-ttu-id="ff00e-118">Check the box for **Analyzer** to see language details.</span><span class="sxs-lookup"><span data-stu-id="ff00e-118">Check the box for **Analyzer** to see language details.</span></span>

    ![Select Analyzer](../media/qnamaker-how-to-language-kb/select-analyzer.png)

6. <span data-ttu-id="ff00e-120">You should find that the Analyzer is set to a particular language.</span><span class="sxs-lookup"><span data-stu-id="ff00e-120">You should find that the Analyzer is set to a particular language.</span></span> <span data-ttu-id="ff00e-121">This language was automatically detected during the knowledge base creation step.</span><span class="sxs-lookup"><span data-stu-id="ff00e-121">This language was automatically detected during the knowledge base creation step.</span></span> <span data-ttu-id="ff00e-122">This language cannot be changed once the resource is created.</span><span class="sxs-lookup"><span data-stu-id="ff00e-122">This language cannot be changed once the resource is created.</span></span>

    ![Selected Analyzer](../media/qnamaker-how-to-language-kb/selected-analyzer.png)

## <a name="next-steps"></a><span data-ttu-id="ff00e-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="ff00e-124">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ff00e-125">Create a QnA bot with Azure Bot Service</span><span class="sxs-lookup"><span data-stu-id="ff00e-125">Create a QnA bot with Azure Bot Service</span></span>](../Tutorials/create-qna-bot.md)
