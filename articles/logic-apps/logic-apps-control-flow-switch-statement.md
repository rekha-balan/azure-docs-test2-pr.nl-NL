---
title: Add switch statements to workflows - Azure Logic Apps | Microsoft Docs
description: How to create switch statements that control workflow actions based on specific values in Azure Logic Apps
services: logic-apps
ms.service: logic-apps
author: ecfan
ms.author: estfan
manager: jeconnoc
ms.date: 03/05/2018
ms.topic: article
ms.reviewer: klam, LADocs
ms.suite: integration
ms.openlocfilehash: e15f89d4b7e33ce7e28676c219344f7d7d9cd465
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870580"
---
# <a name="create-switch-statements-that-run-workflow-actions-based-on-specific-values-in-azure-logic-apps"></a><span data-ttu-id="83fef-103">Create switch statements that run workflow actions based on specific values in Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="83fef-103">Create switch statements that run workflow actions based on specific values in Azure Logic Apps</span></span>

<span data-ttu-id="83fef-104">To run specific actions based on the values of objects, expressions, or tokens, add a *switch* statement.</span><span class="sxs-lookup"><span data-stu-id="83fef-104">To run specific actions based on the values of objects, expressions, or tokens, add a *switch* statement.</span></span> <span data-ttu-id="83fef-105">This structure evaluates the object, expression, or token, chooses the case that matches the result, and runs specific actions only for that case.</span><span class="sxs-lookup"><span data-stu-id="83fef-105">This structure evaluates the object, expression, or token, chooses the case that matches the result, and runs specific actions only for that case.</span></span> <span data-ttu-id="83fef-106">When the switch statement runs, only one case should match the result.</span><span class="sxs-lookup"><span data-stu-id="83fef-106">When the switch statement runs, only one case should match the result.</span></span>

<span data-ttu-id="83fef-107">For example, suppose you want a logic app that takes different steps based on an option selected in email.</span><span class="sxs-lookup"><span data-stu-id="83fef-107">For example, suppose you want a logic app that takes different steps based on an option selected in email.</span></span> <span data-ttu-id="83fef-108">In this example, the logic app checks a website's RSS feed for new content.</span><span class="sxs-lookup"><span data-stu-id="83fef-108">In this example, the logic app checks a website's RSS feed for new content.</span></span> <span data-ttu-id="83fef-109">When a new item appears in the RSS feed, the logic app sends email to an approver.</span><span class="sxs-lookup"><span data-stu-id="83fef-109">When a new item appears in the RSS feed, the logic app sends email to an approver.</span></span> <span data-ttu-id="83fef-110">Based on whether the approver selects "Approve" or "Reject", the logic app follows different steps.</span><span class="sxs-lookup"><span data-stu-id="83fef-110">Based on whether the approver selects "Approve" or "Reject", the logic app follows different steps.</span></span>

> [!TIP]
> <span data-ttu-id="83fef-111">Like all programming languages, switch statements support only equality operators.</span><span class="sxs-lookup"><span data-stu-id="83fef-111">Like all programming languages, switch statements support only equality operators.</span></span> <span data-ttu-id="83fef-112">If you need other relational operators, such as "greater than", use a [conditional statement](#conditions).</span><span class="sxs-lookup"><span data-stu-id="83fef-112">If you need other relational operators, such as "greater than", use a [conditional statement](#conditions).</span></span>
> <span data-ttu-id="83fef-113">To ensure deterministic execution behavior, cases must contain a unique and static value instead of dynamic tokens or expressions.</span><span class="sxs-lookup"><span data-stu-id="83fef-113">To ensure deterministic execution behavior, cases must contain a unique and static value instead of dynamic tokens or expressions.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83fef-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="83fef-114">Prerequisites</span></span>

* <span data-ttu-id="83fef-115">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="83fef-115">An Azure subscription.</span></span> <span data-ttu-id="83fef-116">If you don't have a subscription, [sign up for a free Azure account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="83fef-116">If you don't have a subscription, [sign up for a free Azure account](https://azure.microsoft.com/free/).</span></span>

* <span data-ttu-id="83fef-117">To follow the example in this article, [create this sample logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md) with an Outlook.com or Office 365 Outlook account.</span><span class="sxs-lookup"><span data-stu-id="83fef-117">To follow the example in this article, [create this sample logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md) with an Outlook.com or Office 365 Outlook account.</span></span>

  1. <span data-ttu-id="83fef-118">When you add the action to send email, select **Send an approval email** instead.</span><span class="sxs-lookup"><span data-stu-id="83fef-118">When you add the action to send email, select **Send an approval email** instead.</span></span>

     ![Select "Send an approval email"](./media/logic-apps-control-flow-switch-statement/send-approval-email-action.png)

  2. <span data-ttu-id="83fef-120">Provide the required fields, like the email address for the person who gets the approval email.</span><span class="sxs-lookup"><span data-stu-id="83fef-120">Provide the required fields, like the email address for the person who gets the approval email.</span></span> 
  <span data-ttu-id="83fef-121">Under **User Options**, enter "Approve, Reject".</span><span class="sxs-lookup"><span data-stu-id="83fef-121">Under **User Options**, enter "Approve, Reject".</span></span>

     ![Enter email details](./media/logic-apps-control-flow-switch-statement/send-approval-email-details.png)

## <a name="add-a-switch-statement"></a><span data-ttu-id="83fef-123">Add a switch statement</span><span class="sxs-lookup"><span data-stu-id="83fef-123">Add a switch statement</span></span>

1. <span data-ttu-id="83fef-124">At the end of the sample workflow, choose **+ New step** > **... More** > **Add a switch case**.</span><span class="sxs-lookup"><span data-stu-id="83fef-124">At the end of the sample workflow, choose **+ New step** > **... More** > **Add a switch case**.</span></span> 

   ![Add a switch statement](./media/logic-apps-control-flow-switch-statement/add-switch-statement.png)

   <span data-ttu-id="83fef-126">A switch statement appears with one case and a default case.</span><span class="sxs-lookup"><span data-stu-id="83fef-126">A switch statement appears with one case and a default case.</span></span> 
   <span data-ttu-id="83fef-127">A switch statement requires at least one case plus the default case.</span><span class="sxs-lookup"><span data-stu-id="83fef-127">A switch statement requires at least one case plus the default case.</span></span> 

   <span data-ttu-id="83fef-128">When you want to add a switch statement between steps, move the pointer over the arrow where you want to add the switch statement.</span><span class="sxs-lookup"><span data-stu-id="83fef-128">When you want to add a switch statement between steps, move the pointer over the arrow where you want to add the switch statement.</span></span> 
   <span data-ttu-id="83fef-129">Choose the **plus sign** (**+**) that appears, then choose **Add a switch case**.</span><span class="sxs-lookup"><span data-stu-id="83fef-129">Choose the **plus sign** (**+**) that appears, then choose **Add a switch case**.</span></span>

4. <span data-ttu-id="83fef-130">In the **On** box, select the **SelectedOption** field whose output determines the action to perform.</span><span class="sxs-lookup"><span data-stu-id="83fef-130">In the **On** box, select the **SelectedOption** field whose output determines the action to perform.</span></span> 
   
   <span data-ttu-id="83fef-131">You can select the field from the **Add dynamic content** list that appears.</span><span class="sxs-lookup"><span data-stu-id="83fef-131">You can select the field from the **Add dynamic content** list that appears.</span></span>

5. <span data-ttu-id="83fef-132">To handle the cases where the approver selects `Approve` or `Reject`, add another case between **Case** and **Default**.</span><span class="sxs-lookup"><span data-stu-id="83fef-132">To handle the cases where the approver selects `Approve` or `Reject`, add another case between **Case** and **Default**.</span></span> 
   
6. <span data-ttu-id="83fef-133">Add these actions to the corresponding cases:</span><span class="sxs-lookup"><span data-stu-id="83fef-133">Add these actions to the corresponding cases:</span></span>

   | <span data-ttu-id="83fef-134">Case #</span><span class="sxs-lookup"><span data-stu-id="83fef-134">Case #</span></span> | <span data-ttu-id="83fef-135">**SelectedOption**</span><span class="sxs-lookup"><span data-stu-id="83fef-135">**SelectedOption**</span></span> | <span data-ttu-id="83fef-136">Action</span><span class="sxs-lookup"><span data-stu-id="83fef-136">Action</span></span> |
   |:------ |:-------------------|:------ |
   | <span data-ttu-id="83fef-137">Case 1</span><span class="sxs-lookup"><span data-stu-id="83fef-137">Case 1</span></span> | <span data-ttu-id="83fef-138">**Approve**</span><span class="sxs-lookup"><span data-stu-id="83fef-138">**Approve**</span></span> | <span data-ttu-id="83fef-139">Add the Outlook **Send an email** action for sending details about the RSS item only when the approver selected **Approve**.</span><span class="sxs-lookup"><span data-stu-id="83fef-139">Add the Outlook **Send an email** action for sending details about the RSS item only when the approver selected **Approve**.</span></span> |
   | <span data-ttu-id="83fef-140">Case 2</span><span class="sxs-lookup"><span data-stu-id="83fef-140">Case 2</span></span> | <span data-ttu-id="83fef-141">**Reject**</span><span class="sxs-lookup"><span data-stu-id="83fef-141">**Reject**</span></span> | <span data-ttu-id="83fef-142">Add the Outlook **Send an email** action for notifying other approvers that the RSS item was rejected.</span><span class="sxs-lookup"><span data-stu-id="83fef-142">Add the Outlook **Send an email** action for notifying other approvers that the RSS item was rejected.</span></span> |
   | <span data-ttu-id="83fef-143">Default</span><span class="sxs-lookup"><span data-stu-id="83fef-143">Default</span></span> | <span data-ttu-id="83fef-144">\<none\></span><span class="sxs-lookup"><span data-stu-id="83fef-144">\<none\></span></span> | <span data-ttu-id="83fef-145">No action necessary.</span><span class="sxs-lookup"><span data-stu-id="83fef-145">No action necessary.</span></span> <span data-ttu-id="83fef-146">In this example, the **Default** case is empty because **SelectedOption** has only two options.</span><span class="sxs-lookup"><span data-stu-id="83fef-146">In this example, the **Default** case is empty because **SelectedOption** has only two options.</span></span> |
   |         |          |

   ![Switch statement](./media/logic-apps-control-flow-switch-statement/switch.png)

7. <span data-ttu-id="83fef-148">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="83fef-148">Save your logic app.</span></span> 

   <span data-ttu-id="83fef-149">To manually test this example, choose **Run** until the logic app finds a new RSS item and sends an approval email.</span><span class="sxs-lookup"><span data-stu-id="83fef-149">To manually test this example, choose **Run** until the logic app finds a new RSS item and sends an approval email.</span></span> 
   <span data-ttu-id="83fef-150">Select **Approve** to observe the results.</span><span class="sxs-lookup"><span data-stu-id="83fef-150">Select **Approve** to observe the results.</span></span>

## <a name="json-definition"></a><span data-ttu-id="83fef-151">JSON definition</span><span class="sxs-lookup"><span data-stu-id="83fef-151">JSON definition</span></span>

<span data-ttu-id="83fef-152">Now that you created a logic app using a switch statement, let's look at the high-level code definition behind the switch statement.</span><span class="sxs-lookup"><span data-stu-id="83fef-152">Now that you created a logic app using a switch statement, let's look at the high-level code definition behind the switch statement.</span></span>

``` json
"Switch": {
   "type": "Switch",
   "expression": "@body('Send_approval_email')?['SelectedOption']",
   "cases": {
      "Case" : {
         "actions" : {
           "Send_an_email": { }
         },
         "case" : "Approve"
      },
      "Case_2" : {
         "actions" : {
           "Send_an_email_2": { }
         },
         "case" : "Reject"
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

| <span data-ttu-id="83fef-153">Label</span><span class="sxs-lookup"><span data-stu-id="83fef-153">Label</span></span>              | <span data-ttu-id="83fef-154">Description</span><span class="sxs-lookup"><span data-stu-id="83fef-154">Description</span></span> |
| :----------------- | :---------- |
| `"Switch"`         | <span data-ttu-id="83fef-155">The name of the switch statement, which you can rename for readability</span><span class="sxs-lookup"><span data-stu-id="83fef-155">The name of the switch statement, which you can rename for readability</span></span> |
| `"type": "Switch"` | <span data-ttu-id="83fef-156">Specifies that the action is a switch statement</span><span class="sxs-lookup"><span data-stu-id="83fef-156">Specifies that the action is a switch statement</span></span> |
| `"expression"`     | <span data-ttu-id="83fef-157">In this example, specifies the approver's selected option that's evaluated against each case as declared later in the definition</span><span class="sxs-lookup"><span data-stu-id="83fef-157">In this example, specifies the approver's selected option that's evaluated against each case as declared later in the definition</span></span> |
| `"cases"` | <span data-ttu-id="83fef-158">Defines any number of cases.</span><span class="sxs-lookup"><span data-stu-id="83fef-158">Defines any number of cases.</span></span> <span data-ttu-id="83fef-159">For each case, `"Case_*"` is the default name for that case, which you can rename for readability</span><span class="sxs-lookup"><span data-stu-id="83fef-159">For each case, `"Case_*"` is the default name for that case, which you can rename for readability</span></span> |
| `"case"` | <span data-ttu-id="83fef-160">Specifies the case's value, which must be a constant and unique value that the switch statement uses for comparison.</span><span class="sxs-lookup"><span data-stu-id="83fef-160">Specifies the case's value, which must be a constant and unique value that the switch statement uses for comparison.</span></span> <span data-ttu-id="83fef-161">If no cases match the switch expression result, the actions in the `"default"` section are run.</span><span class="sxs-lookup"><span data-stu-id="83fef-161">If no cases match the switch expression result, the actions in the `"default"` section are run.</span></span>
|           |         |

## <a name="get-support"></a><span data-ttu-id="83fef-162">Get support</span><span class="sxs-lookup"><span data-stu-id="83fef-162">Get support</span></span>

* <span data-ttu-id="83fef-163">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="83fef-163">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>
* <span data-ttu-id="83fef-164">To submit or vote on features or suggestions, visit the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="83fef-164">To submit or vote on features or suggestions, visit the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="83fef-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="83fef-165">Next steps</span></span>

* [<span data-ttu-id="83fef-166">Run steps based on a condition (conditional statements)</span><span class="sxs-lookup"><span data-stu-id="83fef-166">Run steps based on a condition (conditional statements)</span></span>](../logic-apps/logic-apps-control-flow-conditional-statement.md)
* [<span data-ttu-id="83fef-167">Run and repeat steps (loops)</span><span class="sxs-lookup"><span data-stu-id="83fef-167">Run and repeat steps (loops)</span></span>](../logic-apps/logic-apps-control-flow-loops.md)
* [<span data-ttu-id="83fef-168">Run or merge parallel steps (branches)</span><span class="sxs-lookup"><span data-stu-id="83fef-168">Run or merge parallel steps (branches)</span></span>](../logic-apps/logic-apps-control-flow-branches.md)
* [<span data-ttu-id="83fef-169">Run steps based on grouped action status (scopes)</span><span class="sxs-lookup"><span data-stu-id="83fef-169">Run steps based on grouped action status (scopes)</span></span>](../logic-apps/logic-apps-control-flow-run-steps-group-scopes.md)
