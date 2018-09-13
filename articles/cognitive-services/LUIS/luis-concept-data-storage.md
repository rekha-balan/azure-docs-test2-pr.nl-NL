---
title: Data storage in LUIS - Language Understanding
titleSuffix: Azure Cognitive Services
description: Learn how data is stored in Language Understanding (LUIS). LUIS stores data encrypted in an Azure data store corresponding to the region specified by the key.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 05/08/2018
ms.author: diberry
ms.openlocfilehash: a34426efd998a5573277e9129b832f5167c5da5e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855847"
---
# <a name="data-storage-and-removal-in-language-understanding-luis-cognitive-services"></a><span data-ttu-id="48478-104">Data storage and removal in Language Understanding (LUIS) Cognitive Services</span><span class="sxs-lookup"><span data-stu-id="48478-104">Data storage and removal in Language Understanding (LUIS) Cognitive Services</span></span>
<span data-ttu-id="48478-105">LUIS stores data encrypted in an Azure data store corresponding to the region specified by the key.</span><span class="sxs-lookup"><span data-stu-id="48478-105">LUIS stores data encrypted in an Azure data store corresponding to the region specified by the key.</span></span> <span data-ttu-id="48478-106">This data is stored for 30 days.</span><span class="sxs-lookup"><span data-stu-id="48478-106">This data is stored for 30 days.</span></span> 

## <a name="export-and-delete-app"></a><span data-ttu-id="48478-107">Export and delete app</span><span class="sxs-lookup"><span data-stu-id="48478-107">Export and delete app</span></span>
<span data-ttu-id="48478-108">Users have full control over [exporting](luis-how-to-start-new-app.md#export-app) and [deleting](luis-how-to-start-new-app.md#delete-app) the app.</span><span class="sxs-lookup"><span data-stu-id="48478-108">Users have full control over [exporting](luis-how-to-start-new-app.md#export-app) and [deleting](luis-how-to-start-new-app.md#delete-app) the app.</span></span> 

## <a name="utterances-in-an-intent"></a><span data-ttu-id="48478-109">Utterances in an intent</span><span class="sxs-lookup"><span data-stu-id="48478-109">Utterances in an intent</span></span>
<span data-ttu-id="48478-110">Delete example utterances used for training [LUIS](luis-reference-regions.md).</span><span class="sxs-lookup"><span data-stu-id="48478-110">Delete example utterances used for training [LUIS](luis-reference-regions.md).</span></span> <span data-ttu-id="48478-111">If you delete an example utterance from your LUIS app, it is removed from the LUIS web service and is unavailable for export.</span><span class="sxs-lookup"><span data-stu-id="48478-111">If you delete an example utterance from your LUIS app, it is removed from the LUIS web service and is unavailable for export.</span></span>

## <a name="utterances-in-review"></a><span data-ttu-id="48478-112">Utterances in review</span><span class="sxs-lookup"><span data-stu-id="48478-112">Utterances in review</span></span>
<span data-ttu-id="48478-113">You can delete utterances from the list of user utterances that LUIS suggests in the **[Review endpoint utterances page](luis-how-to-review-endoint-utt.md)**.</span><span class="sxs-lookup"><span data-stu-id="48478-113">You can delete utterances from the list of user utterances that LUIS suggests in the **[Review endpoint utterances page](luis-how-to-review-endoint-utt.md)**.</span></span> <span data-ttu-id="48478-114">Deleting utterances from this list prevents them from being suggested, but doesn't delete them from logs.</span><span class="sxs-lookup"><span data-stu-id="48478-114">Deleting utterances from this list prevents them from being suggested, but doesn't delete them from logs.</span></span>

## <a name="accounts"></a><span data-ttu-id="48478-115">Accounts</span><span class="sxs-lookup"><span data-stu-id="48478-115">Accounts</span></span>
<span data-ttu-id="48478-116">If you delete an account, all apps are deleted, along with their example utterances and logs.</span><span class="sxs-lookup"><span data-stu-id="48478-116">If you delete an account, all apps are deleted, along with their example utterances and logs.</span></span> <span data-ttu-id="48478-117">The data is retained for 60 days before the account and data are deleted permanently.</span><span class="sxs-lookup"><span data-stu-id="48478-117">The data is retained for 60 days before the account and data are deleted permanently.</span></span>

<span data-ttu-id="48478-118">Deleting account is available from the **Settings** page.</span><span class="sxs-lookup"><span data-stu-id="48478-118">Deleting account is available from the **Settings** page.</span></span> <span data-ttu-id="48478-119">Select your account name in the top right navigation bar to get to the **Settings** page.</span><span class="sxs-lookup"><span data-stu-id="48478-119">Select your account name in the top right navigation bar to get to the **Settings** page.</span></span>

## <a name="data-inactivity-as-an-expired-subscription"></a><span data-ttu-id="48478-120">Data inactivity as an expired subscription</span><span class="sxs-lookup"><span data-stu-id="48478-120">Data inactivity as an expired subscription</span></span>
<span data-ttu-id="48478-121">For the purposes of data retention and deletion, an inactive LUIS app may at _Microsoft’s discretion_ be treated as an expired subscription.</span><span class="sxs-lookup"><span data-stu-id="48478-121">For the purposes of data retention and deletion, an inactive LUIS app may at _Microsoft’s discretion_ be treated as an expired subscription.</span></span> <span data-ttu-id="48478-122">An app is considered inactive if it meets the following criteria for the last 90 days:</span><span class="sxs-lookup"><span data-stu-id="48478-122">An app is considered inactive if it meets the following criteria for the last 90 days:</span></span> 

* <span data-ttu-id="48478-123">Has had **no** calls made to it.</span><span class="sxs-lookup"><span data-stu-id="48478-123">Has had **no** calls made to it.</span></span>
* <span data-ttu-id="48478-124">Has not been modified.</span><span class="sxs-lookup"><span data-stu-id="48478-124">Has not been modified.</span></span>
* <span data-ttu-id="48478-125">Does not have a current key assigned to it.</span><span class="sxs-lookup"><span data-stu-id="48478-125">Does not have a current key assigned to it.</span></span>
* <span data-ttu-id="48478-126">Has not had a user sign in to it.</span><span class="sxs-lookup"><span data-stu-id="48478-126">Has not had a user sign in to it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48478-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="48478-127">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="48478-128">Learn about exporting and deleting an app</span><span class="sxs-lookup"><span data-stu-id="48478-128">Learn about exporting and deleting an app</span></span>](luis-how-to-start-new-app.md)