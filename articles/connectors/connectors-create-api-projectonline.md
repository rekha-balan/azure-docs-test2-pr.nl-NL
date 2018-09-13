---
title: Connect to Project Online from Azure Logic Apps | Microsoft Docs
description: Automate workflows that monitor, create, and manage Project Online projects, tasks, and resources by using Azure Logic Apps
services: logic-apps
ms.service: logic-apps
author: ecfan
ms.author: estfan
ms.reviewer: klam, LADocs
ms.suite: integration
ms.topic: article
ms.assetid: 40ce621e-4925-4653-93bb-71ab9abcbdf1
tags: connectors
ms.date: 08/24/2018
ms.openlocfilehash: cfcb53b6e95250a1ccbebfdfcfbff5ec8479504b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44782332"
---
# <a name="manage-project-online-projects-tasks-and-resources-by-using-azure-logic-apps"></a><span data-ttu-id="2a6b2-103">Manage Project Online projects, tasks, and resources by using Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="2a6b2-103">Manage Project Online projects, tasks, and resources by using Azure Logic Apps</span></span>

<span data-ttu-id="2a6b2-104">With Azure Logic Apps and the Project Online connector, you can create automated tasks and workflows for your projects, tasks, and resources in Project Online through Office 365.</span><span class="sxs-lookup"><span data-stu-id="2a6b2-104">With Azure Logic Apps and the Project Online connector, you can create automated tasks and workflows for your projects, tasks, and resources in Project Online through Office 365.</span></span> <span data-ttu-id="2a6b2-105">Your workflows can perform these actions and others, for example:</span><span class="sxs-lookup"><span data-stu-id="2a6b2-105">Your workflows can perform these actions and others, for example:</span></span>

* <span data-ttu-id="2a6b2-106">Monitor when new projects, tasks, or resources are created.</span><span class="sxs-lookup"><span data-stu-id="2a6b2-106">Monitor when new projects, tasks, or resources are created.</span></span> <span data-ttu-id="2a6b2-107">Or, monitor when new projects are published.</span><span class="sxs-lookup"><span data-stu-id="2a6b2-107">Or, monitor when new projects are published.</span></span>
* <span data-ttu-id="2a6b2-108">Create new projects, tasks, or resources.</span><span class="sxs-lookup"><span data-stu-id="2a6b2-108">Create new projects, tasks, or resources.</span></span>
* <span data-ttu-id="2a6b2-109">List existing projects or tasks.</span><span class="sxs-lookup"><span data-stu-id="2a6b2-109">List existing projects or tasks.</span></span>
* <span data-ttu-id="2a6b2-110">Check out, check in, or publish projects.</span><span class="sxs-lookup"><span data-stu-id="2a6b2-110">Check out, check in, or publish projects.</span></span>

<span data-ttu-id="2a6b2-111">Project Online helps you plan, prioritize, and manage projects and project portfolio investments from almost anywhere on almost any device by providing powerful project management capabilities.</span><span class="sxs-lookup"><span data-stu-id="2a6b2-111">Project Online helps you plan, prioritize, and manage projects and project portfolio investments from almost anywhere on almost any device by providing powerful project management capabilities.</span></span> <span data-ttu-id="2a6b2-112">You can use Project Online triggers that get responses from Project Online and make the output available to other actions.</span><span class="sxs-lookup"><span data-stu-id="2a6b2-112">You can use Project Online triggers that get responses from Project Online and make the output available to other actions.</span></span> <span data-ttu-id="2a6b2-113">You can use actions in your logic apps to perform various tasks in Project Online.</span><span class="sxs-lookup"><span data-stu-id="2a6b2-113">You can use actions in your logic apps to perform various tasks in Project Online.</span></span> <span data-ttu-id="2a6b2-114">If you're new to logic apps, review [What is Azure Logic Apps?](../logic-apps/logic-apps-overview.md)</span><span class="sxs-lookup"><span data-stu-id="2a6b2-114">If you're new to logic apps, review [What is Azure Logic Apps?](../logic-apps/logic-apps-overview.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a6b2-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2a6b2-115">Prerequisites</span></span>

* <span data-ttu-id="2a6b2-116">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="2a6b2-116">An Azure subscription.</span></span> <span data-ttu-id="2a6b2-117">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span><span class="sxs-lookup"><span data-stu-id="2a6b2-117">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span></span> 

* <span data-ttu-id="2a6b2-118">Project Online, available through an [Office 365 account](https://www.office.com/),</span><span class="sxs-lookup"><span data-stu-id="2a6b2-118">Project Online, available through an [Office 365 account](https://www.office.com/),</span></span> 

* <span data-ttu-id="2a6b2-119">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span><span class="sxs-lookup"><span data-stu-id="2a6b2-119">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span></span>

* <span data-ttu-id="2a6b2-120">The logic app where you want to access your Project Online data.</span><span class="sxs-lookup"><span data-stu-id="2a6b2-120">The logic app where you want to access your Project Online data.</span></span> <span data-ttu-id="2a6b2-121">To start with a Project Online trigger, [create a blank logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="2a6b2-121">To start with a Project Online trigger, [create a blank logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span></span> <span data-ttu-id="2a6b2-122">To use Project Online actions, start your logic app with another trigger, for example, the **Recurrence** trigger.</span><span class="sxs-lookup"><span data-stu-id="2a6b2-122">To use Project Online actions, start your logic app with another trigger, for example, the **Recurrence** trigger.</span></span>

## <a name="connect-to-project-online"></a><span data-ttu-id="2a6b2-123">Connect to Project Online</span><span class="sxs-lookup"><span data-stu-id="2a6b2-123">Connect to Project Online</span></span>

[!INCLUDE [Create connection general intro](../../includes/connectors-create-connection-general-intro.md)]

1. <span data-ttu-id="2a6b2-124">Sign in to the [Azure portal](https://portal.azure.com), and open your logic app in Logic App Designer, if not open already.</span><span class="sxs-lookup"><span data-stu-id="2a6b2-124">Sign in to the [Azure portal](https://portal.azure.com), and open your logic app in Logic App Designer, if not open already.</span></span>

1. <span data-ttu-id="2a6b2-125">Choose a path:</span><span class="sxs-lookup"><span data-stu-id="2a6b2-125">Choose a path:</span></span> 

   * <span data-ttu-id="2a6b2-126">For blank logic apps, in the search box, enter "Project Online" as your filter.</span><span class="sxs-lookup"><span data-stu-id="2a6b2-126">For blank logic apps, in the search box, enter "Project Online" as your filter.</span></span> 
   <span data-ttu-id="2a6b2-127">Under the triggers list, select the trigger you want.</span><span class="sxs-lookup"><span data-stu-id="2a6b2-127">Under the triggers list, select the trigger you want.</span></span> 

     <span data-ttu-id="2a6b2-128">-or-</span><span class="sxs-lookup"><span data-stu-id="2a6b2-128">-or-</span></span>

   * <span data-ttu-id="2a6b2-129">For existing logic apps, under the step where you want to add an action, choose **New step**.</span><span class="sxs-lookup"><span data-stu-id="2a6b2-129">For existing logic apps, under the step where you want to add an action, choose **New step**.</span></span> <span data-ttu-id="2a6b2-130">In the search box, enter "Project Online" as your filter.</span><span class="sxs-lookup"><span data-stu-id="2a6b2-130">In the search box, enter "Project Online" as your filter.</span></span> <span data-ttu-id="2a6b2-131">Under the actions list, select the action you want.</span><span class="sxs-lookup"><span data-stu-id="2a6b2-131">Under the actions list, select the action you want.</span></span>

1. <span data-ttu-id="2a6b2-132">If you're prompted to sign in to Project Online, sign in now.</span><span class="sxs-lookup"><span data-stu-id="2a6b2-132">If you're prompted to sign in to Project Online, sign in now.</span></span>

   <span data-ttu-id="2a6b2-133">Your credentials authorize your logic app to create a connection to Project Online and access your data.</span><span class="sxs-lookup"><span data-stu-id="2a6b2-133">Your credentials authorize your logic app to create a connection to Project Online and access your data.</span></span>

1. <span data-ttu-id="2a6b2-134">Provide the necessary details for your selected trigger or action and continue building your logic app's workflow.</span><span class="sxs-lookup"><span data-stu-id="2a6b2-134">Provide the necessary details for your selected trigger or action and continue building your logic app's workflow.</span></span>

## <a name="connector-reference"></a><span data-ttu-id="2a6b2-135">Connector reference</span><span class="sxs-lookup"><span data-stu-id="2a6b2-135">Connector reference</span></span>

<span data-ttu-id="2a6b2-136">For technical details about triggers, actions, and limits, which are described by the connector's OpenAPI (formerly Swagger) description, review the connector's [reference page](/connectors/projectonline/).</span><span class="sxs-lookup"><span data-stu-id="2a6b2-136">For technical details about triggers, actions, and limits, which are described by the connector's OpenAPI (formerly Swagger) description, review the connector's [reference page](/connectors/projectonline/).</span></span>

## <a name="get-support"></a><span data-ttu-id="2a6b2-137">Get support</span><span class="sxs-lookup"><span data-stu-id="2a6b2-137">Get support</span></span>

* <span data-ttu-id="2a6b2-138">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="2a6b2-138">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>
* <span data-ttu-id="2a6b2-139">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="2a6b2-139">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a6b2-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="2a6b2-140">Next steps</span></span>

* <span data-ttu-id="2a6b2-141">Learn about other [Logic Apps connectors](../connectors/apis-list.md)</span><span class="sxs-lookup"><span data-stu-id="2a6b2-141">Learn about other [Logic Apps connectors](../connectors/apis-list.md)</span></span>