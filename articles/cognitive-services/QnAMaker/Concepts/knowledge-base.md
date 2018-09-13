---
title: Knowledge base - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: About a knowledge base
services: cognitive-services
author: nstulasi
manager: sangitap
ms.service: cognitive-services
ms.component: QnAMaker
ms.topic: article
ms.date: 05/07/2018
ms.author: saneppal
ms.openlocfilehash: 5dfb96f454bf5ce3f030ebfc6a97482fcfc9469b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967446"
---
# <a name="knowledge-base"></a><span data-ttu-id="482da-103">Knowledge base</span><span class="sxs-lookup"><span data-stu-id="482da-103">Knowledge base</span></span>

<span data-ttu-id="482da-104">A QnA Maker knowledge base consists of a set of question/answer (QnA) pairs and optional metadata associated with each QnA pair.</span><span class="sxs-lookup"><span data-stu-id="482da-104">A QnA Maker knowledge base consists of a set of question/answer (QnA) pairs and optional metadata associated with each QnA pair.</span></span>

## <a name="key-knowledge-base-concepts"></a><span data-ttu-id="482da-105">Key knowledge base concepts</span><span class="sxs-lookup"><span data-stu-id="482da-105">Key knowledge base concepts</span></span>

* <span data-ttu-id="482da-106">**Questions** - A question contains text that best represents a user query.</span><span class="sxs-lookup"><span data-stu-id="482da-106">**Questions** - A question contains text that best represents a user query.</span></span> 
* <span data-ttu-id="482da-107">**Answers** - An answer is the response that is returned when a user query is matched with the associated question.</span><span class="sxs-lookup"><span data-stu-id="482da-107">**Answers** - An answer is the response that is returned when a user query is matched with the associated question.</span></span>  
* <span data-ttu-id="482da-108">**Metadata** - Metadata are tags associated with a QnA pair and are represented as key-value pairs.</span><span class="sxs-lookup"><span data-stu-id="482da-108">**Metadata** - Metadata are tags associated with a QnA pair and are represented as key-value pairs.</span></span> <span data-ttu-id="482da-109">Metadata are used to filter QnA pairs and limit the set over which query matching is performed.</span><span class="sxs-lookup"><span data-stu-id="482da-109">Metadata are used to filter QnA pairs and limit the set over which query matching is performed.</span></span>

<span data-ttu-id="482da-110">A single QnA, represented by a numeric QnA ID, has multiple variants of a question (alternate questions) that all map to a single answer.</span><span class="sxs-lookup"><span data-stu-id="482da-110">A single QnA, represented by a numeric QnA ID, has multiple variants of a question (alternate questions) that all map to a single answer.</span></span> <span data-ttu-id="482da-111">Additionally, each such pair can have multiple metadata fields associated with it.</span><span class="sxs-lookup"><span data-stu-id="482da-111">Additionally, each such pair can have multiple metadata fields associated with it.</span></span>

![QnA Maker knowledge bases](../media/qnamaker-concepts-knowledgebase/knowledgebase.png) 

## <a name="knowledge-base-content-format"></a><span data-ttu-id="482da-113">Knowledge base content format</span><span class="sxs-lookup"><span data-stu-id="482da-113">Knowledge base content format</span></span>

<span data-ttu-id="482da-114">When you ingest rich content into a knowledge base, QnA Maker attempts to convert the content to markdown.</span><span class="sxs-lookup"><span data-stu-id="482da-114">When you ingest rich content into a knowledge base, QnA Maker attempts to convert the content to markdown.</span></span> <span data-ttu-id="482da-115">Read [this](https://aka.ms/qnamaker-docs-markdown-support) blog to understand the markdown formats understandable by most chat clients.</span><span class="sxs-lookup"><span data-stu-id="482da-115">Read [this](https://aka.ms/qnamaker-docs-markdown-support) blog to understand the markdown formats understandable by most chat clients.</span></span>

<span data-ttu-id="482da-116">Metadata fields consist of key-value pairs separated by a colon **(Product:Shredder)**.</span><span class="sxs-lookup"><span data-stu-id="482da-116">Metadata fields consist of key-value pairs separated by a colon **(Product:Shredder)**.</span></span> <span data-ttu-id="482da-117">Both key and value must be text-only.</span><span class="sxs-lookup"><span data-stu-id="482da-117">Both key and value must be text-only.</span></span> <span data-ttu-id="482da-118">The metadata key must not contain any spaces.</span><span class="sxs-lookup"><span data-stu-id="482da-118">The metadata key must not contain any spaces.</span></span>

## <a name="next-steps"></a><span data-ttu-id="482da-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="482da-119">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="482da-120">Development lifecycle of a knowledge base</span><span class="sxs-lookup"><span data-stu-id="482da-120">Development lifecycle of a knowledge base</span></span>](./development-lifecycle-knowledge-base.md)

## <a name="see-also"></a><span data-ttu-id="482da-121">See also</span><span class="sxs-lookup"><span data-stu-id="482da-121">See also</span></span>

[<span data-ttu-id="482da-122">QnA Maker overview</span><span class="sxs-lookup"><span data-stu-id="482da-122">QnA Maker overview</span></span>](../Overview/overview.md)