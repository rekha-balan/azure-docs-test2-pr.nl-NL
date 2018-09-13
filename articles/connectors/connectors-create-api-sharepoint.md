---
title: Connect to SharePoint from Azure Logic Apps | Microsoft Docs
description: Automate tasks and workflows that monitor and manage resources in SharePoint Online or SharePoint Server on premises by using Azure Logic Apps
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: ecfan
ms.author: estfan
ms.reviewer: klam, LADocs
ms.assetid: e0ec3149-507a-409d-8e7b-d5fbded006ce
ms.topic: article
tags: connectors
ms.date: 08/25/2018
ms.openlocfilehash: 5a3968e1aec98092767712220d8aaf676aba89cd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864900"
---
# <a name="monitor-and-manage-sharepoint-resources-with-azure-logic-apps"></a><span data-ttu-id="ac526-103">Monitor and manage SharePoint resources with Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="ac526-103">Monitor and manage SharePoint resources with Azure Logic Apps</span></span>

<span data-ttu-id="ac526-104">With Azure Logic Apps and the SharePoint connector, you can create automated tasks and workflows that monitor and manage resources, such as files, folders, lists, items, persons, and so on, in SharePoint Online or in SharePoint Server on premises, for example:</span><span class="sxs-lookup"><span data-stu-id="ac526-104">With Azure Logic Apps and the SharePoint connector, you can create automated tasks and workflows that monitor and manage resources, such as files, folders, lists, items, persons, and so on, in SharePoint Online or in SharePoint Server on premises, for example:</span></span>

* <span data-ttu-id="ac526-105">Monitor when files or items are created, changed, or deleted.</span><span class="sxs-lookup"><span data-stu-id="ac526-105">Monitor when files or items are created, changed, or deleted.</span></span>
* <span data-ttu-id="ac526-106">Create, get, update, or delete items.</span><span class="sxs-lookup"><span data-stu-id="ac526-106">Create, get, update, or delete items.</span></span>
* <span data-ttu-id="ac526-107">Add, get, or delete attachments.</span><span class="sxs-lookup"><span data-stu-id="ac526-107">Add, get, or delete attachments.</span></span> <span data-ttu-id="ac526-108">Get the content from attachments.</span><span class="sxs-lookup"><span data-stu-id="ac526-108">Get the content from attachments.</span></span>
* <span data-ttu-id="ac526-109">Create, copy, update, or delete files.</span><span class="sxs-lookup"><span data-stu-id="ac526-109">Create, copy, update, or delete files.</span></span> 
* <span data-ttu-id="ac526-110">Update file properties.</span><span class="sxs-lookup"><span data-stu-id="ac526-110">Update file properties.</span></span> <span data-ttu-id="ac526-111">Get the content, metadata, or properties for a file.</span><span class="sxs-lookup"><span data-stu-id="ac526-111">Get the content, metadata, or properties for a file.</span></span>
* <span data-ttu-id="ac526-112">List or extract folders.</span><span class="sxs-lookup"><span data-stu-id="ac526-112">List or extract folders.</span></span>
* <span data-ttu-id="ac526-113">Get lists or list views.</span><span class="sxs-lookup"><span data-stu-id="ac526-113">Get lists or list views.</span></span>
* <span data-ttu-id="ac526-114">Set content approval status.</span><span class="sxs-lookup"><span data-stu-id="ac526-114">Set content approval status.</span></span>
* <span data-ttu-id="ac526-115">Resolve persons.</span><span class="sxs-lookup"><span data-stu-id="ac526-115">Resolve persons.</span></span>
* <span data-ttu-id="ac526-116">Send HTTP requests to SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ac526-116">Send HTTP requests to SharePoint.</span></span>
* <span data-ttu-id="ac526-117">Get entity values.</span><span class="sxs-lookup"><span data-stu-id="ac526-117">Get entity values.</span></span>

<span data-ttu-id="ac526-118">You can use triggers that get responses from SharePoint and make the output available to other actions.</span><span class="sxs-lookup"><span data-stu-id="ac526-118">You can use triggers that get responses from SharePoint and make the output available to other actions.</span></span> <span data-ttu-id="ac526-119">You can use actions in your logic apps to perform tasks in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ac526-119">You can use actions in your logic apps to perform tasks in SharePoint.</span></span> <span data-ttu-id="ac526-120">You can also have other actions use the output from SharePoint actions.</span><span class="sxs-lookup"><span data-stu-id="ac526-120">You can also have other actions use the output from SharePoint actions.</span></span> <span data-ttu-id="ac526-121">For example, if you regularly fetch files from SharePoint, you can send messages to your team by using the Slack connector.</span><span class="sxs-lookup"><span data-stu-id="ac526-121">For example, if you regularly fetch files from SharePoint, you can send messages to your team by using the Slack connector.</span></span>
<span data-ttu-id="ac526-122">If you're new to logic apps, review [What is Azure Logic Apps?](../logic-apps/logic-apps-overview.md)</span><span class="sxs-lookup"><span data-stu-id="ac526-122">If you're new to logic apps, review [What is Azure Logic Apps?](../logic-apps/logic-apps-overview.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac526-123">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ac526-123">Prerequisites</span></span>

* <span data-ttu-id="ac526-124">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="ac526-124">An Azure subscription.</span></span> <span data-ttu-id="ac526-125">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span><span class="sxs-lookup"><span data-stu-id="ac526-125">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span></span> 

* <span data-ttu-id="ac526-126">Your SharePoint site address and user credentials</span><span class="sxs-lookup"><span data-stu-id="ac526-126">Your SharePoint site address and user credentials</span></span>

  <span data-ttu-id="ac526-127">Your credentials authorize your logic app to create a connection and access your SharePoint account.</span><span class="sxs-lookup"><span data-stu-id="ac526-127">Your credentials authorize your logic app to create a connection and access your SharePoint account.</span></span> 

* <span data-ttu-id="ac526-128">Before you can connect logic apps to on-premises systems such as SharePoint Server, you need to [install and set up an on-premises data gateway](../logic-apps/logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="ac526-128">Before you can connect logic apps to on-premises systems such as SharePoint Server, you need to [install and set up an on-premises data gateway](../logic-apps/logic-apps-gateway-install.md).</span></span> <span data-ttu-id="ac526-129">That way, you can specify to use your gateway installation when you create the SharePoint Server connection for your logic app.</span><span class="sxs-lookup"><span data-stu-id="ac526-129">That way, you can specify to use your gateway installation when you create the SharePoint Server connection for your logic app.</span></span>

* <span data-ttu-id="ac526-130">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span><span class="sxs-lookup"><span data-stu-id="ac526-130">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span></span>

* <span data-ttu-id="ac526-131">The logic app where you want to access your SharePoint account.</span><span class="sxs-lookup"><span data-stu-id="ac526-131">The logic app where you want to access your SharePoint account.</span></span> <span data-ttu-id="ac526-132">To start with a SharePoint trigger, [create a blank logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="ac526-132">To start with a SharePoint trigger, [create a blank logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span></span> <span data-ttu-id="ac526-133">To use a SharePoint action, start your logic app with a trigger, such as a Salesforce trigger, if you have a Salesforce account.</span><span class="sxs-lookup"><span data-stu-id="ac526-133">To use a SharePoint action, start your logic app with a trigger, such as a Salesforce trigger, if you have a Salesforce account.</span></span>

  <span data-ttu-id="ac526-134">For example, you can start your logic app with the **When a record is created** Salesforce trigger.</span><span class="sxs-lookup"><span data-stu-id="ac526-134">For example, you can start your logic app with the **When a record is created** Salesforce trigger.</span></span> 
  <span data-ttu-id="ac526-135">This trigger fires each time that a new record, such as a lead, is created in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="ac526-135">This trigger fires each time that a new record, such as a lead, is created in Salesforce.</span></span> 
  <span data-ttu-id="ac526-136">You can then follow this trigger with the SharePoint **Create file** action.</span><span class="sxs-lookup"><span data-stu-id="ac526-136">You can then follow this trigger with the SharePoint **Create file** action.</span></span> <span data-ttu-id="ac526-137">That way, when the new record is created, your logic app creates a file in SharePoint with information about that new record.</span><span class="sxs-lookup"><span data-stu-id="ac526-137">That way, when the new record is created, your logic app creates a file in SharePoint with information about that new record.</span></span>

## <a name="connect-to-sharepoint"></a><span data-ttu-id="ac526-138">Connect to SharePoint</span><span class="sxs-lookup"><span data-stu-id="ac526-138">Connect to SharePoint</span></span>

[!INCLUDE [Create connection general intro](../../includes/connectors-create-connection-general-intro.md)]

1. <span data-ttu-id="ac526-139">Sign in to the [Azure portal](https://portal.azure.com), and open your logic app in Logic App Designer, if not open already.</span><span class="sxs-lookup"><span data-stu-id="ac526-139">Sign in to the [Azure portal](https://portal.azure.com), and open your logic app in Logic App Designer, if not open already.</span></span>

1. <span data-ttu-id="ac526-140">For blank logic apps, in the search box, enter "sharepoint" as your filter.</span><span class="sxs-lookup"><span data-stu-id="ac526-140">For blank logic apps, in the search box, enter "sharepoint" as your filter.</span></span> <span data-ttu-id="ac526-141">Under the triggers list, select the trigger you want.</span><span class="sxs-lookup"><span data-stu-id="ac526-141">Under the triggers list, select the trigger you want.</span></span> 

   <span data-ttu-id="ac526-142">-or-</span><span class="sxs-lookup"><span data-stu-id="ac526-142">-or-</span></span>

   <span data-ttu-id="ac526-143">For existing logic apps, under the last step where you want to add a SharePoint action, choose **New step**.</span><span class="sxs-lookup"><span data-stu-id="ac526-143">For existing logic apps, under the last step where you want to add a SharePoint action, choose **New step**.</span></span> 
   <span data-ttu-id="ac526-144">In the search box, enter "sharepoint" as your filter.</span><span class="sxs-lookup"><span data-stu-id="ac526-144">In the search box, enter "sharepoint" as your filter.</span></span> 
   <span data-ttu-id="ac526-145">Under the actions list, select the action you want.</span><span class="sxs-lookup"><span data-stu-id="ac526-145">Under the actions list, select the action you want.</span></span>

   <span data-ttu-id="ac526-146">To add an action between steps, move your pointer over the arrow between steps.</span><span class="sxs-lookup"><span data-stu-id="ac526-146">To add an action between steps, move your pointer over the arrow between steps.</span></span> 
   <span data-ttu-id="ac526-147">Choose the plus sign (**+**) that appears, and then select **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="ac526-147">Choose the plus sign (**+**) that appears, and then select **Add an action**.</span></span>

1. <span data-ttu-id="ac526-148">When you're prompted to sign in, provide the necessary connection information.</span><span class="sxs-lookup"><span data-stu-id="ac526-148">When you're prompted to sign in, provide the necessary connection information.</span></span> <span data-ttu-id="ac526-149">If you're using SharePoint Server, make sure you select **Connect via on-premise data gateway**.</span><span class="sxs-lookup"><span data-stu-id="ac526-149">If you're using SharePoint Server, make sure you select **Connect via on-premise data gateway**.</span></span> <span data-ttu-id="ac526-150">When you're done, choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="ac526-150">When you're done, choose **Create**.</span></span>

1. <span data-ttu-id="ac526-151">Provide the necessary details for your selected trigger or action and continue building your logic app's workflow.</span><span class="sxs-lookup"><span data-stu-id="ac526-151">Provide the necessary details for your selected trigger or action and continue building your logic app's workflow.</span></span>

## <a name="connector-reference"></a><span data-ttu-id="ac526-152">Connector reference</span><span class="sxs-lookup"><span data-stu-id="ac526-152">Connector reference</span></span>

<span data-ttu-id="ac526-153">For technical details about triggers, actions, and limits, which are described by the connector's OpenAPI (formerly Swagger) description, review the connector's [reference page](/connectors/sharepoint/).</span><span class="sxs-lookup"><span data-stu-id="ac526-153">For technical details about triggers, actions, and limits, which are described by the connector's OpenAPI (formerly Swagger) description, review the connector's [reference page](/connectors/sharepoint/).</span></span>

## <a name="get-support"></a><span data-ttu-id="ac526-154">Get support</span><span class="sxs-lookup"><span data-stu-id="ac526-154">Get support</span></span>

* <span data-ttu-id="ac526-155">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="ac526-155">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>
* <span data-ttu-id="ac526-156">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="ac526-156">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac526-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="ac526-157">Next steps</span></span>

* <span data-ttu-id="ac526-158">Learn about other [Logic Apps connectors](../connectors/apis-list.md)</span><span class="sxs-lookup"><span data-stu-id="ac526-158">Learn about other [Logic Apps connectors](../connectors/apis-list.md)</span></span>
