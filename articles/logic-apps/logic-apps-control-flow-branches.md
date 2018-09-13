---
title: Create or join parallel branches - Azure Logic Apps | Microsoft Docs
description: How to create or join parallel branches for workflows in Azure Logic Apps
services: logic-apps
ms.service: logic-apps
author: ecfan
ms.author: estfan
manager: jeconnoc
ms.date: 03/05/2018
ms.topic: article
ms.reviewer: klam, LADocs
ms.suite: integration
ms.openlocfilehash: 2a8dcd82b67ee64e5687d8687415056b0aab39aa
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856470"
---
# <a name="create-or-join-parallel-branches-for-workflow-actions-in-azure-logic-apps"></a><span data-ttu-id="0b1c9-103">Create or join parallel branches for workflow actions in Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="0b1c9-103">Create or join parallel branches for workflow actions in Azure Logic Apps</span></span>

<span data-ttu-id="0b1c9-104">By default, your actions in logic app workflows run sequentially.</span><span class="sxs-lookup"><span data-stu-id="0b1c9-104">By default, your actions in logic app workflows run sequentially.</span></span> <span data-ttu-id="0b1c9-105">To perform independent actions at the same time, you can create [parallel branches](#parallel-branches), and then [join those branches](#join-branches) later in your flow.</span><span class="sxs-lookup"><span data-stu-id="0b1c9-105">To perform independent actions at the same time, you can create [parallel branches](#parallel-branches), and then [join those branches](#join-branches) later in your flow.</span></span> 

> [!TIP] 
> <span data-ttu-id="0b1c9-106">If you have a trigger that receives an array and want to run a workflow for each array item, you can *debatch* that array with the [**SplitOn** trigger property](../logic-apps/logic-apps-workflow-actions-triggers.md#split-on-debatch).</span><span class="sxs-lookup"><span data-stu-id="0b1c9-106">If you have a trigger that receives an array and want to run a workflow for each array item, you can *debatch* that array with the [**SplitOn** trigger property](../logic-apps/logic-apps-workflow-actions-triggers.md#split-on-debatch).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b1c9-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0b1c9-107">Prerequisites</span></span>

* <span data-ttu-id="0b1c9-108">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="0b1c9-108">An Azure subscription.</span></span> <span data-ttu-id="0b1c9-109">If you don't have a subscription, [sign up for a free Azure account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="0b1c9-109">If you don't have a subscription, [sign up for a free Azure account](https://azure.microsoft.com/free/).</span></span> 

* <span data-ttu-id="0b1c9-110">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span><span class="sxs-lookup"><span data-stu-id="0b1c9-110">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span></span>

<a name="parallel-branches"></a>

## <a name="add-a-parallel-branch"></a><span data-ttu-id="0b1c9-111">Add a parallel branch</span><span class="sxs-lookup"><span data-stu-id="0b1c9-111">Add a parallel branch</span></span>

<span data-ttu-id="0b1c9-112">To run independent steps at the same time, you can add parallel branches next to an existing step.</span><span class="sxs-lookup"><span data-stu-id="0b1c9-112">To run independent steps at the same time, you can add parallel branches next to an existing step.</span></span> 

![Run steps in parallel](media/logic-apps-control-flow-branches/parallel.png)

<span data-ttu-id="0b1c9-114">Your logic app waits for all branches to finish before continuing workflow.</span><span class="sxs-lookup"><span data-stu-id="0b1c9-114">Your logic app waits for all branches to finish before continuing workflow.</span></span>
<span data-ttu-id="0b1c9-115">Parallel branches run only when their `runAfter` property values match the finished parent step's status.</span><span class="sxs-lookup"><span data-stu-id="0b1c9-115">Parallel branches run only when their `runAfter` property values match the finished parent step's status.</span></span> <span data-ttu-id="0b1c9-116">For example, both `branchAction1` and `branchAction2` are set to run only when the `parentAction` completes with `Succeded` status.</span><span class="sxs-lookup"><span data-stu-id="0b1c9-116">For example, both `branchAction1` and `branchAction2` are set to run only when the `parentAction` completes with `Succeded` status.</span></span>

> [!NOTE]
> <span data-ttu-id="0b1c9-117">Before you start, your logic app must already have a step where you can add parallel branches.</span><span class="sxs-lookup"><span data-stu-id="0b1c9-117">Before you start, your logic app must already have a step where you can add parallel branches.</span></span>

1. <span data-ttu-id="0b1c9-118">In the <a href="https://portal.azure.com" target="_blank">Azure portal</a>, open your logic app in Logic App Designer.</span><span class="sxs-lookup"><span data-stu-id="0b1c9-118">In the <a href="https://portal.azure.com" target="_blank">Azure portal</a>, open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="0b1c9-119">Move your mouse over the arrow above the step where you want to add parallel branches.</span><span class="sxs-lookup"><span data-stu-id="0b1c9-119">Move your mouse over the arrow above the step where you want to add parallel branches.</span></span>

3. <span data-ttu-id="0b1c9-120">Choose the **plus** sign (**+**), choose **Add a parallel branch**, and select the item that you want to add.</span><span class="sxs-lookup"><span data-stu-id="0b1c9-120">Choose the **plus** sign (**+**), choose **Add a parallel branch**, and select the item that you want to add.</span></span>

   ![Add parallel branch](media/logic-apps-control-flow-branches/add-parallel-branch.png)

   <span data-ttu-id="0b1c9-122">Your selected item now appears in a parallel branch.</span><span class="sxs-lookup"><span data-stu-id="0b1c9-122">Your selected item now appears in a parallel branch.</span></span>

4. <span data-ttu-id="0b1c9-123">For each parallel branch, add the steps that you want.</span><span class="sxs-lookup"><span data-stu-id="0b1c9-123">For each parallel branch, add the steps that you want.</span></span> <span data-ttu-id="0b1c9-124">To add a sequential action to a parallel branch, move your mouse under the action where you want to add the sequential action.</span><span class="sxs-lookup"><span data-stu-id="0b1c9-124">To add a sequential action to a parallel branch, move your mouse under the action where you want to add the sequential action.</span></span> <span data-ttu-id="0b1c9-125">Choose the **plus** (**+**) sign and the step that you want to add.</span><span class="sxs-lookup"><span data-stu-id="0b1c9-125">Choose the **plus** (**+**) sign and the step that you want to add.</span></span>

   ![Add sequential step to parallel branch](media/logic-apps-control-flow-branches/add-sequential-action-parallel-branch.png)

5. <span data-ttu-id="0b1c9-127">To merge branches back together, [join your parallel branches](#join-branches).</span><span class="sxs-lookup"><span data-stu-id="0b1c9-127">To merge branches back together, [join your parallel branches](#join-branches).</span></span> 

<a name="parallel-json"></a>

## <a name="parallel-branch-definition-json"></a><span data-ttu-id="0b1c9-128">Parallel branch definition (JSON)</span><span class="sxs-lookup"><span data-stu-id="0b1c9-128">Parallel branch definition (JSON)</span></span>

<span data-ttu-id="0b1c9-129">If you're working in code view, you can define the parallel structure in your logic app's JSON definition instead, for example:</span><span class="sxs-lookup"><span data-stu-id="0b1c9-129">If you're working in code view, you can define the parallel structure in your logic app's JSON definition instead, for example:</span></span>

``` json
{
  "triggers": {
    "myTrigger": { }
  },
  "actions": {
    "parentAction": {
      "type": "<action-type>",
      "inputs": { },
      "runAfter": {}
    },
    "branchAction1": {
      "type": "<action-type>",
      "inputs": { },
      "runAfter": {
        "parentAction": [
          "Succeeded"
        ]
      }
    },
    "branchAction2": {
      "type": "<action-type>",
      "inputs": { },
      "runAfter": {
        "parentAction": [
          "Succeeded"
        ]
      }
    }
  },
  "outputs": {}
}
```

<a name="join-branches"></a>

## <a name="join-parallel-branches"></a><span data-ttu-id="0b1c9-130">Join parallel branches</span><span class="sxs-lookup"><span data-stu-id="0b1c9-130">Join parallel branches</span></span>

<span data-ttu-id="0b1c9-131">To merge parallel branches together, just add a step at the bottom under all the branches.</span><span class="sxs-lookup"><span data-stu-id="0b1c9-131">To merge parallel branches together, just add a step at the bottom under all the branches.</span></span> <span data-ttu-id="0b1c9-132">This step runs after all the parallel branches finish running.</span><span class="sxs-lookup"><span data-stu-id="0b1c9-132">This step runs after all the parallel branches finish running.</span></span>

![Join parallel branches](media/logic-apps-control-flow-branches/join.png)

1. <span data-ttu-id="0b1c9-134">In the [Azure portal](https://portal.azure.com), find and open your logic app in Logic App Designer.</span><span class="sxs-lookup"><span data-stu-id="0b1c9-134">In the [Azure portal](https://portal.azure.com), find and open your logic app in Logic App Designer.</span></span> 

2. <span data-ttu-id="0b1c9-135">Under the parallel branches that you want to join, add the step that you want to perform.</span><span class="sxs-lookup"><span data-stu-id="0b1c9-135">Under the parallel branches that you want to join, add the step that you want to perform.</span></span>

   ![Add a step that joins parallel branches](media/logic-apps-control-flow-branches/join-steps.png)

   <span data-ttu-id="0b1c9-137">Your parallel branches are now merged.</span><span class="sxs-lookup"><span data-stu-id="0b1c9-137">Your parallel branches are now merged.</span></span>

<a name="join-json"></a>

## <a name="join-definition-json"></a><span data-ttu-id="0b1c9-138">Join definition (JSON)</span><span class="sxs-lookup"><span data-stu-id="0b1c9-138">Join definition (JSON)</span></span>

<span data-ttu-id="0b1c9-139">If you're working in code view, you can define the join structure in your logic app's JSON definition instead, for example:</span><span class="sxs-lookup"><span data-stu-id="0b1c9-139">If you're working in code view, you can define the join structure in your logic app's JSON definition instead, for example:</span></span>

``` json
{
  "triggers": {
    "myTrigger": { }
  },
  "actions": {
    "parentAction": {
      "type": "<action-type>",
      "inputs": { },
      "runAfter": {}
    },
    "branchAction1": {
      "type": "<action-type>",
      "inputs": { },
      "runAfter": {
        "parentAction": [
          "Succeeded"
        ]
      }
    },
    "branchAction2": {
      "type": "<action-type>",
      "inputs": { },
      "runAfter": {
        "parentAction": [
          "Succeeded"
        ]
      }
    },
    "joinAction": {
      "type": "<action-type>",
      "inputs": { },
      "runAfter": {
        "branchAction1": [
          "Succeeded"
        ],
        "branchAction2": [
          "Succeeded"
        ]
      }
    }
  },
  "outputs": {}
}
```

## <a name="get-support"></a><span data-ttu-id="0b1c9-140">Get support</span><span class="sxs-lookup"><span data-stu-id="0b1c9-140">Get support</span></span>

* <span data-ttu-id="0b1c9-141">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="0b1c9-141">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>
* <span data-ttu-id="0b1c9-142">To submit or vote on features and suggestions, visit the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="0b1c9-142">To submit or vote on features and suggestions, visit the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b1c9-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="0b1c9-143">Next steps</span></span>

* [<span data-ttu-id="0b1c9-144">Run steps based on a condition (conditional statements)</span><span class="sxs-lookup"><span data-stu-id="0b1c9-144">Run steps based on a condition (conditional statements)</span></span>](../logic-apps/logic-apps-control-flow-conditional-statement.md)
* [<span data-ttu-id="0b1c9-145">Run steps based on different values (switch statements)</span><span class="sxs-lookup"><span data-stu-id="0b1c9-145">Run steps based on different values (switch statements)</span></span>](../logic-apps/logic-apps-control-flow-switch-statement.md)
* [<span data-ttu-id="0b1c9-146">Run and repeat steps (loops)</span><span class="sxs-lookup"><span data-stu-id="0b1c9-146">Run and repeat steps (loops)</span></span>](../logic-apps/logic-apps-control-flow-loops.md)
* [<span data-ttu-id="0b1c9-147">Run steps based on grouped action status (scopes)</span><span class="sxs-lookup"><span data-stu-id="0b1c9-147">Run steps based on grouped action status (scopes)</span></span>](../logic-apps/logic-apps-control-flow-run-steps-group-scopes.md)
