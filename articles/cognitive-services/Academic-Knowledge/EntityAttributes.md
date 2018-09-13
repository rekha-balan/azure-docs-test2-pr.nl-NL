---
title: Academic Graph entity attributes for the Academic Knowledge API | Microsoft Docs
description: Learn about the entity attributes you can use with the Academic Graph in the Academic Knowledge API.
services: cognitive-services
author: alch-msft
manager: kuansanw
ms.service: cognitive-services
ms.technology: academic-knowledge
ms.topic: article
ms.date: 03/27/2017
ms.author: alch
ms.openlocfilehash: 9240dda95ce06d9f31340afe9ae8fc48593f211c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552491"
---
# <a name="entity-attributes"></a><span data-ttu-id="44a97-103">Entity Attributes</span><span class="sxs-lookup"><span data-stu-id="44a97-103">Entity Attributes</span></span>

<span data-ttu-id="44a97-104">The academic graph is composed of 7 types of entity.</span><span class="sxs-lookup"><span data-stu-id="44a97-104">The academic graph is composed of 7 types of entity.</span></span> <span data-ttu-id="44a97-105">All entities will have a Entity ID and a Entity type.</span><span class="sxs-lookup"><span data-stu-id="44a97-105">All entities will have a Entity ID and a Entity type.</span></span>

## <a name="common-entity-attributes"></a><span data-ttu-id="44a97-106">Common Entity Attributes</span><span class="sxs-lookup"><span data-stu-id="44a97-106">Common Entity Attributes</span></span>
<span data-ttu-id="44a97-107">Name</span><span class="sxs-lookup"><span data-stu-id="44a97-107">Name</span></span>    |<span data-ttu-id="44a97-108">Description</span><span class="sxs-lookup"><span data-stu-id="44a97-108">Description</span></span>                |<span data-ttu-id="44a97-109">Type</span><span class="sxs-lookup"><span data-stu-id="44a97-109">Type</span></span>       | <span data-ttu-id="44a97-110">Operations</span><span class="sxs-lookup"><span data-stu-id="44a97-110">Operations</span></span>
------- | ------------------------- | --------- | ----------------------------
<span data-ttu-id="44a97-111">Id</span><span class="sxs-lookup"><span data-stu-id="44a97-111">Id</span></span>      |<span data-ttu-id="44a97-112">Entity ID</span><span class="sxs-lookup"><span data-stu-id="44a97-112">Entity ID</span></span>                  |<span data-ttu-id="44a97-113">Int64</span><span class="sxs-lookup"><span data-stu-id="44a97-113">Int64</span></span>      |<span data-ttu-id="44a97-114">Equals</span><span class="sxs-lookup"><span data-stu-id="44a97-114">Equals</span></span>
<span data-ttu-id="44a97-115">Ty</span><span class="sxs-lookup"><span data-stu-id="44a97-115">Ty</span></span>      |<span data-ttu-id="44a97-116">Entity type</span><span class="sxs-lookup"><span data-stu-id="44a97-116">Entity type</span></span>                |<span data-ttu-id="44a97-117">enum</span><span class="sxs-lookup"><span data-stu-id="44a97-117">enum</span></span>   |<span data-ttu-id="44a97-118">Equals</span><span class="sxs-lookup"><span data-stu-id="44a97-118">Equals</span></span>

## <a name="entity-type-enum"></a><span data-ttu-id="44a97-119">Entity type enum</span><span class="sxs-lookup"><span data-stu-id="44a97-119">Entity type enum</span></span>
<span data-ttu-id="44a97-120">Name</span><span class="sxs-lookup"><span data-stu-id="44a97-120">Name</span></span>                                                            |<span data-ttu-id="44a97-121">value</span><span class="sxs-lookup"><span data-stu-id="44a97-121">value</span></span>
----------------------------------------------------------------|-----
[<span data-ttu-id="44a97-122">Paper</span><span class="sxs-lookup"><span data-stu-id="44a97-122">Paper</span></span>](PaperEntityAttributes.md)                               |<span data-ttu-id="44a97-123">0</span><span class="sxs-lookup"><span data-stu-id="44a97-123">0</span></span>
[<span data-ttu-id="44a97-124">Author</span><span class="sxs-lookup"><span data-stu-id="44a97-124">Author</span></span>](AuthorEntityAttributes.md)                             |<span data-ttu-id="44a97-125">1</span><span class="sxs-lookup"><span data-stu-id="44a97-125">1</span></span>
[<span data-ttu-id="44a97-126">Journal</span><span class="sxs-lookup"><span data-stu-id="44a97-126">Journal</span></span>](JournalEntityAttributes.md)                           |<span data-ttu-id="44a97-127">2</span><span class="sxs-lookup"><span data-stu-id="44a97-127">2</span></span>
[<span data-ttu-id="44a97-128">Conference Series</span><span class="sxs-lookup"><span data-stu-id="44a97-128">Conference Series</span></span>](JournalEntityAttributes.md)                 |<span data-ttu-id="44a97-129">3</span><span class="sxs-lookup"><span data-stu-id="44a97-129">3</span></span>
[<span data-ttu-id="44a97-130">Conference Instance</span><span class="sxs-lookup"><span data-stu-id="44a97-130">Conference Instance</span></span>](ConferenceInstanceEntityAttributes.md)    |<span data-ttu-id="44a97-131">4</span><span class="sxs-lookup"><span data-stu-id="44a97-131">4</span></span>
[<span data-ttu-id="44a97-132">Affiliation</span><span class="sxs-lookup"><span data-stu-id="44a97-132">Affiliation</span></span>](AffiliationEntityAttributes.md)                   |<span data-ttu-id="44a97-133">5</span><span class="sxs-lookup"><span data-stu-id="44a97-133">5</span></span>
[<span data-ttu-id="44a97-134">Field Of Study</span><span class="sxs-lookup"><span data-stu-id="44a97-134">Field Of Study</span></span>](FieldsOfStudyEntityAttributes.md)                      |<span data-ttu-id="44a97-135">6</span><span class="sxs-lookup"><span data-stu-id="44a97-135">6</span></span>

