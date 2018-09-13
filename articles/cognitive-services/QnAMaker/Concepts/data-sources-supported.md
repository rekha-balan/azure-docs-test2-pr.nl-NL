---
title: Data sources supported - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: Data sources supported
services: cognitive-services
author: nstulasi
manager: sangitap
ms.service: cognitive-services
ms.component: QnAMaker
ms.topic: article
ms.date: 04/21/2018
ms.author: saneppal
ms.openlocfilehash: 698f96b15a9387cd30d26e684ed03ff4cc3346a7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857779"
---
# <a name="data-sources"></a><span data-ttu-id="cc0cf-103">Data sources</span><span class="sxs-lookup"><span data-stu-id="cc0cf-103">Data sources</span></span> 
<span data-ttu-id="cc0cf-104">QnA Maker can automatically extract question-answer pairs from common semi-structured content formats such as FAQs and product manuals.</span><span class="sxs-lookup"><span data-stu-id="cc0cf-104">QnA Maker can automatically extract question-answer pairs from common semi-structured content formats such as FAQs and product manuals.</span></span> <span data-ttu-id="cc0cf-105">Content can also be added to the knowledge base from structured files.</span><span class="sxs-lookup"><span data-stu-id="cc0cf-105">Content can also be added to the knowledge base from structured files.</span></span>

## <a name="plain-faq-pages"></a><span data-ttu-id="cc0cf-106">Plain FAQ pages</span><span class="sxs-lookup"><span data-stu-id="cc0cf-106">Plain FAQ pages</span></span>
<span data-ttu-id="cc0cf-107">This is the most common type of FAQ page, in which the answers immediately follow the questions in the same page.</span><span class="sxs-lookup"><span data-stu-id="cc0cf-107">This is the most common type of FAQ page, in which the answers immediately follow the questions in the same page.</span></span> 

![Plain FAQ page](../media/qnamaker-concepts-datasources/plain-faq.png) 

 

## <a name="faq-pages-with-section-links"></a><span data-ttu-id="cc0cf-109">FAQ pages with Section Links</span><span class="sxs-lookup"><span data-stu-id="cc0cf-109">FAQ pages with Section Links</span></span> 
<span data-ttu-id="cc0cf-110">In this type of FAQ page, questions are aggregated together and are linked to answers that are in different sections on the same page.</span><span class="sxs-lookup"><span data-stu-id="cc0cf-110">In this type of FAQ page, questions are aggregated together and are linked to answers that are in different sections on the same page.</span></span>

 ![Section Link FAQ page](../media/qnamaker-concepts-datasources/sectionlink-faq.png) 


## <a name="faq-pages-with-links-to-different-pages"></a><span data-ttu-id="cc0cf-112">FAQ pages with links to different pages</span><span class="sxs-lookup"><span data-stu-id="cc0cf-112">FAQ pages with links to different pages</span></span> 
<span data-ttu-id="cc0cf-113">This type of FAQ page is similar to a section-linked FAQ page, except that the links redirect to a different page.</span><span class="sxs-lookup"><span data-stu-id="cc0cf-113">This type of FAQ page is similar to a section-linked FAQ page, except that the links redirect to a different page.</span></span> <span data-ttu-id="cc0cf-114">QnA Maker crawls all the linked pages to extract the corresponding answers.</span><span class="sxs-lookup"><span data-stu-id="cc0cf-114">QnA Maker crawls all the linked pages to extract the corresponding answers.</span></span>

 ![Deep link FAQ page](../media/qnamaker-concepts-datasources/deeplink-faq.png) 


## <a name="product-manuals"></a><span data-ttu-id="cc0cf-116">Product manuals</span><span class="sxs-lookup"><span data-stu-id="cc0cf-116">Product manuals</span></span>

<span data-ttu-id="cc0cf-117">A manual is typically guidance material that accompanies a product.</span><span class="sxs-lookup"><span data-stu-id="cc0cf-117">A manual is typically guidance material that accompanies a product.</span></span> <span data-ttu-id="cc0cf-118">It helps the user to set up, use, maintain, and troubleshoot the product.</span><span class="sxs-lookup"><span data-stu-id="cc0cf-118">It helps the user to set up, use, maintain, and troubleshoot the product.</span></span> <span data-ttu-id="cc0cf-119">When QnA Maker processes a manual, it extracts the headings and subheadings as questions and the subsequent content as answers.</span><span class="sxs-lookup"><span data-stu-id="cc0cf-119">When QnA Maker processes a manual, it extracts the headings and subheadings as questions and the subsequent content as answers.</span></span> <span data-ttu-id="cc0cf-120">See an example [here](http://download.microsoft.com/download/2/9/B/29B20383-302C-4517-A006-B0186F04BE28/surface-pro-4-user-guide-EN.pdf).</span><span class="sxs-lookup"><span data-stu-id="cc0cf-120">See an example [here](http://download.microsoft.com/download/2/9/B/29B20383-302C-4517-A006-B0186F04BE28/surface-pro-4-user-guide-EN.pdf).</span></span>

> [!NOTE]
> <span data-ttu-id="cc0cf-121">Extraction works best on manuals that have a table of contents and/or an index page, and a clear structure with hierarchical headings.</span><span class="sxs-lookup"><span data-stu-id="cc0cf-121">Extraction works best on manuals that have a table of contents and/or an index page, and a clear structure with hierarchical headings.</span></span>


## <a name="structured-data-format-through-file-upload"></a><span data-ttu-id="cc0cf-122">Structured data format through file upload</span><span class="sxs-lookup"><span data-stu-id="cc0cf-122">Structured data format through file upload</span></span>

<span data-ttu-id="cc0cf-123">Structured files such as .tsv, .xlsx with formatted columns can also be uploaded to QnA Maker during knowledge base creation.</span><span class="sxs-lookup"><span data-stu-id="cc0cf-123">Structured files such as .tsv, .xlsx with formatted columns can also be uploaded to QnA Maker during knowledge base creation.</span></span> <span data-ttu-id="cc0cf-124">You can also upload files from the **Settings** tab of a knowledge base</span><span class="sxs-lookup"><span data-stu-id="cc0cf-124">You can also upload files from the **Settings** tab of a knowledge base</span></span>

| <span data-ttu-id="cc0cf-125">Question</span><span class="sxs-lookup"><span data-stu-id="cc0cf-125">Question</span></span>  | <span data-ttu-id="cc0cf-126">Answer</span><span class="sxs-lookup"><span data-stu-id="cc0cf-126">Answer</span></span>  | <span data-ttu-id="cc0cf-127">Metadata</span><span class="sxs-lookup"><span data-stu-id="cc0cf-127">Metadata</span></span>                |
|-----------|---------|-------------------------|
| <span data-ttu-id="cc0cf-128">Question1</span><span class="sxs-lookup"><span data-stu-id="cc0cf-128">Question1</span></span> | <span data-ttu-id="cc0cf-129">Answer1</span><span class="sxs-lookup"><span data-stu-id="cc0cf-129">Answer1</span></span> | <span data-ttu-id="cc0cf-130">\`Key1:Value1</span><span class="sxs-lookup"><span data-stu-id="cc0cf-130">\`Key1:Value1</span></span>|<span data-ttu-id="cc0cf-131">Key2:Value2\`</span><span class="sxs-lookup"><span data-stu-id="cc0cf-131">Key2:Value2\`</span></span> |
| <span data-ttu-id="cc0cf-132">Question2</span><span class="sxs-lookup"><span data-stu-id="cc0cf-132">Question2</span></span> | <span data-ttu-id="cc0cf-133">Answer2</span><span class="sxs-lookup"><span data-stu-id="cc0cf-133">Answer2</span></span> |      `Key:Value`           |
<span data-ttu-id="cc0cf-134">Any additional columns in the source file are ignored.</span><span class="sxs-lookup"><span data-stu-id="cc0cf-134">Any additional columns in the source file are ignored.</span></span>

## <a name="structured-data-format-through-import"></a><span data-ttu-id="cc0cf-135">Structured data format through import</span><span class="sxs-lookup"><span data-stu-id="cc0cf-135">Structured data format through import</span></span>
<span data-ttu-id="cc0cf-136">Importing a knowledge base replaces the content of the existing knowledge base.</span><span class="sxs-lookup"><span data-stu-id="cc0cf-136">Importing a knowledge base replaces the content of the existing knowledge base.</span></span> <span data-ttu-id="cc0cf-137">Import requires a structured .tsv file that contains data source information.</span><span class="sxs-lookup"><span data-stu-id="cc0cf-137">Import requires a structured .tsv file that contains data source information.</span></span> <span data-ttu-id="cc0cf-138">This information helps QnA Maker group the question-answer pairs and attribute them to a particular data source.</span><span class="sxs-lookup"><span data-stu-id="cc0cf-138">This information helps QnA Maker group the question-answer pairs and attribute them to a particular data source.</span></span>

| <span data-ttu-id="cc0cf-139">Question</span><span class="sxs-lookup"><span data-stu-id="cc0cf-139">Question</span></span>  | <span data-ttu-id="cc0cf-140">Answer</span><span class="sxs-lookup"><span data-stu-id="cc0cf-140">Answer</span></span>  | <span data-ttu-id="cc0cf-141">Source</span><span class="sxs-lookup"><span data-stu-id="cc0cf-141">Source</span></span>| <span data-ttu-id="cc0cf-142">Metadata</span><span class="sxs-lookup"><span data-stu-id="cc0cf-142">Metadata</span></span>                |
|-----------|---------|----|---------------------|
| <span data-ttu-id="cc0cf-143">Question1</span><span class="sxs-lookup"><span data-stu-id="cc0cf-143">Question1</span></span> | <span data-ttu-id="cc0cf-144">Answer1</span><span class="sxs-lookup"><span data-stu-id="cc0cf-144">Answer1</span></span> | <span data-ttu-id="cc0cf-145">Url1</span><span class="sxs-lookup"><span data-stu-id="cc0cf-145">Url1</span></span>|<span data-ttu-id="cc0cf-146">\`Key1:Value1</span><span class="sxs-lookup"><span data-stu-id="cc0cf-146">\`Key1:Value1</span></span>|<span data-ttu-id="cc0cf-147">Key2:Value2\`</span><span class="sxs-lookup"><span data-stu-id="cc0cf-147">Key2:Value2\`</span></span> |
| <span data-ttu-id="cc0cf-148">Question2</span><span class="sxs-lookup"><span data-stu-id="cc0cf-148">Question2</span></span> | <span data-ttu-id="cc0cf-149">Answer2</span><span class="sxs-lookup"><span data-stu-id="cc0cf-149">Answer2</span></span> | <span data-ttu-id="cc0cf-150">Editorial</span><span class="sxs-lookup"><span data-stu-id="cc0cf-150">Editorial</span></span>|    `Key:Value`       |

## <a name="editorial"></a><span data-ttu-id="cc0cf-151">Editorial</span><span class="sxs-lookup"><span data-stu-id="cc0cf-151">Editorial</span></span>
<span data-ttu-id="cc0cf-152">If you do not have pre-existing content to populate the knowledge base, you can also add them editorially in QnA Maker Knowledge base.</span><span class="sxs-lookup"><span data-stu-id="cc0cf-152">If you do not have pre-existing content to populate the knowledge base, you can also add them editorially in QnA Maker Knowledge base.</span></span> <span data-ttu-id="cc0cf-153">Learn how to update your knowledge base [here](../How-To/edit-knowledge-base.md).</span><span class="sxs-lookup"><span data-stu-id="cc0cf-153">Learn how to update your knowledge base [here](../How-To/edit-knowledge-base.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc0cf-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="cc0cf-154">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cc0cf-155">Set up a QnA Maker service</span><span class="sxs-lookup"><span data-stu-id="cc0cf-155">Set up a QnA Maker service</span></span>](../How-To/set-up-qnamaker-service-azure.md)

## <a name="see-also"></a><span data-ttu-id="cc0cf-156">See also</span><span class="sxs-lookup"><span data-stu-id="cc0cf-156">See also</span></span> 

[<span data-ttu-id="cc0cf-157">QnA Maker overview</span><span class="sxs-lookup"><span data-stu-id="cc0cf-157">QnA Maker overview</span></span>](../Overview/overview.md)
