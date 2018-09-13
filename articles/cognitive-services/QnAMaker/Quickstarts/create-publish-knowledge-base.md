---
title: 'Quickstart: Creating a KB - QnA Maker'
titleSuffix: Azure Cognitive Services
description: You can create a QnA Maker knowledge base (KB) from your own content, such as FAQs or product manuals. The QnA Maker KB in this example is created from a simple FAQ webpage to answer questions on BitLocker key recovery.
author: nitinme
manager: cgronlun
ms.service: cognitive-services
ms.component: qna-maker
ms.topic: article
ms.date: 05/07/2018
ms.author: saneppal
ms.openlocfilehash: 2b8573da6cc87af39a7681fa369940fa7a0b8eb3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866484"
---
# <a name="create-train-and-publish-your-knowledge-base"></a><span data-ttu-id="aef50-104">Create, train, and publish your knowledge base</span><span class="sxs-lookup"><span data-stu-id="aef50-104">Create, train, and publish your knowledge base</span></span>

<span data-ttu-id="aef50-105">You can create a QnA Maker knowledge base (KB) from your own content, such as FAQs or product manuals.</span><span class="sxs-lookup"><span data-stu-id="aef50-105">You can create a QnA Maker knowledge base (KB) from your own content, such as FAQs or product manuals.</span></span> <span data-ttu-id="aef50-106">The QnA Maker KB in this example is created from a simple FAQ webpage to answer questions on BitLocker key recovery.</span><span class="sxs-lookup"><span data-stu-id="aef50-106">The QnA Maker KB in this example is created from a simple FAQ webpage to answer questions on BitLocker key recovery.</span></span>

## <a name="prerequisite"></a><span data-ttu-id="aef50-107">Prerequisite</span><span class="sxs-lookup"><span data-stu-id="aef50-107">Prerequisite</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="aef50-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="aef50-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="create-a-qna-maker-knowledge-base"></a><span data-ttu-id="aef50-109">Create a QnA Maker knowledge base</span><span class="sxs-lookup"><span data-stu-id="aef50-109">Create a QnA Maker knowledge base</span></span>

1. <span data-ttu-id="aef50-110">Sign in to QnAMaker.ai with your Azure credentials.</span><span class="sxs-lookup"><span data-stu-id="aef50-110">Sign in to QnAMaker.ai with your Azure credentials.</span></span>

2. <span data-ttu-id="aef50-111">On the QnA Maker website, select **Create a knowledge base**.</span><span class="sxs-lookup"><span data-stu-id="aef50-111">On the QnA Maker website, select **Create a knowledge base**.</span></span>

   ![Create new KB](../media/qna-maker-create-kb.png)

3. <span data-ttu-id="aef50-113">On the **Create** page, in step 1, select **Create a QnA service**.</span><span class="sxs-lookup"><span data-stu-id="aef50-113">On the **Create** page, in step 1, select **Create a QnA service**.</span></span> <span data-ttu-id="aef50-114">You are directed to the [Azure portal](https://ms.portal.azure.com/#create/Microsoft.CognitiveServicesQnAMaker) to set up a QnA Maker service in your subscription.</span><span class="sxs-lookup"><span data-stu-id="aef50-114">You are directed to the [Azure portal](https://ms.portal.azure.com/#create/Microsoft.CognitiveServicesQnAMaker) to set up a QnA Maker service in your subscription.</span></span> <span data-ttu-id="aef50-115">If the Azure portal times out, select **Try again** on the site.</span><span class="sxs-lookup"><span data-stu-id="aef50-115">If the Azure portal times out, select **Try again** on the site.</span></span> <span data-ttu-id="aef50-116">After you connect, your Azure dashboard appears.</span><span class="sxs-lookup"><span data-stu-id="aef50-116">After you connect, your Azure dashboard appears.</span></span>

4. <span data-ttu-id="aef50-117">After you successfully create a new QnA Maker service in Azure, return to qnamaker.ai/create.</span><span class="sxs-lookup"><span data-stu-id="aef50-117">After you successfully create a new QnA Maker service in Azure, return to qnamaker.ai/create.</span></span> <span data-ttu-id="aef50-118">Select your QnA service from the drop-down lists in step 2.</span><span class="sxs-lookup"><span data-stu-id="aef50-118">Select your QnA service from the drop-down lists in step 2.</span></span> <span data-ttu-id="aef50-119">If you created a new QnA service, be sure to refresh the page.</span><span class="sxs-lookup"><span data-stu-id="aef50-119">If you created a new QnA service, be sure to refresh the page.</span></span>

   ![Select a QnA service KB](../media/qnamaker-quickstart-kb/qnaservice-selection.png)

5. <span data-ttu-id="aef50-121">In step 3, name your KB **My Sample QnA KB**.</span><span class="sxs-lookup"><span data-stu-id="aef50-121">In step 3, name your KB **My Sample QnA KB**.</span></span>

6. <span data-ttu-id="aef50-122">To add content to your KB, select three types of data sources.</span><span class="sxs-lookup"><span data-stu-id="aef50-122">To add content to your KB, select three types of data sources.</span></span> <span data-ttu-id="aef50-123">In step 4, under **Populate your KB**, add the [BitLocker Recovery FAQ](https://docs.microsoft.com/en-us/windows/security/information-protection/bitlocker/bitlocker-overview-and-requirements-faq) URL in the **URL** box.</span><span class="sxs-lookup"><span data-stu-id="aef50-123">In step 4, under **Populate your KB**, add the [BitLocker Recovery FAQ](https://docs.microsoft.com/en-us/windows/security/information-protection/bitlocker/bitlocker-overview-and-requirements-faq) URL in the **URL** box.</span></span>

   ![Select a QnA service KB](../media/qnamaker-quickstart-kb/add-datasources.png)

7. <span data-ttu-id="aef50-125">In step 5, select **Create your KB**.</span><span class="sxs-lookup"><span data-stu-id="aef50-125">In step 5, select **Create your KB**.</span></span>

8. <span data-ttu-id="aef50-126">While the KB is being created, a pop-up window appears.</span><span class="sxs-lookup"><span data-stu-id="aef50-126">While the KB is being created, a pop-up window appears.</span></span> <span data-ttu-id="aef50-127">The extraction process takes a few minutes to read the HTML page and identify questions and answers.</span><span class="sxs-lookup"><span data-stu-id="aef50-127">The extraction process takes a few minutes to read the HTML page and identify questions and answers.</span></span>

9. <span data-ttu-id="aef50-128">After the KB is successfully created, the **Knowledge base** page opens.</span><span class="sxs-lookup"><span data-stu-id="aef50-128">After the KB is successfully created, the **Knowledge base** page opens.</span></span> <span data-ttu-id="aef50-129">You can edit the contents of the KB on this page.</span><span class="sxs-lookup"><span data-stu-id="aef50-129">You can edit the contents of the KB on this page.</span></span>

10. <span data-ttu-id="aef50-130">In the upper right, select **Add QnA pair** to add a new row in the **Editorial** section of the KB.</span><span class="sxs-lookup"><span data-stu-id="aef50-130">In the upper right, select **Add QnA pair** to add a new row in the **Editorial** section of the KB.</span></span> <span data-ttu-id="aef50-131">Under **Question**, enter **Hi.**</span><span class="sxs-lookup"><span data-stu-id="aef50-131">Under **Question**, enter **Hi.**</span></span> <span data-ttu-id="aef50-132">Under **Answer**, enter **Hello. Ask me bitlocker questions.**</span><span class="sxs-lookup"><span data-stu-id="aef50-132">Under **Answer**, enter **Hello. Ask me bitlocker questions.**</span></span>

   ![Add a QnA pair](../media/qnamaker-quickstart-kb/add-qna-pair.png)

11. <span data-ttu-id="aef50-134">In the upper right, select **Save and train** to save your edits and train the QnA Maker model.</span><span class="sxs-lookup"><span data-stu-id="aef50-134">In the upper right, select **Save and train** to save your edits and train the QnA Maker model.</span></span> <span data-ttu-id="aef50-135">Edits aren't kept unless they're saved.</span><span class="sxs-lookup"><span data-stu-id="aef50-135">Edits aren't kept unless they're saved.</span></span>

   ![Save and train](../media/qnamaker-quickstart-kb/add-qna-pair2.png)

12. <span data-ttu-id="aef50-137">In the upper right, select **Test** to test that the changes you made took effect.</span><span class="sxs-lookup"><span data-stu-id="aef50-137">In the upper right, select **Test** to test that the changes you made took effect.</span></span> <span data-ttu-id="aef50-138">Enter **hi there** in the box, and select Enter.</span><span class="sxs-lookup"><span data-stu-id="aef50-138">Enter **hi there** in the box, and select Enter.</span></span> <span data-ttu-id="aef50-139">You should see the answer you created as a response.</span><span class="sxs-lookup"><span data-stu-id="aef50-139">You should see the answer you created as a response.</span></span>

13. <span data-ttu-id="aef50-140">Select **Inspect** to examine the response in more detail.</span><span class="sxs-lookup"><span data-stu-id="aef50-140">Select **Inspect** to examine the response in more detail.</span></span> <span data-ttu-id="aef50-141">The test window is used to test your changes to the KB before they're published.</span><span class="sxs-lookup"><span data-stu-id="aef50-141">The test window is used to test your changes to the KB before they're published.</span></span>

   ![Test Panel](../media/qnamaker-quickstart-kb/inspect-panel.png)

14. <span data-ttu-id="aef50-143">Select **Test** again to close the **Test** pop-up.</span><span class="sxs-lookup"><span data-stu-id="aef50-143">Select **Test** again to close the **Test** pop-up.</span></span>

15. <span data-ttu-id="aef50-144">In the menu next to **Edit**, select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="aef50-144">In the menu next to **Edit**, select **Publish**.</span></span> <span data-ttu-id="aef50-145">Then to confirm, select **Publish** on the page.</span><span class="sxs-lookup"><span data-stu-id="aef50-145">Then to confirm, select **Publish** on the page.</span></span>

16. <span data-ttu-id="aef50-146">The QnA Maker service is now successfully published.</span><span class="sxs-lookup"><span data-stu-id="aef50-146">The QnA Maker service is now successfully published.</span></span> <span data-ttu-id="aef50-147">You can use the endpoint in your application or bot code.</span><span class="sxs-lookup"><span data-stu-id="aef50-147">You can use the endpoint in your application or bot code.</span></span>

   ![Publish](../media/qnamaker-quickstart-kb/publish-sucess.png)

## <a name="next-steps"></a><span data-ttu-id="aef50-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="aef50-149">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="aef50-150">Create a knowledge base</span><span class="sxs-lookup"><span data-stu-id="aef50-150">Create a knowledge base</span></span>](../How-To/create-knowledge-base.md)
