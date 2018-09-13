---
title: Connect to SFTP account from Azure Logic Apps | Microsoft Docs
description: Automate tasks and workflows that monitor, create, manage, send, and receive files for an SFTP server by using Azure Logic Apps
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: ecfan
ms.author: estfan
ms.reviewer: klam, LADocs
ms.assetid: 697eb8b0-4a66-40c7-be7b-6aa6b131c7ad
ms.topic: article
tags: connectors
ms.date: 08/24/2018
ms.openlocfilehash: 8f430477883543aa8f87eb3fb0fb49ab31e2d723
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44824863"
---
# <a name="monitor-create-and-manage-sftp-files-by-using-azure-logic-apps"></a><span data-ttu-id="023ad-103">Monitor, create, and manage SFTP files by using Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="023ad-103">Monitor, create, and manage SFTP files by using Azure Logic Apps</span></span>

<span data-ttu-id="023ad-104">With Azure Logic Apps and the SFTP connector, you can create automated tasks and workflows that monitor, create, send, and receive files through your account on an [SFTP](https://www.ssh.com/ssh/sftp/) server, along with other actions, for example:</span><span class="sxs-lookup"><span data-stu-id="023ad-104">With Azure Logic Apps and the SFTP connector, you can create automated tasks and workflows that monitor, create, send, and receive files through your account on an [SFTP](https://www.ssh.com/ssh/sftp/) server, along with other actions, for example:</span></span>

* <span data-ttu-id="023ad-105">Monitor when files are added or changed.</span><span class="sxs-lookup"><span data-stu-id="023ad-105">Monitor when files are added or changed.</span></span>
* <span data-ttu-id="023ad-106">Get, create, copy, update, list, and delete files.</span><span class="sxs-lookup"><span data-stu-id="023ad-106">Get, create, copy, update, list, and delete files.</span></span>
* <span data-ttu-id="023ad-107">Get file content and metadata.</span><span class="sxs-lookup"><span data-stu-id="023ad-107">Get file content and metadata.</span></span>
* <span data-ttu-id="023ad-108">Extract archives to folders.</span><span class="sxs-lookup"><span data-stu-id="023ad-108">Extract archives to folders.</span></span>

<span data-ttu-id="023ad-109">You can use triggers that get responses from your SFTP server and make the output available to other actions.</span><span class="sxs-lookup"><span data-stu-id="023ad-109">You can use triggers that get responses from your SFTP server and make the output available to other actions.</span></span> <span data-ttu-id="023ad-110">You can use actions in your logic apps to perform tasks with files on your SFTP server.</span><span class="sxs-lookup"><span data-stu-id="023ad-110">You can use actions in your logic apps to perform tasks with files on your SFTP server.</span></span> <span data-ttu-id="023ad-111">You can also have other actions use the output from SFTP actions.</span><span class="sxs-lookup"><span data-stu-id="023ad-111">You can also have other actions use the output from SFTP actions.</span></span> <span data-ttu-id="023ad-112">For example, if you regularly retrieve files from your SFTP server, you can send email about those files and their content by using the Office 365 Outlook connector or Outlook.com connector.</span><span class="sxs-lookup"><span data-stu-id="023ad-112">For example, if you regularly retrieve files from your SFTP server, you can send email about those files and their content by using the Office 365 Outlook connector or Outlook.com connector.</span></span>
<span data-ttu-id="023ad-113">If you're new to logic apps, review [What is Azure Logic Apps?](../logic-apps/logic-apps-overview.md)</span><span class="sxs-lookup"><span data-stu-id="023ad-113">If you're new to logic apps, review [What is Azure Logic Apps?](../logic-apps/logic-apps-overview.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="023ad-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="023ad-114">Prerequisites</span></span>

* <span data-ttu-id="023ad-115">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="023ad-115">An Azure subscription.</span></span> <span data-ttu-id="023ad-116">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span><span class="sxs-lookup"><span data-stu-id="023ad-116">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span></span> 

* <span data-ttu-id="023ad-117">Your SFTP host server address and account credentials</span><span class="sxs-lookup"><span data-stu-id="023ad-117">Your SFTP host server address and account credentials</span></span>

   <span data-ttu-id="023ad-118">Your credentials authorize your logic app to create  a connection and access your SFTP account.</span><span class="sxs-lookup"><span data-stu-id="023ad-118">Your credentials authorize your logic app to create  a connection and access your SFTP account.</span></span>

* <span data-ttu-id="023ad-119">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span><span class="sxs-lookup"><span data-stu-id="023ad-119">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span></span>

* <span data-ttu-id="023ad-120">The logic app where you want to access your SFTP account.</span><span class="sxs-lookup"><span data-stu-id="023ad-120">The logic app where you want to access your SFTP account.</span></span> <span data-ttu-id="023ad-121">To start with an SFTP trigger, [create a blank logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="023ad-121">To start with an SFTP trigger, [create a blank logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span></span> <span data-ttu-id="023ad-122">To use an SFTP action, start your logic app with another trigger, for example, the **Recurrence** trigger.</span><span class="sxs-lookup"><span data-stu-id="023ad-122">To use an SFTP action, start your logic app with another trigger, for example, the **Recurrence** trigger.</span></span>

## <a name="connect-to-sftp"></a><span data-ttu-id="023ad-123">Connect to SFTP</span><span class="sxs-lookup"><span data-stu-id="023ad-123">Connect to SFTP</span></span>

[!INCLUDE [Create connection general intro](../../includes/connectors-create-connection-general-intro.md)]

1. <span data-ttu-id="023ad-124">Sign in to the [Azure portal](https://portal.azure.com), and open your logic app in Logic App Designer, if not open already.</span><span class="sxs-lookup"><span data-stu-id="023ad-124">Sign in to the [Azure portal](https://portal.azure.com), and open your logic app in Logic App Designer, if not open already.</span></span>

1. <span data-ttu-id="023ad-125">For blank logic apps, in the search box, enter "sftp" as your filter.</span><span class="sxs-lookup"><span data-stu-id="023ad-125">For blank logic apps, in the search box, enter "sftp" as your filter.</span></span> <span data-ttu-id="023ad-126">Under the triggers list, select the trigger you want.</span><span class="sxs-lookup"><span data-stu-id="023ad-126">Under the triggers list, select the trigger you want.</span></span> 

   <span data-ttu-id="023ad-127">-or-</span><span class="sxs-lookup"><span data-stu-id="023ad-127">-or-</span></span>

   <span data-ttu-id="023ad-128">For existing logic apps, under the last step where you want to add an action, choose **New step**.</span><span class="sxs-lookup"><span data-stu-id="023ad-128">For existing logic apps, under the last step where you want to add an action, choose **New step**.</span></span> 
   <span data-ttu-id="023ad-129">In the search box, enter "sftp" as your filter.</span><span class="sxs-lookup"><span data-stu-id="023ad-129">In the search box, enter "sftp" as your filter.</span></span> 
   <span data-ttu-id="023ad-130">Under the actions list, select the action you want.</span><span class="sxs-lookup"><span data-stu-id="023ad-130">Under the actions list, select the action you want.</span></span>

   <span data-ttu-id="023ad-131">To add an action between steps, move your pointer over the arrow between steps.</span><span class="sxs-lookup"><span data-stu-id="023ad-131">To add an action between steps, move your pointer over the arrow between steps.</span></span> 
   <span data-ttu-id="023ad-132">Choose the plus sign (**+**) that appears, and then select **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="023ad-132">Choose the plus sign (**+**) that appears, and then select **Add an action**.</span></span>

1. <span data-ttu-id="023ad-133">Provide the necessary details for your connection, and then choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="023ad-133">Provide the necessary details for your connection, and then choose **Create**.</span></span>

1. <span data-ttu-id="023ad-134">Provide the necessary details for your selected trigger or action and continue building your logic app's workflow.</span><span class="sxs-lookup"><span data-stu-id="023ad-134">Provide the necessary details for your selected trigger or action and continue building your logic app's workflow.</span></span>

## <a name="examples"></a><span data-ttu-id="023ad-135">Examples</span><span class="sxs-lookup"><span data-stu-id="023ad-135">Examples</span></span>

### <a name="sftp-trigger-when-a-file-is-added-or-modified"></a><span data-ttu-id="023ad-136">SFTP trigger: When a file is added or modified</span><span class="sxs-lookup"><span data-stu-id="023ad-136">SFTP trigger: When a file is added or modified</span></span>

<span data-ttu-id="023ad-137">This trigger starts a logic app workflow when the trigger detects when a file is added or changed on an SFTP server.</span><span class="sxs-lookup"><span data-stu-id="023ad-137">This trigger starts a logic app workflow when the trigger detects when a file is added or changed on an SFTP server.</span></span> <span data-ttu-id="023ad-138">So for example, you can add a condition that checks the file's content and decides whether to get that content, based on whether that content meets a specified condition.</span><span class="sxs-lookup"><span data-stu-id="023ad-138">So for example, you can add a condition that checks the file's content and decides whether to get that content, based on whether that content meets a specified condition.</span></span> <span data-ttu-id="023ad-139">Finally, you can add an action that gets the file's content, and put that content in a folder on the SFTP server.</span><span class="sxs-lookup"><span data-stu-id="023ad-139">Finally, you can add an action that gets the file's content, and put that content in a folder on the SFTP server.</span></span> 

<span data-ttu-id="023ad-140">**Enterprise example**: You can use this trigger to monitor an SFTP folder for new files that represent customer orders.</span><span class="sxs-lookup"><span data-stu-id="023ad-140">**Enterprise example**: You can use this trigger to monitor an SFTP folder for new files that represent customer orders.</span></span> <span data-ttu-id="023ad-141">You can then use an SFTP action such as **Get file content**, so you can get the order's contents for further processing and store that order in an orders database.</span><span class="sxs-lookup"><span data-stu-id="023ad-141">You can then use an SFTP action such as **Get file content**, so you can get the order's contents for further processing and store that order in an orders database.</span></span>

### <a name="sftp-action-get-content"></a><span data-ttu-id="023ad-142">SFTP action: Get content</span><span class="sxs-lookup"><span data-stu-id="023ad-142">SFTP action: Get content</span></span>

<span data-ttu-id="023ad-143">This action gets the content from a file on an SFTP server.</span><span class="sxs-lookup"><span data-stu-id="023ad-143">This action gets the content from a file on an SFTP server.</span></span> <span data-ttu-id="023ad-144">So for example, you can add the trigger from the previous example and a condition that the file's content must meet.</span><span class="sxs-lookup"><span data-stu-id="023ad-144">So for example, you can add the trigger from the previous example and a condition that the file's content must meet.</span></span> <span data-ttu-id="023ad-145">If the condition is true, the action that gets the content can run.</span><span class="sxs-lookup"><span data-stu-id="023ad-145">If the condition is true, the action that gets the content can run.</span></span> 

## <a name="connector-reference"></a><span data-ttu-id="023ad-146">Connector reference</span><span class="sxs-lookup"><span data-stu-id="023ad-146">Connector reference</span></span>

<span data-ttu-id="023ad-147">For technical details about triggers, actions, and limits, which are described by the connector's OpenAPI (formerly Swagger) description, review the connector's [reference page](/connectors/sftpconnector/).</span><span class="sxs-lookup"><span data-stu-id="023ad-147">For technical details about triggers, actions, and limits, which are described by the connector's OpenAPI (formerly Swagger) description, review the connector's [reference page](/connectors/sftpconnector/).</span></span>

## <a name="get-support"></a><span data-ttu-id="023ad-148">Get support</span><span class="sxs-lookup"><span data-stu-id="023ad-148">Get support</span></span>

* <span data-ttu-id="023ad-149">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="023ad-149">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>
* <span data-ttu-id="023ad-150">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="023ad-150">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="023ad-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="023ad-151">Next steps</span></span>

* <span data-ttu-id="023ad-152">Learn about other [Logic Apps connectors](../connectors/apis-list.md)</span><span class="sxs-lookup"><span data-stu-id="023ad-152">Learn about other [Logic Apps connectors](../connectors/apis-list.md)</span></span>