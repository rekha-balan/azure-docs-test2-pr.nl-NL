---
title: Create a QnA bot with Azure Bot Service - Azure Cognitive Services | Microsoft Docs
services: cognitive-services
author: nstulasi
manager: sangitap
ms.service: cognitive-services
ms.component: QnAMaker
ms.topic: article
ms.date: 05/07/2018
ms.author: saneppal
ms.openlocfilehash: fc430bf3aa7cad279d7a93bb6892aa19abee3378
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857846"
---
# <a name="create-a-qna-bot-with-azure-bot-service"></a><span data-ttu-id="43208-102">Create a QnA Bot with Azure Bot Service</span><span class="sxs-lookup"><span data-stu-id="43208-102">Create a QnA Bot with Azure Bot Service</span></span>
<span data-ttu-id="43208-103">This tutorial walks you through building a QnA bot with Azure Bot service on the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="43208-103">This tutorial walks you through building a QnA bot with Azure Bot service on the Azure portal.</span></span>

## <a name="prerequisite"></a><span data-ttu-id="43208-104">Prerequisite</span><span class="sxs-lookup"><span data-stu-id="43208-104">Prerequisite</span></span>
<span data-ttu-id="43208-105">Before you build, follow the steps in [Create a knowledge base](../How-To/create-knowledge-base.md) to create a QnA Maker service with questions and answers.</span><span class="sxs-lookup"><span data-stu-id="43208-105">Before you build, follow the steps in [Create a knowledge base](../How-To/create-knowledge-base.md) to create a QnA Maker service with questions and answers.</span></span>

<span data-ttu-id="43208-106">The bot responds to questions from the knowledge base you created, via the QnAMakerDialog.</span><span class="sxs-lookup"><span data-stu-id="43208-106">The bot responds to questions from the knowledge base you created, via the QnAMakerDialog.</span></span>

## <a name="create-a-qna-bot"></a><span data-ttu-id="43208-107">Create a QnA Bot</span><span class="sxs-lookup"><span data-stu-id="43208-107">Create a QnA Bot</span></span>
1. <span data-ttu-id="43208-108">In the [Azure portal](https://portal.azure.com), select **Create** new resource in the menu blade, and then select **See all**.</span><span class="sxs-lookup"><span data-stu-id="43208-108">In the [Azure portal](https://portal.azure.com), select **Create** new resource in the menu blade, and then select **See all**.</span></span>

    ![bot service creation](../media/qnamaker-tutorials-create-bot/bot-service-creation.png)

2. <span data-ttu-id="43208-110">In the search box, search for **Web App Bot**.</span><span class="sxs-lookup"><span data-stu-id="43208-110">In the search box, search for **Web App Bot**.</span></span>

    ![bot service selection](../media/qnamaker-tutorials-create-bot/bot-service-selection.png)

3. <span data-ttu-id="43208-112">In the **Bot Service blade**, provide the required information, and select **Create**.</span><span class="sxs-lookup"><span data-stu-id="43208-112">In the **Bot Service blade**, provide the required information, and select **Create**.</span></span> <span data-ttu-id="43208-113">This creates and deploys the bot service with QnAMakerDialog to Azure.</span><span class="sxs-lookup"><span data-stu-id="43208-113">This creates and deploys the bot service with QnAMakerDialog to Azure.</span></span>

    - <span data-ttu-id="43208-114">Set **App name** to your bot’s name.</span><span class="sxs-lookup"><span data-stu-id="43208-114">Set **App name** to your bot’s name.</span></span> <span data-ttu-id="43208-115">The name is used as the subdomain when your bot is deployed to the cloud (for example, mynotesbot.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="43208-115">The name is used as the subdomain when your bot is deployed to the cloud (for example, mynotesbot.azurewebsites.net).</span></span>
    - <span data-ttu-id="43208-116">Select the subscription, resource group, App service plan, and location.</span><span class="sxs-lookup"><span data-stu-id="43208-116">Select the subscription, resource group, App service plan, and location.</span></span>
    - <span data-ttu-id="43208-117">Select the **Question and Answer** (Node.js or C#) template for the Bot template field.</span><span class="sxs-lookup"><span data-stu-id="43208-117">Select the **Question and Answer** (Node.js or C#) template for the Bot template field.</span></span>
    - <span data-ttu-id="43208-118">Select the confirmation checkbox for the legal notice.</span><span class="sxs-lookup"><span data-stu-id="43208-118">Select the confirmation checkbox for the legal notice.</span></span> <span data-ttu-id="43208-119">The terms of the legal notice are below the checkbox.</span><span class="sxs-lookup"><span data-stu-id="43208-119">The terms of the legal notice are below the checkbox.</span></span>

        ![bot service selection](../media/qnamaker-tutorials-create-bot/bot-service-qna-template.PNG)

4. <span data-ttu-id="43208-121">Confirm that the bot service has been deployed.</span><span class="sxs-lookup"><span data-stu-id="43208-121">Confirm that the bot service has been deployed.</span></span>

    - <span data-ttu-id="43208-122">Select **Notifications** (the bell icon that is located along the top edge of the Azure portal).</span><span class="sxs-lookup"><span data-stu-id="43208-122">Select **Notifications** (the bell icon that is located along the top edge of the Azure portal).</span></span> <span data-ttu-id="43208-123">The notification will change from **Deployment started** to **Deployment succeeded**.</span><span class="sxs-lookup"><span data-stu-id="43208-123">The notification will change from **Deployment started** to **Deployment succeeded**.</span></span>
    - <span data-ttu-id="43208-124">After the notification changes to **Deployment succeeded**, select **Go to resource** on that notification.</span><span class="sxs-lookup"><span data-stu-id="43208-124">After the notification changes to **Deployment succeeded**, select **Go to resource** on that notification.</span></span>

## <a name="chat-with-the-bot"></a><span data-ttu-id="43208-125">Chat with the Bot</span><span class="sxs-lookup"><span data-stu-id="43208-125">Chat with the Bot</span></span>
<span data-ttu-id="43208-126">Selecting **Go to resource** takes you to the bot's resource blade.</span><span class="sxs-lookup"><span data-stu-id="43208-126">Selecting **Go to resource** takes you to the bot's resource blade.</span></span>

<span data-ttu-id="43208-127">Once the bot is registered, click **Test in Web Chat** to open the Web Chat pane.</span><span class="sxs-lookup"><span data-stu-id="43208-127">Once the bot is registered, click **Test in Web Chat** to open the Web Chat pane.</span></span> <span data-ttu-id="43208-128">Type "hello" in Web Chat.</span><span class="sxs-lookup"><span data-stu-id="43208-128">Type "hello" in Web Chat.</span></span>

![QnA bot web chat](../media/qnamaker-tutorials-create-bot/qna-bot-web-chat.PNG)

<span data-ttu-id="43208-130">The bot responds with "Please set QnAKnowledgebaseId and QnASubscriptionKey in App Settings.</span><span class="sxs-lookup"><span data-stu-id="43208-130">The bot responds with "Please set QnAKnowledgebaseId and QnASubscriptionKey in App Settings.</span></span> <span data-ttu-id="43208-131">Learn how to get them at https://aka.ms/qnaabssetup".</span><span class="sxs-lookup"><span data-stu-id="43208-131">Learn how to get them at https://aka.ms/qnaabssetup".</span></span> <span data-ttu-id="43208-132">This response confirms that your QnA Bot has received the message, but there is no QnA Maker knowledge base associated with it yet.</span><span class="sxs-lookup"><span data-stu-id="43208-132">This response confirms that your QnA Bot has received the message, but there is no QnA Maker knowledge base associated with it yet.</span></span> <span data-ttu-id="43208-133">Do that in the next step.</span><span class="sxs-lookup"><span data-stu-id="43208-133">Do that in the next step.</span></span>

## <a name="connect-your-qna-maker-knowledge-base-to-the-bot"></a><span data-ttu-id="43208-134">Connect your QnA Maker knowledge base to the bot</span><span class="sxs-lookup"><span data-stu-id="43208-134">Connect your QnA Maker knowledge base to the bot</span></span>

1. <span data-ttu-id="43208-135">Open **Application Settings** and edit the **QnAKnowledgebaseId**, **QnAAuthKey**, and the **QnAEndpointHostName** fields to contain the values of your QnA Maker knowledge base.</span><span class="sxs-lookup"><span data-stu-id="43208-135">Open **Application Settings** and edit the **QnAKnowledgebaseId**, **QnAAuthKey**, and the **QnAEndpointHostName** fields to contain the values of your QnA Maker knowledge base.</span></span>

    ![app settings](../media/qnamaker-tutorials-create-bot/application-settings.PNG)

2. <span data-ttu-id="43208-137">Get your knowledge base ID, host url, and the endpoint key from the settings tab of your knowledge base in https://qnamaker.ai.</span><span class="sxs-lookup"><span data-stu-id="43208-137">Get your knowledge base ID, host url, and the endpoint key from the settings tab of your knowledge base in https://qnamaker.ai.</span></span>
    - <span data-ttu-id="43208-138">Log in to [QnA Maker](https://qnamaker.ai)</span><span class="sxs-lookup"><span data-stu-id="43208-138">Log in to [QnA Maker](https://qnamaker.ai)</span></span>
    - <span data-ttu-id="43208-139">Go to your knowledge base</span><span class="sxs-lookup"><span data-stu-id="43208-139">Go to your knowledge base</span></span>
    - <span data-ttu-id="43208-140">Click on the **Settings** tab</span><span class="sxs-lookup"><span data-stu-id="43208-140">Click on the **Settings** tab</span></span>
    - <span data-ttu-id="43208-141">**Publish** your knowledge base, if not already done so</span><span class="sxs-lookup"><span data-stu-id="43208-141">**Publish** your knowledge base, if not already done so</span></span>

    ![QnA Maker values](../media/qnamaker-tutorials-create-bot/qnamaker-settings-kbid-key.PNG)

> [!NOTE]
> <span data-ttu-id="43208-143">If you want to connect the preview version of the knowledge base with the QnA bot, set the value of **Ocp-Apim-Subscription-Key** to **QnAAuthKey**.</span><span class="sxs-lookup"><span data-stu-id="43208-143">If you want to connect the preview version of the knowledge base with the QnA bot, set the value of **Ocp-Apim-Subscription-Key** to **QnAAuthKey**.</span></span> <span data-ttu-id="43208-144">Leave the **QnAEndpointHostName** empty.</span><span class="sxs-lookup"><span data-stu-id="43208-144">Leave the **QnAEndpointHostName** empty.</span></span>

## <a name="test-the-bot"></a><span data-ttu-id="43208-145">Test the bot</span><span class="sxs-lookup"><span data-stu-id="43208-145">Test the bot</span></span>
<span data-ttu-id="43208-146">In the Azure portal, click on **Test in Web Chat** to test the bot.</span><span class="sxs-lookup"><span data-stu-id="43208-146">In the Azure portal, click on **Test in Web Chat** to test the bot.</span></span> 

![QnA Maker bot](../media/qnamaker-tutorials-create-bot/qna-bot-web-chat-response.PNG)

<span data-ttu-id="43208-148">Your QnA Bot now answers from your knowledge base.</span><span class="sxs-lookup"><span data-stu-id="43208-148">Your QnA Bot now answers from your knowledge base.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43208-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="43208-149">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="43208-150">Integrate QnA Maker and LUIS</span><span class="sxs-lookup"><span data-stu-id="43208-150">Integrate QnA Maker and LUIS</span></span>](./integrate-qnamaker-luis.md)

## <a name="see-also"></a><span data-ttu-id="43208-151">See also</span><span class="sxs-lookup"><span data-stu-id="43208-151">See also</span></span>

- [<span data-ttu-id="43208-152">Manage your knowledge base</span><span class="sxs-lookup"><span data-stu-id="43208-152">Manage your knowledge base</span></span>](https://qnamaker.ai)
- [<span data-ttu-id="43208-153">Enable your bot in different channels</span><span class="sxs-lookup"><span data-stu-id="43208-153">Enable your bot in different channels</span></span>](https://docs.microsoft.com/azure/bot-service/bot-service-manage-channels)
