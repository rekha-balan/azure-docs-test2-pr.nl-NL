---
title: How to edit a knowledge base - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: How to edit a knowledge base
services: cognitive-services
author: nstulasi
manager: sangitap
ms.service: cognitive-services
ms.component: QnAMaker
ms.topic: article
ms.date: 04/21/2018
ms.author: saneppal
ms.openlocfilehash: eaa65bf3d257399fceadaa42f0d9ddbbf8afe234
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966140"
---
# <a name="edit-a-knowledge-base"></a><span data-ttu-id="788cd-103">Edit a knowledge base</span><span class="sxs-lookup"><span data-stu-id="788cd-103">Edit a knowledge base</span></span>

<span data-ttu-id="788cd-104">QnA Maker allows you to manage the content of your knowledge base by providing an easy-to-use editing experience.</span><span class="sxs-lookup"><span data-stu-id="788cd-104">QnA Maker allows you to manage the content of your knowledge base by providing an easy-to-use editing experience.</span></span>

## <a name="edit-your-knowledge-base-content"></a><span data-ttu-id="788cd-105">Edit your knowledge base content</span><span class="sxs-lookup"><span data-stu-id="788cd-105">Edit your knowledge base content</span></span>

1.  <span data-ttu-id="788cd-106">Select **My knowledge bases** in the top navigation bar.</span><span class="sxs-lookup"><span data-stu-id="788cd-106">Select **My knowledge bases** in the top navigation bar.</span></span> 

    <span data-ttu-id="788cd-107">You can see all the services you created or shared with you sorted in the descending order of the **last modified** date.</span><span class="sxs-lookup"><span data-stu-id="788cd-107">You can see all the services you created or shared with you sorted in the descending order of the **last modified** date.</span></span>

    ![My Knowledge Bases](../media/qnamaker-how-to-edit-kb/my-kbs.png)

2. <span data-ttu-id="788cd-109">Select a particular knowledge base to make edits to it.</span><span class="sxs-lookup"><span data-stu-id="788cd-109">Select a particular knowledge base to make edits to it.</span></span>

3. <span data-ttu-id="788cd-110">Once you are done making changes to the Knowledge base, click on **Save and train** in the top right corner of the page in order to persist the changes.</span><span class="sxs-lookup"><span data-stu-id="788cd-110">Once you are done making changes to the Knowledge base, click on **Save and train** in the top right corner of the page in order to persist the changes.</span></span>    

    ![Save and Train](../media/qnamaker-how-to-edit-kb/save-and-train.png)

    >[!NOTE]
    <span data-ttu-id="788cd-112">Leaving the page before clicking on Save and train will not persist the changes.</span><span class="sxs-lookup"><span data-stu-id="788cd-112">Leaving the page before clicking on Save and train will not persist the changes.</span></span>

## <a name="add-a-qna-pair"></a><span data-ttu-id="788cd-113">Add a QnA pair</span><span class="sxs-lookup"><span data-stu-id="788cd-113">Add a QnA pair</span></span>

<span data-ttu-id="788cd-114">Select **Add QnA pair** to add a new row to the knowledge base table.</span><span class="sxs-lookup"><span data-stu-id="788cd-114">Select **Add QnA pair** to add a new row to the knowledge base table.</span></span>

![Add QnA pair](../media/qnamaker-how-to-edit-kb/add-qnapair.png)

## <a name="delete-a-qna-pair"></a><span data-ttu-id="788cd-116">Delete a QnA pair</span><span class="sxs-lookup"><span data-stu-id="788cd-116">Delete a QnA pair</span></span>

<span data-ttu-id="788cd-117">To delete a QnA, click the **delete** icon on the far right of the QnA row.</span><span class="sxs-lookup"><span data-stu-id="788cd-117">To delete a QnA, click the **delete** icon on the far right of the QnA row.</span></span>

![Delete QnA pair](../media/qnamaker-how-to-edit-kb/delete-qnapair.png)

## <a name="add-alternate-questions"></a><span data-ttu-id="788cd-119">Add alternate questions</span><span class="sxs-lookup"><span data-stu-id="788cd-119">Add alternate questions</span></span>

<span data-ttu-id="788cd-120">Add alternate questions to an existing QnA pair to improve the likelihood of a match to a user query.</span><span class="sxs-lookup"><span data-stu-id="788cd-120">Add alternate questions to an existing QnA pair to improve the likelihood of a match to a user query.</span></span>

![Add Alternate Questions](../media/qnamaker-how-to-edit-kb/add-alternate-question.png)

## <a name="add-metadata"></a><span data-ttu-id="788cd-122">Add metadata</span><span class="sxs-lookup"><span data-stu-id="788cd-122">Add metadata</span></span>


<span data-ttu-id="788cd-123">Add metadata pairs by selecting the filter icon</span><span class="sxs-lookup"><span data-stu-id="788cd-123">Add metadata pairs by selecting the filter icon</span></span>

![Add Metadata](../media/qnamaker-how-to-edit-kb/add-metadata.png)

> [!TIP]
> <span data-ttu-id="788cd-125">Make sure to periodically Save and train the knowledge base after making edits to avoid losing changes.</span><span class="sxs-lookup"><span data-stu-id="788cd-125">Make sure to periodically Save and train the knowledge base after making edits to avoid losing changes.</span></span>

## <a name="manage-large-knowledge-bases"></a><span data-ttu-id="788cd-126">Manage large knowledge bases</span><span class="sxs-lookup"><span data-stu-id="788cd-126">Manage large knowledge bases</span></span>

1. <span data-ttu-id="788cd-127">The QnAs are **grouped** by the data source from which they were extracted.</span><span class="sxs-lookup"><span data-stu-id="788cd-127">The QnAs are **grouped** by the data source from which they were extracted.</span></span> <span data-ttu-id="788cd-128">You can expand or collapse the data source.</span><span class="sxs-lookup"><span data-stu-id="788cd-128">You can expand or collapse the data source.</span></span>
2. <span data-ttu-id="788cd-129">You can **search** the knowledge base by typing in the text box at the top of the Knowledge Base table.</span><span class="sxs-lookup"><span data-stu-id="788cd-129">You can **search** the knowledge base by typing in the text box at the top of the Knowledge Base table.</span></span> <span data-ttu-id="788cd-130">Click enter to search on the question, answer or metadata content.</span><span class="sxs-lookup"><span data-stu-id="788cd-130">Click enter to search on the question, answer or metadata content.</span></span> <span data-ttu-id="788cd-131">Click on the X icon to remove the search filter.</span><span class="sxs-lookup"><span data-stu-id="788cd-131">Click on the X icon to remove the search filter.</span></span>
3. <span data-ttu-id="788cd-132">**Pagination** allows you to manage large knowledge bases</span><span class="sxs-lookup"><span data-stu-id="788cd-132">**Pagination** allows you to manage large knowledge bases</span></span>

    ![Search, Paginate, Group](../media/qnamaker-how-to-edit-kb/search-paginate-group.png)

## <a name="next-steps"></a><span data-ttu-id="788cd-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="788cd-134">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="788cd-135">Collaborate on a knowledge base</span><span class="sxs-lookup"><span data-stu-id="788cd-135">Collaborate on a knowledge base</span></span>](./collaborate-knowledge-base.md)
