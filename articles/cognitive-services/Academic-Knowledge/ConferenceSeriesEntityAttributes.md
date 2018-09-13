---
title: Conference Series entity attributes in the Academic Knowledge API | Microsoft Docs
description: Learn about the attributes you can use with the Conference Series entity in Cognitive Services.
services: cognitive-services
author: alch-msft
manager: kuansanw
ms.service: cognitive-services
ms.technology: academic-knowledge
ms.topic: article
ms.date: 03/23/2017
ms.author: alch
ms.openlocfilehash: 58d63c6a93c011d9a1460f25f8cb85f8b5f1c05b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671152"
---
# <a name="conference-series-entity"></a><span data-ttu-id="25bcd-103">Conference Series Entity</span><span class="sxs-lookup"><span data-stu-id="25bcd-103">Conference Series Entity</span></span>

<span data-ttu-id="25bcd-104"><sub> \*Below attributes are specific to conference series entity. (Ty = '3') </sub></span><span class="sxs-lookup"><span data-stu-id="25bcd-104"><sub> \*Below attributes are specific to conference series entity. (Ty = '3') </sub></span></span>

<span data-ttu-id="25bcd-105">Name</span><span class="sxs-lookup"><span data-stu-id="25bcd-105">Name</span></span>    |<span data-ttu-id="25bcd-106">Description</span><span class="sxs-lookup"><span data-stu-id="25bcd-106">Description</span></span>                            |<span data-ttu-id="25bcd-107">Type</span><span class="sxs-lookup"><span data-stu-id="25bcd-107">Type</span></span>       | <span data-ttu-id="25bcd-108">Operations</span><span class="sxs-lookup"><span data-stu-id="25bcd-108">Operations</span></span>
------- | ------------------------------------- | --------- | ----------------------------
<span data-ttu-id="25bcd-109">Id</span><span class="sxs-lookup"><span data-stu-id="25bcd-109">Id</span></span>      |<span data-ttu-id="25bcd-110">Entity ID</span><span class="sxs-lookup"><span data-stu-id="25bcd-110">Entity ID</span></span>                              |<span data-ttu-id="25bcd-111">Int64</span><span class="sxs-lookup"><span data-stu-id="25bcd-111">Int64</span></span>      |<span data-ttu-id="25bcd-112">Equals</span><span class="sxs-lookup"><span data-stu-id="25bcd-112">Equals</span></span>
<span data-ttu-id="25bcd-113">CN</span><span class="sxs-lookup"><span data-stu-id="25bcd-113">CN</span></span>      |<span data-ttu-id="25bcd-114">Conference series normalized name</span><span class="sxs-lookup"><span data-stu-id="25bcd-114">Conference series normalized name</span></span>      |<span data-ttu-id="25bcd-115">String</span><span class="sxs-lookup"><span data-stu-id="25bcd-115">String</span></span>     |<span data-ttu-id="25bcd-116">Equals</span><span class="sxs-lookup"><span data-stu-id="25bcd-116">Equals</span></span>
<span data-ttu-id="25bcd-117">DCN</span><span class="sxs-lookup"><span data-stu-id="25bcd-117">DCN</span></span>     |<span data-ttu-id="25bcd-118">Conference series display name</span><span class="sxs-lookup"><span data-stu-id="25bcd-118">Conference series display name</span></span>         |<span data-ttu-id="25bcd-119">String</span><span class="sxs-lookup"><span data-stu-id="25bcd-119">String</span></span>     |<span data-ttu-id="25bcd-120">none</span><span class="sxs-lookup"><span data-stu-id="25bcd-120">none</span></span>
<span data-ttu-id="25bcd-121">CC</span><span class="sxs-lookup"><span data-stu-id="25bcd-121">CC</span></span>      |<span data-ttu-id="25bcd-122">Conference series total citation count</span><span class="sxs-lookup"><span data-stu-id="25bcd-122">Conference series total citation count</span></span>         |<span data-ttu-id="25bcd-123">Int32</span><span class="sxs-lookup"><span data-stu-id="25bcd-123">Int32</span></span>      |<span data-ttu-id="25bcd-124">none</span><span class="sxs-lookup"><span data-stu-id="25bcd-124">none</span></span>  
<span data-ttu-id="25bcd-125">ECC</span><span class="sxs-lookup"><span data-stu-id="25bcd-125">ECC</span></span>     |<span data-ttu-id="25bcd-126">Conference series total estimated citation count</span><span class="sxs-lookup"><span data-stu-id="25bcd-126">Conference series total estimated citation count</span></span>   |<span data-ttu-id="25bcd-127">Int32</span><span class="sxs-lookup"><span data-stu-id="25bcd-127">Int32</span></span>      |<span data-ttu-id="25bcd-128">none</span><span class="sxs-lookup"><span data-stu-id="25bcd-128">none</span></span>
<span data-ttu-id="25bcd-129">F.FId</span><span class="sxs-lookup"><span data-stu-id="25bcd-129">F.FId</span></span>   |<span data-ttu-id="25bcd-130">Field of study entity ID associated with the conference series</span><span class="sxs-lookup"><span data-stu-id="25bcd-130">Field of study entity ID associated with the conference series</span></span> |<span data-ttu-id="25bcd-131">Int64</span><span class="sxs-lookup"><span data-stu-id="25bcd-131">Int64</span></span>  | <span data-ttu-id="25bcd-132">Equals</span><span class="sxs-lookup"><span data-stu-id="25bcd-132">Equals</span></span>
<span data-ttu-id="25bcd-133">F.FN</span><span class="sxs-lookup"><span data-stu-id="25bcd-133">F.FN</span></span>    |<span data-ttu-id="25bcd-134">Field of study name associated with the conference series</span><span class="sxs-lookup"><span data-stu-id="25bcd-134">Field of study name associated with the conference series</span></span>  | <span data-ttu-id="25bcd-135">Equals,</span><span class="sxs-lookup"><span data-stu-id="25bcd-135">Equals,</span></span><br/><span data-ttu-id="25bcd-136">StartsWith</span><span class="sxs-lookup"><span data-stu-id="25bcd-136">StartsWith</span></span>
<span data-ttu-id="25bcd-137">SSD</span><span class="sxs-lookup"><span data-stu-id="25bcd-137">SSD</span></span>     |<span data-ttu-id="25bcd-138">Satori data</span><span class="sxs-lookup"><span data-stu-id="25bcd-138">Satori data</span></span>                            |<span data-ttu-id="25bcd-139">String</span><span class="sxs-lookup"><span data-stu-id="25bcd-139">String</span></span>     |<span data-ttu-id="25bcd-140">none</span><span class="sxs-lookup"><span data-stu-id="25bcd-140">none</span></span>
