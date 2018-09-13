---
title: Similarity method in the Academic Knowledge API | Microsoft Docs
description: Use the Similarity method to calculate the academic similarity of two strings in Microsoft Cognitive Services.
services: cognitive-services
author: alch-msft
manager: kuansanw
ms.service: cognitive-services
ms.technology: academic-knowledge
ms.topic: article
ms.date: 01/18/2017
ms.author: alch
ms.openlocfilehash: 49b715be436fcc44db0c151773fcc3daf0c50163
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540909"
---
# <a name="similarity-method"></a><span data-ttu-id="490eb-103">Similarity Method</span><span class="sxs-lookup"><span data-stu-id="490eb-103">Similarity Method</span></span>

<span data-ttu-id="490eb-104">The **similarity** REST API is used to calculate the academic similarity between two strings.</span><span class="sxs-lookup"><span data-stu-id="490eb-104">The **similarity** REST API is used to calculate the academic similarity between two strings.</span></span> 
<br>

<span data-ttu-id="490eb-105">**REST endpoint:**</span><span class="sxs-lookup"><span data-stu-id="490eb-105">**REST endpoint:**</span></span>
```
https://westus.api.cognitive.microsoft.com/academic/v1.0/similarity?
```

## <a name="request-parameters"></a><span data-ttu-id="490eb-106">Request Parameters</span><span class="sxs-lookup"><span data-stu-id="490eb-106">Request Parameters</span></span>
<span data-ttu-id="490eb-107">Parameter</span><span class="sxs-lookup"><span data-stu-id="490eb-107">Parameter</span></span>        |<span data-ttu-id="490eb-108">Data Type</span><span class="sxs-lookup"><span data-stu-id="490eb-108">Data Type</span></span>      |<span data-ttu-id="490eb-109">Required</span><span class="sxs-lookup"><span data-stu-id="490eb-109">Required</span></span> | <span data-ttu-id="490eb-110">Description</span><span class="sxs-lookup"><span data-stu-id="490eb-110">Description</span></span>
----------|----------|----------|------------
<span data-ttu-id="490eb-111">**s1**</span><span class="sxs-lookup"><span data-stu-id="490eb-111">**s1**</span></span>        |<span data-ttu-id="490eb-112">String</span><span class="sxs-lookup"><span data-stu-id="490eb-112">String</span></span>   |<span data-ttu-id="490eb-113">Yes</span><span class="sxs-lookup"><span data-stu-id="490eb-113">Yes</span></span>  |<span data-ttu-id="490eb-114">String\* to be compared</span><span class="sxs-lookup"><span data-stu-id="490eb-114">String\* to be compared</span></span>
<span data-ttu-id="490eb-115">**s2**</span><span class="sxs-lookup"><span data-stu-id="490eb-115">**s2**</span></span>        |<span data-ttu-id="490eb-116">String</span><span class="sxs-lookup"><span data-stu-id="490eb-116">String</span></span>   |<span data-ttu-id="490eb-117">Yes</span><span class="sxs-lookup"><span data-stu-id="490eb-117">Yes</span></span>  |<span data-ttu-id="490eb-118">String\* to be compared</span><span class="sxs-lookup"><span data-stu-id="490eb-118">String\* to be compared</span></span>
<span data-ttu-id="490eb-119"><sub> \*Strings to compare have a maxium length of 1MB. </sub></span><span class="sxs-lookup"><span data-stu-id="490eb-119"><sub> \*Strings to compare have a maxium length of 1MB. </sub></span></span>
<br>
## <a name="response"></a><span data-ttu-id="490eb-120">Response</span><span class="sxs-lookup"><span data-stu-id="490eb-120">Response</span></span>
<span data-ttu-id="490eb-121">Name</span><span class="sxs-lookup"><span data-stu-id="490eb-121">Name</span></span> | <span data-ttu-id="490eb-122">Description</span><span class="sxs-lookup"><span data-stu-id="490eb-122">Description</span></span>
--------|---------
<span data-ttu-id="490eb-123">**SimilarityScore**</span><span class="sxs-lookup"><span data-stu-id="490eb-123">**SimilarityScore**</span></span>        |<span data-ttu-id="490eb-124">A floating point value representing the cosine similarity of s1 and s2, with values closer to 1.0 meaning more similar and values closer to -1.0 meaning less</span><span class="sxs-lookup"><span data-stu-id="490eb-124">A floating point value representing the cosine similarity of s1 and s2, with values closer to 1.0 meaning more similar and values closer to -1.0 meaning less</span></span>
<br>

## <a name="successerror-conditions"></a><span data-ttu-id="490eb-125">Success/Error Conditions</span><span class="sxs-lookup"><span data-stu-id="490eb-125">Success/Error Conditions</span></span>
<span data-ttu-id="490eb-126">HTTP Status</span><span class="sxs-lookup"><span data-stu-id="490eb-126">HTTP Status</span></span> | <span data-ttu-id="490eb-127">Reason</span><span class="sxs-lookup"><span data-stu-id="490eb-127">Reason</span></span> | <span data-ttu-id="490eb-128">Response</span><span class="sxs-lookup"><span data-stu-id="490eb-128">Response</span></span>
-----------|----------|--------
<span data-ttu-id="490eb-129">**200**</span><span class="sxs-lookup"><span data-stu-id="490eb-129">**200**</span></span>         |<span data-ttu-id="490eb-130">Success</span><span class="sxs-lookup"><span data-stu-id="490eb-130">Success</span></span> | <span data-ttu-id="490eb-131">Floating point number</span><span class="sxs-lookup"><span data-stu-id="490eb-131">Floating point number</span></span>
<span data-ttu-id="490eb-132">**400**</span><span class="sxs-lookup"><span data-stu-id="490eb-132">**400**</span></span>         | <span data-ttu-id="490eb-133">Bad request or request invalid</span><span class="sxs-lookup"><span data-stu-id="490eb-133">Bad request or request invalid</span></span> | <span data-ttu-id="490eb-134">Error message</span><span class="sxs-lookup"><span data-stu-id="490eb-134">Error message</span></span>      
<span data-ttu-id="490eb-135">**500**</span><span class="sxs-lookup"><span data-stu-id="490eb-135">**500**</span></span>         |<span data-ttu-id="490eb-136">Internal server error</span><span class="sxs-lookup"><span data-stu-id="490eb-136">Internal server error</span></span> | <span data-ttu-id="490eb-137">Error message</span><span class="sxs-lookup"><span data-stu-id="490eb-137">Error message</span></span>
<span data-ttu-id="490eb-138">**Timed out**</span><span class="sxs-lookup"><span data-stu-id="490eb-138">**Timed out**</span></span>     | <span data-ttu-id="490eb-139">Request timed out.</span><span class="sxs-lookup"><span data-stu-id="490eb-139">Request timed out.</span></span>  | <span data-ttu-id="490eb-140">Error message</span><span class="sxs-lookup"><span data-stu-id="490eb-140">Error message</span></span>
<br>
##<a name="example-calculate-similarity-of-two-partial-abstracts"></a><span data-ttu-id="490eb-141">Example: Calculate similarity of two partial abstracts</span><span class="sxs-lookup"><span data-stu-id="490eb-141">Example: Calculate similarity of two partial abstracts</span></span>
####<a name="request"></a><span data-ttu-id="490eb-142">Request:</span><span class="sxs-lookup"><span data-stu-id="490eb-142">Request:</span></span>
```
https://westus.api.cognitive.microsoft.com/academic/v1.0/similarity?s1=Using complementary priors, we derive a fast greedy algorithm that can learn deep directed belief networks one layer at a time, provided the top two layers form an undirected associative memory
&s2=Deepneural nets with a large number of parameters are very powerful machine learning systems. However, overfitting is a serious problem in such networks
```
<span data-ttu-id="490eb-143">In this example, we generate the similarity score between two partial abstracts using the **similarity** API.</span><span class="sxs-lookup"><span data-stu-id="490eb-143">In this example, we generate the similarity score between two partial abstracts using the **similarity** API.</span></span>
####<a name="response"></a><span data-ttu-id="490eb-144">Response:</span><span class="sxs-lookup"><span data-stu-id="490eb-144">Response:</span></span>
```
0.520
```
####<a name="remarks"></a><span data-ttu-id="490eb-145">Remarks:</span><span class="sxs-lookup"><span data-stu-id="490eb-145">Remarks:</span></span>
<span data-ttu-id="490eb-146">The similarity score is determined by assessing the academic concepts through word embedding.</span><span class="sxs-lookup"><span data-stu-id="490eb-146">The similarity score is determined by assessing the academic concepts through word embedding.</span></span> <span data-ttu-id="490eb-147">In this example, 0.52 means that the two partial abstracts are somewhat similar.</span><span class="sxs-lookup"><span data-stu-id="490eb-147">In this example, 0.52 means that the two partial abstracts are somewhat similar.</span></span>
<br>