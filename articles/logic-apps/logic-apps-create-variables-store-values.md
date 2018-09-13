---
title: Create variables for saving values - Azure Logic Apps | Microsoft Docs
description: How to save and manage values by creating variables in Azure Logic Apps
services: logic-apps
author: ecfan
manager: jeconnoc
ms.author: estfan
ms.topic: article
ms.date: 05/30/2018
ms.service: logic-apps
ms.reviewer: klam, LADocs
ms.suite: integration
ms.openlocfilehash: 0efce9fbbbd241f335f08bb258b6ba343982fdb9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865304"
---
# <a name="create-variables-for-saving-and-managing-values-in-azure-logic-apps"></a><span data-ttu-id="827ba-103">Create variables for saving and managing values in Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="827ba-103">Create variables for saving and managing values in Azure Logic Apps</span></span>

<span data-ttu-id="827ba-104">This article shows how you can store and work with values throughout your logic app by creating variables.</span><span class="sxs-lookup"><span data-stu-id="827ba-104">This article shows how you can store and work with values throughout your logic app by creating variables.</span></span> <span data-ttu-id="827ba-105">For example, variables can help you count the number of times that a loop runs.</span><span class="sxs-lookup"><span data-stu-id="827ba-105">For example, variables can help you count the number of times that a loop runs.</span></span> <span data-ttu-id="827ba-106">When iterating over an array or checking an array for a specific item, you can use a variable to reference the index number for each array item.</span><span class="sxs-lookup"><span data-stu-id="827ba-106">When iterating over an array or checking an array for a specific item, you can use a variable to reference the index number for each array item.</span></span> 

<span data-ttu-id="827ba-107">You can create variables for data types such as integer, float, boolean, string, array, and object.</span><span class="sxs-lookup"><span data-stu-id="827ba-107">You can create variables for data types such as integer, float, boolean, string, array, and object.</span></span> <span data-ttu-id="827ba-108">After you create a variable, you can perform other tasks, for example:</span><span class="sxs-lookup"><span data-stu-id="827ba-108">After you create a variable, you can perform other tasks, for example:</span></span>

* <span data-ttu-id="827ba-109">Get or reference the variable's value.</span><span class="sxs-lookup"><span data-stu-id="827ba-109">Get or reference the variable's value.</span></span>
* <span data-ttu-id="827ba-110">Increase or decrease the variable by a constant value, also known as *increment* and *decrement*.</span><span class="sxs-lookup"><span data-stu-id="827ba-110">Increase or decrease the variable by a constant value, also known as *increment* and *decrement*.</span></span>
* <span data-ttu-id="827ba-111">Assign a different value to the variable.</span><span class="sxs-lookup"><span data-stu-id="827ba-111">Assign a different value to the variable.</span></span>
* <span data-ttu-id="827ba-112">Insert or *append* the variable's value as the last time in a string or array.</span><span class="sxs-lookup"><span data-stu-id="827ba-112">Insert or *append* the variable's value as the last time in a string or array.</span></span>

<span data-ttu-id="827ba-113">Variables exist and are global only within the logic app instance that creates them.</span><span class="sxs-lookup"><span data-stu-id="827ba-113">Variables exist and are global only within the logic app instance that creates them.</span></span> <span data-ttu-id="827ba-114">Also, they persist across any loop iterations inside a logic app instance.</span><span class="sxs-lookup"><span data-stu-id="827ba-114">Also, they persist across any loop iterations inside a logic app instance.</span></span> <span data-ttu-id="827ba-115">When referencing a variable, use the variable's name as the token, not the action's name, which is the usual way to reference an action's outputs.</span><span class="sxs-lookup"><span data-stu-id="827ba-115">When referencing a variable, use the variable's name as the token, not the action's name, which is the usual way to reference an action's outputs.</span></span>

<span data-ttu-id="827ba-116">If you don't have an Azure subscription yet, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span><span class="sxs-lookup"><span data-stu-id="827ba-116">If you don't have an Azure subscription yet, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="827ba-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="827ba-117">Prerequisites</span></span>

<span data-ttu-id="827ba-118">To follow this article, here are the items you need:</span><span class="sxs-lookup"><span data-stu-id="827ba-118">To follow this article, here are the items you need:</span></span>

* <span data-ttu-id="827ba-119">The logic app where you want to create a variable</span><span class="sxs-lookup"><span data-stu-id="827ba-119">The logic app where you want to create a variable</span></span> 

  <span data-ttu-id="827ba-120">If you're new to logic apps, review [What is Azure Logic Apps](../logic-apps/logic-apps-overview.md) and [Quickstart: Create your first logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="827ba-120">If you're new to logic apps, review [What is Azure Logic Apps](../logic-apps/logic-apps-overview.md) and [Quickstart: Create your first logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span></span>

* <span data-ttu-id="827ba-121">A [trigger](../logic-apps/logic-apps-overview.md#logic-app-concepts) as the first step in your logic app</span><span class="sxs-lookup"><span data-stu-id="827ba-121">A [trigger](../logic-apps/logic-apps-overview.md#logic-app-concepts) as the first step in your logic app</span></span> 

  <span data-ttu-id="827ba-122">Before you can add actions for creating and working with variables, your logic app must start with a trigger.</span><span class="sxs-lookup"><span data-stu-id="827ba-122">Before you can add actions for creating and working with variables, your logic app must start with a trigger.</span></span>

<a name="create-variable"></a>

## <a name="initialize-variable"></a><span data-ttu-id="827ba-123">Initialize variable</span><span class="sxs-lookup"><span data-stu-id="827ba-123">Initialize variable</span></span>

<span data-ttu-id="827ba-124">You can create a variable and declare its data type and initial value - all within one action in your logic app.</span><span class="sxs-lookup"><span data-stu-id="827ba-124">You can create a variable and declare its data type and initial value - all within one action in your logic app.</span></span> <span data-ttu-id="827ba-125">You can only declare variables at the global level, not within scopes, conditions, and loops.</span><span class="sxs-lookup"><span data-stu-id="827ba-125">You can only declare variables at the global level, not within scopes, conditions, and loops.</span></span> 

1. <span data-ttu-id="827ba-126">In the <a href="https://portal.azure.com" target="_blank">Azure portal</a> or Visual Studio, open your logic app in Logic App Designer.</span><span class="sxs-lookup"><span data-stu-id="827ba-126">In the <a href="https://portal.azure.com" target="_blank">Azure portal</a> or Visual Studio, open your logic app in Logic App Designer.</span></span> 

   <span data-ttu-id="827ba-127">This example uses the Azure portal and a logic app with an existing trigger.</span><span class="sxs-lookup"><span data-stu-id="827ba-127">This example uses the Azure portal and a logic app with an existing trigger.</span></span>

2. <span data-ttu-id="827ba-128">In your logic app, under the step where you want to add a variable, follow one of these steps:</span><span class="sxs-lookup"><span data-stu-id="827ba-128">In your logic app, under the step where you want to add a variable, follow one of these steps:</span></span> 

   * <span data-ttu-id="827ba-129">To add an action under the last step, choose **New step** > **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="827ba-129">To add an action under the last step, choose **New step** > **Add an action**.</span></span>

     ![Add action](./media/logic-apps-create-variables-store-values/add-action.png)

   * <span data-ttu-id="827ba-131">To add an action between steps, move your mouse over the connecting arrow so the plus sign (+) appears.</span><span class="sxs-lookup"><span data-stu-id="827ba-131">To add an action between steps, move your mouse over the connecting arrow so the plus sign (+) appears.</span></span> 
   <span data-ttu-id="827ba-132">Choose the plus sign, and then choose **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="827ba-132">Choose the plus sign, and then choose **Add an action**.</span></span>

3. <span data-ttu-id="827ba-133">In the search box, enter "variables" as your filter.</span><span class="sxs-lookup"><span data-stu-id="827ba-133">In the search box, enter "variables" as your filter.</span></span> <span data-ttu-id="827ba-134">From the actions list, select **Variables - Initialize variable**.</span><span class="sxs-lookup"><span data-stu-id="827ba-134">From the actions list, select **Variables - Initialize variable**.</span></span>

   ![Select action](./media/logic-apps-create-variables-store-values/select-initialize-variable-action.png)

4. <span data-ttu-id="827ba-136">Provide this information for your variable:</span><span class="sxs-lookup"><span data-stu-id="827ba-136">Provide this information for your variable:</span></span>

   | <span data-ttu-id="827ba-137">Property</span><span class="sxs-lookup"><span data-stu-id="827ba-137">Property</span></span> | <span data-ttu-id="827ba-138">Required</span><span class="sxs-lookup"><span data-stu-id="827ba-138">Required</span></span> | <span data-ttu-id="827ba-139">Value</span><span class="sxs-lookup"><span data-stu-id="827ba-139">Value</span></span> |  <span data-ttu-id="827ba-140">Description</span><span class="sxs-lookup"><span data-stu-id="827ba-140">Description</span></span> |
   |----------|----------|-------|--------------|
   | <span data-ttu-id="827ba-141">Name</span><span class="sxs-lookup"><span data-stu-id="827ba-141">Name</span></span> | <span data-ttu-id="827ba-142">Yes</span><span class="sxs-lookup"><span data-stu-id="827ba-142">Yes</span></span> | <span data-ttu-id="827ba-143"><*variable-name*></span><span class="sxs-lookup"><span data-stu-id="827ba-143"><*variable-name*></span></span> | <span data-ttu-id="827ba-144">The name for the variable to increment</span><span class="sxs-lookup"><span data-stu-id="827ba-144">The name for the variable to increment</span></span> | 
   | <span data-ttu-id="827ba-145">Type</span><span class="sxs-lookup"><span data-stu-id="827ba-145">Type</span></span> | <span data-ttu-id="827ba-146">Yes</span><span class="sxs-lookup"><span data-stu-id="827ba-146">Yes</span></span> | <span data-ttu-id="827ba-147"><*variable-type*></span><span class="sxs-lookup"><span data-stu-id="827ba-147"><*variable-type*></span></span> | <span data-ttu-id="827ba-148">The data type for the variable</span><span class="sxs-lookup"><span data-stu-id="827ba-148">The data type for the variable</span></span> | 
   | <span data-ttu-id="827ba-149">Value</span><span class="sxs-lookup"><span data-stu-id="827ba-149">Value</span></span> | <span data-ttu-id="827ba-150">No</span><span class="sxs-lookup"><span data-stu-id="827ba-150">No</span></span> | <span data-ttu-id="827ba-151"><*start-value*></span><span class="sxs-lookup"><span data-stu-id="827ba-151"><*start-value*></span></span> | <span data-ttu-id="827ba-152">The initial value for your variable</span><span class="sxs-lookup"><span data-stu-id="827ba-152">The initial value for your variable</span></span> <p><p><span data-ttu-id="827ba-153">**Tip**: Although optional, set this value as a best practice so you always know the start value for your variable.</span><span class="sxs-lookup"><span data-stu-id="827ba-153">**Tip**: Although optional, set this value as a best practice so you always know the start value for your variable.</span></span> | 
   ||||| 

   ![Initialize variable](./media/logic-apps-create-variables-store-values/initialize-variable.png)

5. <span data-ttu-id="827ba-155">Now continue adding the actions you want.</span><span class="sxs-lookup"><span data-stu-id="827ba-155">Now continue adding the actions you want.</span></span> <span data-ttu-id="827ba-156">When you're done, on the designer toolbar, choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="827ba-156">When you're done, on the designer toolbar, choose **Save**.</span></span>

<span data-ttu-id="827ba-157">If you switch from the designer to the code view editor, here is the way the **Initialize variable** action appears inside your logic app definition, which is in JavaScript Object Notation (JSON) format:</span><span class="sxs-lookup"><span data-stu-id="827ba-157">If you switch from the designer to the code view editor, here is the way the **Initialize variable** action appears inside your logic app definition, which is in JavaScript Object Notation (JSON) format:</span></span>

```json
"actions": {
   "Initialize_variable": {
      "type": "InitializeVariable",
      "inputs": {
         "variables": [ {
               "name": "Count",
               "type": "Integer",
               "value": 0
          } ]
      },
      "runAfter": {}
   }
},
```

<span data-ttu-id="827ba-158">Here are examples for some other variable types:</span><span class="sxs-lookup"><span data-stu-id="827ba-158">Here are examples for some other variable types:</span></span>

<span data-ttu-id="827ba-159">*String variable*</span><span class="sxs-lookup"><span data-stu-id="827ba-159">*String variable*</span></span>

```json
"actions": {
   "Initialize_variable": {
      "type": "InitializeVariable",
      "inputs": {
         "variables": [ {
               "name": "myStringVariable",
               "type": "String",
               "value": "lorem ipsum"
          } ]
      },
      "runAfter": {}
   }
},
```

<span data-ttu-id="827ba-160">*Boolean variable*</span><span class="sxs-lookup"><span data-stu-id="827ba-160">*Boolean variable*</span></span>

```json
"actions": {
   "Initialize_variable": {
      "type": "InitializeVariable",
      "inputs": {
         "variables": [ {
               "name": "myBooleanVariable",
               "type": "Boolean",
               "value": false
          } ]
      },
      "runAfter": {}
   }
},
```

<span data-ttu-id="827ba-161">*Array with integers*</span><span class="sxs-lookup"><span data-stu-id="827ba-161">*Array with integers*</span></span>

```json
"actions": {
   "Initialize_variable": {
      "type": "InitializeVariable",
      "inputs": {
         "variables": [ {
               "name": "myArrayVariable",
               "type": "Array",
               "value": [1, 2, 3]
          } ]
      },
      "runAfter": {}
   }
},
```

<span data-ttu-id="827ba-162">*Array with strings*</span><span class="sxs-lookup"><span data-stu-id="827ba-162">*Array with strings*</span></span>

```json
"actions": {
   "Initialize_variable": {
      "type": "InitializeVariable",
      "inputs": {
         "variables": [ {
               "name": "myArrayVariable",
               "type": "Array",
               "value": ["red", "orange", "yellow"]
          } ]
      },
      "runAfter": {}
   }
},
```

<a name="get-value"></a>

## <a name="get-the-variables-value"></a><span data-ttu-id="827ba-163">Get the variable's value</span><span class="sxs-lookup"><span data-stu-id="827ba-163">Get the variable's value</span></span>

<span data-ttu-id="827ba-164">To retrieve or reference a variable's contents, you can also use the [variables() function](../logic-apps/workflow-definition-language-functions-reference.md#variables) in the Logic App Designer and the code view editor.</span><span class="sxs-lookup"><span data-stu-id="827ba-164">To retrieve or reference a variable's contents, you can also use the [variables() function](../logic-apps/workflow-definition-language-functions-reference.md#variables) in the Logic App Designer and the code view editor.</span></span>
<span data-ttu-id="827ba-165">When referencing a variable, use the variable's name as the token, not the action's name, which is the usual way to reference an action's outputs.</span><span class="sxs-lookup"><span data-stu-id="827ba-165">When referencing a variable, use the variable's name as the token, not the action's name, which is the usual way to reference an action's outputs.</span></span> 

<span data-ttu-id="827ba-166">For example, this expression gets the items from the array variable [created previously in this article](#append-value) by using the **variables()** function.</span><span class="sxs-lookup"><span data-stu-id="827ba-166">For example, this expression gets the items from the array variable [created previously in this article](#append-value) by using the **variables()** function.</span></span> <span data-ttu-id="827ba-167">The **string()** function returns the variable's contents in string format: `"1, 2, 3, red"`</span><span class="sxs-lookup"><span data-stu-id="827ba-167">The **string()** function returns the variable's contents in string format: `"1, 2, 3, red"`</span></span>

```json
@{string(variables('myArrayVariable'))}
```

<a name="increment-value"></a>

## <a name="increment-variable"></a><span data-ttu-id="827ba-168">Increment variable</span><span class="sxs-lookup"><span data-stu-id="827ba-168">Increment variable</span></span> 

<span data-ttu-id="827ba-169">To increase or *increment* a variable by a constant value, add the **Variables - Increment variable** action to your logic app.</span><span class="sxs-lookup"><span data-stu-id="827ba-169">To increase or *increment* a variable by a constant value, add the **Variables - Increment variable** action to your logic app.</span></span> <span data-ttu-id="827ba-170">This action works only with integer and float variables.</span><span class="sxs-lookup"><span data-stu-id="827ba-170">This action works only with integer and float variables.</span></span>

1. <span data-ttu-id="827ba-171">In Logic App Designer, under the step where you want to increase an existing variable, choose **New step** > **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="827ba-171">In Logic App Designer, under the step where you want to increase an existing variable, choose **New step** > **Add an action**.</span></span> 

   <span data-ttu-id="827ba-172">For example, this logic app already has a trigger and an action that created a variable.</span><span class="sxs-lookup"><span data-stu-id="827ba-172">For example, this logic app already has a trigger and an action that created a variable.</span></span> <span data-ttu-id="827ba-173">So, add a new action under these steps:</span><span class="sxs-lookup"><span data-stu-id="827ba-173">So, add a new action under these steps:</span></span>

   ![Add action](./media/logic-apps-create-variables-store-values/add-increment-variable-action.png)

   <span data-ttu-id="827ba-175">To add an action between existing steps, move your mouse over the connecting arrow so that the plus sign (+) appears.</span><span class="sxs-lookup"><span data-stu-id="827ba-175">To add an action between existing steps, move your mouse over the connecting arrow so that the plus sign (+) appears.</span></span> <span data-ttu-id="827ba-176">Choose the plus sign, and then choose **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="827ba-176">Choose the plus sign, and then choose **Add an action**.</span></span>

2. <span data-ttu-id="827ba-177">In the search box, enter "increment variable" as your filter.</span><span class="sxs-lookup"><span data-stu-id="827ba-177">In the search box, enter "increment variable" as your filter.</span></span> <span data-ttu-id="827ba-178">In the actions list, select **Variables - Increment variable**.</span><span class="sxs-lookup"><span data-stu-id="827ba-178">In the actions list, select **Variables - Increment variable**.</span></span>

   ![Select "Increment variable" action](./media/logic-apps-create-variables-store-values/select-increment-variable-action.png)

3. <span data-ttu-id="827ba-180">Provide this information for incrementing your variable:</span><span class="sxs-lookup"><span data-stu-id="827ba-180">Provide this information for incrementing your variable:</span></span>

   | <span data-ttu-id="827ba-181">Property</span><span class="sxs-lookup"><span data-stu-id="827ba-181">Property</span></span> | <span data-ttu-id="827ba-182">Required</span><span class="sxs-lookup"><span data-stu-id="827ba-182">Required</span></span> | <span data-ttu-id="827ba-183">Value</span><span class="sxs-lookup"><span data-stu-id="827ba-183">Value</span></span> |  <span data-ttu-id="827ba-184">Description</span><span class="sxs-lookup"><span data-stu-id="827ba-184">Description</span></span> |
   |----------|----------|-------|--------------|
   | <span data-ttu-id="827ba-185">Name</span><span class="sxs-lookup"><span data-stu-id="827ba-185">Name</span></span> | <span data-ttu-id="827ba-186">Yes</span><span class="sxs-lookup"><span data-stu-id="827ba-186">Yes</span></span> | <span data-ttu-id="827ba-187"><*variable-name*></span><span class="sxs-lookup"><span data-stu-id="827ba-187"><*variable-name*></span></span> | <span data-ttu-id="827ba-188">The name for the variable to increment</span><span class="sxs-lookup"><span data-stu-id="827ba-188">The name for the variable to increment</span></span> | 
   | <span data-ttu-id="827ba-189">Value</span><span class="sxs-lookup"><span data-stu-id="827ba-189">Value</span></span> | <span data-ttu-id="827ba-190">No</span><span class="sxs-lookup"><span data-stu-id="827ba-190">No</span></span> | <span data-ttu-id="827ba-191"><*increment-value*></span><span class="sxs-lookup"><span data-stu-id="827ba-191"><*increment-value*></span></span> | <span data-ttu-id="827ba-192">The value used for incrementing the variable.</span><span class="sxs-lookup"><span data-stu-id="827ba-192">The value used for incrementing the variable.</span></span> <span data-ttu-id="827ba-193">The default value is one.</span><span class="sxs-lookup"><span data-stu-id="827ba-193">The default value is one.</span></span> <p><p><span data-ttu-id="827ba-194">**Tip**: Although optional, set this value as a best practice so you always know the specific value for incrementing your variable.</span><span class="sxs-lookup"><span data-stu-id="827ba-194">**Tip**: Although optional, set this value as a best practice so you always know the specific value for incrementing your variable.</span></span> | 
   |||| 

   <span data-ttu-id="827ba-195">For example:</span><span class="sxs-lookup"><span data-stu-id="827ba-195">For example:</span></span> 
   
   ![Increment value example](./media/logic-apps-create-variables-store-values/increment-variable-action-information.png)

4. <span data-ttu-id="827ba-197">When you're done, on the designer toolbar, choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="827ba-197">When you're done, on the designer toolbar, choose **Save**.</span></span> 

<span data-ttu-id="827ba-198">If you switch from the designer to the code view editor, here is the way the **Increment variable** action appears inside your logic app definition, which is in JSON format:</span><span class="sxs-lookup"><span data-stu-id="827ba-198">If you switch from the designer to the code view editor, here is the way the **Increment variable** action appears inside your logic app definition, which is in JSON format:</span></span>

```json
"actions": {
   "Increment_variable": {
      "type": "IncrementVariable",
      "inputs": {
         "name": "Count",
         "value": 1
      },
      "runAfter": {}
   }
},
```

## <a name="example-create-loop-counter"></a><span data-ttu-id="827ba-199">Example: Create loop counter</span><span class="sxs-lookup"><span data-stu-id="827ba-199">Example: Create loop counter</span></span>

<span data-ttu-id="827ba-200">Variables are commonly used for counting the number of times that a loop runs.</span><span class="sxs-lookup"><span data-stu-id="827ba-200">Variables are commonly used for counting the number of times that a loop runs.</span></span> <span data-ttu-id="827ba-201">This example shows how you create and use variables for this task by creating a loop that counts the attachments in an email.</span><span class="sxs-lookup"><span data-stu-id="827ba-201">This example shows how you create and use variables for this task by creating a loop that counts the attachments in an email.</span></span>

1. <span data-ttu-id="827ba-202">In the Azure portal, create a blank logic app.</span><span class="sxs-lookup"><span data-stu-id="827ba-202">In the Azure portal, create a blank logic app.</span></span> <span data-ttu-id="827ba-203">Add a trigger that checks for new email and any attachments.</span><span class="sxs-lookup"><span data-stu-id="827ba-203">Add a trigger that checks for new email and any attachments.</span></span> 

   <span data-ttu-id="827ba-204">This example uses the Office 365 Outlook trigger for **When a new email arrives**.</span><span class="sxs-lookup"><span data-stu-id="827ba-204">This example uses the Office 365 Outlook trigger for **When a new email arrives**.</span></span> 
   <span data-ttu-id="827ba-205">You can set up this trigger to fire only when the email has attachments.</span><span class="sxs-lookup"><span data-stu-id="827ba-205">You can set up this trigger to fire only when the email has attachments.</span></span>
   <span data-ttu-id="827ba-206">However, you can use any connector that checks for new emails with attachments, such as the Outlook.com connector.</span><span class="sxs-lookup"><span data-stu-id="827ba-206">However, you can use any connector that checks for new emails with attachments, such as the Outlook.com connector.</span></span>

2. <span data-ttu-id="827ba-207">In the trigger, choose **Show advanced options**.</span><span class="sxs-lookup"><span data-stu-id="827ba-207">In the trigger, choose **Show advanced options**.</span></span> <span data-ttu-id="827ba-208">To have the trigger check for attachments and pass those attachments into your logic app's workflow, select **Yes** for these properties:</span><span class="sxs-lookup"><span data-stu-id="827ba-208">To have the trigger check for attachments and pass those attachments into your logic app's workflow, select **Yes** for these properties:</span></span>
   
   * <span data-ttu-id="827ba-209">**Has Attachment**</span><span class="sxs-lookup"><span data-stu-id="827ba-209">**Has Attachment**</span></span> 
   * <span data-ttu-id="827ba-210">**Include Attachments**</span><span class="sxs-lookup"><span data-stu-id="827ba-210">**Include Attachments**</span></span> 

   ![Check for and include attachments](./media/logic-apps-create-variables-store-values/check-include-attachments.png)

3. <span data-ttu-id="827ba-212">Add the [**Initialize variable** action](#create-variable).</span><span class="sxs-lookup"><span data-stu-id="827ba-212">Add the [**Initialize variable** action](#create-variable).</span></span> <span data-ttu-id="827ba-213">Create an integer variable named **Count** with a zero start value.</span><span class="sxs-lookup"><span data-stu-id="827ba-213">Create an integer variable named **Count** with a zero start value.</span></span>

   ![Add action for "Initialize variable"](./media/logic-apps-create-variables-store-values/initialize-variable.png)

4. <span data-ttu-id="827ba-215">To cycle through each attachment, add a *for each* loop by choosing **New step** > **More** > **Add a for each**.</span><span class="sxs-lookup"><span data-stu-id="827ba-215">To cycle through each attachment, add a *for each* loop by choosing **New step** > **More** > **Add a for each**.</span></span>

   ![Add a "for each" loop](./media/logic-apps-create-variables-store-values/add-loop.png)

5. <span data-ttu-id="827ba-217">In the loop, click inside the **Select an output from previous steps** box.</span><span class="sxs-lookup"><span data-stu-id="827ba-217">In the loop, click inside the **Select an output from previous steps** box.</span></span> <span data-ttu-id="827ba-218">When the dynamic content list appears, select **Attachments**.</span><span class="sxs-lookup"><span data-stu-id="827ba-218">When the dynamic content list appears, select **Attachments**.</span></span> 

   ![Select "Attachments"](./media/logic-apps-create-variables-store-values/select-attachments.png)

   <span data-ttu-id="827ba-220">The **Attachments** field passes an array that has the email attachments from the trigger's output into your loop.</span><span class="sxs-lookup"><span data-stu-id="827ba-220">The **Attachments** field passes an array that has the email attachments from the trigger's output into your loop.</span></span>

6. <span data-ttu-id="827ba-221">In the "for each" loop, select **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="827ba-221">In the "for each" loop, select **Add an action**.</span></span> 

   ![Select "Add an action"](./media/logic-apps-create-variables-store-values/add-action-2.png)

7. <span data-ttu-id="827ba-223">In the search box, enter "increment variable" as your filter.</span><span class="sxs-lookup"><span data-stu-id="827ba-223">In the search box, enter "increment variable" as your filter.</span></span> <span data-ttu-id="827ba-224">From the actions list, select **Variables - Increment variable**.</span><span class="sxs-lookup"><span data-stu-id="827ba-224">From the actions list, select **Variables - Increment variable**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="827ba-225">Make sure the **Increment variable** action appears inside the loop.</span><span class="sxs-lookup"><span data-stu-id="827ba-225">Make sure the **Increment variable** action appears inside the loop.</span></span> <span data-ttu-id="827ba-226">If the action appears outside the loop, drag the action into the loop.</span><span class="sxs-lookup"><span data-stu-id="827ba-226">If the action appears outside the loop, drag the action into the loop.</span></span>

8. <span data-ttu-id="827ba-227">In the **Increment variable** action, from the **Name** list, select the **Count** variable.</span><span class="sxs-lookup"><span data-stu-id="827ba-227">In the **Increment variable** action, from the **Name** list, select the **Count** variable.</span></span> 

   ![Select "Count" variable](./media/logic-apps-create-variables-store-values/add-increment-variable-example.png)

9. <span data-ttu-id="827ba-229">Under the loop, add any action that sends you the number of attachments.</span><span class="sxs-lookup"><span data-stu-id="827ba-229">Under the loop, add any action that sends you the number of attachments.</span></span> <span data-ttu-id="827ba-230">In your action, include the value from the **Count** variable, for example:</span><span class="sxs-lookup"><span data-stu-id="827ba-230">In your action, include the value from the **Count** variable, for example:</span></span> 

   ![Add an action that sends results](./media/logic-apps-create-variables-store-values/send-email-results.png)

10. <span data-ttu-id="827ba-232">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="827ba-232">Save your logic app.</span></span> <span data-ttu-id="827ba-233">On the designer toolbar, choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="827ba-233">On the designer toolbar, choose **Save**.</span></span> 

### <a name="test-your-logic-app"></a><span data-ttu-id="827ba-234">Test your logic app</span><span class="sxs-lookup"><span data-stu-id="827ba-234">Test your logic app</span></span>

1. <span data-ttu-id="827ba-235">If your logic app isn't enabled, on your logic app menu, choose **Overview**.</span><span class="sxs-lookup"><span data-stu-id="827ba-235">If your logic app isn't enabled, on your logic app menu, choose **Overview**.</span></span> <span data-ttu-id="827ba-236">On the toolbar, choose **Enable**.</span><span class="sxs-lookup"><span data-stu-id="827ba-236">On the toolbar, choose **Enable**.</span></span> 

2. <span data-ttu-id="827ba-237">On the Logic App Designer toolbar, choose **Run**.</span><span class="sxs-lookup"><span data-stu-id="827ba-237">On the Logic App Designer toolbar, choose **Run**.</span></span> <span data-ttu-id="827ba-238">This step manually starts your logic app.</span><span class="sxs-lookup"><span data-stu-id="827ba-238">This step manually starts your logic app.</span></span>

3. <span data-ttu-id="827ba-239">Send an email with one or more attachments to the email account you used in this example.</span><span class="sxs-lookup"><span data-stu-id="827ba-239">Send an email with one or more attachments to the email account you used in this example.</span></span>

   <span data-ttu-id="827ba-240">This step fires the logic app's trigger, which creates and runs an instance for your logic app's workflow.</span><span class="sxs-lookup"><span data-stu-id="827ba-240">This step fires the logic app's trigger, which creates and runs an instance for your logic app's workflow.</span></span>
   <span data-ttu-id="827ba-241">As a result, the logic app sends you a message or email that shows the number of attachments in the email you sent.</span><span class="sxs-lookup"><span data-stu-id="827ba-241">As a result, the logic app sends you a message or email that shows the number of attachments in the email you sent.</span></span>

<span data-ttu-id="827ba-242">If you switch from the designer to the code view editor, here is the way the "for each" loop appears with the **Increment variable** action inside your logic app definition, which is in JSON format.</span><span class="sxs-lookup"><span data-stu-id="827ba-242">If you switch from the designer to the code view editor, here is the way the "for each" loop appears with the **Increment variable** action inside your logic app definition, which is in JSON format.</span></span>

```json
"actions": {
   "For_each": {
      "type": "Foreach",
      "actions": {
         "Increment_variable": {
           "type": "IncrementVariable",
            "inputs": {
               "name": "Count",
               "value": 1
            },
            "runAfter": {}
         }
      },
      "foreach": "@triggerBody()?['Attachments']",
      "runAfter": {
         "Initialize_variable": [ "Succeeded" ]
      }
   }
},
```

<a name="decrement-value"></a>

## <a name="decrement-variable"></a><span data-ttu-id="827ba-243">Decrement variable</span><span class="sxs-lookup"><span data-stu-id="827ba-243">Decrement variable</span></span>

<span data-ttu-id="827ba-244">To decrease or *decrement* a variable by a constant value, follow the steps for [increasing a variable](#increment-value) except that you find and select the **Variables - Decrement variable** action instead.</span><span class="sxs-lookup"><span data-stu-id="827ba-244">To decrease or *decrement* a variable by a constant value, follow the steps for [increasing a variable](#increment-value) except that you find and select the **Variables - Decrement variable** action instead.</span></span> <span data-ttu-id="827ba-245">This action works only with integer and float variables.</span><span class="sxs-lookup"><span data-stu-id="827ba-245">This action works only with integer and float variables.</span></span>

<span data-ttu-id="827ba-246">Here are the properties for the **Decrement variable** action:</span><span class="sxs-lookup"><span data-stu-id="827ba-246">Here are the properties for the **Decrement variable** action:</span></span>

| <span data-ttu-id="827ba-247">Property</span><span class="sxs-lookup"><span data-stu-id="827ba-247">Property</span></span> | <span data-ttu-id="827ba-248">Required</span><span class="sxs-lookup"><span data-stu-id="827ba-248">Required</span></span> | <span data-ttu-id="827ba-249">Value</span><span class="sxs-lookup"><span data-stu-id="827ba-249">Value</span></span> |  <span data-ttu-id="827ba-250">Description</span><span class="sxs-lookup"><span data-stu-id="827ba-250">Description</span></span> |
|----------|----------|-------|--------------|
| <span data-ttu-id="827ba-251">Name</span><span class="sxs-lookup"><span data-stu-id="827ba-251">Name</span></span> | <span data-ttu-id="827ba-252">Yes</span><span class="sxs-lookup"><span data-stu-id="827ba-252">Yes</span></span> | <span data-ttu-id="827ba-253"><*variable-name*></span><span class="sxs-lookup"><span data-stu-id="827ba-253"><*variable-name*></span></span> | <span data-ttu-id="827ba-254">The name for the variable to decrement</span><span class="sxs-lookup"><span data-stu-id="827ba-254">The name for the variable to decrement</span></span> | 
| <span data-ttu-id="827ba-255">Value</span><span class="sxs-lookup"><span data-stu-id="827ba-255">Value</span></span> | <span data-ttu-id="827ba-256">No</span><span class="sxs-lookup"><span data-stu-id="827ba-256">No</span></span> | <span data-ttu-id="827ba-257"><*increment-value*></span><span class="sxs-lookup"><span data-stu-id="827ba-257"><*increment-value*></span></span> | <span data-ttu-id="827ba-258">The value for decrementing the variable.</span><span class="sxs-lookup"><span data-stu-id="827ba-258">The value for decrementing the variable.</span></span> <span data-ttu-id="827ba-259">The default value is one.</span><span class="sxs-lookup"><span data-stu-id="827ba-259">The default value is one.</span></span> <p><p><span data-ttu-id="827ba-260">**Tip**: Although optional, set this value as a best practice so you always know the specific value for decrementing your variable.</span><span class="sxs-lookup"><span data-stu-id="827ba-260">**Tip**: Although optional, set this value as a best practice so you always know the specific value for decrementing your variable.</span></span> | 
||||| 

<span data-ttu-id="827ba-261">If you switch from the designer to the code view editor, here is the way the **Decrement variable** action appears inside your logic app definition, which is in JSON format.</span><span class="sxs-lookup"><span data-stu-id="827ba-261">If you switch from the designer to the code view editor, here is the way the **Decrement variable** action appears inside your logic app definition, which is in JSON format.</span></span>

```json
"actions": {
   "Decrement_variable": {
      "type": "DecrementVariable",
      "inputs": {
         "name": "Count",
         "value": 1
      },
      "runAfter": {}
   }
},
```


<a name="assign-value"></a>

## <a name="set-variable"></a><span data-ttu-id="827ba-262">Set variable</span><span class="sxs-lookup"><span data-stu-id="827ba-262">Set variable</span></span>

<span data-ttu-id="827ba-263">To assign a different value to an existing variable, follow the steps for [increasing a variable](#increment-value) except that you:</span><span class="sxs-lookup"><span data-stu-id="827ba-263">To assign a different value to an existing variable, follow the steps for [increasing a variable](#increment-value) except that you:</span></span> 

1. <span data-ttu-id="827ba-264">Find and select the **Variables - Set variable** action instead.</span><span class="sxs-lookup"><span data-stu-id="827ba-264">Find and select the **Variables - Set variable** action instead.</span></span> 

2. <span data-ttu-id="827ba-265">Provide the variable name and value you want to assign.</span><span class="sxs-lookup"><span data-stu-id="827ba-265">Provide the variable name and value you want to assign.</span></span> <span data-ttu-id="827ba-266">Both the new value and the variable must have the same data type.</span><span class="sxs-lookup"><span data-stu-id="827ba-266">Both the new value and the variable must have the same data type.</span></span>
<span data-ttu-id="827ba-267">The value is required because this action doesn't have a default value.</span><span class="sxs-lookup"><span data-stu-id="827ba-267">The value is required because this action doesn't have a default value.</span></span> 

<span data-ttu-id="827ba-268">Here are the properties for the **Set variable** action:</span><span class="sxs-lookup"><span data-stu-id="827ba-268">Here are the properties for the **Set variable** action:</span></span>

| <span data-ttu-id="827ba-269">Property</span><span class="sxs-lookup"><span data-stu-id="827ba-269">Property</span></span> | <span data-ttu-id="827ba-270">Required</span><span class="sxs-lookup"><span data-stu-id="827ba-270">Required</span></span> | <span data-ttu-id="827ba-271">Value</span><span class="sxs-lookup"><span data-stu-id="827ba-271">Value</span></span> |  <span data-ttu-id="827ba-272">Description</span><span class="sxs-lookup"><span data-stu-id="827ba-272">Description</span></span> | 
|----------|----------|-------|--------------| 
| <span data-ttu-id="827ba-273">Name</span><span class="sxs-lookup"><span data-stu-id="827ba-273">Name</span></span> | <span data-ttu-id="827ba-274">Yes</span><span class="sxs-lookup"><span data-stu-id="827ba-274">Yes</span></span> | <span data-ttu-id="827ba-275"><*variable-name*></span><span class="sxs-lookup"><span data-stu-id="827ba-275"><*variable-name*></span></span> | <span data-ttu-id="827ba-276">The name for the variable to change</span><span class="sxs-lookup"><span data-stu-id="827ba-276">The name for the variable to change</span></span> | 
| <span data-ttu-id="827ba-277">Value</span><span class="sxs-lookup"><span data-stu-id="827ba-277">Value</span></span> | <span data-ttu-id="827ba-278">Yes</span><span class="sxs-lookup"><span data-stu-id="827ba-278">Yes</span></span> | <span data-ttu-id="827ba-279"><*new-value*></span><span class="sxs-lookup"><span data-stu-id="827ba-279"><*new-value*></span></span> | <span data-ttu-id="827ba-280">The value you want to assign the variable.</span><span class="sxs-lookup"><span data-stu-id="827ba-280">The value you want to assign the variable.</span></span> <span data-ttu-id="827ba-281">Both must have the same data type.</span><span class="sxs-lookup"><span data-stu-id="827ba-281">Both must have the same data type.</span></span> | 
||||| 

> [!NOTE]
> <span data-ttu-id="827ba-282">Unless you're incrementing or decrementing variables, changing variables inside loops *might* create unexpected results because loops run in parallel, or concurrently, by default.</span><span class="sxs-lookup"><span data-stu-id="827ba-282">Unless you're incrementing or decrementing variables, changing variables inside loops *might* create unexpected results because loops run in parallel, or concurrently, by default.</span></span> <span data-ttu-id="827ba-283">For these cases, try setting your loop to run sequentially.</span><span class="sxs-lookup"><span data-stu-id="827ba-283">For these cases, try setting your loop to run sequentially.</span></span> <span data-ttu-id="827ba-284">For example, when you want to reference the variable value inside the loop and expect same value at the start and end of that loop instance, follow these steps to change how the loop runs:</span><span class="sxs-lookup"><span data-stu-id="827ba-284">For example, when you want to reference the variable value inside the loop and expect same value at the start and end of that loop instance, follow these steps to change how the loop runs:</span></span> 
>
> 1. <span data-ttu-id="827ba-285">In your loop's upper-right corner, choose the ellipsis (...) button, and then choose **Settings**.</span><span class="sxs-lookup"><span data-stu-id="827ba-285">In your loop's upper-right corner, choose the ellipsis (...) button, and then choose **Settings**.</span></span>
> 
> 2. <span data-ttu-id="827ba-286">Under **Concurrency Control**, change the **Override Default** setting to **On**.</span><span class="sxs-lookup"><span data-stu-id="827ba-286">Under **Concurrency Control**, change the **Override Default** setting to **On**.</span></span>
>
> 3. <span data-ttu-id="827ba-287">Drag the **Degree of Parallelism** slider to **1**.</span><span class="sxs-lookup"><span data-stu-id="827ba-287">Drag the **Degree of Parallelism** slider to **1**.</span></span>

<span data-ttu-id="827ba-288">If you switch from the designer to the code view editor, here is the way the **Set variable** action appears inside your logic app definition, which is in JSON format.</span><span class="sxs-lookup"><span data-stu-id="827ba-288">If you switch from the designer to the code view editor, here is the way the **Set variable** action appears inside your logic app definition, which is in JSON format.</span></span> <span data-ttu-id="827ba-289">This example changes the "Count" variable's current value to another value.</span><span class="sxs-lookup"><span data-stu-id="827ba-289">This example changes the "Count" variable's current value to another value.</span></span> 

```json
"actions": {
   "Initialize_variable": {
      "type": "InitializeVariable",
      "inputs": {
         "variables": [ {
               "name": "Count",
               "type": "Integer",
               "value": 0
          } ]
      },
      "runAfter": {}
   },
   "Set_variable": {
      "type": "SetVariable",
      "inputs": {
         "name": "Count",
         "value": 100
      },
      "runAfter": {
         "Initialize_variable": [ "Succeeded" ]
      }
   }
},
```

<a name="append-value"></a>

## <a name="append-to-variable"></a><span data-ttu-id="827ba-290">Append to variable</span><span class="sxs-lookup"><span data-stu-id="827ba-290">Append to variable</span></span>

<span data-ttu-id="827ba-291">For variables that store strings or arrays, you can insert or *append* a variable's value as the last item in those strings or arrays.</span><span class="sxs-lookup"><span data-stu-id="827ba-291">For variables that store strings or arrays, you can insert or *append* a variable's value as the last item in those strings or arrays.</span></span> <span data-ttu-id="827ba-292">You can follow the steps for [increasing a variable](#increment-value) except that you follow these steps instead:</span><span class="sxs-lookup"><span data-stu-id="827ba-292">You can follow the steps for [increasing a variable](#increment-value) except that you follow these steps instead:</span></span> 

1. <span data-ttu-id="827ba-293">Find and select one of these actions based on whether your variable is a string or an array:</span><span class="sxs-lookup"><span data-stu-id="827ba-293">Find and select one of these actions based on whether your variable is a string or an array:</span></span> 

  * <span data-ttu-id="827ba-294">**Variables - Append to string variable**</span><span class="sxs-lookup"><span data-stu-id="827ba-294">**Variables - Append to string variable**</span></span>
  * <span data-ttu-id="827ba-295">**Variables - Append to array variable**</span><span class="sxs-lookup"><span data-stu-id="827ba-295">**Variables - Append to array variable**</span></span> 

2. <span data-ttu-id="827ba-296">Provide the value to append as the last item in the string or array.</span><span class="sxs-lookup"><span data-stu-id="827ba-296">Provide the value to append as the last item in the string or array.</span></span> <span data-ttu-id="827ba-297">This value is required.</span><span class="sxs-lookup"><span data-stu-id="827ba-297">This value is required.</span></span> 

<span data-ttu-id="827ba-298">Here are the properties for the **Append to...** actions:</span><span class="sxs-lookup"><span data-stu-id="827ba-298">Here are the properties for the **Append to...** actions:</span></span>

| <span data-ttu-id="827ba-299">Property</span><span class="sxs-lookup"><span data-stu-id="827ba-299">Property</span></span> | <span data-ttu-id="827ba-300">Required</span><span class="sxs-lookup"><span data-stu-id="827ba-300">Required</span></span> | <span data-ttu-id="827ba-301">Value</span><span class="sxs-lookup"><span data-stu-id="827ba-301">Value</span></span> |  <span data-ttu-id="827ba-302">Description</span><span class="sxs-lookup"><span data-stu-id="827ba-302">Description</span></span> | 
|----------|----------|-------|--------------| 
| <span data-ttu-id="827ba-303">Name</span><span class="sxs-lookup"><span data-stu-id="827ba-303">Name</span></span> | <span data-ttu-id="827ba-304">Yes</span><span class="sxs-lookup"><span data-stu-id="827ba-304">Yes</span></span> | <span data-ttu-id="827ba-305"><*variable-name*></span><span class="sxs-lookup"><span data-stu-id="827ba-305"><*variable-name*></span></span> | <span data-ttu-id="827ba-306">The name for the variable to change</span><span class="sxs-lookup"><span data-stu-id="827ba-306">The name for the variable to change</span></span> | 
| <span data-ttu-id="827ba-307">Value</span><span class="sxs-lookup"><span data-stu-id="827ba-307">Value</span></span> | <span data-ttu-id="827ba-308">Yes</span><span class="sxs-lookup"><span data-stu-id="827ba-308">Yes</span></span> | <span data-ttu-id="827ba-309"><*append-value*></span><span class="sxs-lookup"><span data-stu-id="827ba-309"><*append-value*></span></span> | <span data-ttu-id="827ba-310">The value you want to append, which can have any type</span><span class="sxs-lookup"><span data-stu-id="827ba-310">The value you want to append, which can have any type</span></span> | 
|||||  

<span data-ttu-id="827ba-311">If you switch from the designer to the code view editor, here is the way the **Append to array variable** action appears inside your logic app definition, which is in JSON format.</span><span class="sxs-lookup"><span data-stu-id="827ba-311">If you switch from the designer to the code view editor, here is the way the **Append to array variable** action appears inside your logic app definition, which is in JSON format.</span></span>
<span data-ttu-id="827ba-312">This example creates an array variable, and adds another value as the last item in the array.</span><span class="sxs-lookup"><span data-stu-id="827ba-312">This example creates an array variable, and adds another value as the last item in the array.</span></span> <span data-ttu-id="827ba-313">Your result is an updated variable that contains this array: `[1,2,3,"red"]`</span><span class="sxs-lookup"><span data-stu-id="827ba-313">Your result is an updated variable that contains this array: `[1,2,3,"red"]`</span></span> 

```json
"actions": {
   "Initialize_variable": {
      "type": "InitializeVariable",
      "inputs": {
         "variables": [ {
            "name": "myArrayVariable",
            "type": "Array",
            "value": [1, 2, 3]
         } ]
      },
      "runAfter": {}
   },
   "Append_to_array_variable": {
      "type": "AppendToArrayVariable",
      "inputs": {
         "name": "myArrayVariable",
         "value": "red"
      },
      "runAfter": {
        "Initialize_variable": [ "Succeeded" ]
      }
   }
},
```

## <a name="get-support"></a><span data-ttu-id="827ba-314">Get support</span><span class="sxs-lookup"><span data-stu-id="827ba-314">Get support</span></span>

* <span data-ttu-id="827ba-315">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="827ba-315">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>
* <span data-ttu-id="827ba-316">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="827ba-316">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="827ba-317">Next steps</span><span class="sxs-lookup"><span data-stu-id="827ba-317">Next steps</span></span>

* <span data-ttu-id="827ba-318">Learn about [Logic Apps connectors](../connectors/apis-list.md)</span><span class="sxs-lookup"><span data-stu-id="827ba-318">Learn about [Logic Apps connectors](../connectors/apis-list.md)</span></span>
