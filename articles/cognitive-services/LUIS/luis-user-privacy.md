---
title: Export and deletion of customer data - LUIS - Azure Cognitive Services | | Microsoft Docs
description: Reference for export and deletion of customer data from Language Understanding service (LUIS).
services: cognitive-services
author: v-geberr
manager: kaiqb
ms.service: cognitive-services
ms.technology: luis
ms.topic: article
ms.date: 05/23/2018
ms.author: diberry
ms.openlocfilehash: c6fba28ea3a4b24f02b62b6c3f124569378e5bc8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966859"
---
# <a name="export-and-delete-your-customer-data-in-language-understanding-luis-in-cognitive-services"></a><span data-ttu-id="56656-103">Export and delete your customer data in Language Understanding (LUIS) in Cognitive Services</span><span class="sxs-lookup"><span data-stu-id="56656-103">Export and delete your customer data in Language Understanding (LUIS) in Cognitive Services</span></span>

## <a name="summary-of-customer-data-request-features"></a><span data-ttu-id="56656-104">Summary of customer data request features</span><span class="sxs-lookup"><span data-stu-id="56656-104">Summary of customer data request features</span></span>
<span data-ttu-id="56656-105">Language Understanding Intelligent Service (LUIS) preserves customer content to operate the service, but the LUIS user has full control over viewing, exporting, and deleting their data.</span><span class="sxs-lookup"><span data-stu-id="56656-105">Language Understanding Intelligent Service (LUIS) preserves customer content to operate the service, but the LUIS user has full control over viewing, exporting, and deleting their data.</span></span> <span data-ttu-id="56656-106">This can be done through the LUIS web [portal](luis-reference-regions.md) or the [LUIS Programmatic APIs](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c2f).</span><span class="sxs-lookup"><span data-stu-id="56656-106">This can be done through the LUIS web [portal](luis-reference-regions.md) or the [LUIS Programmatic APIs](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c2f).</span></span>

[!INCLUDE [GDPR-related guidance](../../../includes/gdpr-intro-sentence.md)]

<span data-ttu-id="56656-107">Customer content is stored encrypted in Microsoft regional Azure storage and includes:</span><span class="sxs-lookup"><span data-stu-id="56656-107">Customer content is stored encrypted in Microsoft regional Azure storage and includes:</span></span>

- <span data-ttu-id="56656-108">User account content collected at registration</span><span class="sxs-lookup"><span data-stu-id="56656-108">User account content collected at registration</span></span>
- <span data-ttu-id="56656-109">Training data required to build the models (i.e. intent & entities)</span><span class="sxs-lookup"><span data-stu-id="56656-109">Training data required to build the models (i.e. intent & entities)</span></span>
- <span data-ttu-id="56656-110">User queries logged at runtime to help improve the user models</span><span class="sxs-lookup"><span data-stu-id="56656-110">User queries logged at runtime to help improve the user models</span></span>
  - <span data-ttu-id="56656-111">Users can turn off query logging by appending `&log=false` to the request, details [here](luis-resources-faq.md#how-can-i-disable-the-logging-of-utterances)</span><span class="sxs-lookup"><span data-stu-id="56656-111">Users can turn off query logging by appending `&log=false` to the request, details [here](luis-resources-faq.md#how-can-i-disable-the-logging-of-utterances)</span></span>

## <a name="deleting-customer-data"></a><span data-ttu-id="56656-112">Deleting customer data</span><span class="sxs-lookup"><span data-stu-id="56656-112">Deleting customer data</span></span>
<span data-ttu-id="56656-113">LUIS users have full control to delete any user content, either through the LUIS web portal or the LUIS Programmatic APIs.</span><span class="sxs-lookup"><span data-stu-id="56656-113">LUIS users have full control to delete any user content, either through the LUIS web portal or the LUIS Programmatic APIs.</span></span> <span data-ttu-id="56656-114">The following table displays links assisting with both:</span><span class="sxs-lookup"><span data-stu-id="56656-114">The following table displays links assisting with both:</span></span>

| | <span data-ttu-id="56656-115">**User Account**</span><span class="sxs-lookup"><span data-stu-id="56656-115">**User Account**</span></span> | <span data-ttu-id="56656-116">**Application**</span><span class="sxs-lookup"><span data-stu-id="56656-116">**Application**</span></span> | <span data-ttu-id="56656-117">**Utterance(s)**</span><span class="sxs-lookup"><span data-stu-id="56656-117">**Utterance(s)**</span></span> | <span data-ttu-id="56656-118">**End-user queries**</span><span class="sxs-lookup"><span data-stu-id="56656-118">**End-user queries**</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="56656-119">**Portal**</span><span class="sxs-lookup"><span data-stu-id="56656-119">**Portal**</span></span> | [<span data-ttu-id="56656-120">Link</span><span class="sxs-lookup"><span data-stu-id="56656-120">Link</span></span>](luis-how-to-account-settings.md) | [<span data-ttu-id="56656-121">Link</span><span class="sxs-lookup"><span data-stu-id="56656-121">Link</span></span>](luis-how-to-start-new-app.md#delete-app) | [<span data-ttu-id="56656-122">Link</span><span class="sxs-lookup"><span data-stu-id="56656-122">Link</span></span>](luis-how-to-start-new-app.md#delete-app) | [<span data-ttu-id="56656-123">Link</span><span class="sxs-lookup"><span data-stu-id="56656-123">Link</span></span>](luis-how-to-start-new-app.md#delete-app) |
| <span data-ttu-id="56656-124">**APIs**</span><span class="sxs-lookup"><span data-stu-id="56656-124">**APIs**</span></span> | [<span data-ttu-id="56656-125">Link</span><span class="sxs-lookup"><span data-stu-id="56656-125">Link</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c4c) | [<span data-ttu-id="56656-126">Link</span><span class="sxs-lookup"><span data-stu-id="56656-126">Link</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c39) | [<span data-ttu-id="56656-127">Link</span><span class="sxs-lookup"><span data-stu-id="56656-127">Link</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c0b) | [<span data-ttu-id="56656-128">Link</span><span class="sxs-lookup"><span data-stu-id="56656-128">Link</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/58b6f32139e2bb139ce823c9) |


## <a name="exporting-customer-data"></a><span data-ttu-id="56656-129">Exporting customer data</span><span class="sxs-lookup"><span data-stu-id="56656-129">Exporting customer data</span></span>
<span data-ttu-id="56656-130">LUIS users have full control to view the data on the portal, however it must be exported through the LUIS Programmatic APIs.</span><span class="sxs-lookup"><span data-stu-id="56656-130">LUIS users have full control to view the data on the portal, however it must be exported through the LUIS Programmatic APIs.</span></span> <span data-ttu-id="56656-131">The following table displays links assisting with data exports via the LUIS Programmatic APIs:</span><span class="sxs-lookup"><span data-stu-id="56656-131">The following table displays links assisting with data exports via the LUIS Programmatic APIs:</span></span>

| | <span data-ttu-id="56656-132">**User Account**</span><span class="sxs-lookup"><span data-stu-id="56656-132">**User Account**</span></span> | <span data-ttu-id="56656-133">**Application**</span><span class="sxs-lookup"><span data-stu-id="56656-133">**Application**</span></span> | <span data-ttu-id="56656-134">**Utterance(s)**</span><span class="sxs-lookup"><span data-stu-id="56656-134">**Utterance(s)**</span></span> | <span data-ttu-id="56656-135">**End-user queries**</span><span class="sxs-lookup"><span data-stu-id="56656-135">**End-user queries**</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="56656-136">**APIs**</span><span class="sxs-lookup"><span data-stu-id="56656-136">**APIs**</span></span> | [<span data-ttu-id="56656-137">Link</span><span class="sxs-lookup"><span data-stu-id="56656-137">Link</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c48) | [<span data-ttu-id="56656-138">Link</span><span class="sxs-lookup"><span data-stu-id="56656-138">Link</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c40) | [<span data-ttu-id="56656-139">Link</span><span class="sxs-lookup"><span data-stu-id="56656-139">Link</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c0a) | [<span data-ttu-id="56656-140">Link</span><span class="sxs-lookup"><span data-stu-id="56656-140">Link</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c36) |


## <a name="next-steps"></a><span data-ttu-id="56656-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="56656-141">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="56656-142">LUIS regions reference</span><span class="sxs-lookup"><span data-stu-id="56656-142">LUIS regions reference</span></span>](./luis-reference-regions.md)
