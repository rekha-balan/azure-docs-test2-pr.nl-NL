---
title: Phrase lists to enhance entity detection
titleSuffix: Azure Cognitive Services
description: Use Language Understanding (LUIS) to add app features that can improve the detection or prediction of intents and entities that categories and patterns
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 09/06/2018
ms.author: diberry
ms.openlocfilehash: 0fe4e1c64d1d443148f1d0a8ba2a9856e3566f30
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867206"
---
# <a name="use-phrase-lists-to-boost-signal-of-word-list"></a><span data-ttu-id="e5e7a-103">Use phrase lists to boost signal of word list</span><span class="sxs-lookup"><span data-stu-id="e5e7a-103">Use phrase lists to boost signal of word list</span></span>

<span data-ttu-id="e5e7a-104">You can add features to your LUIS app to improve its accuracy.</span><span class="sxs-lookup"><span data-stu-id="e5e7a-104">You can add features to your LUIS app to improve its accuracy.</span></span> <span data-ttu-id="e5e7a-105">Features help LUIS by providing hints that certain words and phrases are part of an app domain vocabulary.</span><span class="sxs-lookup"><span data-stu-id="e5e7a-105">Features help LUIS by providing hints that certain words and phrases are part of an app domain vocabulary.</span></span> 

## <a name="add-phrase-list"></a><span data-ttu-id="e5e7a-106">Add phrase list</span><span class="sxs-lookup"><span data-stu-id="e5e7a-106">Add phrase list</span></span>

1. <span data-ttu-id="e5e7a-107">Open your app by clicking its name on **My Apps** page, and then click **Build**, then click **Phrase lists** in your app's left panel.</span><span class="sxs-lookup"><span data-stu-id="e5e7a-107">Open your app by clicking its name on **My Apps** page, and then click **Build**, then click **Phrase lists** in your app's left panel.</span></span> 

2. <span data-ttu-id="e5e7a-108">On the **Phrase lists** page, click **Create new phrase list**.</span><span class="sxs-lookup"><span data-stu-id="e5e7a-108">On the **Phrase lists** page, click **Create new phrase list**.</span></span> 
 
3. <span data-ttu-id="e5e7a-109">In the **Add Phrase List** dialog box, type "Cities" as the name of the phrase list.</span><span class="sxs-lookup"><span data-stu-id="e5e7a-109">In the **Add Phrase List** dialog box, type "Cities" as the name of the phrase list.</span></span> <span data-ttu-id="e5e7a-110">In the **Value** box, type the values of the phrase list.</span><span class="sxs-lookup"><span data-stu-id="e5e7a-110">In the **Value** box, type the values of the phrase list.</span></span> <span data-ttu-id="e5e7a-111">You can type one value at a time, or a set of values separated by commas, and then press **Enter**.</span><span class="sxs-lookup"><span data-stu-id="e5e7a-111">You can type one value at a time, or a set of values separated by commas, and then press **Enter**.</span></span>

    ![Add phrase list Cities](./media/luis-add-features/add-phrase-list-cities.png)

4. <span data-ttu-id="e5e7a-113">LUIS can propose related values to add to your phrase list.</span><span class="sxs-lookup"><span data-stu-id="e5e7a-113">LUIS can propose related values to add to your phrase list.</span></span> <span data-ttu-id="e5e7a-114">Click **Recommend** to get a group of proposed values that are semantically related to the added value(s).</span><span class="sxs-lookup"><span data-stu-id="e5e7a-114">Click **Recommend** to get a group of proposed values that are semantically related to the added value(s).</span></span> <span data-ttu-id="e5e7a-115">You can click any of the proposed values, or click **Add All** to add them all.</span><span class="sxs-lookup"><span data-stu-id="e5e7a-115">You can click any of the proposed values, or click **Add All** to add them all.</span></span>

    ![Phrase List Proposed Values](./media/luis-add-features/related-values.png)

5. <span data-ttu-id="e5e7a-117">Click **These values are interchangeable** if the added phrase list values are alternatives that can be used interchangeably.</span><span class="sxs-lookup"><span data-stu-id="e5e7a-117">Click **These values are interchangeable** if the added phrase list values are alternatives that can be used interchangeably.</span></span>

    ![Phrase List Proposed Values](./media/luis-add-features/interchangeable.png)

6. <span data-ttu-id="e5e7a-119">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="e5e7a-119">Click **Save**.</span></span> <span data-ttu-id="e5e7a-120">The "Cities" phrase list is added to the **Phrase lists** page.</span><span class="sxs-lookup"><span data-stu-id="e5e7a-120">The "Cities" phrase list is added to the **Phrase lists** page.</span></span>

<a name="edit-phrase-list"></a>
<a name="delete-phrase-list"></a>
<a name="deactivate-phrase-list"></a>

> [!Note]
> <span data-ttu-id="e5e7a-121">You can edit, delete, or deactivate a phrase list from the ellipsis (***...***) button at the end of the row of eac phrase list.</span><span class="sxs-lookup"><span data-stu-id="e5e7a-121">You can edit, delete, or deactivate a phrase list from the ellipsis (***...***) button at the end of the row of eac phrase list.</span></span>

## <a name="pattern-regular-expression-feature"></a><span data-ttu-id="e5e7a-122">Pattern (regular expression) feature</span><span class="sxs-lookup"><span data-stu-id="e5e7a-122">Pattern (regular expression) feature</span></span> 
<span data-ttu-id="e5e7a-123">**This feature is deprecated**.</span><span class="sxs-lookup"><span data-stu-id="e5e7a-123">**This feature is deprecated**.</span></span> <span data-ttu-id="e5e7a-124">New pattern features cannot be added to LUIS.</span><span class="sxs-lookup"><span data-stu-id="e5e7a-124">New pattern features cannot be added to LUIS.</span></span> <span data-ttu-id="e5e7a-125">Any existing pattern features are supported until May 2018.</span><span class="sxs-lookup"><span data-stu-id="e5e7a-125">Any existing pattern features are supported until May 2018.</span></span> <span data-ttu-id="e5e7a-126">Contribute to standard LUIS regular expression matching with a PR to the [Recognizers-Text Github repository](https://github.com/Microsoft/Recognizers-Text).</span><span class="sxs-lookup"><span data-stu-id="e5e7a-126">Contribute to standard LUIS regular expression matching with a PR to the [Recognizers-Text Github repository](https://github.com/Microsoft/Recognizers-Text).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e5e7a-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="e5e7a-127">Next steps</span></span>

<span data-ttu-id="e5e7a-128">After adding, editing, deleting, or deactivating a phrase list, [train and test the app](luis-interactive-test.md) again to see if performance improves.</span><span class="sxs-lookup"><span data-stu-id="e5e7a-128">After adding, editing, deleting, or deactivating a phrase list, [train and test the app](luis-interactive-test.md) again to see if performance improves.</span></span>
