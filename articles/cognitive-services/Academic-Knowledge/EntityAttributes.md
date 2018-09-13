---
title: Academic Graph entity attributes for the Academic Knowledge API | Microsoft Docs
description: Learn about the entity attributes you can use with the Academic Graph in the Academic Knowledge API.
services: cognitive-services
author: alch-msft
manager: kuansanw
ms.service: cognitive-services
ms.component: academic-knowledge
ms.topic: article
ms.date: 03/27/2017
ms.author: alch
ms.openlocfilehash: f771969c3c6f05e5d2c99b1fbf593ae039ccb12c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44818355"
---
# <a name="entity-attributes"></a><span data-ttu-id="358d7-103">Entity Attributes</span><span class="sxs-lookup"><span data-stu-id="358d7-103">Entity Attributes</span></span>

<span data-ttu-id="358d7-104">The academic graph is composed of 7 types of entity.</span><span class="sxs-lookup"><span data-stu-id="358d7-104">The academic graph is composed of 7 types of entity.</span></span> <span data-ttu-id="358d7-105">All entities will have a Entity ID and a Entity type.</span><span class="sxs-lookup"><span data-stu-id="358d7-105">All entities will have a Entity ID and a Entity type.</span></span>

## <a name="common-entity-attributes"></a><span data-ttu-id="358d7-106">Common Entity Attributes</span><span class="sxs-lookup"><span data-stu-id="358d7-106">Common Entity Attributes</span></span>
<span data-ttu-id="358d7-107">Name</span><span class="sxs-lookup"><span data-stu-id="358d7-107">Name</span></span>    |<span data-ttu-id="358d7-108">Description</span><span class="sxs-lookup"><span data-stu-id="358d7-108">Description</span></span>                |<span data-ttu-id="358d7-109">Type</span><span class="sxs-lookup"><span data-stu-id="358d7-109">Type</span></span>       | <span data-ttu-id="358d7-110">Operations</span><span class="sxs-lookup"><span data-stu-id="358d7-110">Operations</span></span>
------- | ------------------------- | --------- | ----------------------------
<span data-ttu-id="358d7-111">Id</span><span class="sxs-lookup"><span data-stu-id="358d7-111">Id</span></span>      |<span data-ttu-id="358d7-112">Entity ID</span><span class="sxs-lookup"><span data-stu-id="358d7-112">Entity ID</span></span>                  |<span data-ttu-id="358d7-113">Int64</span><span class="sxs-lookup"><span data-stu-id="358d7-113">Int64</span></span>      |<span data-ttu-id="358d7-114">Equals</span><span class="sxs-lookup"><span data-stu-id="358d7-114">Equals</span></span>
<span data-ttu-id="358d7-115">Ty</span><span class="sxs-lookup"><span data-stu-id="358d7-115">Ty</span></span>      |<span data-ttu-id="358d7-116">Entity type</span><span class="sxs-lookup"><span data-stu-id="358d7-116">Entity type</span></span>                |<span data-ttu-id="358d7-117">enum</span><span class="sxs-lookup"><span data-stu-id="358d7-117">enum</span></span>   |<span data-ttu-id="358d7-118">Equals</span><span class="sxs-lookup"><span data-stu-id="358d7-118">Equals</span></span>

## <a name="entity-type-enum"></a><span data-ttu-id="358d7-119">Entity type enum</span><span class="sxs-lookup"><span data-stu-id="358d7-119">Entity type enum</span></span>
<span data-ttu-id="358d7-120">Name</span><span class="sxs-lookup"><span data-stu-id="358d7-120">Name</span></span>                                                            |<span data-ttu-id="358d7-121">value</span><span class="sxs-lookup"><span data-stu-id="358d7-121">value</span></span>
----------------------------------------------------------------|-----
[<span data-ttu-id="358d7-122">Paper</span><span class="sxs-lookup"><span data-stu-id="358d7-122">Paper</span></span>](PaperEntityAttributes.md)                               |<span data-ttu-id="358d7-123">0</span><span class="sxs-lookup"><span data-stu-id="358d7-123">0</span></span>
[<span data-ttu-id="358d7-124">Author</span><span class="sxs-lookup"><span data-stu-id="358d7-124">Author</span></span>](AuthorEntityAttributes.md)                             |<span data-ttu-id="358d7-125">1</span><span class="sxs-lookup"><span data-stu-id="358d7-125">1</span></span>
[<span data-ttu-id="358d7-126">Journal</span><span class="sxs-lookup"><span data-stu-id="358d7-126">Journal</span></span>](JournalEntityAttributes.md)                           |<span data-ttu-id="358d7-127">2</span><span class="sxs-lookup"><span data-stu-id="358d7-127">2</span></span>
[<span data-ttu-id="358d7-128">Conference Series</span><span class="sxs-lookup"><span data-stu-id="358d7-128">Conference Series</span></span>](JournalEntityAttributes.md)                 |<span data-ttu-id="358d7-129">3</span><span class="sxs-lookup"><span data-stu-id="358d7-129">3</span></span>
[<span data-ttu-id="358d7-130">Conference Instance</span><span class="sxs-lookup"><span data-stu-id="358d7-130">Conference Instance</span></span>](ConferenceInstanceEntityAttributes.md)    |<span data-ttu-id="358d7-131">4</span><span class="sxs-lookup"><span data-stu-id="358d7-131">4</span></span>
[<span data-ttu-id="358d7-132">Affiliation</span><span class="sxs-lookup"><span data-stu-id="358d7-132">Affiliation</span></span>](AffiliationEntityAttributes.md)                   |<span data-ttu-id="358d7-133">5</span><span class="sxs-lookup"><span data-stu-id="358d7-133">5</span></span>
[<span data-ttu-id="358d7-134">Field Of Study</span><span class="sxs-lookup"><span data-stu-id="358d7-134">Field Of Study</span></span>](FieldsOfStudyEntityAttributes.md)                      |<span data-ttu-id="358d7-135">6</span><span class="sxs-lookup"><span data-stu-id="358d7-135">6</span></span>

