---
title: Author entity attributes in the Academic Knowledge API | Microsoft Docs
description: Learn the attributes you can use with the Author entity in the Academic Knowledge API in Cognitive Services.
services: cognitive-services
author: alch-msft
manager: kuansanw
ms.service: cognitive-services
ms.technology: academic-knowledge
ms.topic: article
ms.date: 03/23/2017
ms.author: alch
ms.openlocfilehash: cf7a0bd3f1ece12ee2b00d32ae80e5b4c82f6bcf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563010"
---
# <a name="author-entity"></a><span data-ttu-id="63246-103">Author Entity</span><span class="sxs-lookup"><span data-stu-id="63246-103">Author Entity</span></span>
<span data-ttu-id="63246-104"><sub> \*Below attributes are specific to author entity. (Ty = '1') </sub></span><span class="sxs-lookup"><span data-stu-id="63246-104"><sub> \*Below attributes are specific to author entity. (Ty = '1') </sub></span></span>

<span data-ttu-id="63246-105">Name</span><span class="sxs-lookup"><span data-stu-id="63246-105">Name</span></span>    |<span data-ttu-id="63246-106">Description</span><span class="sxs-lookup"><span data-stu-id="63246-106">Description</span></span>                            |<span data-ttu-id="63246-107">Type</span><span class="sxs-lookup"><span data-stu-id="63246-107">Type</span></span>       | <span data-ttu-id="63246-108">Operations</span><span class="sxs-lookup"><span data-stu-id="63246-108">Operations</span></span>
------- | ------------------------------------- | --------- | ----------------------------
<span data-ttu-id="63246-109">Id</span><span class="sxs-lookup"><span data-stu-id="63246-109">Id</span></span>      |<span data-ttu-id="63246-110">Entity ID</span><span class="sxs-lookup"><span data-stu-id="63246-110">Entity ID</span></span>                              |<span data-ttu-id="63246-111">Int64</span><span class="sxs-lookup"><span data-stu-id="63246-111">Int64</span></span>      |<span data-ttu-id="63246-112">Equals</span><span class="sxs-lookup"><span data-stu-id="63246-112">Equals</span></span>
<span data-ttu-id="63246-113">AuN</span><span class="sxs-lookup"><span data-stu-id="63246-113">AuN</span></span>     |<span data-ttu-id="63246-114">Author normalized name</span><span class="sxs-lookup"><span data-stu-id="63246-114">Author normalized name</span></span>                 |<span data-ttu-id="63246-115">String</span><span class="sxs-lookup"><span data-stu-id="63246-115">String</span></span>     |<span data-ttu-id="63246-116">Equals</span><span class="sxs-lookup"><span data-stu-id="63246-116">Equals</span></span>
<span data-ttu-id="63246-117">DAuN</span><span class="sxs-lookup"><span data-stu-id="63246-117">DAuN</span></span>    |<span data-ttu-id="63246-118">Author display name</span><span class="sxs-lookup"><span data-stu-id="63246-118">Author display name</span></span>                    |<span data-ttu-id="63246-119">String</span><span class="sxs-lookup"><span data-stu-id="63246-119">String</span></span>     |<span data-ttu-id="63246-120">none</span><span class="sxs-lookup"><span data-stu-id="63246-120">none</span></span>
<span data-ttu-id="63246-121">CC</span><span class="sxs-lookup"><span data-stu-id="63246-121">CC</span></span>      |<span data-ttu-id="63246-122">Author total citation count</span><span class="sxs-lookup"><span data-stu-id="63246-122">Author total citation count</span></span>            |<span data-ttu-id="63246-123">Int32</span><span class="sxs-lookup"><span data-stu-id="63246-123">Int32</span></span>      |<span data-ttu-id="63246-124">none</span><span class="sxs-lookup"><span data-stu-id="63246-124">none</span></span>  
<span data-ttu-id="63246-125">ECC</span><span class="sxs-lookup"><span data-stu-id="63246-125">ECC</span></span>     |<span data-ttu-id="63246-126">Author total estimated citation count</span><span class="sxs-lookup"><span data-stu-id="63246-126">Author total estimated citation count</span></span>  |<span data-ttu-id="63246-127">Int32</span><span class="sxs-lookup"><span data-stu-id="63246-127">Int32</span></span>      |<span data-ttu-id="63246-128">none</span><span class="sxs-lookup"><span data-stu-id="63246-128">none</span></span>
<span data-ttu-id="63246-129">E</span><span class="sxs-lookup"><span data-stu-id="63246-129">E</span></span>       |<span data-ttu-id="63246-130">Extended metadata (see table below)</span><span class="sxs-lookup"><span data-stu-id="63246-130">Extended metadata (see table below)</span></span>    |<span data-ttu-id="63246-131">String</span><span class="sxs-lookup"><span data-stu-id="63246-131">String</span></span>     |<span data-ttu-id="63246-132">none</span><span class="sxs-lookup"><span data-stu-id="63246-132">none</span></span>  
<span data-ttu-id="63246-133">SSD</span><span class="sxs-lookup"><span data-stu-id="63246-133">SSD</span></span>     |<span data-ttu-id="63246-134">Satori data</span><span class="sxs-lookup"><span data-stu-id="63246-134">Satori data</span></span>                            |<span data-ttu-id="63246-135">String</span><span class="sxs-lookup"><span data-stu-id="63246-135">String</span></span>     |<span data-ttu-id="63246-136">none</span><span class="sxs-lookup"><span data-stu-id="63246-136">none</span></span>

## <a name="extended-metadata-attributes"></a><span data-ttu-id="63246-137">Extended Metadata Attributes</span><span class="sxs-lookup"><span data-stu-id="63246-137">Extended Metadata Attributes</span></span> ##

<span data-ttu-id="63246-138">Name</span><span class="sxs-lookup"><span data-stu-id="63246-138">Name</span></span>    | <span data-ttu-id="63246-139">Description</span><span class="sxs-lookup"><span data-stu-id="63246-139">Description</span></span>               
--------|---------------------------    
<span data-ttu-id="63246-140">LKA.Afn</span><span class="sxs-lookup"><span data-stu-id="63246-140">LKA.Afn</span></span>     | <span data-ttu-id="63246-141">affiliation's display name associated with the author</span><span class="sxs-lookup"><span data-stu-id="63246-141">affiliation's display name associated with the author</span></span>  
<span data-ttu-id="63246-142">LKA.AfId</span><span class="sxs-lookup"><span data-stu-id="63246-142">LKA.AfId</span></span>        | <span data-ttu-id="63246-143">affiliation's entity ID associated with the author</span><span class="sxs-lookup"><span data-stu-id="63246-143">affiliation's entity ID associated with the author</span></span>