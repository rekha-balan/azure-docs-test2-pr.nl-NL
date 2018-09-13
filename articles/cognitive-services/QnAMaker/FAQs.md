---
title: FAQ - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: FAQs
services: cognitive-services
author: nstulasi
manager: sangitap
ms.service: cognitive-services
ms.component: QnAMaker
ms.topic: article
ms.date: 04/21/2018
ms.author: saneppal
ms.openlocfilehash: a6bf32549715d0357771b3f3b0ff72f64788ec20
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44800493"
---
# <a name="frequently-asked-questions"></a><span data-ttu-id="7439a-103">Frequently Asked Questions</span><span class="sxs-lookup"><span data-stu-id="7439a-103">Frequently Asked Questions</span></span>

## <a name="why-is-my-urlsfiles-is-not-extracting-question-answer-pairs"></a><span data-ttu-id="7439a-104">Why is my URL(s)/file(s) is not extracting question-answer pairs?</span><span class="sxs-lookup"><span data-stu-id="7439a-104">Why is my URL(s)/file(s) is not extracting question-answer pairs?</span></span>

<span data-ttu-id="7439a-105">It's possible that QnA Maker can't auto-extract some question-and-answer (QnA) content from valid FAQ URLs.</span><span class="sxs-lookup"><span data-stu-id="7439a-105">It's possible that QnA Maker can't auto-extract some question-and-answer (QnA) content from valid FAQ URLs.</span></span> <span data-ttu-id="7439a-106">In such cases, you can paste the QnA content in a .txt file and see if the tool can ingest it.</span><span class="sxs-lookup"><span data-stu-id="7439a-106">In such cases, you can paste the QnA content in a .txt file and see if the tool can ingest it.</span></span> <span data-ttu-id="7439a-107">Alternately, you can editorially add content to your knowledge base.</span><span class="sxs-lookup"><span data-stu-id="7439a-107">Alternately, you can editorially add content to your knowledge base.</span></span>

## <a name="how-large-a-knowledge-base-can-i-create"></a><span data-ttu-id="7439a-108">How large a knowledge base can I create?</span><span class="sxs-lookup"><span data-stu-id="7439a-108">How large a knowledge base can I create?</span></span>

<span data-ttu-id="7439a-109">The size of the knowledge base depends on the SKU of Azure search you choose when creating the QnA Maker service.</span><span class="sxs-lookup"><span data-stu-id="7439a-109">The size of the knowledge base depends on the SKU of Azure search you choose when creating the QnA Maker service.</span></span> <span data-ttu-id="7439a-110">Read [here](./Tutorials/choosing-capacity-qnamaker-deployment.md) for more details.</span><span class="sxs-lookup"><span data-stu-id="7439a-110">Read [here](./Tutorials/choosing-capacity-qnamaker-deployment.md) for more details.</span></span>

## <a name="why-do-i-not-see-anything-in-the-drop-down-for-when-i-try-to-create-a-new-knowledge-base"></a><span data-ttu-id="7439a-111">Why do I not see anything in the drop-down for when I try to create a new knowledge base?</span><span class="sxs-lookup"><span data-stu-id="7439a-111">Why do I not see anything in the drop-down for when I try to create a new knowledge base?</span></span>

<span data-ttu-id="7439a-112">You haven't created any QnA Maker services in Azure yet.</span><span class="sxs-lookup"><span data-stu-id="7439a-112">You haven't created any QnA Maker services in Azure yet.</span></span> <span data-ttu-id="7439a-113">Read [here](./How-To/set-up-qnamaker-service-azure.md) how to do that.</span><span class="sxs-lookup"><span data-stu-id="7439a-113">Read [here](./How-To/set-up-qnamaker-service-azure.md) how to do that.</span></span>

## <a name="how-do-i-share-a-knowledge-base-with-other"></a><span data-ttu-id="7439a-114">How do I share a knowledge base with other?</span><span class="sxs-lookup"><span data-stu-id="7439a-114">How do I share a knowledge base with other?</span></span>

<span data-ttu-id="7439a-115">Sharing works at the level of a QnA Maker service, i.e. all knowledge bases in the services will be shared.</span><span class="sxs-lookup"><span data-stu-id="7439a-115">Sharing works at the level of a QnA Maker service, i.e. all knowledge bases in the services will be shared.</span></span> <span data-ttu-id="7439a-116">Read [here](./How-To/collaborate-knowledge-base.md) how to collaborate on a knowledge base.</span><span class="sxs-lookup"><span data-stu-id="7439a-116">Read [here](./How-To/collaborate-knowledge-base.md) how to collaborate on a knowledge base.</span></span>

## <a name="how-can-i-change-the-default-message-when-no-good-match-is-found"></a><span data-ttu-id="7439a-117">How can I change the default message when no good match is found?</span><span class="sxs-lookup"><span data-stu-id="7439a-117">How can I change the default message when no good match is found?</span></span>

<span data-ttu-id="7439a-118">The default message is part of the settings in your App service.</span><span class="sxs-lookup"><span data-stu-id="7439a-118">The default message is part of the settings in your App service.</span></span>
- <span data-ttu-id="7439a-119">Go to the your App service resource in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="7439a-119">Go to the your App service resource in the Azure portal</span></span>

![qnamaker appservice](./media/qnamaker-faq/qnamaker-resource-list-appservice.png)
- <span data-ttu-id="7439a-121">Click on the **Settings** option</span><span class="sxs-lookup"><span data-stu-id="7439a-121">Click on the **Settings** option</span></span>

![qnamaker appservice settings](./media/qnamaker-faq/qnamaker-appservice-settings.png)
- <span data-ttu-id="7439a-123">Change the value of the **DefaultAnswer** setting</span><span class="sxs-lookup"><span data-stu-id="7439a-123">Change the value of the **DefaultAnswer** setting</span></span>
- <span data-ttu-id="7439a-124">Restart your App service</span><span class="sxs-lookup"><span data-stu-id="7439a-124">Restart your App service</span></span>

![qnamaker appservice restart](./media/qnamaker-faq/qnamaker-appservice-restart.png)

## <a name="why-is-my-sharepoint-link-not-getting-extracted"></a><span data-ttu-id="7439a-126">Why is my SharePoint link not getting extracted?</span><span class="sxs-lookup"><span data-stu-id="7439a-126">Why is my SharePoint link not getting extracted?</span></span>

<span data-ttu-id="7439a-127">The tool parses only public URLs and does not support authenticated data sources at this time.</span><span class="sxs-lookup"><span data-stu-id="7439a-127">The tool parses only public URLs and does not support authenticated data sources at this time.</span></span> <span data-ttu-id="7439a-128">Alternately, you can download the file and use the file-upload option to extract questions and answers.</span><span class="sxs-lookup"><span data-stu-id="7439a-128">Alternately, you can download the file and use the file-upload option to extract questions and answers.</span></span>


## <a name="the-updates-that-i-made-to-my-knowledge-base-are-not-reflected-on-publish-why-not"></a><span data-ttu-id="7439a-129">The updates that I made to my knowledge base are not reflected on publish.</span><span class="sxs-lookup"><span data-stu-id="7439a-129">The updates that I made to my knowledge base are not reflected on publish.</span></span> <span data-ttu-id="7439a-130">Why not?</span><span class="sxs-lookup"><span data-stu-id="7439a-130">Why not?</span></span>

<span data-ttu-id="7439a-131">Every edit operation, whether in a table update, test, or settings, needs to be saved before it can be published.</span><span class="sxs-lookup"><span data-stu-id="7439a-131">Every edit operation, whether in a table update, test, or settings, needs to be saved before it can be published.</span></span> <span data-ttu-id="7439a-132">Be sure to click the Save and train button after every edit operation.</span><span class="sxs-lookup"><span data-stu-id="7439a-132">Be sure to click the Save and train button after every edit operation.</span></span>

## <a name="when-should-i-refresh-my-endpoint-keys"></a><span data-ttu-id="7439a-133">When should I refresh my endpoint keys?</span><span class="sxs-lookup"><span data-stu-id="7439a-133">When should I refresh my endpoint keys?</span></span>

<span data-ttu-id="7439a-134">You should refresh your endpoint keys if you suspect that they have been compromised.</span><span class="sxs-lookup"><span data-stu-id="7439a-134">You should refresh your endpoint keys if you suspect that they have been compromised.</span></span>

## <a name="does-the-knowledge-base-support-rich-data-or-multimedia"></a><span data-ttu-id="7439a-135">Does the knowledge base support rich data or multimedia?</span><span class="sxs-lookup"><span data-stu-id="7439a-135">Does the knowledge base support rich data or multimedia?</span></span>

<span data-ttu-id="7439a-136">The knowledge base supports Markdown.</span><span class="sxs-lookup"><span data-stu-id="7439a-136">The knowledge base supports Markdown.</span></span> <span data-ttu-id="7439a-137">However, the auto-extraction from URLs has limited HTML-to-Markdown conversion capability.</span><span class="sxs-lookup"><span data-stu-id="7439a-137">However, the auto-extraction from URLs has limited HTML-to-Markdown conversion capability.</span></span> <span data-ttu-id="7439a-138">If you want to use full-fledged Markdown, you can modify your content directly in the table, or upload a knowledge base with the rich content.</span><span class="sxs-lookup"><span data-stu-id="7439a-138">If you want to use full-fledged Markdown, you can modify your content directly in the table, or upload a knowledge base with the rich content.</span></span>

<span data-ttu-id="7439a-139">Multimedia, such as images and videos, is not supported at this time.</span><span class="sxs-lookup"><span data-stu-id="7439a-139">Multimedia, such as images and videos, is not supported at this time.</span></span>

## <a name="does-qna-maker-support-non-english-languages"></a><span data-ttu-id="7439a-140">Does QnA Maker support non-English languages?</span><span class="sxs-lookup"><span data-stu-id="7439a-140">Does QnA Maker support non-English languages?</span></span>

<span data-ttu-id="7439a-141">See more details about [supported languages](./Overview/languages-supported.md).</span><span class="sxs-lookup"><span data-stu-id="7439a-141">See more details about [supported languages](./Overview/languages-supported.md).</span></span>

<span data-ttu-id="7439a-142">If you have content from multiple languages, be sure to create a separate service for each language.</span><span class="sxs-lookup"><span data-stu-id="7439a-142">If you have content from multiple languages, be sure to create a separate service for each language.</span></span>

## <a name="do-i-need-to-use-bot-framework-in-order-to-use-qna-maker"></a><span data-ttu-id="7439a-143">Do I need to use Bot Framework in order to use QnA Maker?</span><span class="sxs-lookup"><span data-stu-id="7439a-143">Do I need to use Bot Framework in order to use QnA Maker?</span></span>

<span data-ttu-id="7439a-144">No, you do not need to use the Bot Framework with QnA Maker.</span><span class="sxs-lookup"><span data-stu-id="7439a-144">No, you do not need to use the Bot Framework with QnA Maker.</span></span> <span data-ttu-id="7439a-145">However, QnA Maker is offered as one of several templates in Azure Bot Service.</span><span class="sxs-lookup"><span data-stu-id="7439a-145">However, QnA Maker is offered as one of several templates in Azure Bot Service.</span></span> <span data-ttu-id="7439a-146">Bot Service enables rapid intelligent bot development through Microsoft Bot Framework, and it runs in a server less environment.</span><span class="sxs-lookup"><span data-stu-id="7439a-146">Bot Service enables rapid intelligent bot development through Microsoft Bot Framework, and it runs in a server less environment.</span></span>

## <a name="how-can-i-create-a-bot-with-qna-maker"></a><span data-ttu-id="7439a-147">How can I create a bot with QnA Maker?</span><span class="sxs-lookup"><span data-stu-id="7439a-147">How can I create a bot with QnA Maker?</span></span>

<span data-ttu-id="7439a-148">Follow the instructions in [this](./Tutorials/create-qna-bot.md) documentation to create your Bot with Azure Bot.</span><span class="sxs-lookup"><span data-stu-id="7439a-148">Follow the instructions in [this](./Tutorials/create-qna-bot.md) documentation to create your Bot with Azure Bot.</span></span>

## <a name="how-do-i-embed-the-qna-maker-service-in-my-website"></a><span data-ttu-id="7439a-149">How do I embed the QnA Maker service in my website?</span><span class="sxs-lookup"><span data-stu-id="7439a-149">How do I embed the QnA Maker service in my website?</span></span>

<span data-ttu-id="7439a-150">Follow these steps to embed the QnA Maker service as a web-chat control in your website:</span><span class="sxs-lookup"><span data-stu-id="7439a-150">Follow these steps to embed the QnA Maker service as a web-chat control in your website:</span></span>

1. <span data-ttu-id="7439a-151">Create your FAQ bot by following the instructions [here](./Tutorials/create-qna-bot.md).</span><span class="sxs-lookup"><span data-stu-id="7439a-151">Create your FAQ bot by following the instructions [here](./Tutorials/create-qna-bot.md).</span></span>
2. <span data-ttu-id="7439a-152">Enable the web chat by following the steps [here](https://docs.microsoft.com/en-us/azure/bot-service/bot-service-channel-connect-webchat)</span><span class="sxs-lookup"><span data-stu-id="7439a-152">Enable the web chat by following the steps [here](https://docs.microsoft.com/en-us/azure/bot-service/bot-service-channel-connect-webchat)</span></span>


