---
title: QnA Maker Limits - Azure Cognitive Services | Microsoft Docs
description: QnA Maker Limits
services: cognitive-services
author: nstulasi
manager: sangitap
ms.service: cognitive-services
ms.component: QnAMaker
ms.topic: article
ms.date: 05/07/2018
ms.author: saneppal
ms.openlocfilehash: 93471faab9aac94616c770cbee21fb0364f73639
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868466"
---
# <a name="qna-maker-limits"></a><span data-ttu-id="14e02-103">QnA Maker Limits</span><span class="sxs-lookup"><span data-stu-id="14e02-103">QnA Maker Limits</span></span>
<span data-ttu-id="14e02-104">Comprehensive list of limits across QnA Maker.</span><span class="sxs-lookup"><span data-stu-id="14e02-104">Comprehensive list of limits across QnA Maker.</span></span>

## <a name="knowledge-bases"></a><span data-ttu-id="14e02-105">Knowledge Bases</span><span class="sxs-lookup"><span data-stu-id="14e02-105">Knowledge Bases</span></span>

* <span data-ttu-id="14e02-106">Maximum number of knowledge bases based on [Azure Search tier limits](https://docs.microsoft.com/en-us/azure/search/search-limits-quotas-capacity)</span><span class="sxs-lookup"><span data-stu-id="14e02-106">Maximum number of knowledge bases based on [Azure Search tier limits](https://docs.microsoft.com/en-us/azure/search/search-limits-quotas-capacity)</span></span>

|<span data-ttu-id="14e02-107">**Azure Search tier**</span><span class="sxs-lookup"><span data-stu-id="14e02-107">**Azure Search tier**</span></span> | <span data-ttu-id="14e02-108">**Free**</span><span class="sxs-lookup"><span data-stu-id="14e02-108">**Free**</span></span> | <span data-ttu-id="14e02-109">**Basic**</span><span class="sxs-lookup"><span data-stu-id="14e02-109">**Basic**</span></span> |<span data-ttu-id="14e02-110">**S1**</span><span class="sxs-lookup"><span data-stu-id="14e02-110">**S1**</span></span> | <span data-ttu-id="14e02-111">**S2**</span><span class="sxs-lookup"><span data-stu-id="14e02-111">**S2**</span></span>| <span data-ttu-id="14e02-112">**S3**</span><span class="sxs-lookup"><span data-stu-id="14e02-112">**S3**</span></span> |<span data-ttu-id="14e02-113">**S3 HD**</span><span class="sxs-lookup"><span data-stu-id="14e02-113">**S3 HD**</span></span>|
|---|---|---|---|---|---|----|
|<span data-ttu-id="14e02-114">Maximum number of published knowledge bases allowed (Max indexes -- 1 (reserved for test)</span><span class="sxs-lookup"><span data-stu-id="14e02-114">Maximum number of published knowledge bases allowed (Max indexes -- 1 (reserved for test)</span></span>|<span data-ttu-id="14e02-115">2</span><span class="sxs-lookup"><span data-stu-id="14e02-115">2</span></span>|<span data-ttu-id="14e02-116">14</span><span class="sxs-lookup"><span data-stu-id="14e02-116">14</span></span>|<span data-ttu-id="14e02-117">49</span><span class="sxs-lookup"><span data-stu-id="14e02-117">49</span></span>|<span data-ttu-id="14e02-118">199</span><span class="sxs-lookup"><span data-stu-id="14e02-118">199</span></span>|<span data-ttu-id="14e02-119">199</span><span class="sxs-lookup"><span data-stu-id="14e02-119">199</span></span>|<span data-ttu-id="14e02-120">2999</span><span class="sxs-lookup"><span data-stu-id="14e02-120">2999</span></span>|

## <a name="extraction-limits"></a><span data-ttu-id="14e02-121">Extraction Limits</span><span class="sxs-lookup"><span data-stu-id="14e02-121">Extraction Limits</span></span>
* <span data-ttu-id="14e02-122">Maximum number of files that can be extracted and maximum file size: See [QnAMaker pricing](https://azure.microsoft.com/en-in/pricing/details/cognitive-services/qna-maker/)</span><span class="sxs-lookup"><span data-stu-id="14e02-122">Maximum number of files that can be extracted and maximum file size: See [QnAMaker pricing](https://azure.microsoft.com/en-in/pricing/details/cognitive-services/qna-maker/)</span></span>
* <span data-ttu-id="14e02-123">Maximum number of deep-links that can be crawled for extraction of QnAs from FAQ HTML pages: 20</span><span class="sxs-lookup"><span data-stu-id="14e02-123">Maximum number of deep-links that can be crawled for extraction of QnAs from FAQ HTML pages: 20</span></span>

## <a name="metadata-limits"></a><span data-ttu-id="14e02-124">Metadata Limits</span><span class="sxs-lookup"><span data-stu-id="14e02-124">Metadata Limits</span></span>
* <span data-ttu-id="14e02-125">Maximum number of metadata fields per knowledge base, based on [Azure Search tier limits](https://docs.microsoft.com/en-us/azure/search/search-limits-quotas-capacity)</span><span class="sxs-lookup"><span data-stu-id="14e02-125">Maximum number of metadata fields per knowledge base, based on [Azure Search tier limits](https://docs.microsoft.com/en-us/azure/search/search-limits-quotas-capacity)</span></span>

|<span data-ttu-id="14e02-126">**Azure Search tier**</span><span class="sxs-lookup"><span data-stu-id="14e02-126">**Azure Search tier**</span></span> | <span data-ttu-id="14e02-127">**Free**</span><span class="sxs-lookup"><span data-stu-id="14e02-127">**Free**</span></span> | <span data-ttu-id="14e02-128">**Basic**</span><span class="sxs-lookup"><span data-stu-id="14e02-128">**Basic**</span></span> |<span data-ttu-id="14e02-129">**S1**</span><span class="sxs-lookup"><span data-stu-id="14e02-129">**S1**</span></span> | <span data-ttu-id="14e02-130">**S2**</span><span class="sxs-lookup"><span data-stu-id="14e02-130">**S2**</span></span>| <span data-ttu-id="14e02-131">**S3**</span><span class="sxs-lookup"><span data-stu-id="14e02-131">**S3**</span></span> |<span data-ttu-id="14e02-132">**S3 HD**</span><span class="sxs-lookup"><span data-stu-id="14e02-132">**S3 HD**</span></span>|
|---|---|---|---|---|---|----|
|<span data-ttu-id="14e02-133">Maximum metadata fields per QnA Maker service (across all KBs)</span><span class="sxs-lookup"><span data-stu-id="14e02-133">Maximum metadata fields per QnA Maker service (across all KBs)</span></span>|<span data-ttu-id="14e02-134">1000</span><span class="sxs-lookup"><span data-stu-id="14e02-134">1000</span></span>|<span data-ttu-id="14e02-135">100\*</span><span class="sxs-lookup"><span data-stu-id="14e02-135">100\*</span></span>|<span data-ttu-id="14e02-136">1000</span><span class="sxs-lookup"><span data-stu-id="14e02-136">1000</span></span>|<span data-ttu-id="14e02-137">1000</span><span class="sxs-lookup"><span data-stu-id="14e02-137">1000</span></span>|<span data-ttu-id="14e02-138">1000</span><span class="sxs-lookup"><span data-stu-id="14e02-138">1000</span></span>|<span data-ttu-id="14e02-139">1000</span><span class="sxs-lookup"><span data-stu-id="14e02-139">1000</span></span>|

## <a name="knowledge-base-content-limits"></a><span data-ttu-id="14e02-140">Knowledge Base content limits</span><span class="sxs-lookup"><span data-stu-id="14e02-140">Knowledge Base content limits</span></span>
<span data-ttu-id="14e02-141">Overall limits on the content in the knowledge base:</span><span class="sxs-lookup"><span data-stu-id="14e02-141">Overall limits on the content in the knowledge base:</span></span>
* <span data-ttu-id="14e02-142">Length of answer text: 250000</span><span class="sxs-lookup"><span data-stu-id="14e02-142">Length of answer text: 250000</span></span>
* <span data-ttu-id="14e02-143">Length of question text: 1000</span><span class="sxs-lookup"><span data-stu-id="14e02-143">Length of question text: 1000</span></span>
* <span data-ttu-id="14e02-144">Length of metadata key/value text: 100</span><span class="sxs-lookup"><span data-stu-id="14e02-144">Length of metadata key/value text: 100</span></span>
* <span data-ttu-id="14e02-145">Supported characters for metadata name: Alphabets, digits and _</span><span class="sxs-lookup"><span data-stu-id="14e02-145">Supported characters for metadata name: Alphabets, digits and _</span></span>  
* <span data-ttu-id="14e02-146">Supported characters for metadata value: All except : and |</span><span class="sxs-lookup"><span data-stu-id="14e02-146">Supported characters for metadata value: All except : and |</span></span> 
* <span data-ttu-id="14e02-147">Length of file name: 200</span><span class="sxs-lookup"><span data-stu-id="14e02-147">Length of file name: 200</span></span>
* <span data-ttu-id="14e02-148">Supported file formats: ".tsv", ".pdf", ".txt", ".docx", ".xlsx".</span><span class="sxs-lookup"><span data-stu-id="14e02-148">Supported file formats: ".tsv", ".pdf", ".txt", ".docx", ".xlsx".</span></span>
* <span data-ttu-id="14e02-149">Maximum number of alternate questions: 100</span><span class="sxs-lookup"><span data-stu-id="14e02-149">Maximum number of alternate questions: 100</span></span>
* <span data-ttu-id="14e02-150">Maximum number of question-answer pairs: Depends on the [Azure Search tier](https://docs.microsoft.com/en-in/azure/search/search-limits-quotas-capacity#document-limits) chosen</span><span class="sxs-lookup"><span data-stu-id="14e02-150">Maximum number of question-answer pairs: Depends on the [Azure Search tier](https://docs.microsoft.com/en-in/azure/search/search-limits-quotas-capacity#document-limits) chosen</span></span> 

## <a name="create-knowledge-base-call-limits"></a><span data-ttu-id="14e02-151">Create Knowledge base call limits:</span><span class="sxs-lookup"><span data-stu-id="14e02-151">Create Knowledge base call limits:</span></span>
<span data-ttu-id="14e02-152">These represent the limits for each create knowledge base action; that is, clicking *Create KB* or calling the CreateKnowledgeBase API.</span><span class="sxs-lookup"><span data-stu-id="14e02-152">These represent the limits for each create knowledge base action; that is, clicking *Create KB* or calling the CreateKnowledgeBase API.</span></span>
* <span data-ttu-id="14e02-153">Maximum number of alternate questions per answer: 100</span><span class="sxs-lookup"><span data-stu-id="14e02-153">Maximum number of alternate questions per answer: 100</span></span>
* <span data-ttu-id="14e02-154">Maximum number of URLs: 10</span><span class="sxs-lookup"><span data-stu-id="14e02-154">Maximum number of URLs: 10</span></span>
* <span data-ttu-id="14e02-155">Maximum number of files: 10</span><span class="sxs-lookup"><span data-stu-id="14e02-155">Maximum number of files: 10</span></span>

## <a name="update-knowledge-base-call-limits"></a><span data-ttu-id="14e02-156">Update Knowledge base call limits</span><span class="sxs-lookup"><span data-stu-id="14e02-156">Update Knowledge base call limits</span></span>
<span data-ttu-id="14e02-157">These represent the limits for each update action; that is, clicking *Save and train* or calling the UpdateKnowledgeBase API.</span><span class="sxs-lookup"><span data-stu-id="14e02-157">These represent the limits for each update action; that is, clicking *Save and train* or calling the UpdateKnowledgeBase API.</span></span>
* <span data-ttu-id="14e02-158">Length of each source name: 300</span><span class="sxs-lookup"><span data-stu-id="14e02-158">Length of each source name: 300</span></span>
* <span data-ttu-id="14e02-159">Maximum number of alternate questions added or deleted: 100</span><span class="sxs-lookup"><span data-stu-id="14e02-159">Maximum number of alternate questions added or deleted: 100</span></span>
* <span data-ttu-id="14e02-160">Maximum number of metadata fields added or deleted: 10</span><span class="sxs-lookup"><span data-stu-id="14e02-160">Maximum number of metadata fields added or deleted: 10</span></span>
* <span data-ttu-id="14e02-161">Maximum number of URLs that can be refreshed: 5</span><span class="sxs-lookup"><span data-stu-id="14e02-161">Maximum number of URLs that can be refreshed: 5</span></span>
