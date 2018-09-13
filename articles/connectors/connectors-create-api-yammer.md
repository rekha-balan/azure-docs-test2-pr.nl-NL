---
title: Connect to Yammer from Azure Logic Apps | Microsoft Docs
description: Automate tasks and workflows that monitor, post, and manage messages, feeds, and more in Yammer by using Azure Logic Apps
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: ecfan
ms.author: estfan
ms.reviewer: klam, LADocs
ms.assetid: b5ae0827-fbb3-45ec-8f45-ad1cc2e7eccc
ms.topic: article
tags: connectors
ms.date: 08/25/2018
ms.openlocfilehash: 41855d6e562ddbb78df5d1d8794127e1064cc2ca
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44804861"
---
# <a name="monitor-and-manage-your-yammer-account-by-using-azure-logic-apps"></a><span data-ttu-id="ec160-103">Monitor and manage your Yammer account by using Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="ec160-103">Monitor and manage your Yammer account by using Azure Logic Apps</span></span>

<span data-ttu-id="ec160-104">With Azure Logic Apps and the Yammer connector, you can create automated tasks and workflows that monitor and manage messages, feeds, and more in your Yammer account, along with other actions, for example:</span><span class="sxs-lookup"><span data-stu-id="ec160-104">With Azure Logic Apps and the Yammer connector, you can create automated tasks and workflows that monitor and manage messages, feeds, and more in your Yammer account, along with other actions, for example:</span></span>

* <span data-ttu-id="ec160-105">Monitor when new messages appear in followed feeds and groups.</span><span class="sxs-lookup"><span data-stu-id="ec160-105">Monitor when new messages appear in followed feeds and groups.</span></span>
* <span data-ttu-id="ec160-106">Get messages, groups, networks, users' details, and more.</span><span class="sxs-lookup"><span data-stu-id="ec160-106">Get messages, groups, networks, users' details, and more.</span></span>
* <span data-ttu-id="ec160-107">Post and like messages.</span><span class="sxs-lookup"><span data-stu-id="ec160-107">Post and like messages.</span></span>

<span data-ttu-id="ec160-108">You can use triggers that get responses from your Yammer account and make the output available to other actions.</span><span class="sxs-lookup"><span data-stu-id="ec160-108">You can use triggers that get responses from your Yammer account and make the output available to other actions.</span></span> <span data-ttu-id="ec160-109">You can use actions that perform tasks with your Yammer account.</span><span class="sxs-lookup"><span data-stu-id="ec160-109">You can use actions that perform tasks with your Yammer account.</span></span> <span data-ttu-id="ec160-110">You can also have other actions use the output from Yammer actions.</span><span class="sxs-lookup"><span data-stu-id="ec160-110">You can also have other actions use the output from Yammer actions.</span></span> <span data-ttu-id="ec160-111">For example, when new messages appear in feeds or groups, you can share those messages with the Slack connector.</span><span class="sxs-lookup"><span data-stu-id="ec160-111">For example, when new messages appear in feeds or groups, you can share those messages with the Slack connector.</span></span> <span data-ttu-id="ec160-112">If you're new to logic apps, review [What is Azure Logic Apps?](../logic-apps/logic-apps-overview.md)</span><span class="sxs-lookup"><span data-stu-id="ec160-112">If you're new to logic apps, review [What is Azure Logic Apps?](../logic-apps/logic-apps-overview.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec160-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ec160-113">Prerequisites</span></span>

* <span data-ttu-id="ec160-114">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="ec160-114">An Azure subscription.</span></span> <span data-ttu-id="ec160-115">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span><span class="sxs-lookup"><span data-stu-id="ec160-115">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span></span> 

* <span data-ttu-id="ec160-116">Your Yammer account and user credentials</span><span class="sxs-lookup"><span data-stu-id="ec160-116">Your Yammer account and user credentials</span></span>

   <span data-ttu-id="ec160-117">Your credentials authorize your logic app to create  a connection and access your Yammer account.</span><span class="sxs-lookup"><span data-stu-id="ec160-117">Your credentials authorize your logic app to create  a connection and access your Yammer account.</span></span>

* <span data-ttu-id="ec160-118">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span><span class="sxs-lookup"><span data-stu-id="ec160-118">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span></span>

* <span data-ttu-id="ec160-119">The logic app where you want to access your Yammer account.</span><span class="sxs-lookup"><span data-stu-id="ec160-119">The logic app where you want to access your Yammer account.</span></span> <span data-ttu-id="ec160-120">To start with a Yammer trigger, [create a blank logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="ec160-120">To start with a Yammer trigger, [create a blank logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span></span> <span data-ttu-id="ec160-121">To use a Yammer action, start your logic app with another trigger, for example, the **Recurrence** trigger.</span><span class="sxs-lookup"><span data-stu-id="ec160-121">To use a Yammer action, start your logic app with another trigger, for example, the **Recurrence** trigger.</span></span>

## <a name="connect-to-yammer"></a><span data-ttu-id="ec160-122">Connect to Yammer</span><span class="sxs-lookup"><span data-stu-id="ec160-122">Connect to Yammer</span></span>

[!INCLUDE [Create connection general intro](../../includes/connectors-create-connection-general-intro.md)]

1. <span data-ttu-id="ec160-123">Sign in to the [Azure portal](https://portal.azure.com), and open your logic app in Logic App Designer, if not open already.</span><span class="sxs-lookup"><span data-stu-id="ec160-123">Sign in to the [Azure portal](https://portal.azure.com), and open your logic app in Logic App Designer, if not open already.</span></span>

1. <span data-ttu-id="ec160-124">Choose a path:</span><span class="sxs-lookup"><span data-stu-id="ec160-124">Choose a path:</span></span> 

   * <span data-ttu-id="ec160-125">For blank logic apps, in the search box, enter "yammer" as your filter.</span><span class="sxs-lookup"><span data-stu-id="ec160-125">For blank logic apps, in the search box, enter "yammer" as your filter.</span></span> 
   <span data-ttu-id="ec160-126">Under the triggers list, select the trigger you want.</span><span class="sxs-lookup"><span data-stu-id="ec160-126">Under the triggers list, select the trigger you want.</span></span> 

     <span data-ttu-id="ec160-127">-or-</span><span class="sxs-lookup"><span data-stu-id="ec160-127">-or-</span></span>

   * <span data-ttu-id="ec160-128">For existing logic apps:</span><span class="sxs-lookup"><span data-stu-id="ec160-128">For existing logic apps:</span></span> 
   
     * <span data-ttu-id="ec160-129">Under the last step where you want to add an action, choose **New step**.</span><span class="sxs-lookup"><span data-stu-id="ec160-129">Under the last step where you want to add an action, choose **New step**.</span></span> 

       <span data-ttu-id="ec160-130">-or-</span><span class="sxs-lookup"><span data-stu-id="ec160-130">-or-</span></span>

     * <span data-ttu-id="ec160-131">Between the steps where you want to add an action, move your pointer over the arrow between steps.</span><span class="sxs-lookup"><span data-stu-id="ec160-131">Between the steps where you want to add an action, move your pointer over the arrow between steps.</span></span> 
     <span data-ttu-id="ec160-132">Choose the plus sign (**+**) that appears, and then select **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="ec160-132">Choose the plus sign (**+**) that appears, and then select **Add an action**.</span></span>
     
       <span data-ttu-id="ec160-133">In the search box, enter "yammer" as your filter.</span><span class="sxs-lookup"><span data-stu-id="ec160-133">In the search box, enter "yammer" as your filter.</span></span> 
       <span data-ttu-id="ec160-134">Under the actions list, select the action you want.</span><span class="sxs-lookup"><span data-stu-id="ec160-134">Under the actions list, select the action you want.</span></span>

1. <span data-ttu-id="ec160-135">If you're prompted to sign in to Yammer, sign in now sign in now so you can allow access.</span><span class="sxs-lookup"><span data-stu-id="ec160-135">If you're prompted to sign in to Yammer, sign in now sign in now so you can allow access.</span></span>

1. <span data-ttu-id="ec160-136">Provide the necessary details for your selected trigger or action and continue building your logic app's workflow.</span><span class="sxs-lookup"><span data-stu-id="ec160-136">Provide the necessary details for your selected trigger or action and continue building your logic app's workflow.</span></span>

## <a name="connector-reference"></a><span data-ttu-id="ec160-137">Connector reference</span><span class="sxs-lookup"><span data-stu-id="ec160-137">Connector reference</span></span>

<span data-ttu-id="ec160-138">For technical details about triggers, actions, and limits, which are described by the connector's OpenAPI (formerly Swagger) description, review the connector's [reference page](/connectors/yammer/).</span><span class="sxs-lookup"><span data-stu-id="ec160-138">For technical details about triggers, actions, and limits, which are described by the connector's OpenAPI (formerly Swagger) description, review the connector's [reference page](/connectors/yammer/).</span></span>

## <a name="get-support"></a><span data-ttu-id="ec160-139">Get support</span><span class="sxs-lookup"><span data-stu-id="ec160-139">Get support</span></span>

* <span data-ttu-id="ec160-140">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="ec160-140">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>
* <span data-ttu-id="ec160-141">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="ec160-141">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec160-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="ec160-142">Next steps</span></span>

* <span data-ttu-id="ec160-143">Learn about other [Logic Apps connectors](../connectors/apis-list.md)</span><span class="sxs-lookup"><span data-stu-id="ec160-143">Learn about other [Logic Apps connectors](../connectors/apis-list.md)</span></span>