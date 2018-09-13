---
title: Connect to Slack from Azure Logic Apps | Microsoft Docs
description: Automate tasks and workflows that monitor files and manage channels, groups, and messages in your Slack account by using Azure Logic Apps
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: ecfan
ms.author: estfan
ms.reviewer: klam, LADocs
ms.assetid: 234cad64-b13d-4494-ae78-18b17119ba24
ms.topic: article
tags: connectors
ms.date: 08/25/2018
ms.openlocfilehash: 7af2db528866d687064e854e00e43e81d2601b2b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44783892"
---
# <a name="monitor-and-manage-slack-with-azure-logic-apps"></a><span data-ttu-id="d3f81-103">Monitor and manage Slack with Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="d3f81-103">Monitor and manage Slack with Azure Logic Apps</span></span>

<span data-ttu-id="d3f81-104">With Azure Logic Apps and the Slack connector, you can create automated tasks and workflows that monitor your Slack files and manage your Slack channels, messages, groups, and so on, for example:</span><span class="sxs-lookup"><span data-stu-id="d3f81-104">With Azure Logic Apps and the Slack connector, you can create automated tasks and workflows that monitor your Slack files and manage your Slack channels, messages, groups, and so on, for example:</span></span>

* <span data-ttu-id="d3f81-105">Monitor when new files are created.</span><span class="sxs-lookup"><span data-stu-id="d3f81-105">Monitor when new files are created.</span></span>
* <span data-ttu-id="d3f81-106">Create, list, and join channels</span><span class="sxs-lookup"><span data-stu-id="d3f81-106">Create, list, and join channels</span></span> 
* <span data-ttu-id="d3f81-107">Post messages.</span><span class="sxs-lookup"><span data-stu-id="d3f81-107">Post messages.</span></span>
* <span data-ttu-id="d3f81-108">Create groups and set do not disturb.</span><span class="sxs-lookup"><span data-stu-id="d3f81-108">Create groups and set do not disturb.</span></span>

<span data-ttu-id="d3f81-109">You can use triggers that get responses from your Slack account and make the output available to other actions.</span><span class="sxs-lookup"><span data-stu-id="d3f81-109">You can use triggers that get responses from your Slack account and make the output available to other actions.</span></span> <span data-ttu-id="d3f81-110">You can use actions that perform tasks with your Slack account.</span><span class="sxs-lookup"><span data-stu-id="d3f81-110">You can use actions that perform tasks with your Slack account.</span></span> <span data-ttu-id="d3f81-111">You can also have other actions use the output from Slack actions.</span><span class="sxs-lookup"><span data-stu-id="d3f81-111">You can also have other actions use the output from Slack actions.</span></span> <span data-ttu-id="d3f81-112">For example, when a new file is created, you can send email with the Office 365 Outlook connector.</span><span class="sxs-lookup"><span data-stu-id="d3f81-112">For example, when a new file is created, you can send email with the Office 365 Outlook connector.</span></span> <span data-ttu-id="d3f81-113">If you're new to logic apps, review [What is Azure Logic Apps?](../logic-apps/logic-apps-overview.md)</span><span class="sxs-lookup"><span data-stu-id="d3f81-113">If you're new to logic apps, review [What is Azure Logic Apps?](../logic-apps/logic-apps-overview.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3f81-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d3f81-114">Prerequisites</span></span>

* <span data-ttu-id="d3f81-115">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="d3f81-115">An Azure subscription.</span></span> <span data-ttu-id="d3f81-116">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span><span class="sxs-lookup"><span data-stu-id="d3f81-116">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span></span> 

* <span data-ttu-id="d3f81-117">Your [Slack](https://slack.com/) account and user credentials</span><span class="sxs-lookup"><span data-stu-id="d3f81-117">Your [Slack](https://slack.com/) account and user credentials</span></span>

  <span data-ttu-id="d3f81-118">Your credentials authorize your logic app to create a connection and access your Slack account.</span><span class="sxs-lookup"><span data-stu-id="d3f81-118">Your credentials authorize your logic app to create a connection and access your Slack account.</span></span>

* <span data-ttu-id="d3f81-119">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span><span class="sxs-lookup"><span data-stu-id="d3f81-119">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span></span>

* <span data-ttu-id="d3f81-120">The logic app where you want to access your Slack account.</span><span class="sxs-lookup"><span data-stu-id="d3f81-120">The logic app where you want to access your Slack account.</span></span> <span data-ttu-id="d3f81-121">To start with a Slack trigger, [create a blank logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="d3f81-121">To start with a Slack trigger, [create a blank logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span></span> <span data-ttu-id="d3f81-122">To use a Slack action, start your logic app with a trigger, such as a Slack trigger or another trigger, such as the **Recurrence** trigger.</span><span class="sxs-lookup"><span data-stu-id="d3f81-122">To use a Slack action, start your logic app with a trigger, such as a Slack trigger or another trigger, such as the **Recurrence** trigger.</span></span>

## <a name="connect-to-slack"></a><span data-ttu-id="d3f81-123">Connect to Slack</span><span class="sxs-lookup"><span data-stu-id="d3f81-123">Connect to Slack</span></span>

[!INCLUDE [Create connection general intro](../../includes/connectors-create-connection-general-intro.md)]

1. <span data-ttu-id="d3f81-124">Sign in to the [Azure portal](https://portal.azure.com), and open your logic app in Logic App Designer, if not open already.</span><span class="sxs-lookup"><span data-stu-id="d3f81-124">Sign in to the [Azure portal](https://portal.azure.com), and open your logic app in Logic App Designer, if not open already.</span></span>

1. <span data-ttu-id="d3f81-125">For blank logic apps, in the search box, enter "slack" as your filter.</span><span class="sxs-lookup"><span data-stu-id="d3f81-125">For blank logic apps, in the search box, enter "slack" as your filter.</span></span> <span data-ttu-id="d3f81-126">Under the triggers list, select the trigger you want.</span><span class="sxs-lookup"><span data-stu-id="d3f81-126">Under the triggers list, select the trigger you want.</span></span> 

   <span data-ttu-id="d3f81-127">-or-</span><span class="sxs-lookup"><span data-stu-id="d3f81-127">-or-</span></span>

   <span data-ttu-id="d3f81-128">For existing logic apps, under the last step where you want to add an action, choose **New step**.</span><span class="sxs-lookup"><span data-stu-id="d3f81-128">For existing logic apps, under the last step where you want to add an action, choose **New step**.</span></span> 
   <span data-ttu-id="d3f81-129">In the search box, enter "slack" as your filter.</span><span class="sxs-lookup"><span data-stu-id="d3f81-129">In the search box, enter "slack" as your filter.</span></span> 
   <span data-ttu-id="d3f81-130">Under the actions list, select the action you want.</span><span class="sxs-lookup"><span data-stu-id="d3f81-130">Under the actions list, select the action you want.</span></span>

   <span data-ttu-id="d3f81-131">To add an action between steps, move your pointer over the arrow between steps.</span><span class="sxs-lookup"><span data-stu-id="d3f81-131">To add an action between steps, move your pointer over the arrow between steps.</span></span> 
   <span data-ttu-id="d3f81-132">Choose the plus sign (**+**) that appears, and then select **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="d3f81-132">Choose the plus sign (**+**) that appears, and then select **Add an action**.</span></span>

1. <span data-ttu-id="d3f81-133">If you're prompted to sign in to Slack, sign in to your Slack workspace.</span><span class="sxs-lookup"><span data-stu-id="d3f81-133">If you're prompted to sign in to Slack, sign in to your Slack workspace.</span></span> 

   ![Sign in to Slack workspace](./media/connectors-create-api-slack/slack-sign-in-workspace.png)

1. <span data-ttu-id="d3f81-135">Authorize access for your logic app.</span><span class="sxs-lookup"><span data-stu-id="d3f81-135">Authorize access for your logic app.</span></span>

   ![Authorize access to Slack](./media/connectors-create-api-slack/slack-authorize-access.png)

1. <span data-ttu-id="d3f81-137">Provide the necessary details for your selected trigger or action.</span><span class="sxs-lookup"><span data-stu-id="d3f81-137">Provide the necessary details for your selected trigger or action.</span></span> <span data-ttu-id="d3f81-138">To continue building your logic app's workflow, add more actions.</span><span class="sxs-lookup"><span data-stu-id="d3f81-138">To continue building your logic app's workflow, add more actions.</span></span>

## <a name="connector-reference"></a><span data-ttu-id="d3f81-139">Connector reference</span><span class="sxs-lookup"><span data-stu-id="d3f81-139">Connector reference</span></span>

<span data-ttu-id="d3f81-140">For technical details about triggers, actions, and limits, which are described by the connector's OpenAPI (formerly Swagger) description, review the connector's [reference page](/connectors/slack/).</span><span class="sxs-lookup"><span data-stu-id="d3f81-140">For technical details about triggers, actions, and limits, which are described by the connector's OpenAPI (formerly Swagger) description, review the connector's [reference page](/connectors/slack/).</span></span>

## <a name="get-support"></a><span data-ttu-id="d3f81-141">Get support</span><span class="sxs-lookup"><span data-stu-id="d3f81-141">Get support</span></span>

* <span data-ttu-id="d3f81-142">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="d3f81-142">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>
* <span data-ttu-id="d3f81-143">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="d3f81-143">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3f81-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="d3f81-144">Next steps</span></span>

* <span data-ttu-id="d3f81-145">Learn about other [Logic Apps connectors](../connectors/apis-list.md)</span><span class="sxs-lookup"><span data-stu-id="d3f81-145">Learn about other [Logic Apps connectors](../connectors/apis-list.md)</span></span>
