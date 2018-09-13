---
title: Switch statement for different actions in Azure Logic Apps | Microsoft Docs
description: Choose different actions to perform in logic apps based on expression values by using a switch statement
services: logic-apps
keywords: switch statement
author: derek1ee
manager: anneta
editor: ''
documentationcenter: ''
ms.assetid: ''
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: deli; LADocs
ms.openlocfilehash: c564ea51530bad885d0a0c120dd3bf4616107771
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563370"
---
# <a name="perform-different-actions-in-logic-apps-with-a-switch-statement"></a><span data-ttu-id="2e4f7-104">Perform different actions in logic apps with a switch statement</span><span class="sxs-lookup"><span data-stu-id="2e4f7-104">Perform different actions in logic apps with a switch statement</span></span>

<span data-ttu-id="2e4f7-105">When authoring a workflow, you often have to take different actions based on the value of an object or expression.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-105">When authoring a workflow, you often have to take different actions based on the value of an object or expression.</span></span> <span data-ttu-id="2e4f7-106">For example, you might want your logic app to behave differently based on the status code of an HTTP request, or an option selected in an email.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-106">For example, you might want your logic app to behave differently based on the status code of an HTTP request, or an option selected in an email.</span></span>

<span data-ttu-id="2e4f7-107">You can use a switch statement to implement these scenarios.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-107">You can use a switch statement to implement these scenarios.</span></span> <span data-ttu-id="2e4f7-108">Your logic app can evaluate a token or expression, and choose the case with the same value to execute the specified actions.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-108">Your logic app can evaluate a token or expression, and choose the case with the same value to execute the specified actions.</span></span> <span data-ttu-id="2e4f7-109">Only one case should match the switch statement.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-109">Only one case should match the switch statement.</span></span>

> [!TIP]
> <span data-ttu-id="2e4f7-110">Like all programming languages, switch statements support only equality operators.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-110">Like all programming languages, switch statements support only equality operators.</span></span> <span data-ttu-id="2e4f7-111">If you need other relational operators, such as "greater than", use a condition statement.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-111">If you need other relational operators, such as "greater than", use a condition statement.</span></span>
> <span data-ttu-id="2e4f7-112">To ensure deterministic execution behavior, cases must contain a unique and static value instead of dynamic tokens or expression.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-112">To ensure deterministic execution behavior, cases must contain a unique and static value instead of dynamic tokens or expression.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e4f7-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2e4f7-113">Prerequisites</span></span>

- <span data-ttu-id="2e4f7-114">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-114">An active Azure subscription.</span></span> <span data-ttu-id="2e4f7-115">If you don't have an active Azure subscription, [create a free account](https://azure.microsoft.com/free/), or try [Logic Apps for free](https://tryappservice.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2e4f7-115">If you don't have an active Azure subscription, [create a free account](https://azure.microsoft.com/free/), or try [Logic Apps for free](https://tryappservice.azure.com/).</span></span>
- [<span data-ttu-id="2e4f7-116">Basic knowledge about logic apps</span><span class="sxs-lookup"><span data-stu-id="2e4f7-116">Basic knowledge about logic apps</span></span>](logic-apps-what-are-logic-apps.md)

## <a name="add-a-switch-statement-to-your-workflow"></a><span data-ttu-id="2e4f7-117">Add a switch statement to your workflow</span><span class="sxs-lookup"><span data-stu-id="2e4f7-117">Add a switch statement to your workflow</span></span>

<span data-ttu-id="2e4f7-118">To show how a switch statement works, this example creates a logic app that monitors files uploaded to Dropbox.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-118">To show how a switch statement works, this example creates a logic app that monitors files uploaded to Dropbox.</span></span> <span data-ttu-id="2e4f7-119">When the new files are uploaded, the logic app sends email to an approver who chooses whether to transfer those files to SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-119">When the new files are uploaded, the logic app sends email to an approver who chooses whether to transfer those files to SharePoint.</span></span> <span data-ttu-id="2e4f7-120">The app uses a switch statement that performs different actions based on the value that the approver selects.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-120">The app uses a switch statement that performs different actions based on the value that the approver selects.</span></span>

1. <span data-ttu-id="2e4f7-121">Create a logic app, and select this trigger: **Dropbox - When a file is created**.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-121">Create a logic app, and select this trigger: **Dropbox - When a file is created**.</span></span>

   ![Use Dropbox - When a file is created trigger](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-switch-case/dropbox-trigger.jpg)

2. <span data-ttu-id="2e4f7-123">Under the trigger, add this action: **Outlook.com - Send approval email**</span><span class="sxs-lookup"><span data-stu-id="2e4f7-123">Under the trigger, add this action: **Outlook.com - Send approval email**</span></span>

   > [!TIP]
   > <span data-ttu-id="2e4f7-124">Logic apps also support sending approval email scenarios from an Office 365 Outlook account.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-124">Logic apps also support sending approval email scenarios from an Office 365 Outlook account.</span></span>

   - <span data-ttu-id="2e4f7-125">If you don't have an existing connection, you're prompted to create one.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-125">If you don't have an existing connection, you're prompted to create one.</span></span>
   - <span data-ttu-id="2e4f7-126">Fill in the required fields.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-126">Fill in the required fields.</span></span> <span data-ttu-id="2e4f7-127">For example, under **To**, specify the email address for sending the approver email.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-127">For example, under **To**, specify the email address for sending the approver email.</span></span>
   - <span data-ttu-id="2e4f7-128">Under **User Options**, enter `Approve, Reject`.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-128">Under **User Options**, enter `Approve, Reject`.</span></span>

   ![Configure connection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-switch-case/send-approval-email-action.jpg)

3. <span data-ttu-id="2e4f7-130">Add a switch statement.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-130">Add a switch statement.</span></span>

   - <span data-ttu-id="2e4f7-131">Select **+ New step** > **... More** > **Add a switch case**.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-131">Select **+ New step** > **... More** > **Add a switch case**.</span></span> 
   - <span data-ttu-id="2e4f7-132">Now we want to select the action to perform based on the `SelectedOptions` output from the *Send approval email* action.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-132">Now we want to select the action to perform based on the `SelectedOptions` output from the *Send approval email* action.</span></span> 
   <span data-ttu-id="2e4f7-133">You can find this field in the **Add dynamic content** selector.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-133">You can find this field in the **Add dynamic content** selector.</span></span>
   - <span data-ttu-id="2e4f7-134">Use *Case 1* to handle when the approver selects `Approve`.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-134">Use *Case 1* to handle when the approver selects `Approve`.</span></span>
     - <span data-ttu-id="2e4f7-135">If approved, copy the original file to SharePoint Online with the [**SharePoint Online - Create file** action](../connectors/connectors-create-api-sharepointonline.md).</span><span class="sxs-lookup"><span data-stu-id="2e4f7-135">If approved, copy the original file to SharePoint Online with the [**SharePoint Online - Create file** action](../connectors/connectors-create-api-sharepointonline.md).</span></span>
     - <span data-ttu-id="2e4f7-136">Add another action within the case to notify users that a new file is available on SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-136">Add another action within the case to notify users that a new file is available on SharePoint.</span></span>
   - <span data-ttu-id="2e4f7-137">Add another case to handle when user selects `Reject`.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-137">Add another case to handle when user selects `Reject`.</span></span>
     - <span data-ttu-id="2e4f7-138">If rejected, send a notification email informing other approvers that the file is rejected and no further action is required.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-138">If rejected, send a notification email informing other approvers that the file is rejected and no further action is required.</span></span>
   - <span data-ttu-id="2e4f7-139">`SelectedOptions` provides only two options, so we can leave the **Default** case empty.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-139">`SelectedOptions` provides only two options, so we can leave the **Default** case empty.</span></span>

   ![Switch statement](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-switch-case/switch.jpg)

   > [!NOTE]
   > <span data-ttu-id="2e4f7-141">A switch statement needs at least one case in addition to the default case.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-141">A switch statement needs at least one case in addition to the default case.</span></span>

4. <span data-ttu-id="2e4f7-142">After the switch statement, delete the original file uploaded to Dropbox by adding this action: **Dropbox - Delete file**</span><span class="sxs-lookup"><span data-stu-id="2e4f7-142">After the switch statement, delete the original file uploaded to Dropbox by adding this action: **Dropbox - Delete file**</span></span>

5. <span data-ttu-id="2e4f7-143">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-143">Save your logic app.</span></span> <span data-ttu-id="2e4f7-144">Test your app by uploading a file to Dropbox.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-144">Test your app by uploading a file to Dropbox.</span></span> <span data-ttu-id="2e4f7-145">You should receive an approval email shortly.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-145">You should receive an approval email shortly.</span></span> <span data-ttu-id="2e4f7-146">Select an option, and observe the behavior.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-146">Select an option, and observe the behavior.</span></span>

   > [!TIP]
   > <span data-ttu-id="2e4f7-147">Check out how to [monitor your logic apps](logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="2e4f7-147">Check out how to [monitor your logic apps](logic-apps-monitor-your-logic-apps.md).</span></span>

## <a name="understand-the-code-behind-switch-statements"></a><span data-ttu-id="2e4f7-148">Understand the code behind switch statements</span><span class="sxs-lookup"><span data-stu-id="2e4f7-148">Understand the code behind switch statements</span></span>

<span data-ttu-id="2e4f7-149">Now that you successfully created a logic app using a switch statement, let's look at the code definition behind the switch statement.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-149">Now that you successfully created a logic app using a switch statement, let's look at the code definition behind the switch statement.</span></span>

```json
"Switch": {
    "type": "Switch",
    "expression": "@body('Send_approval_email')?['SelectedOption']",
    "cases": {
        "Case 1" : {
            "case" : "Approved",
            "actions" : {}
        },
        "Case 2" : {
            "case" : "Rejected",
            "actions" : {}
        }
    },
    "default": {
        "actions": {}
    },
    "runAfter": {
        "Send_approval_email": [
            "Succeeded"
        ]
    }
}
```

* <span data-ttu-id="2e4f7-150">`"Switch"` is the name of the switch statement, which you can rename for readability.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-150">`"Switch"` is the name of the switch statement, which you can rename for readability.</span></span> 
* <span data-ttu-id="2e4f7-151">`"type": "Switch"` indicates that the action is a switch statement.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-151">`"type": "Switch"` indicates that the action is a switch statement.</span></span> 
* <span data-ttu-id="2e4f7-152">`"expression"` is the approver's selected option in this example and is evaluated against each case declared later in the definition.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-152">`"expression"` is the approver's selected option in this example and is evaluated against each case declared later in the definition.</span></span> 
* <span data-ttu-id="2e4f7-153">`"cases"` can contain any number of cases.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-153">`"cases"` can contain any number of cases.</span></span> <span data-ttu-id="2e4f7-154">For each case, `"Case *"` is the default name of the case, which you can rename for readability.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-154">For each case, `"Case *"` is the default name of the case, which you can rename for readability.</span></span> 
<span data-ttu-id="2e4f7-155">`"case"` specifies the case label, which the switch expression uses for comparison, and must be a constant and unique value.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-155">`"case"` specifies the case label, which the switch expression uses for comparison, and must be a constant and unique value.</span></span> <span data-ttu-id="2e4f7-156">If none of the cases match the switch expression, actions under `"default"` are executed.</span><span class="sxs-lookup"><span data-stu-id="2e4f7-156">If none of the cases match the switch expression, actions under `"default"` are executed.</span></span>

## <a name="get-help"></a><span data-ttu-id="2e4f7-157">Get help</span><span class="sxs-lookup"><span data-stu-id="2e4f7-157">Get help</span></span>

<span data-ttu-id="2e4f7-158">To ask questions, answer questions, and see what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="2e4f7-158">To ask questions, answer questions, and see what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="2e4f7-159">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="2e4f7-159">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e4f7-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="2e4f7-160">Next steps</span></span>

- <span data-ttu-id="2e4f7-161">Learn how to [add conditions](logic-apps-use-logic-app-features.md)</span><span class="sxs-lookup"><span data-stu-id="2e4f7-161">Learn how to [add conditions](logic-apps-use-logic-app-features.md)</span></span>
- <span data-ttu-id="2e4f7-162">Learn about [error and exception handling](logic-apps-exception-handling.md)</span><span class="sxs-lookup"><span data-stu-id="2e4f7-162">Learn about [error and exception handling](logic-apps-exception-handling.md)</span></span>
- <span data-ttu-id="2e4f7-163">Explore more [workflow language capabilities](logic-apps-author-definitions.md)</span><span class="sxs-lookup"><span data-stu-id="2e4f7-163">Explore more [workflow language capabilities](logic-apps-author-definitions.md)</span></span>


