---
title: Connect to OneDrive - Azure Logic Apps | Microsoft Docs
description: Upload and manage files with OneDrive REST APIs and Azure Logic Apps
author: ecfan
manager: jeconnoc
ms.author: estfan
ms.date: 10/18/2016
ms.topic: article
ms.service: logic-apps
services: logic-apps
ms.reviewer: klam, LADocs
ms.suite: integration
tags: connectors
ms.openlocfilehash: 50bd9ecdd665cf72c146c63ae25efa6773934a3e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44787064"
---
# <a name="get-started-with-the-onedrive-connector"></a><span data-ttu-id="50776-103">Get started with the OneDrive connector</span><span class="sxs-lookup"><span data-stu-id="50776-103">Get started with the OneDrive connector</span></span>
<span data-ttu-id="50776-104">Connect to OneDrive to manage your files, including upload, get, delete files, and more.</span><span class="sxs-lookup"><span data-stu-id="50776-104">Connect to OneDrive to manage your files, including upload, get, delete files, and more.</span></span> 

<span data-ttu-id="50776-105">With OneDrive, you:</span><span class="sxs-lookup"><span data-stu-id="50776-105">With OneDrive, you:</span></span> 

* <span data-ttu-id="50776-106">Build your workflow by storing files in OneDrive, or update existing files in OneDrive.</span><span class="sxs-lookup"><span data-stu-id="50776-106">Build your workflow by storing files in OneDrive, or update existing files in OneDrive.</span></span> 
* <span data-ttu-id="50776-107">Use triggers to start your workflow when a file is created or updated within your OneDrive.</span><span class="sxs-lookup"><span data-stu-id="50776-107">Use triggers to start your workflow when a file is created or updated within your OneDrive.</span></span>
* <span data-ttu-id="50776-108">Use actions to create a file, delete a file, and more.</span><span class="sxs-lookup"><span data-stu-id="50776-108">Use actions to create a file, delete a file, and more.</span></span> <span data-ttu-id="50776-109">For example, when a new Office 365 email is received with an attachment (a trigger), create a new file in OneDrive (an action).</span><span class="sxs-lookup"><span data-stu-id="50776-109">For example, when a new Office 365 email is received with an attachment (a trigger), create a new file in OneDrive (an action).</span></span>

<span data-ttu-id="50776-110">This article shows you how to use the OneDrive connector in a logic app, and also lists the triggers and actions.</span><span class="sxs-lookup"><span data-stu-id="50776-110">This article shows you how to use the OneDrive connector in a logic app, and also lists the triggers and actions.</span></span>

<span data-ttu-id="50776-111">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-overview.md) and [create a logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="50776-111">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-overview.md) and [create a logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span></span>

## <a name="connect-to-onedrive"></a><span data-ttu-id="50776-112">Connect to OneDrive</span><span class="sxs-lookup"><span data-stu-id="50776-112">Connect to OneDrive</span></span>
<span data-ttu-id="50776-113">Before your logic app can access any service, you first create a *connection* to the service.</span><span class="sxs-lookup"><span data-stu-id="50776-113">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="50776-114">A connection provides connectivity between a logic app and another service.</span><span class="sxs-lookup"><span data-stu-id="50776-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="50776-115">For example, to connect to OneDrive, you first need a OneDrive *connection*.</span><span class="sxs-lookup"><span data-stu-id="50776-115">For example, to connect to OneDrive, you first need a OneDrive *connection*.</span></span> <span data-ttu-id="50776-116">To create a connection, enter the credentials you normally use to access the service you wish to connect to.</span><span class="sxs-lookup"><span data-stu-id="50776-116">To create a connection, enter the credentials you normally use to access the service you wish to connect to.</span></span> <span data-ttu-id="50776-117">So, with OneDrive, enter the credentials to your OneDrive account  to create the connection.</span><span class="sxs-lookup"><span data-stu-id="50776-117">So, with OneDrive, enter the credentials to your OneDrive account  to create the connection.</span></span>

### <a name="create-the-connection"></a><span data-ttu-id="50776-118">Create the connection</span><span class="sxs-lookup"><span data-stu-id="50776-118">Create the connection</span></span>
> [!INCLUDE [Steps to create a connection to OneDrive](../../includes/connectors-create-api-onedrive.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="50776-119">Use a trigger</span><span class="sxs-lookup"><span data-stu-id="50776-119">Use a trigger</span></span>
<span data-ttu-id="50776-120">A trigger is an event that can be used to start the workflow defined in a logic app.</span><span class="sxs-lookup"><span data-stu-id="50776-120">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="50776-121">Triggers "poll" the service at an interval and frequency that you want.</span><span class="sxs-lookup"><span data-stu-id="50776-121">Triggers "poll" the service at an interval and frequency that you want.</span></span> <span data-ttu-id="50776-122">[Learn more about triggers](../logic-apps/logic-apps-overview.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="50776-122">[Learn more about triggers](../logic-apps/logic-apps-overview.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="50776-123">In the logic app, type "onedrive" to get a list of the triggers:</span><span class="sxs-lookup"><span data-stu-id="50776-123">In the logic app, type "onedrive" to get a list of the triggers:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/onedrive-1.png)
2. <span data-ttu-id="50776-124">Select **When a file is modified**.</span><span class="sxs-lookup"><span data-stu-id="50776-124">Select **When a file is modified**.</span></span> <span data-ttu-id="50776-125">If a connection already exists, then select the Show Picker button to select a folder.</span><span class="sxs-lookup"><span data-stu-id="50776-125">If a connection already exists, then select the Show Picker button to select a folder.</span></span>
   
    ![](./media/connectors-create-api-onedrive/sample-folder.png)
   
    <span data-ttu-id="50776-126">If you are prompted to sign in, then enter the sign in details to create the connection.</span><span class="sxs-lookup"><span data-stu-id="50776-126">If you are prompted to sign in, then enter the sign in details to create the connection.</span></span> <span data-ttu-id="50776-127">[Create the connection](connectors-create-api-onedrive.md#create-the-connection) in this article lists the steps.</span><span class="sxs-lookup"><span data-stu-id="50776-127">[Create the connection](connectors-create-api-onedrive.md#create-the-connection) in this article lists the steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="50776-128">In this example, the logic app runs when a file in the folder you choose is updated.</span><span class="sxs-lookup"><span data-stu-id="50776-128">In this example, the logic app runs when a file in the folder you choose is updated.</span></span> <span data-ttu-id="50776-129">To see the results of this trigger, add another action that sends you an email.</span><span class="sxs-lookup"><span data-stu-id="50776-129">To see the results of this trigger, add another action that sends you an email.</span></span> <span data-ttu-id="50776-130">For example, add the Office 365 Outlook *Send an email* action that emails you when a file is updated.</span><span class="sxs-lookup"><span data-stu-id="50776-130">For example, add the Office 365 Outlook *Send an email* action that emails you when a file is updated.</span></span> 

3. <span data-ttu-id="50776-131">Select the **Edit** button and set the **Frequency** and **Interval** values.</span><span class="sxs-lookup"><span data-stu-id="50776-131">Select the **Edit** button and set the **Frequency** and **Interval** values.</span></span> <span data-ttu-id="50776-132">For example, if you want the trigger to poll every 15 minutes, then set the **Frequency** to **Minute**, and set the **Interval** to **15**.</span><span class="sxs-lookup"><span data-stu-id="50776-132">For example, if you want the trigger to poll every 15 minutes, then set the **Frequency** to **Minute**, and set the **Interval** to **15**.</span></span> 
   
    ![](./media/connectors-create-api-onedrive/trigger-properties.png)
4. <span data-ttu-id="50776-133">**Save** your changes (top left corner of the toolbar).</span><span class="sxs-lookup"><span data-stu-id="50776-133">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="50776-134">Your logic app is saved and may be automatically enabled.</span><span class="sxs-lookup"><span data-stu-id="50776-134">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="50776-135">Use an action</span><span class="sxs-lookup"><span data-stu-id="50776-135">Use an action</span></span>
<span data-ttu-id="50776-136">An action is an operation carried out by the workflow defined in a logic app.</span><span class="sxs-lookup"><span data-stu-id="50776-136">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="50776-137">[Learn more about actions](../logic-apps/logic-apps-overview.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="50776-137">[Learn more about actions](../logic-apps/logic-apps-overview.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="50776-138">Select the plus sign.</span><span class="sxs-lookup"><span data-stu-id="50776-138">Select the plus sign.</span></span> <span data-ttu-id="50776-139">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span><span class="sxs-lookup"><span data-stu-id="50776-139">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](./media/connectors-create-api-onedrive/add-action.png)
2. <span data-ttu-id="50776-140">Choose **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="50776-140">Choose **Add an action**.</span></span>
3. <span data-ttu-id="50776-141">In the text box, type “onedrive” to get a list of all the available actions.</span><span class="sxs-lookup"><span data-stu-id="50776-141">In the text box, type “onedrive” to get a list of all the available actions.</span></span>
   
    ![](./media/connectors-create-api-onedrive/onedrive-actions.png) 
4. <span data-ttu-id="50776-142">In our example, choose **OneDrive - Create file**.</span><span class="sxs-lookup"><span data-stu-id="50776-142">In our example, choose **OneDrive - Create file**.</span></span> <span data-ttu-id="50776-143">If a connection already exists, then select the **Folder Path** to put the file, enter the **File Name**, and choose the **File Content** you want:</span><span class="sxs-lookup"><span data-stu-id="50776-143">If a connection already exists, then select the **Folder Path** to put the file, enter the **File Name**, and choose the **File Content** you want:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/sample-action.png)
   
    <span data-ttu-id="50776-144">If you are prompted for the connection information, then enter the details to create the connection.</span><span class="sxs-lookup"><span data-stu-id="50776-144">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="50776-145">[Create the connection](connectors-create-api-onedrive.md#create-the-connection) in this article describes these properties.</span><span class="sxs-lookup"><span data-stu-id="50776-145">[Create the connection](connectors-create-api-onedrive.md#create-the-connection) in this article describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="50776-146">In this example, we create a new file in a OneDrive folder.</span><span class="sxs-lookup"><span data-stu-id="50776-146">In this example, we create a new file in a OneDrive folder.</span></span> <span data-ttu-id="50776-147">You can use output from another trigger to create the OneDrive file.</span><span class="sxs-lookup"><span data-stu-id="50776-147">You can use output from another trigger to create the OneDrive file.</span></span> <span data-ttu-id="50776-148">For example, add the Office 365 Outlook *When a new email arrives* trigger.</span><span class="sxs-lookup"><span data-stu-id="50776-148">For example, add the Office 365 Outlook *When a new email arrives* trigger.</span></span> <span data-ttu-id="50776-149">Then add the OneDrive *Create file* action that uses the Attachments and Content-Type fields within a ForEach to create the new file in OneDrive.</span><span class="sxs-lookup"><span data-stu-id="50776-149">Then add the OneDrive *Create file* action that uses the Attachments and Content-Type fields within a ForEach to create the new file in OneDrive.</span></span> 
   > 
   > ![](./media/connectors-create-api-onedrive/foreach-action.png)

5. <span data-ttu-id="50776-150">**Save** your changes (top left corner of the toolbar).</span><span class="sxs-lookup"><span data-stu-id="50776-150">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="50776-151">Your logic app is saved and may be automatically enabled.</span><span class="sxs-lookup"><span data-stu-id="50776-151">Your logic app is saved and may be automatically enabled.</span></span>


## <a name="connector-specific-details"></a><span data-ttu-id="50776-152">Connector-specific details</span><span class="sxs-lookup"><span data-stu-id="50776-152">Connector-specific details</span></span>

<span data-ttu-id="50776-153">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/onedriveconnector/).</span><span class="sxs-lookup"><span data-stu-id="50776-153">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/onedriveconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="50776-154">More connectors</span><span class="sxs-lookup"><span data-stu-id="50776-154">More connectors</span></span>
<span data-ttu-id="50776-155">Go back to the [APIs list](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="50776-155">Go back to the [APIs list](apis-list.md).</span></span>