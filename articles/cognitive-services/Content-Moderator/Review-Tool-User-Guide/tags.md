---
title: Using tags in Azure Content Moderator | Microsoft Docs
description: Content Moderator includes default tags, and you can create custom tags for moderating content specific to your business.
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.component: content-moderator
ms.topic: article
ms.date: 06/25/2017
ms.author: sajagtap
ms.openlocfilehash: add4c685c07c63944ae89f48a47ac78df28c1623
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871461"
---
# <a name="about-tags"></a><span data-ttu-id="5b10b-103">About Tags</span><span class="sxs-lookup"><span data-stu-id="5b10b-103">About Tags</span></span> #

<span data-ttu-id="5b10b-104">In addition to the two default tags (a – isadult and r – isracy), you can create custom tags for more targeted scanning.</span><span class="sxs-lookup"><span data-stu-id="5b10b-104">In addition to the two default tags (a – isadult and r – isracy), you can create custom tags for more targeted scanning.</span></span> <span data-ttu-id="5b10b-105">These custom tags are then available for human reviewers to assign to images or text.</span><span class="sxs-lookup"><span data-stu-id="5b10b-105">These custom tags are then available for human reviewers to assign to images or text.</span></span>

## <a name="create-tags"></a><span data-ttu-id="5b10b-106">Create tags</span><span class="sxs-lookup"><span data-stu-id="5b10b-106">Create tags</span></span> ##

1.  <span data-ttu-id="5b10b-107">Select Tags from the Settings tab.</span><span class="sxs-lookup"><span data-stu-id="5b10b-107">Select Tags from the Settings tab.</span></span>

  ![Content Moderation Tags](images/tags-1.png)

2.  <span data-ttu-id="5b10b-109">Enter a two-letter Short code for the tag.</span><span class="sxs-lookup"><span data-stu-id="5b10b-109">Enter a two-letter Short code for the tag.</span></span>
3.  <span data-ttu-id="5b10b-110">Enter a Name for the tag.</span><span class="sxs-lookup"><span data-stu-id="5b10b-110">Enter a Name for the tag.</span></span> <span data-ttu-id="5b10b-111">Keep the name short and descriptive.</span><span class="sxs-lookup"><span data-stu-id="5b10b-111">Keep the name short and descriptive.</span></span> <span data-ttu-id="5b10b-112">For example, “isNudity”.</span><span class="sxs-lookup"><span data-stu-id="5b10b-112">For example, “isNudity”.</span></span>
4.  <span data-ttu-id="5b10b-113">Enter a Description.</span><span class="sxs-lookup"><span data-stu-id="5b10b-113">Enter a Description.</span></span>
5.  <span data-ttu-id="5b10b-114">Click Add.</span><span class="sxs-lookup"><span data-stu-id="5b10b-114">Click Add.</span></span>
6.  <span data-ttu-id="5b10b-115">Click Save when you are done creating tags.</span><span class="sxs-lookup"><span data-stu-id="5b10b-115">Click Save when you are done creating tags.</span></span>

![Defining Content Moderation Tags](images/tags-2-define.png)

## <a name="using-custom-tags"></a><span data-ttu-id="5b10b-117">Using Custom Tags</span><span class="sxs-lookup"><span data-stu-id="5b10b-117">Using Custom Tags</span></span> ##

<span data-ttu-id="5b10b-118">Custom tags are used during human review.</span><span class="sxs-lookup"><span data-stu-id="5b10b-118">Custom tags are used during human review.</span></span> <span data-ttu-id="5b10b-119">They display on the preview, and the reviewer selects it by clicking on it.</span><span class="sxs-lookup"><span data-stu-id="5b10b-119">They display on the preview, and the reviewer selects it by clicking on it.</span></span>

![Using Content Moderation Tags](images/tags-3-use.png)

<span data-ttu-id="5b10b-121">You can turn off different tags for different reviews, by checking or unchecking Is Visible.</span><span class="sxs-lookup"><span data-stu-id="5b10b-121">You can turn off different tags for different reviews, by checking or unchecking Is Visible.</span></span>
 
![Disabling Content Moderation Tags](images/tags-4-disable.png)

<span data-ttu-id="5b10b-123">While you can’t delete the two default tags, isadult and isracy, you can delete any custom tags that you have defined.</span><span class="sxs-lookup"><span data-stu-id="5b10b-123">While you can’t delete the two default tags, isadult and isracy, you can delete any custom tags that you have defined.</span></span> <span data-ttu-id="5b10b-124">Click the garbage can next to the tag you want to delete.</span><span class="sxs-lookup"><span data-stu-id="5b10b-124">Click the garbage can next to the tag you want to delete.</span></span>

![Deleting Content Moderation Tags](images/tags-5-delete.png)

## <a name="next-steps"></a><span data-ttu-id="5b10b-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="5b10b-126">Next steps</span></span> ##

<span data-ttu-id="5b10b-127">To learn how to use tags for image moderation, see [how to review moderated images](Review-Moderated-Images.md).</span><span class="sxs-lookup"><span data-stu-id="5b10b-127">To learn how to use tags for image moderation, see [how to review moderated images](Review-Moderated-Images.md).</span></span>
