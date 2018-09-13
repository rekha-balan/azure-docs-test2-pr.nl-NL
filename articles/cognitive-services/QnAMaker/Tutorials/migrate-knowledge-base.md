---
title: How to import a knowledge base - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: How to import a knowledge base
services: cognitive-services
author: nstulasi
manager: sangitap
ms.service: cognitive-services
ms.component: QnAMaker
ms.topic: article
ms.date: 04/21/2018
ms.author: saneppal
ms.openlocfilehash: ce8f98f9bdb37d5f326e942fe5b5e815e5272c56
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865579"
---
# <a name="migrate-a-knowledge-base-using-export-import"></a><span data-ttu-id="65224-103">Migrate a knowledge base using export-import</span><span class="sxs-lookup"><span data-stu-id="65224-103">Migrate a knowledge base using export-import</span></span>
<span data-ttu-id="65224-104">QnA Maker announced General Availability on May 7, 2018 at the \\\build\ conference.</span><span class="sxs-lookup"><span data-stu-id="65224-104">QnA Maker announced General Availability on May 7, 2018 at the \\\build\ conference.</span></span> <span data-ttu-id="65224-105">QnA Maker GA has a new architecture built on Azure.</span><span class="sxs-lookup"><span data-stu-id="65224-105">QnA Maker GA has a new architecture built on Azure.</span></span> <span data-ttu-id="65224-106">Knowledge bases created with QnA Maker Free Preview will need to be migrated to QnA Maker GA.</span><span class="sxs-lookup"><span data-stu-id="65224-106">Knowledge bases created with QnA Maker Free Preview will need to be migrated to QnA Maker GA.</span></span> <span data-ttu-id="65224-107">QnA Maker Preview will be deprecated in November 2018.</span><span class="sxs-lookup"><span data-stu-id="65224-107">QnA Maker Preview will be deprecated in November 2018.</span></span> <span data-ttu-id="65224-108">For more information about the changes in QnA Maker GA, see the QnA Maker GA announcement [blog post](https://aka.ms/qnamakerga-blog).</span><span class="sxs-lookup"><span data-stu-id="65224-108">For more information about the changes in QnA Maker GA, see the QnA Maker GA announcement [blog post](https://aka.ms/qnamakerga-blog).</span></span>

<span data-ttu-id="65224-109">QnA Maker now has a [pricing model](https://azure.microsoft.com/en-us/pricing/details/cognitive-services/qna-maker/).</span><span class="sxs-lookup"><span data-stu-id="65224-109">QnA Maker now has a [pricing model](https://azure.microsoft.com/en-us/pricing/details/cognitive-services/qna-maker/).</span></span>

<span data-ttu-id="65224-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="65224-110">Prerequisites</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="65224-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="65224-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>
> * <span data-ttu-id="65224-112">Setup a new [QnA Maker service](../How-To/set-up-qnamaker-service-azure.md)</span><span class="sxs-lookup"><span data-stu-id="65224-112">Setup a new [QnA Maker service](../How-To/set-up-qnamaker-service-azure.md)</span></span>

## <a name="migrate-a-knowledge-base-from-qna-maker-preview-portal"></a><span data-ttu-id="65224-113">Migrate a knowledge base from QnA Maker Preview portal</span><span class="sxs-lookup"><span data-stu-id="65224-113">Migrate a knowledge base from QnA Maker Preview portal</span></span>
1. <span data-ttu-id="65224-114">Navigate to [QnA Maker Preview portal](https://aka.ms/qnamaker-old-portal
) and click on **My services**.</span><span class="sxs-lookup"><span data-stu-id="65224-114">Navigate to [QnA Maker Preview portal](https://aka.ms/qnamaker-old-portal
) and click on **My services**.</span></span>
2. <span data-ttu-id="65224-115">Select the knowledge base you want to migrate by clicking on the edit icon.</span><span class="sxs-lookup"><span data-stu-id="65224-115">Select the knowledge base you want to migrate by clicking on the edit icon.</span></span>

    ![Edit knowledge base](../media/qnamaker-how-to-migrate-kb/preview-editkb.png)

3. <span data-ttu-id="65224-117">Click on **Download knowledge base** to download a .tsv file that contains the content of your knowledge base - questions, answers, metadata, and the data source names from which they were extracted.</span><span class="sxs-lookup"><span data-stu-id="65224-117">Click on **Download knowledge base** to download a .tsv file that contains the content of your knowledge base - questions, answers, metadata, and the data source names from which they were extracted.</span></span>

    ![Download knowledge base](../media/qnamaker-how-to-migrate-kb/preview-download.png)

4. <span data-ttu-id="65224-119">Sign into to the [QnA Maker portal](https://qnamaker.ai) with your azure credentials and click on **Create new service**.</span><span class="sxs-lookup"><span data-stu-id="65224-119">Sign into to the [QnA Maker portal](https://qnamaker.ai) with your azure credentials and click on **Create new service**.</span></span>

    ![<span data-ttu-id="65224-120">Create KB</span><span class="sxs-lookup"><span data-stu-id="65224-120">Create KB</span></span> ](../media/qnamaker-how-to-create-kb/create-new-service.png)
    
5. <span data-ttu-id="65224-121">If you have not already created a QnA Maker service, select **Create a QnA service**.</span><span class="sxs-lookup"><span data-stu-id="65224-121">If you have not already created a QnA Maker service, select **Create a QnA service**.</span></span> <span data-ttu-id="65224-122">Otherwise, choose a QnA Maker service from the drop-downs in Step 2.</span><span class="sxs-lookup"><span data-stu-id="65224-122">Otherwise, choose a QnA Maker service from the drop-downs in Step 2.</span></span> <span data-ttu-id="65224-123">Select the QnA Maker service that will host the Knowledge Base.</span><span class="sxs-lookup"><span data-stu-id="65224-123">Select the QnA Maker service that will host the Knowledge Base.</span></span>

    ![Setup QnA service](../media/qnamaker-how-to-create-kb/setup-qna-resource.png)

6. <span data-ttu-id="65224-125">Create an empty knowledge base</span><span class="sxs-lookup"><span data-stu-id="65224-125">Create an empty knowledge base</span></span> 

    ![Set data sources](../media/qnamaker-how-to-create-kb/set-data-sources.png)

    - <span data-ttu-id="65224-127">Give your service a **name.**</span><span class="sxs-lookup"><span data-stu-id="65224-127">Give your service a **name.**</span></span> <span data-ttu-id="65224-128">Duplicate names are supported and special characters are supported as well.</span><span class="sxs-lookup"><span data-stu-id="65224-128">Duplicate names are supported and special characters are supported as well.</span></span>
    - <span data-ttu-id="65224-129">Skip uploading files or URLs as you want to use the data from your Preview knowledge base.</span><span class="sxs-lookup"><span data-stu-id="65224-129">Skip uploading files or URLs as you want to use the data from your Preview knowledge base.</span></span> <span data-ttu-id="65224-130">For now, you will create an empty knowledge base.</span><span class="sxs-lookup"><span data-stu-id="65224-130">For now, you will create an empty knowledge base.</span></span>

7. <span data-ttu-id="65224-131">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="65224-131">Select **Create**.</span></span>

    ![Create KB](../media/qnamaker-how-to-create-kb/create-kb.png)

8. <span data-ttu-id="65224-133">In this new Knowledge base, open the **Settings** tab and click on **Import knowledge base**.</span><span class="sxs-lookup"><span data-stu-id="65224-133">In this new Knowledge base, open the **Settings** tab and click on **Import knowledge base**.</span></span> <span data-ttu-id="65224-134">This imports the questions, answers, and metadata, and retains the data source names from which they were extracted.</span><span class="sxs-lookup"><span data-stu-id="65224-134">This imports the questions, answers, and metadata, and retains the data source names from which they were extracted.</span></span>

   ![Import knowledge base](../media/qnamaker-how-to-migrate-kb/Import.png)

9. <span data-ttu-id="65224-136">**Test** the new knowledge base using the Test panel.</span><span class="sxs-lookup"><span data-stu-id="65224-136">**Test** the new knowledge base using the Test panel.</span></span> <span data-ttu-id="65224-137">Learn how to [test your knowledge base](../How-To/test-knowledge-base.md).</span><span class="sxs-lookup"><span data-stu-id="65224-137">Learn how to [test your knowledge base](../How-To/test-knowledge-base.md).</span></span>
10. <span data-ttu-id="65224-138">**Publish** the knowledge base.</span><span class="sxs-lookup"><span data-stu-id="65224-138">**Publish** the knowledge base.</span></span> <span data-ttu-id="65224-139">Learn how to [publish your knowledge base](../How-To/publish-knowledge-base.md).</span><span class="sxs-lookup"><span data-stu-id="65224-139">Learn how to [publish your knowledge base](../How-To/publish-knowledge-base.md).</span></span>
11. <span data-ttu-id="65224-140">Use the endpoint below in your application or bot code.</span><span class="sxs-lookup"><span data-stu-id="65224-140">Use the endpoint below in your application or bot code.</span></span> <span data-ttu-id="65224-141">See here how to [create a QnA bot](../Tutorials/create-qna-bot.md).</span><span class="sxs-lookup"><span data-stu-id="65224-141">See here how to [create a QnA bot](../Tutorials/create-qna-bot.md).</span></span>

    ![QnA Maker values](../media/qnamaker-tutorials-create-bot/qnamaker-settings-kbid-key.PNG)

<span data-ttu-id="65224-143">At this point, all the knowledge base content - questions, answers and metadata, along with the names of the source files and the URLs, are imported to the new knowledge base.</span><span class="sxs-lookup"><span data-stu-id="65224-143">At this point, all the knowledge base content - questions, answers and metadata, along with the names of the source files and the URLs, are imported to the new knowledge base.</span></span> 

## <a name="chatlogs-and-alterations"></a><span data-ttu-id="65224-144">Chatlogs and alterations</span><span class="sxs-lookup"><span data-stu-id="65224-144">Chatlogs and alterations</span></span>
<span data-ttu-id="65224-145">Alterations (synonyms) are not imported automatically.</span><span class="sxs-lookup"><span data-stu-id="65224-145">Alterations (synonyms) are not imported automatically.</span></span> <span data-ttu-id="65224-146">Use the [V2 APIs](https://aka.ms/qnamaker-v2-apis) to export the alterations from the preview stack and the [V4 APIs](https://aka.ms/qnamaker-v4-apis) to replace in the new stack.</span><span class="sxs-lookup"><span data-stu-id="65224-146">Use the [V2 APIs](https://aka.ms/qnamaker-v2-apis) to export the alterations from the preview stack and the [V4 APIs](https://aka.ms/qnamaker-v4-apis) to replace in the new stack.</span></span>

<span data-ttu-id="65224-147">There is no way to migrate chatlogs, since the new stack uses Application Insights for storing chatlogs.</span><span class="sxs-lookup"><span data-stu-id="65224-147">There is no way to migrate chatlogs, since the new stack uses Application Insights for storing chatlogs.</span></span> <span data-ttu-id="65224-148">You can however download the chatlogs from the [preview portal](https://aka.ms/qnamaker-old-portal).</span><span class="sxs-lookup"><span data-stu-id="65224-148">You can however download the chatlogs from the [preview portal](https://aka.ms/qnamaker-old-portal).</span></span>

## <a name="next-steps"></a><span data-ttu-id="65224-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="65224-149">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="65224-150">Edit a knowledge base</span><span class="sxs-lookup"><span data-stu-id="65224-150">Edit a knowledge base</span></span>](../How-To/edit-knowledge-base.md)
