---
title: Connect to Twilio from Azure Logic Apps | Microsoft Docs
description: Automate tasks and workflows that manage global SMS, MMS, and IP messages through your Twilio account by using Azure Logic Apps
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: ecfan
ms.author: estfan
ms.reviewer: klam, LADocs
ms.assetid: 43116187-4a2f-42e5-9852-a0d62f08c5fc
ms.topic: article
tags: connectors
ms.date: 08/25/2018
ms.openlocfilehash: db7677042737ea1377af54cc02ee1c82c05435c8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44793447"
---
# <a name="manage-messages-in-twilio-with-azure-logic-apps"></a><span data-ttu-id="fbdef-103">Manage messages in Twilio with Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="fbdef-103">Manage messages in Twilio with Azure Logic Apps</span></span>

<span data-ttu-id="fbdef-104">With Azure Logic Apps and the Twilio connector, you can create automated tasks and workflows that get, send, and list messages in Twilio, which include global SMS, MMS, and IP messages.</span><span class="sxs-lookup"><span data-stu-id="fbdef-104">With Azure Logic Apps and the Twilio connector, you can create automated tasks and workflows that get, send, and list messages in Twilio, which include global SMS, MMS, and IP messages.</span></span> <span data-ttu-id="fbdef-105">You can use these actions to perform tasks with your Twilio account.</span><span class="sxs-lookup"><span data-stu-id="fbdef-105">You can use these actions to perform tasks with your Twilio account.</span></span> <span data-ttu-id="fbdef-106">You can also have other actions use the output from Twilio actions.</span><span class="sxs-lookup"><span data-stu-id="fbdef-106">You can also have other actions use the output from Twilio actions.</span></span> <span data-ttu-id="fbdef-107">For example, when a new message arrives, you can send the message content with the Slack connector.</span><span class="sxs-lookup"><span data-stu-id="fbdef-107">For example, when a new message arrives, you can send the message content with the Slack connector.</span></span> <span data-ttu-id="fbdef-108">If you're new to logic apps, review [What is Azure Logic Apps?](../logic-apps/logic-apps-overview.md)</span><span class="sxs-lookup"><span data-stu-id="fbdef-108">If you're new to logic apps, review [What is Azure Logic Apps?](../logic-apps/logic-apps-overview.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fbdef-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fbdef-109">Prerequisites</span></span>

* <span data-ttu-id="fbdef-110">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="fbdef-110">An Azure subscription.</span></span> <span data-ttu-id="fbdef-111">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span><span class="sxs-lookup"><span data-stu-id="fbdef-111">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span></span> 

* <span data-ttu-id="fbdef-112">From [Twilio](https://www.twilio.com/):</span><span class="sxs-lookup"><span data-stu-id="fbdef-112">From [Twilio](https://www.twilio.com/):</span></span> 

  * <span data-ttu-id="fbdef-113">Your Twilio account ID and [authentication token](https://support.twilio.com/hc/en-us/articles/223136027-Auth-Tokens-and-How-to-Change-Them), which you can find on your Twilio dashboard</span><span class="sxs-lookup"><span data-stu-id="fbdef-113">Your Twilio account ID and [authentication token](https://support.twilio.com/hc/en-us/articles/223136027-Auth-Tokens-and-How-to-Change-Them), which you can find on your Twilio dashboard</span></span>

    <span data-ttu-id="fbdef-114">Your credentials authorize your logic app to create a connection and access your Twilio account from your logic app.</span><span class="sxs-lookup"><span data-stu-id="fbdef-114">Your credentials authorize your logic app to create a connection and access your Twilio account from your logic app.</span></span> 
    <span data-ttu-id="fbdef-115">If you're using a Twilio trial account, you can send SMS only to *verified* phone numbers.</span><span class="sxs-lookup"><span data-stu-id="fbdef-115">If you're using a Twilio trial account, you can send SMS only to *verified* phone numbers.</span></span>

  * <span data-ttu-id="fbdef-116">A verified Twilio phone number that can send SMS</span><span class="sxs-lookup"><span data-stu-id="fbdef-116">A verified Twilio phone number that can send SMS</span></span>

  * <span data-ttu-id="fbdef-117">A verified Twilio phone number that can receive SMS</span><span class="sxs-lookup"><span data-stu-id="fbdef-117">A verified Twilio phone number that can receive SMS</span></span>

* <span data-ttu-id="fbdef-118">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span><span class="sxs-lookup"><span data-stu-id="fbdef-118">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span></span>

* <span data-ttu-id="fbdef-119">The logic app where you want to access your Twilio account.</span><span class="sxs-lookup"><span data-stu-id="fbdef-119">The logic app where you want to access your Twilio account.</span></span> <span data-ttu-id="fbdef-120">To use a Twilio action, start your logic app with another trigger, for example, the **Recurrence** trigger.</span><span class="sxs-lookup"><span data-stu-id="fbdef-120">To use a Twilio action, start your logic app with another trigger, for example, the **Recurrence** trigger.</span></span>

## <a name="connect-to-twilio"></a><span data-ttu-id="fbdef-121">Connect to Twilio</span><span class="sxs-lookup"><span data-stu-id="fbdef-121">Connect to Twilio</span></span>

[!INCLUDE [Create connection general intro](../../includes/connectors-create-connection-general-intro.md)]

1. <span data-ttu-id="fbdef-122">Sign in to the [Azure portal](https://portal.azure.com), and open your logic app in Logic App Designer, if not open already.</span><span class="sxs-lookup"><span data-stu-id="fbdef-122">Sign in to the [Azure portal](https://portal.azure.com), and open your logic app in Logic App Designer, if not open already.</span></span>

1. <span data-ttu-id="fbdef-123">Choose a path:</span><span class="sxs-lookup"><span data-stu-id="fbdef-123">Choose a path:</span></span> 

     * <span data-ttu-id="fbdef-124">Under the last step where you want to add an action, choose **New step**.</span><span class="sxs-lookup"><span data-stu-id="fbdef-124">Under the last step where you want to add an action, choose **New step**.</span></span> 

       <span data-ttu-id="fbdef-125">-or-</span><span class="sxs-lookup"><span data-stu-id="fbdef-125">-or-</span></span>

     * <span data-ttu-id="fbdef-126">Between the steps where you want to add an action, move your pointer over the arrow between steps.</span><span class="sxs-lookup"><span data-stu-id="fbdef-126">Between the steps where you want to add an action, move your pointer over the arrow between steps.</span></span> 
     <span data-ttu-id="fbdef-127">Choose the plus sign (**+**) that appears, and then select **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="fbdef-127">Choose the plus sign (**+**) that appears, and then select **Add an action**.</span></span>
     
       <span data-ttu-id="fbdef-128">In the search box, enter "twilio" as your filter.</span><span class="sxs-lookup"><span data-stu-id="fbdef-128">In the search box, enter "twilio" as your filter.</span></span> 
       <span data-ttu-id="fbdef-129">Under the actions list, select the action you want.</span><span class="sxs-lookup"><span data-stu-id="fbdef-129">Under the actions list, select the action you want.</span></span>

1. <span data-ttu-id="fbdef-130">Provide the necessary details for your connection, and then choose **Create**:</span><span class="sxs-lookup"><span data-stu-id="fbdef-130">Provide the necessary details for your connection, and then choose **Create**:</span></span>

   * <span data-ttu-id="fbdef-131">The name to use for your connection</span><span class="sxs-lookup"><span data-stu-id="fbdef-131">The name to use for your connection</span></span>
   * <span data-ttu-id="fbdef-132">Your Twilio account ID</span><span class="sxs-lookup"><span data-stu-id="fbdef-132">Your Twilio account ID</span></span> 
   * <span data-ttu-id="fbdef-133">Your Twilio access (authentication) token</span><span class="sxs-lookup"><span data-stu-id="fbdef-133">Your Twilio access (authentication) token</span></span>

1. <span data-ttu-id="fbdef-134">Provide the necessary details for your selected action and continue building your logic app's workflow.</span><span class="sxs-lookup"><span data-stu-id="fbdef-134">Provide the necessary details for your selected action and continue building your logic app's workflow.</span></span>

## <a name="connector-reference"></a><span data-ttu-id="fbdef-135">Connector reference</span><span class="sxs-lookup"><span data-stu-id="fbdef-135">Connector reference</span></span>

<span data-ttu-id="fbdef-136">For technical details about triggers, actions, and limits, which are described by the connector's OpenAPI (formerly Swagger) description, review the connector's [reference page](/connectors/twilio/).</span><span class="sxs-lookup"><span data-stu-id="fbdef-136">For technical details about triggers, actions, and limits, which are described by the connector's OpenAPI (formerly Swagger) description, review the connector's [reference page](/connectors/twilio/).</span></span>

## <a name="get-support"></a><span data-ttu-id="fbdef-137">Get support</span><span class="sxs-lookup"><span data-stu-id="fbdef-137">Get support</span></span>

* <span data-ttu-id="fbdef-138">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="fbdef-138">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>
* <span data-ttu-id="fbdef-139">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="fbdef-139">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fbdef-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="fbdef-140">Next steps</span></span>

* <span data-ttu-id="fbdef-141">Learn about other [Logic Apps connectors](../connectors/apis-list.md)</span><span class="sxs-lookup"><span data-stu-id="fbdef-141">Learn about other [Logic Apps connectors](../connectors/apis-list.md)</span></span>