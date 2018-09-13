---
title: Connect to Wunderlist from Azure Logic Apps | Microsoft Docs
description: Automate tasks and workflows that monitor and manage lists, tasks, reminders, and more in your Wunderlist account by using Azure Logic Apps
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: ecfan
ms.author: estfan
ms.reviewer: klam, LADocs
ms.assetid: e4773ecf-3ad3-44b4-a1b5-ee5f58baeadd
ms.topic: article
tags: connectors
ms.date: 08/25/2018
ms.openlocfilehash: 7226b59504c7112c039061ab0c184fe14f6e59d0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44803457"
---
# <a name="monitor-and-manage-wunderlist-by-using-azure-logic-apps"></a><span data-ttu-id="079dd-103">Monitor and manage Wunderlist by using Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="079dd-103">Monitor and manage Wunderlist by using Azure Logic Apps</span></span>

<span data-ttu-id="079dd-104">With Azure Logic Apps and the Wunderlist connector, you can create automated tasks and workflows that monitor and manage todo lists, tasks, reminders, and more in your Wunderlist account, along with other actions, for example:</span><span class="sxs-lookup"><span data-stu-id="079dd-104">With Azure Logic Apps and the Wunderlist connector, you can create automated tasks and workflows that monitor and manage todo lists, tasks, reminders, and more in your Wunderlist account, along with other actions, for example:</span></span>

* <span data-ttu-id="079dd-105">Monitor when new tasks get created, when tasks are due, or reminders happen.</span><span class="sxs-lookup"><span data-stu-id="079dd-105">Monitor when new tasks get created, when tasks are due, or reminders happen.</span></span>
* <span data-ttu-id="079dd-106">Create and manage lists, notes, tasks, subtasks, and more.</span><span class="sxs-lookup"><span data-stu-id="079dd-106">Create and manage lists, notes, tasks, subtasks, and more.</span></span>
* <span data-ttu-id="079dd-107">Set reminders.</span><span class="sxs-lookup"><span data-stu-id="079dd-107">Set reminders.</span></span>
* <span data-ttu-id="079dd-108">Get lists, tasks, subtasks, reminders, files, notes, comments, and more.</span><span class="sxs-lookup"><span data-stu-id="079dd-108">Get lists, tasks, subtasks, reminders, files, notes, comments, and more.</span></span>

<span data-ttu-id="079dd-109">[Wunderlist](https://www.wunderlist.com/) is a service that helps you plan, manage, and finish your projects, todo lists, and tasks - on any device, anywhere.</span><span class="sxs-lookup"><span data-stu-id="079dd-109">[Wunderlist](https://www.wunderlist.com/) is a service that helps you plan, manage, and finish your projects, todo lists, and tasks - on any device, anywhere.</span></span> <span data-ttu-id="079dd-110">You can use triggers that get responses from your Wunderlist account and make the output available to other actions.</span><span class="sxs-lookup"><span data-stu-id="079dd-110">You can use triggers that get responses from your Wunderlist account and make the output available to other actions.</span></span> <span data-ttu-id="079dd-111">You can use actions that perform tasks with your Wunderlist account.</span><span class="sxs-lookup"><span data-stu-id="079dd-111">You can use actions that perform tasks with your Wunderlist account.</span></span> <span data-ttu-id="079dd-112">You can also have other actions use the output from Wunderlist actions.</span><span class="sxs-lookup"><span data-stu-id="079dd-112">You can also have other actions use the output from Wunderlist actions.</span></span> <span data-ttu-id="079dd-113">For example, when new tasks are due, you can post messages with the Slack connector.</span><span class="sxs-lookup"><span data-stu-id="079dd-113">For example, when new tasks are due, you can post messages with the Slack connector.</span></span> <span data-ttu-id="079dd-114">If you're new to logic apps, review [What is Azure Logic Apps?](../logic-apps/logic-apps-overview.md)</span><span class="sxs-lookup"><span data-stu-id="079dd-114">If you're new to logic apps, review [What is Azure Logic Apps?](../logic-apps/logic-apps-overview.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="079dd-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="079dd-115">Prerequisites</span></span>

* <span data-ttu-id="079dd-116">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="079dd-116">An Azure subscription.</span></span> <span data-ttu-id="079dd-117">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span><span class="sxs-lookup"><span data-stu-id="079dd-117">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span></span> 

* <span data-ttu-id="079dd-118">Your Wunderlist account and user credentials</span><span class="sxs-lookup"><span data-stu-id="079dd-118">Your Wunderlist account and user credentials</span></span>

   <span data-ttu-id="079dd-119">Your credentials authorize your logic app to create  a connection and access your Wunderlist account.</span><span class="sxs-lookup"><span data-stu-id="079dd-119">Your credentials authorize your logic app to create  a connection and access your Wunderlist account.</span></span>

* <span data-ttu-id="079dd-120">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span><span class="sxs-lookup"><span data-stu-id="079dd-120">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span></span>

* <span data-ttu-id="079dd-121">The logic app where you want to access your Yammer account.</span><span class="sxs-lookup"><span data-stu-id="079dd-121">The logic app where you want to access your Yammer account.</span></span> <span data-ttu-id="079dd-122">To start with a Wunderlist trigger, [create a blank logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="079dd-122">To start with a Wunderlist trigger, [create a blank logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span></span> <span data-ttu-id="079dd-123">To use a Wunderlist action, start your logic app with another trigger, for example, the **Recurrence** trigger.</span><span class="sxs-lookup"><span data-stu-id="079dd-123">To use a Wunderlist action, start your logic app with another trigger, for example, the **Recurrence** trigger.</span></span>

## <a name="connect-to-wunderlist"></a><span data-ttu-id="079dd-124">Connect to Wunderlist</span><span class="sxs-lookup"><span data-stu-id="079dd-124">Connect to Wunderlist</span></span>

[!INCLUDE [Create connection general intro](../../includes/connectors-create-connection-general-intro.md)]

1. <span data-ttu-id="079dd-125">Sign in to the [Azure portal](https://portal.azure.com), and open your logic app in Logic App Designer, if not open already.</span><span class="sxs-lookup"><span data-stu-id="079dd-125">Sign in to the [Azure portal](https://portal.azure.com), and open your logic app in Logic App Designer, if not open already.</span></span>

1. <span data-ttu-id="079dd-126">Choose a path:</span><span class="sxs-lookup"><span data-stu-id="079dd-126">Choose a path:</span></span> 

   * <span data-ttu-id="079dd-127">For blank logic apps, in the search box, enter "wunderlist" as your filter.</span><span class="sxs-lookup"><span data-stu-id="079dd-127">For blank logic apps, in the search box, enter "wunderlist" as your filter.</span></span> 
   <span data-ttu-id="079dd-128">Under the triggers list, select the trigger you want.</span><span class="sxs-lookup"><span data-stu-id="079dd-128">Under the triggers list, select the trigger you want.</span></span> 

     <span data-ttu-id="079dd-129">-or-</span><span class="sxs-lookup"><span data-stu-id="079dd-129">-or-</span></span>

   * <span data-ttu-id="079dd-130">For existing logic apps:</span><span class="sxs-lookup"><span data-stu-id="079dd-130">For existing logic apps:</span></span> 
   
     * <span data-ttu-id="079dd-131">Under the last step where you want to add an action, choose **New step**.</span><span class="sxs-lookup"><span data-stu-id="079dd-131">Under the last step where you want to add an action, choose **New step**.</span></span> 

       <span data-ttu-id="079dd-132">-or-</span><span class="sxs-lookup"><span data-stu-id="079dd-132">-or-</span></span>

     * <span data-ttu-id="079dd-133">Between the steps where you want to add an action, move your pointer over the arrow between steps.</span><span class="sxs-lookup"><span data-stu-id="079dd-133">Between the steps where you want to add an action, move your pointer over the arrow between steps.</span></span> 
     <span data-ttu-id="079dd-134">Choose the plus sign (**+**) that appears, and then select **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="079dd-134">Choose the plus sign (**+**) that appears, and then select **Add an action**.</span></span>
     
       <span data-ttu-id="079dd-135">In the search box, enter "wunderlist" as your filter.</span><span class="sxs-lookup"><span data-stu-id="079dd-135">In the search box, enter "wunderlist" as your filter.</span></span> 
       <span data-ttu-id="079dd-136">Under the actions list, select the action you want.</span><span class="sxs-lookup"><span data-stu-id="079dd-136">Under the actions list, select the action you want.</span></span>

1. <span data-ttu-id="079dd-137">If you're prompted to sign in to Wunderlist, sign in now so you can allow access.</span><span class="sxs-lookup"><span data-stu-id="079dd-137">If you're prompted to sign in to Wunderlist, sign in now so you can allow access.</span></span>

1. <span data-ttu-id="079dd-138">Provide the necessary details for your selected trigger or action and continue building your logic app's workflow.</span><span class="sxs-lookup"><span data-stu-id="079dd-138">Provide the necessary details for your selected trigger or action and continue building your logic app's workflow.</span></span>

## <a name="connector-reference"></a><span data-ttu-id="079dd-139">Connector reference</span><span class="sxs-lookup"><span data-stu-id="079dd-139">Connector reference</span></span>

<span data-ttu-id="079dd-140">For technical details about triggers, actions, and limits, which are described by the connector's OpenAPI (formerly Swagger) description, review the connector's [reference page](/connectors/wunderlist/).</span><span class="sxs-lookup"><span data-stu-id="079dd-140">For technical details about triggers, actions, and limits, which are described by the connector's OpenAPI (formerly Swagger) description, review the connector's [reference page](/connectors/wunderlist/).</span></span>

## <a name="get-support"></a><span data-ttu-id="079dd-141">Get support</span><span class="sxs-lookup"><span data-stu-id="079dd-141">Get support</span></span>

* <span data-ttu-id="079dd-142">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="079dd-142">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>
* <span data-ttu-id="079dd-143">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="079dd-143">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="079dd-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="079dd-144">Next steps</span></span>

* <span data-ttu-id="079dd-145">Learn about other [Logic Apps connectors](../connectors/apis-list.md)</span><span class="sxs-lookup"><span data-stu-id="079dd-145">Learn about other [Logic Apps connectors](../connectors/apis-list.md)</span></span>