---
title: Author entity attributes in the Academic Knowledge API | Microsoft Docs
description: Learn the attributes you can use with the Author entity in the Academic Knowledge API in Cognitive Services.
services: cognitive-services
author: alch-msft
manager: kuansanw
ms.service: cognitive-services
ms.component: academic-knowledge
ms.topic: article
ms.date: 03/23/2017
ms.author: alch
ms.openlocfilehash: afcc3257c49522a4631c4aae0e0c2b88373f9af1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44782462"
---
# <a name="author-entity"></a><span data-ttu-id="59e04-103">Author Entity</span><span class="sxs-lookup"><span data-stu-id="59e04-103">Author Entity</span></span>
<span data-ttu-id="59e04-104"><sub> \*Following attributes are specific to author entity. (Ty = '1') </sub></span><span class="sxs-lookup"><span data-stu-id="59e04-104"><sub> \*Following attributes are specific to author entity. (Ty = '1') </sub></span></span>

<span data-ttu-id="59e04-105">Name</span><span class="sxs-lookup"><span data-stu-id="59e04-105">Name</span></span>    |<span data-ttu-id="59e04-106">Description</span><span class="sxs-lookup"><span data-stu-id="59e04-106">Description</span></span>                            |<span data-ttu-id="59e04-107">Type</span><span class="sxs-lookup"><span data-stu-id="59e04-107">Type</span></span>       | <span data-ttu-id="59e04-108">Operations</span><span class="sxs-lookup"><span data-stu-id="59e04-108">Operations</span></span>
------- | ------------------------------------- | --------- | ----------------------------
<span data-ttu-id="59e04-109">Id</span><span class="sxs-lookup"><span data-stu-id="59e04-109">Id</span></span>      |<span data-ttu-id="59e04-110">Entity ID</span><span class="sxs-lookup"><span data-stu-id="59e04-110">Entity ID</span></span>                              |<span data-ttu-id="59e04-111">Int64</span><span class="sxs-lookup"><span data-stu-id="59e04-111">Int64</span></span>      |<span data-ttu-id="59e04-112">Equals</span><span class="sxs-lookup"><span data-stu-id="59e04-112">Equals</span></span>
<span data-ttu-id="59e04-113">AuN</span><span class="sxs-lookup"><span data-stu-id="59e04-113">AuN</span></span>     |<span data-ttu-id="59e04-114">Author normalized name</span><span class="sxs-lookup"><span data-stu-id="59e04-114">Author normalized name</span></span>                 |<span data-ttu-id="59e04-115">String</span><span class="sxs-lookup"><span data-stu-id="59e04-115">String</span></span>     |<span data-ttu-id="59e04-116">Equals</span><span class="sxs-lookup"><span data-stu-id="59e04-116">Equals</span></span>
<span data-ttu-id="59e04-117">DAuN</span><span class="sxs-lookup"><span data-stu-id="59e04-117">DAuN</span></span>    |<span data-ttu-id="59e04-118">Author display name</span><span class="sxs-lookup"><span data-stu-id="59e04-118">Author display name</span></span>                    |<span data-ttu-id="59e04-119">String</span><span class="sxs-lookup"><span data-stu-id="59e04-119">String</span></span>     |<span data-ttu-id="59e04-120">none</span><span class="sxs-lookup"><span data-stu-id="59e04-120">none</span></span>
<span data-ttu-id="59e04-121">CC</span><span class="sxs-lookup"><span data-stu-id="59e04-121">CC</span></span>      |<span data-ttu-id="59e04-122">Author total citation count</span><span class="sxs-lookup"><span data-stu-id="59e04-122">Author total citation count</span></span>            |<span data-ttu-id="59e04-123">Int32</span><span class="sxs-lookup"><span data-stu-id="59e04-123">Int32</span></span>      |<span data-ttu-id="59e04-124">none</span><span class="sxs-lookup"><span data-stu-id="59e04-124">none</span></span>  
<span data-ttu-id="59e04-125">ECC</span><span class="sxs-lookup"><span data-stu-id="59e04-125">ECC</span></span>     |<span data-ttu-id="59e04-126">Author total estimated citation count</span><span class="sxs-lookup"><span data-stu-id="59e04-126">Author total estimated citation count</span></span>  |<span data-ttu-id="59e04-127">Int32</span><span class="sxs-lookup"><span data-stu-id="59e04-127">Int32</span></span>      |<span data-ttu-id="59e04-128">none</span><span class="sxs-lookup"><span data-stu-id="59e04-128">none</span></span>
<span data-ttu-id="59e04-129">E</span><span class="sxs-lookup"><span data-stu-id="59e04-129">E</span></span>       |<span data-ttu-id="59e04-130">Extended metadata (see "Extended Meta Attributes" table )</span><span class="sxs-lookup"><span data-stu-id="59e04-130">Extended metadata (see "Extended Meta Attributes" table )</span></span>  |<span data-ttu-id="59e04-131">String</span><span class="sxs-lookup"><span data-stu-id="59e04-131">String</span></span>     |<span data-ttu-id="59e04-132">none</span><span class="sxs-lookup"><span data-stu-id="59e04-132">none</span></span>  


## <a name="extended-metadata-attributes"></a><span data-ttu-id="59e04-133">Extended Metadata Attributes</span><span class="sxs-lookup"><span data-stu-id="59e04-133">Extended Metadata Attributes</span></span> ##

<span data-ttu-id="59e04-134">Name</span><span class="sxs-lookup"><span data-stu-id="59e04-134">Name</span></span>    | <span data-ttu-id="59e04-135">Description</span><span class="sxs-lookup"><span data-stu-id="59e04-135">Description</span></span>               
--------|---------------------------    
<span data-ttu-id="59e04-136">LKA.Afn</span><span class="sxs-lookup"><span data-stu-id="59e04-136">LKA.Afn</span></span>     | <span data-ttu-id="59e04-137">affiliation's display name associated with the author</span><span class="sxs-lookup"><span data-stu-id="59e04-137">affiliation's display name associated with the author</span></span>  
<span data-ttu-id="59e04-138">LKA.AfId</span><span class="sxs-lookup"><span data-stu-id="59e04-138">LKA.AfId</span></span>        | <span data-ttu-id="59e04-139">affiliation's entity ID associated with the author</span><span class="sxs-lookup"><span data-stu-id="59e04-139">affiliation's entity ID associated with the author</span></span>