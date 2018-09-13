---
title: Add conditional statements to workflows - Azure Logic Apps | Microsoft Docs
description: How to create conditions that control actions in workflows in Azure Logic Apps
services: logic-apps
ms.service: logic-apps
author: ecfan
ms.author: estfan
manager: jeconnoc
ms.date: 03/05/2018
ms.topic: article
ms.reviewer: klam, LADocs
ms.suite: integration
ms.openlocfilehash: d4e69d33e07f484b4ccc5343786865230368c7ca
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856664"
---
# <a name="create-conditional-statements-that-control-workflow-actions-in-azure-logic-apps"></a><span data-ttu-id="f964f-103">Create conditional statements that control workflow actions in Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="f964f-103">Create conditional statements that control workflow actions in Azure Logic Apps</span></span>

<span data-ttu-id="f964f-104">To run specific actions in your logic app only after passing a specified condition, add a *conditional statement*.</span><span class="sxs-lookup"><span data-stu-id="f964f-104">To run specific actions in your logic app only after passing a specified condition, add a *conditional statement*.</span></span> <span data-ttu-id="f964f-105">This structure compares the data in your workflow against specific values or fields.</span><span class="sxs-lookup"><span data-stu-id="f964f-105">This structure compares the data in your workflow against specific values or fields.</span></span> <span data-ttu-id="f964f-106">You can then define different actions that run based on whether or not the data meets the condition.</span><span class="sxs-lookup"><span data-stu-id="f964f-106">You can then define different actions that run based on whether or not the data meets the condition.</span></span> <span data-ttu-id="f964f-107">You can nest conditions inside each other.</span><span class="sxs-lookup"><span data-stu-id="f964f-107">You can nest conditions inside each other.</span></span>

<span data-ttu-id="f964f-108">For example, suppose you have a logic app that sends too many emails when new items appear on a website's RSS feed.</span><span class="sxs-lookup"><span data-stu-id="f964f-108">For example, suppose you have a logic app that sends too many emails when new items appear on a website's RSS feed.</span></span> <span data-ttu-id="f964f-109">You can add a conditional statement to send email only when the new item includes a specific string.</span><span class="sxs-lookup"><span data-stu-id="f964f-109">You can add a conditional statement to send email only when the new item includes a specific string.</span></span> 

> [!TIP]
> <span data-ttu-id="f964f-110">To run different steps based on different specific values, use a [*switch statement*](../logic-apps/logic-apps-control-flow-switch-statement.md) instead.</span><span class="sxs-lookup"><span data-stu-id="f964f-110">To run different steps based on different specific values, use a [*switch statement*](../logic-apps/logic-apps-control-flow-switch-statement.md) instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f964f-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f964f-111">Prerequisites</span></span>

* <span data-ttu-id="f964f-112">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="f964f-112">An Azure subscription.</span></span> <span data-ttu-id="f964f-113">If you don't have a subscription, [sign up for a free Azure account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="f964f-113">If you don't have a subscription, [sign up for a free Azure account](https://azure.microsoft.com/free/).</span></span>

* <span data-ttu-id="f964f-114">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span><span class="sxs-lookup"><span data-stu-id="f964f-114">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span></span>

* <span data-ttu-id="f964f-115">To follow the example in this article, [create this sample logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md) with an Outlook.com or Office 365 Outlook account.</span><span class="sxs-lookup"><span data-stu-id="f964f-115">To follow the example in this article, [create this sample logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md) with an Outlook.com or Office 365 Outlook account.</span></span>

## <a name="add-a-condition"></a><span data-ttu-id="f964f-116">Add a condition</span><span class="sxs-lookup"><span data-stu-id="f964f-116">Add a condition</span></span>

1. <span data-ttu-id="f964f-117">In the <a href="https://portal.azure.com" target="_blank">Azure portal</a>, open your logic app in Logic App Designer.</span><span class="sxs-lookup"><span data-stu-id="f964f-117">In the <a href="https://portal.azure.com" target="_blank">Azure portal</a>, open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="f964f-118">Add a condition at the location that you want.</span><span class="sxs-lookup"><span data-stu-id="f964f-118">Add a condition at the location that you want.</span></span> 

   <span data-ttu-id="f964f-119">To add a condition between steps, move the pointer over the arrow where you want to add the condition.</span><span class="sxs-lookup"><span data-stu-id="f964f-119">To add a condition between steps, move the pointer over the arrow where you want to add the condition.</span></span> <span data-ttu-id="f964f-120">Choose the **plus sign** (**+**) that appears, then choose **Add a condition**.</span><span class="sxs-lookup"><span data-stu-id="f964f-120">Choose the **plus sign** (**+**) that appears, then choose **Add a condition**.</span></span> <span data-ttu-id="f964f-121">For example:</span><span class="sxs-lookup"><span data-stu-id="f964f-121">For example:</span></span>

   ![Add condition between steps](./media/logic-apps-control-flow-conditional-statement/add-condition.png)

   <span data-ttu-id="f964f-123">When you want to add a condition at the end of your workflow, at the bottom of your logic app, choose  **+ New step** > **Add a condition**.</span><span class="sxs-lookup"><span data-stu-id="f964f-123">When you want to add a condition at the end of your workflow, at the bottom of your logic app, choose  **+ New step** > **Add a condition**.</span></span>

3. <span data-ttu-id="f964f-124">Under **Condition**, build your condition.</span><span class="sxs-lookup"><span data-stu-id="f964f-124">Under **Condition**, build your condition.</span></span> 

   1. <span data-ttu-id="f964f-125">In the left box, specify the data or field that you want to compare.</span><span class="sxs-lookup"><span data-stu-id="f964f-125">In the left box, specify the data or field that you want to compare.</span></span>

      <span data-ttu-id="f964f-126">When you click inside the left box, the dynamic content list appears so you can select outputs from previous steps in your logic app.</span><span class="sxs-lookup"><span data-stu-id="f964f-126">When you click inside the left box, the dynamic content list appears so you can select outputs from previous steps in your logic app.</span></span> 
      <span data-ttu-id="f964f-127">For this example, select the RSS feed summary.</span><span class="sxs-lookup"><span data-stu-id="f964f-127">For this example, select the RSS feed summary.</span></span>

      ![Build your condition](./media/logic-apps-control-flow-conditional-statement/edit-condition.png)

   2. <span data-ttu-id="f964f-129">In the middle list, select the operation to perform.</span><span class="sxs-lookup"><span data-stu-id="f964f-129">In the middle list, select the operation to perform.</span></span> 
   <span data-ttu-id="f964f-130">For this example, select "**contains**".</span><span class="sxs-lookup"><span data-stu-id="f964f-130">For this example, select "**contains**".</span></span> 

   3. <span data-ttu-id="f964f-131">In the right box, specify a value or field as your criteria.</span><span class="sxs-lookup"><span data-stu-id="f964f-131">In the right box, specify a value or field as your criteria.</span></span> 
   <span data-ttu-id="f964f-132">For this example, specify this string: **Microsoft**</span><span class="sxs-lookup"><span data-stu-id="f964f-132">For this example, specify this string: **Microsoft**</span></span>

   <span data-ttu-id="f964f-133">Here's the complete condition:</span><span class="sxs-lookup"><span data-stu-id="f964f-133">Here's the complete condition:</span></span>

   ![Complete condition](./media/logic-apps-control-flow-conditional-statement/edit-condition-2.png)

5. <span data-ttu-id="f964f-135">Under **If true** and **If false**, add the steps to perform based on whether the condition is met.</span><span class="sxs-lookup"><span data-stu-id="f964f-135">Under **If true** and **If false**, add the steps to perform based on whether the condition is met.</span></span> <span data-ttu-id="f964f-136">For example:</span><span class="sxs-lookup"><span data-stu-id="f964f-136">For example:</span></span>

   ![Condition with "If true" and "If false" paths](./media/logic-apps-control-flow-conditional-statement/condition-yes-no-path.png)

   > [!TIP]
   > <span data-ttu-id="f964f-138">You can drag existing actions into the **If true** and **If false** paths.</span><span class="sxs-lookup"><span data-stu-id="f964f-138">You can drag existing actions into the **If true** and **If false** paths.</span></span>

6. <span data-ttu-id="f964f-139">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="f964f-139">Save your logic app.</span></span>

<span data-ttu-id="f964f-140">Now this logic app only sends mail when the new items in the RSS feed meet your condition.</span><span class="sxs-lookup"><span data-stu-id="f964f-140">Now this logic app only sends mail when the new items in the RSS feed meet your condition.</span></span>

## <a name="json-definition"></a><span data-ttu-id="f964f-141">JSON definition</span><span class="sxs-lookup"><span data-stu-id="f964f-141">JSON definition</span></span>

<span data-ttu-id="f964f-142">Now that you created a logic app using a conditional statement, let's look at the high-level code definition behind the conditional statement.</span><span class="sxs-lookup"><span data-stu-id="f964f-142">Now that you created a logic app using a conditional statement, let's look at the high-level code definition behind the conditional statement.</span></span>

``` json
"actions": {
  "Condition": {
    "type": "If",
    "actions": {
      "Send_an_email": {
        "inputs": {},
        "runAfter": {}
    },
    "expression": {
      "and": [ 
        { 
          "contains": [ 
            "@triggerBody()?['summary']", "Microsoft"
          ]
        } 
      ]
    },
    "runAfter": {}
  }
},
```

## <a name="get-support"></a><span data-ttu-id="f964f-143">Get support</span><span class="sxs-lookup"><span data-stu-id="f964f-143">Get support</span></span>

* <span data-ttu-id="f964f-144">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="f964f-144">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>
* <span data-ttu-id="f964f-145">To submit or vote on features and suggestions, visit the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="f964f-145">To submit or vote on features and suggestions, visit the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f964f-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="f964f-146">Next steps</span></span>

* [<span data-ttu-id="f964f-147">Run steps based on different values (switch statements)</span><span class="sxs-lookup"><span data-stu-id="f964f-147">Run steps based on different values (switch statements)</span></span>](../logic-apps/logic-apps-control-flow-switch-statement.md)
* [<span data-ttu-id="f964f-148">Run and repeat steps (loops)</span><span class="sxs-lookup"><span data-stu-id="f964f-148">Run and repeat steps (loops)</span></span>](../logic-apps/logic-apps-control-flow-loops.md)
* [<span data-ttu-id="f964f-149">Run or merge parallel steps (branches)</span><span class="sxs-lookup"><span data-stu-id="f964f-149">Run or merge parallel steps (branches)</span></span>](../logic-apps/logic-apps-control-flow-branches.md)
* [<span data-ttu-id="f964f-150">Run steps based on grouped action status (scopes)</span><span class="sxs-lookup"><span data-stu-id="f964f-150">Run steps based on grouped action status (scopes)</span></span>](../logic-apps/logic-apps-control-flow-run-steps-group-scopes.md)
