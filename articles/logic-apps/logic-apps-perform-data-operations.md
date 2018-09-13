---
title: Perform operations on data - Azure Logic Apps | Microsoft Docs
description: Convert, manage, and manipulate data outputs and formats in Azure Logic Apps
services: logic-apps
ms.service: logic-apps
author: ecfan
ms.author: estfan
manager: jeconnoc
ms.topic: article
ms.date: 07/30/2018
ms.reviewer: klam, LADocs
ms.suite: integration
ms.openlocfilehash: 7e62986569888ebbcd9f17b4eb4cfb2c70411d4a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867374"
---
# <a name="perform-data-operations-in-azure-logic-apps"></a><span data-ttu-id="1d15a-103">Perform data operations in Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="1d15a-103">Perform data operations in Azure Logic Apps</span></span>

<span data-ttu-id="1d15a-104">This article shows how you can work with data in your logic apps by adding actions for these tasks and more:</span><span class="sxs-lookup"><span data-stu-id="1d15a-104">This article shows how you can work with data in your logic apps by adding actions for these tasks and more:</span></span>

* <span data-ttu-id="1d15a-105">Create tables from arrays.</span><span class="sxs-lookup"><span data-stu-id="1d15a-105">Create tables from arrays.</span></span>
* <span data-ttu-id="1d15a-106">Create arrays from other arrays based on a condition.</span><span class="sxs-lookup"><span data-stu-id="1d15a-106">Create arrays from other arrays based on a condition.</span></span>
* <span data-ttu-id="1d15a-107">Create user-friendly tokens from JavaScript Object Notation (JSON) object properties so you can easily use those properties in your workflow.</span><span class="sxs-lookup"><span data-stu-id="1d15a-107">Create user-friendly tokens from JavaScript Object Notation (JSON) object properties so you can easily use those properties in your workflow.</span></span>

<span data-ttu-id="1d15a-108">If you don't find the action you want here, try browsing the many various [data manipulation functions](../logic-apps/workflow-definition-language-functions-reference.md) that Logic Apps provides.</span><span class="sxs-lookup"><span data-stu-id="1d15a-108">If you don't find the action you want here, try browsing the many various [data manipulation functions](../logic-apps/workflow-definition-language-functions-reference.md) that Logic Apps provides.</span></span> 

<span data-ttu-id="1d15a-109">These tables summarize the data operations you can use and are organized based on the source data types that the operations work on, but each description appears alphabetically.</span><span class="sxs-lookup"><span data-stu-id="1d15a-109">These tables summarize the data operations you can use and are organized based on the source data types that the operations work on, but each description appears alphabetically.</span></span>

<span data-ttu-id="1d15a-110">**Array actions**</span><span class="sxs-lookup"><span data-stu-id="1d15a-110">**Array actions**</span></span> 

<span data-ttu-id="1d15a-111">These actions help you work with data in arrays.</span><span class="sxs-lookup"><span data-stu-id="1d15a-111">These actions help you work with data in arrays.</span></span>

| <span data-ttu-id="1d15a-112">Action</span><span class="sxs-lookup"><span data-stu-id="1d15a-112">Action</span></span> | <span data-ttu-id="1d15a-113">Description</span><span class="sxs-lookup"><span data-stu-id="1d15a-113">Description</span></span> | 
|--------|-------------| 
| [<span data-ttu-id="1d15a-114">**Create CSV table**</span><span class="sxs-lookup"><span data-stu-id="1d15a-114">**Create CSV table**</span></span>](#create-csv-table-action) | <span data-ttu-id="1d15a-115">Create a comma-separated value (CSV) table from an array.</span><span class="sxs-lookup"><span data-stu-id="1d15a-115">Create a comma-separated value (CSV) table from an array.</span></span> | 
| [<span data-ttu-id="1d15a-116">**Create HTML table**</span><span class="sxs-lookup"><span data-stu-id="1d15a-116">**Create HTML table**</span></span>](#create-html-table-action) | <span data-ttu-id="1d15a-117">Create an HTML table from an array.</span><span class="sxs-lookup"><span data-stu-id="1d15a-117">Create an HTML table from an array.</span></span> | 
| [<span data-ttu-id="1d15a-118">**Filter array**</span><span class="sxs-lookup"><span data-stu-id="1d15a-118">**Filter array**</span></span>](#filter-array-action) | <span data-ttu-id="1d15a-119">Create an array subset from an array based on the specified filter or condition.</span><span class="sxs-lookup"><span data-stu-id="1d15a-119">Create an array subset from an array based on the specified filter or condition.</span></span> | 
| [<span data-ttu-id="1d15a-120">**Join**</span><span class="sxs-lookup"><span data-stu-id="1d15a-120">**Join**</span></span>](#join-action) | <span data-ttu-id="1d15a-121">Create a string from all the items in an array and separate each item with the specified character.</span><span class="sxs-lookup"><span data-stu-id="1d15a-121">Create a string from all the items in an array and separate each item with the specified character.</span></span> | 
| [<span data-ttu-id="1d15a-122">**Select**</span><span class="sxs-lookup"><span data-stu-id="1d15a-122">**Select**</span></span>](#select-action) | <span data-ttu-id="1d15a-123">Create an array from the specified properties for all the items in a different array.</span><span class="sxs-lookup"><span data-stu-id="1d15a-123">Create an array from the specified properties for all the items in a different array.</span></span> | 
||| 

<span data-ttu-id="1d15a-124">**JSON actions**</span><span class="sxs-lookup"><span data-stu-id="1d15a-124">**JSON actions**</span></span>

<span data-ttu-id="1d15a-125">These actions help you work with data in JavaScript Object Notation (JSON) format.</span><span class="sxs-lookup"><span data-stu-id="1d15a-125">These actions help you work with data in JavaScript Object Notation (JSON) format.</span></span>

| <span data-ttu-id="1d15a-126">Action</span><span class="sxs-lookup"><span data-stu-id="1d15a-126">Action</span></span> | <span data-ttu-id="1d15a-127">Description</span><span class="sxs-lookup"><span data-stu-id="1d15a-127">Description</span></span> | 
|--------|-------------| 
| [<span data-ttu-id="1d15a-128">**Compose**</span><span class="sxs-lookup"><span data-stu-id="1d15a-128">**Compose**</span></span>](#compose-action) | <span data-ttu-id="1d15a-129">Create a message, or string, from multiple inputs that can have various data types.</span><span class="sxs-lookup"><span data-stu-id="1d15a-129">Create a message, or string, from multiple inputs that can have various data types.</span></span> <span data-ttu-id="1d15a-130">You can then use this string as a single input, rather than repeatedly entering the same inputs.</span><span class="sxs-lookup"><span data-stu-id="1d15a-130">You can then use this string as a single input, rather than repeatedly entering the same inputs.</span></span> <span data-ttu-id="1d15a-131">For example, you can create a single JSON message from various inputs.</span><span class="sxs-lookup"><span data-stu-id="1d15a-131">For example, you can create a single JSON message from various inputs.</span></span> | 
| [<span data-ttu-id="1d15a-132">**Parse JSON**</span><span class="sxs-lookup"><span data-stu-id="1d15a-132">**Parse JSON**</span></span>](#parse-json-action) | <span data-ttu-id="1d15a-133">Create user-friendly data tokens for properties in JSON content so you can more easily use the properties in your logic apps.</span><span class="sxs-lookup"><span data-stu-id="1d15a-133">Create user-friendly data tokens for properties in JSON content so you can more easily use the properties in your logic apps.</span></span> | 
||| 

<span data-ttu-id="1d15a-134">To create more complex JSON transformations, see [Perform advanced JSON transformations with Liquid templates](../logic-apps/logic-apps-enterprise-integration-liquid-transform.md).</span><span class="sxs-lookup"><span data-stu-id="1d15a-134">To create more complex JSON transformations, see [Perform advanced JSON transformations with Liquid templates](../logic-apps/logic-apps-enterprise-integration-liquid-transform.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d15a-135">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1d15a-135">Prerequisites</span></span>

<span data-ttu-id="1d15a-136">To follow the examples in this article, you need these items:</span><span class="sxs-lookup"><span data-stu-id="1d15a-136">To follow the examples in this article, you need these items:</span></span>

* <span data-ttu-id="1d15a-137">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="1d15a-137">An Azure subscription.</span></span> <span data-ttu-id="1d15a-138">If you don't have an Azure subscription yet, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span><span class="sxs-lookup"><span data-stu-id="1d15a-138">If you don't have an Azure subscription yet, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span></span>

* <span data-ttu-id="1d15a-139">The logic app where you need the operation for working with data</span><span class="sxs-lookup"><span data-stu-id="1d15a-139">The logic app where you need the operation for working with data</span></span> 

  <span data-ttu-id="1d15a-140">If you're new to logic apps, review [What is Azure Logic Apps](../logic-apps/logic-apps-overview.md) and [Quickstart: Create your first logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="1d15a-140">If you're new to logic apps, review [What is Azure Logic Apps](../logic-apps/logic-apps-overview.md) and [Quickstart: Create your first logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span></span>

* <span data-ttu-id="1d15a-141">A [trigger](../logic-apps/logic-apps-overview.md#logic-app-concepts) as the first step in your logic app</span><span class="sxs-lookup"><span data-stu-id="1d15a-141">A [trigger](../logic-apps/logic-apps-overview.md#logic-app-concepts) as the first step in your logic app</span></span> 

  <span data-ttu-id="1d15a-142">Data operations are available only as actions, so before you can use these actions, start your logic app with a trigger and include any other actions required for creating the outputs you want.</span><span class="sxs-lookup"><span data-stu-id="1d15a-142">Data operations are available only as actions, so before you can use these actions, start your logic app with a trigger and include any other actions required for creating the outputs you want.</span></span>

<a name="compose-action"></a>

## <a name="compose-action"></a><span data-ttu-id="1d15a-143">Compose action</span><span class="sxs-lookup"><span data-stu-id="1d15a-143">Compose action</span></span>

<span data-ttu-id="1d15a-144">To construct a single output such as a JSON object from multiple inputs, you can use the **Data Operations - Compose** action.</span><span class="sxs-lookup"><span data-stu-id="1d15a-144">To construct a single output such as a JSON object from multiple inputs, you can use the **Data Operations - Compose** action.</span></span> <span data-ttu-id="1d15a-145">Your inputs can have various types such as integers, Booleans, arrays, JSON objects, and any other native type that Azure Logic Apps supports, for example, binary and XML.</span><span class="sxs-lookup"><span data-stu-id="1d15a-145">Your inputs can have various types such as integers, Booleans, arrays, JSON objects, and any other native type that Azure Logic Apps supports, for example, binary and XML.</span></span> <span data-ttu-id="1d15a-146">You can then use the output in actions that follow after the **Compose** action.</span><span class="sxs-lookup"><span data-stu-id="1d15a-146">You can then use the output in actions that follow after the **Compose** action.</span></span> <span data-ttu-id="1d15a-147">The **Compose** action can also save you from repeatedly entering the same inputs while you build your logic app's workflow.</span><span class="sxs-lookup"><span data-stu-id="1d15a-147">The **Compose** action can also save you from repeatedly entering the same inputs while you build your logic app's workflow.</span></span> 

<span data-ttu-id="1d15a-148">For example, you can construct a JSON message from multiple variables, such as string variables that store people's first names and last names, and an integer variable that stores people's ages.</span><span class="sxs-lookup"><span data-stu-id="1d15a-148">For example, you can construct a JSON message from multiple variables, such as string variables that store people's first names and last names, and an integer variable that stores people's ages.</span></span> <span data-ttu-id="1d15a-149">Here, the **Compose** action accepts these inputs:</span><span class="sxs-lookup"><span data-stu-id="1d15a-149">Here, the **Compose** action accepts these inputs:</span></span>

`{ "age": <ageVar>, "fullName": "<lastNameVar>, <firstNameVar>" }`

<span data-ttu-id="1d15a-150">and creates this output:</span><span class="sxs-lookup"><span data-stu-id="1d15a-150">and creates this output:</span></span>

`{"age":35,"fullName":"Owens,Sophie"}`

<span data-ttu-id="1d15a-151">To try an example, follow these steps by using the Logic App Designer.</span><span class="sxs-lookup"><span data-stu-id="1d15a-151">To try an example, follow these steps by using the Logic App Designer.</span></span> <span data-ttu-id="1d15a-152">Or, if you prefer working in the code view editor, you can copy the example **Compose** and **Initialize variable** action definitions from this article into your own logic app's underlying workflow definition: [Data operation code examples - Compose](../logic-apps/logic-apps-data-operations-code-samples.md#compose-action-example)</span><span class="sxs-lookup"><span data-stu-id="1d15a-152">Or, if you prefer working in the code view editor, you can copy the example **Compose** and **Initialize variable** action definitions from this article into your own logic app's underlying workflow definition: [Data operation code examples - Compose](../logic-apps/logic-apps-data-operations-code-samples.md#compose-action-example)</span></span> 

1. <span data-ttu-id="1d15a-153">In the <a href="https://portal.azure.com" target="_blank">Azure portal</a> or Visual Studio, open your logic app in Logic App Designer.</span><span class="sxs-lookup"><span data-stu-id="1d15a-153">In the <a href="https://portal.azure.com" target="_blank">Azure portal</a> or Visual Studio, open your logic app in Logic App Designer.</span></span> 

   <span data-ttu-id="1d15a-154">This example uses the Azure portal and a logic app with a **Recurrence** trigger and several **Initialize variable** actions.</span><span class="sxs-lookup"><span data-stu-id="1d15a-154">This example uses the Azure portal and a logic app with a **Recurrence** trigger and several **Initialize variable** actions.</span></span> 
   <span data-ttu-id="1d15a-155">These actions are set up for creating two string variables and an integer variable.</span><span class="sxs-lookup"><span data-stu-id="1d15a-155">These actions are set up for creating two string variables and an integer variable.</span></span> <span data-ttu-id="1d15a-156">When you later test your logic app, you can manually run your app without waiting for the trigger to fire.</span><span class="sxs-lookup"><span data-stu-id="1d15a-156">When you later test your logic app, you can manually run your app without waiting for the trigger to fire.</span></span>

   ![Starting sample logic app](./media/logic-apps-perform-data-operations/sample-starting-logic-app-compose-action.png)

2. <span data-ttu-id="1d15a-158">In your logic app where you want to create the output, follow one of these steps:</span><span class="sxs-lookup"><span data-stu-id="1d15a-158">In your logic app where you want to create the output, follow one of these steps:</span></span> 

   * <span data-ttu-id="1d15a-159">To add an action under the last step, choose **New step** > **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-159">To add an action under the last step, choose **New step** > **Add an action**.</span></span>

     ![Add action](./media/logic-apps-perform-data-operations/add-compose-action.png)

   * <span data-ttu-id="1d15a-161">To add an action between steps, move your mouse over the connecting arrow so the plus sign (+) appears.</span><span class="sxs-lookup"><span data-stu-id="1d15a-161">To add an action between steps, move your mouse over the connecting arrow so the plus sign (+) appears.</span></span> 
   <span data-ttu-id="1d15a-162">Choose the plus sign, and then select **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-162">Choose the plus sign, and then select **Add an action**.</span></span>

3. <span data-ttu-id="1d15a-163">In the search box, enter "compose" as your filter.</span><span class="sxs-lookup"><span data-stu-id="1d15a-163">In the search box, enter "compose" as your filter.</span></span> <span data-ttu-id="1d15a-164">From the actions list, select this action: **Compose**</span><span class="sxs-lookup"><span data-stu-id="1d15a-164">From the actions list, select this action: **Compose**</span></span>

   ![Select "Compose" action](./media/logic-apps-perform-data-operations/select-compose-action.png)

4. <span data-ttu-id="1d15a-166">In the **Inputs** box, provide the inputs you want for creating the output.</span><span class="sxs-lookup"><span data-stu-id="1d15a-166">In the **Inputs** box, provide the inputs you want for creating the output.</span></span> 

   <span data-ttu-id="1d15a-167">For this example, when you click inside the **Inputs** box, the dynamic content list appears so you can select the previously created variables:</span><span class="sxs-lookup"><span data-stu-id="1d15a-167">For this example, when you click inside the **Inputs** box, the dynamic content list appears so you can select the previously created variables:</span></span>

   ![Select inputs to compose](./media/logic-apps-perform-data-operations/configure-compose-action.png)

   <span data-ttu-id="1d15a-169">Here is the finished example **Compose** action:</span><span class="sxs-lookup"><span data-stu-id="1d15a-169">Here is the finished example **Compose** action:</span></span> 

   ![Finished "Compose" action](./media/logic-apps-perform-data-operations/finished-compose-action.png)

5. <span data-ttu-id="1d15a-171">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="1d15a-171">Save your logic app.</span></span> <span data-ttu-id="1d15a-172">On the designer toolbar, choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-172">On the designer toolbar, choose **Save**.</span></span>

<span data-ttu-id="1d15a-173">For more information about this action in your underlying workflow definition, see the [Compose action](../logic-apps/logic-apps-workflow-actions-triggers.md#compose-action).</span><span class="sxs-lookup"><span data-stu-id="1d15a-173">For more information about this action in your underlying workflow definition, see the [Compose action](../logic-apps/logic-apps-workflow-actions-triggers.md#compose-action).</span></span> 

### <a name="test-your-logic-app"></a><span data-ttu-id="1d15a-174">Test your logic app</span><span class="sxs-lookup"><span data-stu-id="1d15a-174">Test your logic app</span></span>

<span data-ttu-id="1d15a-175">To confirm whether the **Compose** action creates the expected results, send yourself a notification that includes output from the **Compose** action.</span><span class="sxs-lookup"><span data-stu-id="1d15a-175">To confirm whether the **Compose** action creates the expected results, send yourself a notification that includes output from the **Compose** action.</span></span>

1. <span data-ttu-id="1d15a-176">In your logic app, add an action that can send you the results from the **Compose** action.</span><span class="sxs-lookup"><span data-stu-id="1d15a-176">In your logic app, add an action that can send you the results from the **Compose** action.</span></span>

2. <span data-ttu-id="1d15a-177">In that action, click anywhere you want the results to appear.</span><span class="sxs-lookup"><span data-stu-id="1d15a-177">In that action, click anywhere you want the results to appear.</span></span> <span data-ttu-id="1d15a-178">When the dynamic content list opens, under the **Compose** action, select **Output**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-178">When the dynamic content list opens, under the **Compose** action, select **Output**.</span></span> 

   <span data-ttu-id="1d15a-179">This example uses the **Office 365 Outlook - Send an email** action and includes the **Output** fields in the email's body and subject:</span><span class="sxs-lookup"><span data-stu-id="1d15a-179">This example uses the **Office 365 Outlook - Send an email** action and includes the **Output** fields in the email's body and subject:</span></span>

   !["Output" fields in the "Send an email" action](./media/logic-apps-perform-data-operations/send-email-compose-action.png)

3. <span data-ttu-id="1d15a-181">Now, manually run your logic app.</span><span class="sxs-lookup"><span data-stu-id="1d15a-181">Now, manually run your logic app.</span></span> <span data-ttu-id="1d15a-182">On the designer toolbar, choose **Run**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-182">On the designer toolbar, choose **Run**.</span></span> 

   <span data-ttu-id="1d15a-183">Based on the email connector you used, here are the results you get:</span><span class="sxs-lookup"><span data-stu-id="1d15a-183">Based on the email connector you used, here are the results you get:</span></span>

   ![Email with "Compose" action results](./media/logic-apps-perform-data-operations/compose-email-results.png)

<a name="create-csv-table-action"></a>

## <a name="create-csv-table-action"></a><span data-ttu-id="1d15a-185">Create CSV table action</span><span class="sxs-lookup"><span data-stu-id="1d15a-185">Create CSV table action</span></span>

<span data-ttu-id="1d15a-186">To create a comma-separated value (CSV) table that has the properties and values from JavaScript Object Notation (JSON) objects in an array, use the **Data Operations - Create CSV table** action.</span><span class="sxs-lookup"><span data-stu-id="1d15a-186">To create a comma-separated value (CSV) table that has the properties and values from JavaScript Object Notation (JSON) objects in an array, use the **Data Operations - Create CSV table** action.</span></span> <span data-ttu-id="1d15a-187">You can then use the resulting table in actions that follow the **Create CSV table** action.</span><span class="sxs-lookup"><span data-stu-id="1d15a-187">You can then use the resulting table in actions that follow the **Create CSV table** action.</span></span> 

<span data-ttu-id="1d15a-188">If you prefer working in the code view editor, you can copy the example **Create CSV table** and **Initialize variable** action definitions from this article into your own logic app's underlying workflow definition: [Data operation code examples - Create CSV table](../logic-apps/logic-apps-data-operations-code-samples.md#create-csv-table-action-example)</span><span class="sxs-lookup"><span data-stu-id="1d15a-188">If you prefer working in the code view editor, you can copy the example **Create CSV table** and **Initialize variable** action definitions from this article into your own logic app's underlying workflow definition: [Data operation code examples - Create CSV table](../logic-apps/logic-apps-data-operations-code-samples.md#create-csv-table-action-example)</span></span> 

1. <span data-ttu-id="1d15a-189">In the <a href="https://portal.azure.com" target="_blank">Azure portal</a> or Visual Studio, open your logic app in Logic App Designer.</span><span class="sxs-lookup"><span data-stu-id="1d15a-189">In the <a href="https://portal.azure.com" target="_blank">Azure portal</a> or Visual Studio, open your logic app in Logic App Designer.</span></span> 

   <span data-ttu-id="1d15a-190">This example uses the Azure portal and a logic app with a **Recurrence** trigger and an **Initialize variable** action.</span><span class="sxs-lookup"><span data-stu-id="1d15a-190">This example uses the Azure portal and a logic app with a **Recurrence** trigger and an **Initialize variable** action.</span></span> 
   <span data-ttu-id="1d15a-191">The action is set up for creating a variable whose initial value is an array that has some properties and values in JSON format.</span><span class="sxs-lookup"><span data-stu-id="1d15a-191">The action is set up for creating a variable whose initial value is an array that has some properties and values in JSON format.</span></span> 
   <span data-ttu-id="1d15a-192">When you later test your logic app, you can manually run your app without waiting for the trigger to fire.</span><span class="sxs-lookup"><span data-stu-id="1d15a-192">When you later test your logic app, you can manually run your app without waiting for the trigger to fire.</span></span>

   ![Starting sample logic app](./media/logic-apps-perform-data-operations/sample-starting-logic-app-create-table-action.png)

2. <span data-ttu-id="1d15a-194">In your logic app where you want to create the CSV table, follow one of these steps:</span><span class="sxs-lookup"><span data-stu-id="1d15a-194">In your logic app where you want to create the CSV table, follow one of these steps:</span></span> 

   * <span data-ttu-id="1d15a-195">To add an action under the last step, choose **New step** > **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-195">To add an action under the last step, choose **New step** > **Add an action**.</span></span>

     ![Add action](./media/logic-apps-perform-data-operations/add-create-table-action.png)

   * <span data-ttu-id="1d15a-197">To add an action between steps, move your mouse over the connecting arrow so the plus sign (+) appears.</span><span class="sxs-lookup"><span data-stu-id="1d15a-197">To add an action between steps, move your mouse over the connecting arrow so the plus sign (+) appears.</span></span> 
   <span data-ttu-id="1d15a-198">Choose the plus sign, and then select **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-198">Choose the plus sign, and then select **Add an action**.</span></span>

3. <span data-ttu-id="1d15a-199">In the search box, enter "create csv table" as your filter.</span><span class="sxs-lookup"><span data-stu-id="1d15a-199">In the search box, enter "create csv table" as your filter.</span></span> <span data-ttu-id="1d15a-200">From the actions list, select this action: **Create CSV table**</span><span class="sxs-lookup"><span data-stu-id="1d15a-200">From the actions list, select this action: **Create CSV table**</span></span>

   ![Select "Create CSV table" action](./media/logic-apps-perform-data-operations/select-create-csv-table-action.png)

4. <span data-ttu-id="1d15a-202">In the **From** box, provide the array or expression you want for creating the table.</span><span class="sxs-lookup"><span data-stu-id="1d15a-202">In the **From** box, provide the array or expression you want for creating the table.</span></span> 

   <span data-ttu-id="1d15a-203">For this example, when you click inside the **From** box, the dynamic content list appears so you can select the previously created variable:</span><span class="sxs-lookup"><span data-stu-id="1d15a-203">For this example, when you click inside the **From** box, the dynamic content list appears so you can select the previously created variable:</span></span>

   ![Select array output for creating CSV table](./media/logic-apps-perform-data-operations/configure-create-csv-table-action.png)

   <span data-ttu-id="1d15a-205">Here is the finished example **Create CSV table** action:</span><span class="sxs-lookup"><span data-stu-id="1d15a-205">Here is the finished example **Create CSV table** action:</span></span> 

   ![Finished "Create CSV table" action](./media/logic-apps-perform-data-operations/finished-create-csv-table-action.png)

   <span data-ttu-id="1d15a-207">By default, this action automatically creates the columns based on the array items.</span><span class="sxs-lookup"><span data-stu-id="1d15a-207">By default, this action automatically creates the columns based on the array items.</span></span> 
   <span data-ttu-id="1d15a-208">To manually create the column headers and values, choose **Show advanced options**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-208">To manually create the column headers and values, choose **Show advanced options**.</span></span> 
   <span data-ttu-id="1d15a-209">To provide only custom values, change **Columns** to **Custom**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-209">To provide only custom values, change **Columns** to **Custom**.</span></span> 
   <span data-ttu-id="1d15a-210">To provide custom column headers too, change **Include headers** to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-210">To provide custom column headers too, change **Include headers** to **Yes**.</span></span> 

   > [!TIP]
   > <span data-ttu-id="1d15a-211">To create user-friendly tokens for the properties in JSON objects so you can select those properties as inputs, use the [Parse JSON](#parse-json-action) before calling the **Create CSV table** action.</span><span class="sxs-lookup"><span data-stu-id="1d15a-211">To create user-friendly tokens for the properties in JSON objects so you can select those properties as inputs, use the [Parse JSON](#parse-json-action) before calling the **Create CSV table** action.</span></span>

5. <span data-ttu-id="1d15a-212">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="1d15a-212">Save your logic app.</span></span> <span data-ttu-id="1d15a-213">On the designer toolbar, choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-213">On the designer toolbar, choose **Save**.</span></span>

<span data-ttu-id="1d15a-214">For more information about this action in your underlying workflow definition, see the [Table action](../logic-apps/logic-apps-workflow-actions-triggers.md#table-action).</span><span class="sxs-lookup"><span data-stu-id="1d15a-214">For more information about this action in your underlying workflow definition, see the [Table action](../logic-apps/logic-apps-workflow-actions-triggers.md#table-action).</span></span>

### <a name="test-your-logic-app"></a><span data-ttu-id="1d15a-215">Test your logic app</span><span class="sxs-lookup"><span data-stu-id="1d15a-215">Test your logic app</span></span>

<span data-ttu-id="1d15a-216">To confirm whether the **Create CSV table** action creates the expected results, send yourself a notification that includes output from the **Create CSV table** action.</span><span class="sxs-lookup"><span data-stu-id="1d15a-216">To confirm whether the **Create CSV table** action creates the expected results, send yourself a notification that includes output from the **Create CSV table** action.</span></span>

1. <span data-ttu-id="1d15a-217">In your logic app, add an action that can send you the results from the **Create CSV table** action.</span><span class="sxs-lookup"><span data-stu-id="1d15a-217">In your logic app, add an action that can send you the results from the **Create CSV table** action.</span></span>

2. <span data-ttu-id="1d15a-218">In that action, click anywhere you want the results to appear.</span><span class="sxs-lookup"><span data-stu-id="1d15a-218">In that action, click anywhere you want the results to appear.</span></span> <span data-ttu-id="1d15a-219">When the dynamic content list opens, under the **Create CSV table** action, select **Output**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-219">When the dynamic content list opens, under the **Create CSV table** action, select **Output**.</span></span> 

   <span data-ttu-id="1d15a-220">This example uses the **Office 365 Outlook - Send an email** action and includes the **Output** field in the email's body:</span><span class="sxs-lookup"><span data-stu-id="1d15a-220">This example uses the **Office 365 Outlook - Send an email** action and includes the **Output** field in the email's body:</span></span>

   !["Output" fields in the "Send an email" action](./media/logic-apps-perform-data-operations/send-email-create-csv-table-action.png)

3. <span data-ttu-id="1d15a-222">Now, manually run your logic app.</span><span class="sxs-lookup"><span data-stu-id="1d15a-222">Now, manually run your logic app.</span></span> <span data-ttu-id="1d15a-223">On the designer toolbar, choose **Run**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-223">On the designer toolbar, choose **Run**.</span></span> 

   <span data-ttu-id="1d15a-224">Based on the email connector you used, here are the results you get:</span><span class="sxs-lookup"><span data-stu-id="1d15a-224">Based on the email connector you used, here are the results you get:</span></span>

   ![Email with "Create CSV table" action results](./media/logic-apps-perform-data-operations/create-csv-table-email-results.png)

<a name="create-html-table-action"></a>

## <a name="create-html-table-action"></a><span data-ttu-id="1d15a-226">Create HTML table action</span><span class="sxs-lookup"><span data-stu-id="1d15a-226">Create HTML table action</span></span>

<span data-ttu-id="1d15a-227">To create an HTML table that has the properties and values from JavaScript Object Notation (JSON) objects in an array, use the **Data Operations - Create HTML table** action.</span><span class="sxs-lookup"><span data-stu-id="1d15a-227">To create an HTML table that has the properties and values from JavaScript Object Notation (JSON) objects in an array, use the **Data Operations - Create HTML table** action.</span></span> <span data-ttu-id="1d15a-228">You can then use the resulting table in actions that follow the **Create HTML table** action.</span><span class="sxs-lookup"><span data-stu-id="1d15a-228">You can then use the resulting table in actions that follow the **Create HTML table** action.</span></span>

<span data-ttu-id="1d15a-229">If you prefer working in the code view editor, you can copy the example **Create HTML table** and **Initialize variable** action definitions from this article into your own logic app's underlying workflow definition: [Data operation code examples - Create HTML table](../logic-apps/logic-apps-data-operations-code-samples.md#create-html-table-action-example)</span><span class="sxs-lookup"><span data-stu-id="1d15a-229">If you prefer working in the code view editor, you can copy the example **Create HTML table** and **Initialize variable** action definitions from this article into your own logic app's underlying workflow definition: [Data operation code examples - Create HTML table](../logic-apps/logic-apps-data-operations-code-samples.md#create-html-table-action-example)</span></span> 

1. <span data-ttu-id="1d15a-230">In the <a href="https://portal.azure.com" target="_blank">Azure portal</a> or Visual Studio, open your logic app in Logic App Designer.</span><span class="sxs-lookup"><span data-stu-id="1d15a-230">In the <a href="https://portal.azure.com" target="_blank">Azure portal</a> or Visual Studio, open your logic app in Logic App Designer.</span></span> 

   <span data-ttu-id="1d15a-231">This example uses the Azure portal and a logic app with a **Recurrence** trigger and an **Initialize variable** action.</span><span class="sxs-lookup"><span data-stu-id="1d15a-231">This example uses the Azure portal and a logic app with a **Recurrence** trigger and an **Initialize variable** action.</span></span> 
   <span data-ttu-id="1d15a-232">The action is set up for creating a variable whose initial value is an array that has some properties and values in JSON format.</span><span class="sxs-lookup"><span data-stu-id="1d15a-232">The action is set up for creating a variable whose initial value is an array that has some properties and values in JSON format.</span></span> 
   <span data-ttu-id="1d15a-233">When you later test your logic app, you can manually run your app without waiting for the trigger to fire.</span><span class="sxs-lookup"><span data-stu-id="1d15a-233">When you later test your logic app, you can manually run your app without waiting for the trigger to fire.</span></span>

   ![Starting sample logic app](./media/logic-apps-perform-data-operations/sample-starting-logic-app-create-table-action.png)

2. <span data-ttu-id="1d15a-235">In your logic app where you want to create an HTML table, follow one of these steps:</span><span class="sxs-lookup"><span data-stu-id="1d15a-235">In your logic app where you want to create an HTML table, follow one of these steps:</span></span> 

   * <span data-ttu-id="1d15a-236">To add an action under the last step, choose **New step** > **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-236">To add an action under the last step, choose **New step** > **Add an action**.</span></span>

     ![Add action](./media/logic-apps-perform-data-operations/add-create-table-action.png)

   * <span data-ttu-id="1d15a-238">To add an action between steps, move your mouse over the connecting arrow so the plus sign (+) appears.</span><span class="sxs-lookup"><span data-stu-id="1d15a-238">To add an action between steps, move your mouse over the connecting arrow so the plus sign (+) appears.</span></span> 
   <span data-ttu-id="1d15a-239">Choose the plus sign, and then select **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-239">Choose the plus sign, and then select **Add an action**.</span></span>

3. <span data-ttu-id="1d15a-240">In the search box, enter "create html table" as your filter.</span><span class="sxs-lookup"><span data-stu-id="1d15a-240">In the search box, enter "create html table" as your filter.</span></span> <span data-ttu-id="1d15a-241">From the actions list, select this action: **Create HTML table**</span><span class="sxs-lookup"><span data-stu-id="1d15a-241">From the actions list, select this action: **Create HTML table**</span></span>

   ![Select "Create HTML table" action](./media/logic-apps-perform-data-operations/select-create-html-table-action.png)

4. <span data-ttu-id="1d15a-243">In the **From** box, provide the array or expression you want for creating the table.</span><span class="sxs-lookup"><span data-stu-id="1d15a-243">In the **From** box, provide the array or expression you want for creating the table.</span></span> 

   <span data-ttu-id="1d15a-244">For this example, when you click inside the **From** box, the dynamic content list appears so you can select the previously created variable:</span><span class="sxs-lookup"><span data-stu-id="1d15a-244">For this example, when you click inside the **From** box, the dynamic content list appears so you can select the previously created variable:</span></span>

   ![Select array output for creating HTML table](./media/logic-apps-perform-data-operations/configure-create-html-table-action.png)

   <span data-ttu-id="1d15a-246">Here is the finished example **Create HTML table** action:</span><span class="sxs-lookup"><span data-stu-id="1d15a-246">Here is the finished example **Create HTML table** action:</span></span> 

   ![Finished "Create HTML table" action](./media/logic-apps-perform-data-operations/finished-create-html-table-action.png)

   <span data-ttu-id="1d15a-248">By default, this action automatically creates the columns based on the array items.</span><span class="sxs-lookup"><span data-stu-id="1d15a-248">By default, this action automatically creates the columns based on the array items.</span></span> 
   <span data-ttu-id="1d15a-249">To manually create the column headers and values, choose **Show advanced options**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-249">To manually create the column headers and values, choose **Show advanced options**.</span></span> 
   <span data-ttu-id="1d15a-250">To provide only custom values, change **Columns** to **Custom**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-250">To provide only custom values, change **Columns** to **Custom**.</span></span> 
   <span data-ttu-id="1d15a-251">To provide custom column headers too, change **Include headers** to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-251">To provide custom column headers too, change **Include headers** to **Yes**.</span></span> 

   > [!TIP]
   > <span data-ttu-id="1d15a-252">To create user-friendly tokens for the properties in JSON objects so you can select those properties as inputs, use the [Parse JSON](#parse-json-action) before calling the **Create HTML table** action.</span><span class="sxs-lookup"><span data-stu-id="1d15a-252">To create user-friendly tokens for the properties in JSON objects so you can select those properties as inputs, use the [Parse JSON](#parse-json-action) before calling the **Create HTML table** action.</span></span>

5. <span data-ttu-id="1d15a-253">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="1d15a-253">Save your logic app.</span></span> <span data-ttu-id="1d15a-254">On the designer toolbar, choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-254">On the designer toolbar, choose **Save**.</span></span>

<span data-ttu-id="1d15a-255">For more information about this action in your underlying workflow definition, see the [Table action](../logic-apps/logic-apps-workflow-actions-triggers.md#table-action).</span><span class="sxs-lookup"><span data-stu-id="1d15a-255">For more information about this action in your underlying workflow definition, see the [Table action](../logic-apps/logic-apps-workflow-actions-triggers.md#table-action).</span></span>

### <a name="test-your-logic-app"></a><span data-ttu-id="1d15a-256">Test your logic app</span><span class="sxs-lookup"><span data-stu-id="1d15a-256">Test your logic app</span></span>

<span data-ttu-id="1d15a-257">To confirm whether the **Create HTML table** action creates the expected results, send yourself a notification that includes output from the **Create HTML table** action.</span><span class="sxs-lookup"><span data-stu-id="1d15a-257">To confirm whether the **Create HTML table** action creates the expected results, send yourself a notification that includes output from the **Create HTML table** action.</span></span>

1. <span data-ttu-id="1d15a-258">In your logic app, add an action that can send you the results from the **Create HTML table** action.</span><span class="sxs-lookup"><span data-stu-id="1d15a-258">In your logic app, add an action that can send you the results from the **Create HTML table** action.</span></span>

2. <span data-ttu-id="1d15a-259">In that action, click anywhere you want the results to appear.</span><span class="sxs-lookup"><span data-stu-id="1d15a-259">In that action, click anywhere you want the results to appear.</span></span> <span data-ttu-id="1d15a-260">When the dynamic content list opens, under the **Create HTML table** action, select **Output**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-260">When the dynamic content list opens, under the **Create HTML table** action, select **Output**.</span></span> 

   <span data-ttu-id="1d15a-261">This example uses the **Office 365 Outlook - Send an email** action and includes the **Output** field in the email's body:</span><span class="sxs-lookup"><span data-stu-id="1d15a-261">This example uses the **Office 365 Outlook - Send an email** action and includes the **Output** field in the email's body:</span></span>

   !["Output" fields in the "Send an email" action](./media/logic-apps-perform-data-operations/send-email-create-html-table-action.png)
   
   > [!NOTE]
   > <span data-ttu-id="1d15a-263">When including the HTML table output in an email action, make sure that you set the **Is HTML** property to **Yes** in the email action's advanced options.</span><span class="sxs-lookup"><span data-stu-id="1d15a-263">When including the HTML table output in an email action, make sure that you set the **Is HTML** property to **Yes** in the email action's advanced options.</span></span> <span data-ttu-id="1d15a-264">That way, the email action correctly formats the HTML table.</span><span class="sxs-lookup"><span data-stu-id="1d15a-264">That way, the email action correctly formats the HTML table.</span></span>

3. <span data-ttu-id="1d15a-265">Now, manually run your logic app.</span><span class="sxs-lookup"><span data-stu-id="1d15a-265">Now, manually run your logic app.</span></span> <span data-ttu-id="1d15a-266">On the designer toolbar, choose **Run**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-266">On the designer toolbar, choose **Run**.</span></span> 

   <span data-ttu-id="1d15a-267">Based on the email connector you used, here are the results you get:</span><span class="sxs-lookup"><span data-stu-id="1d15a-267">Based on the email connector you used, here are the results you get:</span></span>

   ![Email with "Create HTML table" action results](./media/logic-apps-perform-data-operations/create-html-table-email-results.png)

<a name="filter-array-action"></a>

## <a name="filter-array-action"></a><span data-ttu-id="1d15a-269">Filter array action</span><span class="sxs-lookup"><span data-stu-id="1d15a-269">Filter array action</span></span>

<span data-ttu-id="1d15a-270">To create a smaller array that has items, which meet specific criteria, from an existing array, use the **Data Operations - Filter array** action.</span><span class="sxs-lookup"><span data-stu-id="1d15a-270">To create a smaller array that has items, which meet specific criteria, from an existing array, use the **Data Operations - Filter array** action.</span></span> <span data-ttu-id="1d15a-271">You can then use the filtered array in actions that follow after the **Filter array** action.</span><span class="sxs-lookup"><span data-stu-id="1d15a-271">You can then use the filtered array in actions that follow after the **Filter array** action.</span></span> 

> [!NOTE]
> <span data-ttu-id="1d15a-272">Any filter text that you use in your condition is case sensitive.</span><span class="sxs-lookup"><span data-stu-id="1d15a-272">Any filter text that you use in your condition is case sensitive.</span></span> <span data-ttu-id="1d15a-273">Also, this action can't change the format or components of items in the array.</span><span class="sxs-lookup"><span data-stu-id="1d15a-273">Also, this action can't change the format or components of items in the array.</span></span> 
> 
> <span data-ttu-id="1d15a-274">For actions to use the array output from the **Filter array** action, either those actions must accept arrays as input, or you might have to transform the output array into another compatible format.</span><span class="sxs-lookup"><span data-stu-id="1d15a-274">For actions to use the array output from the **Filter array** action, either those actions must accept arrays as input, or you might have to transform the output array into another compatible format.</span></span> 

<span data-ttu-id="1d15a-275">If you prefer working in the code view editor, you can copy the example **Filter array** and **Initialize variable** action definitions from this article into your own logic app's underlying workflow definition: [Data operation code examples - Filter array](../logic-apps/logic-apps-data-operations-code-samples.md#filter-array-action-example)</span><span class="sxs-lookup"><span data-stu-id="1d15a-275">If you prefer working in the code view editor, you can copy the example **Filter array** and **Initialize variable** action definitions from this article into your own logic app's underlying workflow definition: [Data operation code examples - Filter array](../logic-apps/logic-apps-data-operations-code-samples.md#filter-array-action-example)</span></span> 

1. <span data-ttu-id="1d15a-276">In the <a href="https://portal.azure.com" target="_blank">Azure portal</a> or Visual Studio, open your logic app in Logic App Designer.</span><span class="sxs-lookup"><span data-stu-id="1d15a-276">In the <a href="https://portal.azure.com" target="_blank">Azure portal</a> or Visual Studio, open your logic app in Logic App Designer.</span></span> 

   <span data-ttu-id="1d15a-277">This example uses the Azure portal and a logic app with a **Recurrence** trigger and an **Initialize variable** action.</span><span class="sxs-lookup"><span data-stu-id="1d15a-277">This example uses the Azure portal and a logic app with a **Recurrence** trigger and an **Initialize variable** action.</span></span> 
   <span data-ttu-id="1d15a-278">The action is set up for creating a variable whose initial value is an array that has some sample integers.</span><span class="sxs-lookup"><span data-stu-id="1d15a-278">The action is set up for creating a variable whose initial value is an array that has some sample integers.</span></span> <span data-ttu-id="1d15a-279">When you later test your logic app, you can manually run your app without waiting for the trigger to fire.</span><span class="sxs-lookup"><span data-stu-id="1d15a-279">When you later test your logic app, you can manually run your app without waiting for the trigger to fire.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1d15a-280">Although this example uses a simple integer array, this action is especially useful for JSON object arrays where you can filter based on the objects' properties and values.</span><span class="sxs-lookup"><span data-stu-id="1d15a-280">Although this example uses a simple integer array, this action is especially useful for JSON object arrays where you can filter based on the objects' properties and values.</span></span>

   ![Starting sample logic app](./media/logic-apps-perform-data-operations/sample-starting-logic-app-filter-array-action.png)

2. <span data-ttu-id="1d15a-282">In your logic app where you want to create the filtered array, follow one of these steps:</span><span class="sxs-lookup"><span data-stu-id="1d15a-282">In your logic app where you want to create the filtered array, follow one of these steps:</span></span> 

   * <span data-ttu-id="1d15a-283">To add an action under the last step, choose **New step** > **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-283">To add an action under the last step, choose **New step** > **Add an action**.</span></span>

     ![Add action](./media/logic-apps-perform-data-operations/add-filter-array-action.png)

   * <span data-ttu-id="1d15a-285">To add an action between steps, move your mouse over the connecting arrow so the plus sign (+) appears.</span><span class="sxs-lookup"><span data-stu-id="1d15a-285">To add an action between steps, move your mouse over the connecting arrow so the plus sign (+) appears.</span></span> 
   <span data-ttu-id="1d15a-286">Choose the plus sign, and then select **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-286">Choose the plus sign, and then select **Add an action**.</span></span>

3. <span data-ttu-id="1d15a-287">In the search box, enter "filter array" as your filter.</span><span class="sxs-lookup"><span data-stu-id="1d15a-287">In the search box, enter "filter array" as your filter.</span></span> <span data-ttu-id="1d15a-288">From the actions list, select this action: **Filter array**</span><span class="sxs-lookup"><span data-stu-id="1d15a-288">From the actions list, select this action: **Filter array**</span></span>

   ![Select "Filter array" action](./media/logic-apps-perform-data-operations/select-filter-array-action.png)

4. <span data-ttu-id="1d15a-290">In the **From** box, provide the array or expression you want to filter.</span><span class="sxs-lookup"><span data-stu-id="1d15a-290">In the **From** box, provide the array or expression you want to filter.</span></span> 

   <span data-ttu-id="1d15a-291">For this example, when you click inside the **From** box, the dynamic content list appears so you can select the previously created variable:</span><span class="sxs-lookup"><span data-stu-id="1d15a-291">For this example, when you click inside the **From** box, the dynamic content list appears so you can select the previously created variable:</span></span>

   ![Select array output for creating filtered array](./media/logic-apps-perform-data-operations/configure-filter-array-action.png)

5. <span data-ttu-id="1d15a-293">For the condition, specify the array items to compare, select the comparison operator, and specify the comparison value.</span><span class="sxs-lookup"><span data-stu-id="1d15a-293">For the condition, specify the array items to compare, select the comparison operator, and specify the comparison value.</span></span>

   <span data-ttu-id="1d15a-294">This example uses the **item()** function for accessing each item in the array while the **Filter array** action searches for array items whose value is greater than 1:</span><span class="sxs-lookup"><span data-stu-id="1d15a-294">This example uses the **item()** function for accessing each item in the array while the **Filter array** action searches for array items whose value is greater than 1:</span></span>
   
   ![Finished "Filter array" action](./media/logic-apps-perform-data-operations/finished-filter-array-action.png)

6. <span data-ttu-id="1d15a-296">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="1d15a-296">Save your logic app.</span></span> <span data-ttu-id="1d15a-297">On the designer toolbar, choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-297">On the designer toolbar, choose **Save**.</span></span>

<span data-ttu-id="1d15a-298">For more information about this action in your underlying workflow definition, see [Query action](../logic-apps/logic-apps-workflow-actions-triggers.md#query-action).</span><span class="sxs-lookup"><span data-stu-id="1d15a-298">For more information about this action in your underlying workflow definition, see [Query action](../logic-apps/logic-apps-workflow-actions-triggers.md#query-action).</span></span>

### <a name="test-your-logic-app"></a><span data-ttu-id="1d15a-299">Test your logic app</span><span class="sxs-lookup"><span data-stu-id="1d15a-299">Test your logic app</span></span>

<span data-ttu-id="1d15a-300">To confirm whether **Filter array** action creates the expected results, send yourself a notification that includes output from the **Filter array** action.</span><span class="sxs-lookup"><span data-stu-id="1d15a-300">To confirm whether **Filter array** action creates the expected results, send yourself a notification that includes output from the **Filter array** action.</span></span>

1. <span data-ttu-id="1d15a-301">In your logic app, add an action that can send you the results from the **Filter array** action.</span><span class="sxs-lookup"><span data-stu-id="1d15a-301">In your logic app, add an action that can send you the results from the **Filter array** action.</span></span>

2. <span data-ttu-id="1d15a-302">In that action, click anywhere you want the results to appear.</span><span class="sxs-lookup"><span data-stu-id="1d15a-302">In that action, click anywhere you want the results to appear.</span></span> <span data-ttu-id="1d15a-303">When the dynamic content list opens, choose **Expression**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-303">When the dynamic content list opens, choose **Expression**.</span></span> <span data-ttu-id="1d15a-304">To get the array output from the **Filter array** action, enter this expression that includes the **Filter array** action's name:</span><span class="sxs-lookup"><span data-stu-id="1d15a-304">To get the array output from the **Filter array** action, enter this expression that includes the **Filter array** action's name:</span></span>

   ```
   @actionBody('Filter_array')
   ```

   <span data-ttu-id="1d15a-305">This example uses the **Office 365 Outlook - Send an email** action and includes the outputs from the **actionBody('Filter_array')** expression in the email's body:</span><span class="sxs-lookup"><span data-stu-id="1d15a-305">This example uses the **Office 365 Outlook - Send an email** action and includes the outputs from the **actionBody('Filter_array')** expression in the email's body:</span></span>

   ![Action outputs in the "Send an email" action](./media/logic-apps-perform-data-operations/send-email-filter-array-action.png)

3. <span data-ttu-id="1d15a-307">Now, manually run your logic app.</span><span class="sxs-lookup"><span data-stu-id="1d15a-307">Now, manually run your logic app.</span></span> <span data-ttu-id="1d15a-308">On the designer toolbar, choose **Run**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-308">On the designer toolbar, choose **Run**.</span></span> 

   <span data-ttu-id="1d15a-309">Based on the email connector you used, here are the results you get:</span><span class="sxs-lookup"><span data-stu-id="1d15a-309">Based on the email connector you used, here are the results you get:</span></span>

   ![Email with "Filter array" action results](./media/logic-apps-perform-data-operations/filter-array-email-results.png)

<a name="join-action"></a>

## <a name="join-action"></a><span data-ttu-id="1d15a-311">Join action</span><span class="sxs-lookup"><span data-stu-id="1d15a-311">Join action</span></span>

<span data-ttu-id="1d15a-312">To create a string that has all the items from an array and separate those items with a specific delimiter character, use the **Data Operations - Join** action.</span><span class="sxs-lookup"><span data-stu-id="1d15a-312">To create a string that has all the items from an array and separate those items with a specific delimiter character, use the **Data Operations - Join** action.</span></span> <span data-ttu-id="1d15a-313">You can then use the string in actions that follow after the **Join** action.</span><span class="sxs-lookup"><span data-stu-id="1d15a-313">You can then use the string in actions that follow after the **Join** action.</span></span>

<span data-ttu-id="1d15a-314">If you prefer working in the code view editor, you can copy the example **Join** and **Initialize variable** action definitions from this article into your own logic app's underlying workflow definition: [Data operation code examples - Join](../logic-apps/logic-apps-data-operations-code-samples.md#join-action-example)</span><span class="sxs-lookup"><span data-stu-id="1d15a-314">If you prefer working in the code view editor, you can copy the example **Join** and **Initialize variable** action definitions from this article into your own logic app's underlying workflow definition: [Data operation code examples - Join](../logic-apps/logic-apps-data-operations-code-samples.md#join-action-example)</span></span> 

1. <span data-ttu-id="1d15a-315">In the <a href="https://portal.azure.com" target="_blank">Azure portal</a> or Visual Studio, open your logic app in Logic App Designer.</span><span class="sxs-lookup"><span data-stu-id="1d15a-315">In the <a href="https://portal.azure.com" target="_blank">Azure portal</a> or Visual Studio, open your logic app in Logic App Designer.</span></span> 

   <span data-ttu-id="1d15a-316">This example uses the Azure portal and a logic app with a **Recurrence** trigger and an **Initialize variable** action.</span><span class="sxs-lookup"><span data-stu-id="1d15a-316">This example uses the Azure portal and a logic app with a **Recurrence** trigger and an **Initialize variable** action.</span></span> 
   <span data-ttu-id="1d15a-317">This action is set up for creating a variable whose initial value is an array that has some sample integers.</span><span class="sxs-lookup"><span data-stu-id="1d15a-317">This action is set up for creating a variable whose initial value is an array that has some sample integers.</span></span> 
   <span data-ttu-id="1d15a-318">When you test your logic app later, you can manually run your app without waiting for the trigger to fire.</span><span class="sxs-lookup"><span data-stu-id="1d15a-318">When you test your logic app later, you can manually run your app without waiting for the trigger to fire.</span></span>

   ![Starting sample logic app](./media/logic-apps-perform-data-operations/sample-starting-logic-app-join-action.png)

2. <span data-ttu-id="1d15a-320">In your logic app where you want to create the string from an array, follow one of these steps:</span><span class="sxs-lookup"><span data-stu-id="1d15a-320">In your logic app where you want to create the string from an array, follow one of these steps:</span></span> 

   * <span data-ttu-id="1d15a-321">To add an action under the last step, choose **New step** > **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-321">To add an action under the last step, choose **New step** > **Add an action**.</span></span>

     ![Add action](./media/logic-apps-perform-data-operations/add-join-action.png)

   * <span data-ttu-id="1d15a-323">To add an action between steps, move your mouse over the connecting arrow so the plus sign (+) appears.</span><span class="sxs-lookup"><span data-stu-id="1d15a-323">To add an action between steps, move your mouse over the connecting arrow so the plus sign (+) appears.</span></span> 
   <span data-ttu-id="1d15a-324">Choose the plus sign, and then select **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-324">Choose the plus sign, and then select **Add an action**.</span></span>

3. <span data-ttu-id="1d15a-325">In the search box, enter "join" as your filter.</span><span class="sxs-lookup"><span data-stu-id="1d15a-325">In the search box, enter "join" as your filter.</span></span> <span data-ttu-id="1d15a-326">From the actions list, select this action: **Join**</span><span class="sxs-lookup"><span data-stu-id="1d15a-326">From the actions list, select this action: **Join**</span></span>

   ![Select "Data Operations - Join" action](./media/logic-apps-perform-data-operations/select-join-action.png)

4. <span data-ttu-id="1d15a-328">In the **From** box, provide the array that has the items you want to join as a string.</span><span class="sxs-lookup"><span data-stu-id="1d15a-328">In the **From** box, provide the array that has the items you want to join as a string.</span></span> 

   <span data-ttu-id="1d15a-329">For this example, when you click inside the **From** box, the dynamic content list that appears so you can select the previously created variable:</span><span class="sxs-lookup"><span data-stu-id="1d15a-329">For this example, when you click inside the **From** box, the dynamic content list that appears so you can select the previously created variable:</span></span>  

   ![Select array output for creating the string](./media/logic-apps-perform-data-operations/configure-join-action.png)

5. <span data-ttu-id="1d15a-331">In the **Join with** box, enter the character you want for separating each array item.</span><span class="sxs-lookup"><span data-stu-id="1d15a-331">In the **Join with** box, enter the character you want for separating each array item.</span></span> 

   <span data-ttu-id="1d15a-332">This example uses a colon (:) as the separator.</span><span class="sxs-lookup"><span data-stu-id="1d15a-332">This example uses a colon (:) as the separator.</span></span>

   ![Provide the separator character](./media/logic-apps-perform-data-operations/finished-join-action.png)

6. <span data-ttu-id="1d15a-334">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="1d15a-334">Save your logic app.</span></span> <span data-ttu-id="1d15a-335">On the designer toolbar, choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-335">On the designer toolbar, choose **Save**.</span></span>

<span data-ttu-id="1d15a-336">For more information about this action in your underlying workflow definition, see the [Join action](../logic-apps/logic-apps-workflow-actions-triggers.md#join-action).</span><span class="sxs-lookup"><span data-stu-id="1d15a-336">For more information about this action in your underlying workflow definition, see the [Join action](../logic-apps/logic-apps-workflow-actions-triggers.md#join-action).</span></span>

### <a name="test-your-logic-app"></a><span data-ttu-id="1d15a-337">Test your logic app</span><span class="sxs-lookup"><span data-stu-id="1d15a-337">Test your logic app</span></span>

<span data-ttu-id="1d15a-338">To confirm whether the **Join** action creates the expected results, send yourself a notification that includes output from the **Join** action.</span><span class="sxs-lookup"><span data-stu-id="1d15a-338">To confirm whether the **Join** action creates the expected results, send yourself a notification that includes output from the **Join** action.</span></span> 

1. <span data-ttu-id="1d15a-339">In your logic app, add an action that can send you the results from the **Join** action.</span><span class="sxs-lookup"><span data-stu-id="1d15a-339">In your logic app, add an action that can send you the results from the **Join** action.</span></span>

2. <span data-ttu-id="1d15a-340">In that action, click anywhere you want the results to appear.</span><span class="sxs-lookup"><span data-stu-id="1d15a-340">In that action, click anywhere you want the results to appear.</span></span> <span data-ttu-id="1d15a-341">When the dynamic content list opens, under the **Join** action, select **Output**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-341">When the dynamic content list opens, under the **Join** action, select **Output**.</span></span> 

   <span data-ttu-id="1d15a-342">This example uses the **Office 365 Outlook - Send an email** action and includes the **Output** field in the email's body:</span><span class="sxs-lookup"><span data-stu-id="1d15a-342">This example uses the **Office 365 Outlook - Send an email** action and includes the **Output** field in the email's body:</span></span>

   !["Output" fields in the "Send an email" action](./media/logic-apps-perform-data-operations/send-email-join-action.png)

3. <span data-ttu-id="1d15a-344">Now, manually run your logic app.</span><span class="sxs-lookup"><span data-stu-id="1d15a-344">Now, manually run your logic app.</span></span> <span data-ttu-id="1d15a-345">On the designer toolbar, choose **Run**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-345">On the designer toolbar, choose **Run**.</span></span> 

   <span data-ttu-id="1d15a-346">Based on the email connector you used, here are the results you get:</span><span class="sxs-lookup"><span data-stu-id="1d15a-346">Based on the email connector you used, here are the results you get:</span></span>

   ![Email with "Join" action results](./media/logic-apps-perform-data-operations/join-email-results.png)

<a name="parse-json-action"></a>

## <a name="parse-json-action"></a><span data-ttu-id="1d15a-348">Parse JSON action</span><span class="sxs-lookup"><span data-stu-id="1d15a-348">Parse JSON action</span></span>

<span data-ttu-id="1d15a-349">To reference or access properties in JavaScript Object Notation (JSON) content, you can create user-friendly fields or tokens for those properties by using the **Data operations - Parse JSON** action.</span><span class="sxs-lookup"><span data-stu-id="1d15a-349">To reference or access properties in JavaScript Object Notation (JSON) content, you can create user-friendly fields or tokens for those properties by using the **Data operations - Parse JSON** action.</span></span>
<span data-ttu-id="1d15a-350">That way, you can select those properties from the dynamic content list when you specify inputs for your logic app.</span><span class="sxs-lookup"><span data-stu-id="1d15a-350">That way, you can select those properties from the dynamic content list when you specify inputs for your logic app.</span></span> <span data-ttu-id="1d15a-351">For this action, you can either provide a JSON schema or generate a JSON schema from your sample JSON content or payload.</span><span class="sxs-lookup"><span data-stu-id="1d15a-351">For this action, you can either provide a JSON schema or generate a JSON schema from your sample JSON content or payload.</span></span>

<span data-ttu-id="1d15a-352">If you prefer working in the code view editor, you can copy the example **Parse JSON** and **Initialize variable** action definitions from this article into your own logic app's underlying workflow definition: [Data operation code examples - Parse JSON](../logic-apps/logic-apps-data-operations-code-samples.md#parse-json-action-example)</span><span class="sxs-lookup"><span data-stu-id="1d15a-352">If you prefer working in the code view editor, you can copy the example **Parse JSON** and **Initialize variable** action definitions from this article into your own logic app's underlying workflow definition: [Data operation code examples - Parse JSON](../logic-apps/logic-apps-data-operations-code-samples.md#parse-json-action-example)</span></span> 

1. <span data-ttu-id="1d15a-353">In the <a href="https://portal.azure.com" target="_blank">Azure portal</a> or Visual Studio, open your logic app in Logic App Designer.</span><span class="sxs-lookup"><span data-stu-id="1d15a-353">In the <a href="https://portal.azure.com" target="_blank">Azure portal</a> or Visual Studio, open your logic app in Logic App Designer.</span></span> 

   <span data-ttu-id="1d15a-354">This example uses the Azure portal and a logic app with a **Recurrence** trigger and an **Initialize variable** action.</span><span class="sxs-lookup"><span data-stu-id="1d15a-354">This example uses the Azure portal and a logic app with a **Recurrence** trigger and an **Initialize variable** action.</span></span> 
   <span data-ttu-id="1d15a-355">The action is set up for creating a variable whose initial value is a JSON object that has properties and values.</span><span class="sxs-lookup"><span data-stu-id="1d15a-355">The action is set up for creating a variable whose initial value is a JSON object that has properties and values.</span></span> 
   <span data-ttu-id="1d15a-356">When you later test your logic app, you can manually run your app without waiting for the trigger to fire.</span><span class="sxs-lookup"><span data-stu-id="1d15a-356">When you later test your logic app, you can manually run your app without waiting for the trigger to fire.</span></span>

   ![Starting sample logic app](./media/logic-apps-perform-data-operations/sample-starting-logic-app-parse-json-action.png)

2. <span data-ttu-id="1d15a-358">In your logic app where you want to parse the JSON content, follow one of these steps:</span><span class="sxs-lookup"><span data-stu-id="1d15a-358">In your logic app where you want to parse the JSON content, follow one of these steps:</span></span> 

   * <span data-ttu-id="1d15a-359">To add an action under the last step, choose **New step** > **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-359">To add an action under the last step, choose **New step** > **Add an action**.</span></span>

     ![Add action](./media/logic-apps-perform-data-operations/add-parse-json-action.png)

   * <span data-ttu-id="1d15a-361">To add an action between steps, move your mouse over the connecting arrow so the plus sign (+) appears.</span><span class="sxs-lookup"><span data-stu-id="1d15a-361">To add an action between steps, move your mouse over the connecting arrow so the plus sign (+) appears.</span></span> 
   <span data-ttu-id="1d15a-362">Choose the plus sign, and then select **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-362">Choose the plus sign, and then select **Add an action**.</span></span>

3. <span data-ttu-id="1d15a-363">In the search box, enter "parse json" as your filter.</span><span class="sxs-lookup"><span data-stu-id="1d15a-363">In the search box, enter "parse json" as your filter.</span></span> <span data-ttu-id="1d15a-364">From the actions list, select this action: **Parse JSON**</span><span class="sxs-lookup"><span data-stu-id="1d15a-364">From the actions list, select this action: **Parse JSON**</span></span>

   ![Select "Parse JSON" action](./media/logic-apps-perform-data-operations/select-parse-json-action.png)

4. <span data-ttu-id="1d15a-366">In the **Content** box, provide the JSON content you want to parse.</span><span class="sxs-lookup"><span data-stu-id="1d15a-366">In the **Content** box, provide the JSON content you want to parse.</span></span> 

   <span data-ttu-id="1d15a-367">For this example, when you click inside the **Content** box, the dynamic content list appears so you can select the previously created variable:</span><span class="sxs-lookup"><span data-stu-id="1d15a-367">For this example, when you click inside the **Content** box, the dynamic content list appears so you can select the previously created variable:</span></span>

   ![Select JSON object for parse JSON action](./media/logic-apps-perform-data-operations/configure-parse-json-action.png)

5. <span data-ttu-id="1d15a-369">Enter the JSON schema that describes the JSON content you're parsing.</span><span class="sxs-lookup"><span data-stu-id="1d15a-369">Enter the JSON schema that describes the JSON content you're parsing.</span></span> 

   <span data-ttu-id="1d15a-370">For this example, here is the JSON schema:</span><span class="sxs-lookup"><span data-stu-id="1d15a-370">For this example, here is the JSON schema:</span></span>

   ![Provide JSON schema for the JSON object you want to parse](./media/logic-apps-perform-data-operations/provide-schema-parse-json-action.png)

   <span data-ttu-id="1d15a-372">If you don't have the schema, you can generate that schema from the JSON content, or *payload*, you're parsing.</span><span class="sxs-lookup"><span data-stu-id="1d15a-372">If you don't have the schema, you can generate that schema from the JSON content, or *payload*, you're parsing.</span></span> 
   
   1. <span data-ttu-id="1d15a-373">In the **Parse JSON** action, select **Use sample payload to generate schema**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-373">In the **Parse JSON** action, select **Use sample payload to generate schema**.</span></span>

   2. <span data-ttu-id="1d15a-374">Under **Enter or paste a sample JSON payload**, provide the JSON content, and then choose **Done**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-374">Under **Enter or paste a sample JSON payload**, provide the JSON content, and then choose **Done**.</span></span>

      ![Enter the JSON content for generating the schema](./media/logic-apps-perform-data-operations/generate-schema-parse-json-action.png)

6. <span data-ttu-id="1d15a-376">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="1d15a-376">Save your logic app.</span></span> <span data-ttu-id="1d15a-377">On the designer toolbar, choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-377">On the designer toolbar, choose **Save**.</span></span>

<span data-ttu-id="1d15a-378">For more information about this action in your underlying workflow definition, see [Parse JSON action](../logic-apps/logic-apps-workflow-actions-triggers.md).</span><span class="sxs-lookup"><span data-stu-id="1d15a-378">For more information about this action in your underlying workflow definition, see [Parse JSON action](../logic-apps/logic-apps-workflow-actions-triggers.md).</span></span>

### <a name="test-your-logic-app"></a><span data-ttu-id="1d15a-379">Test your logic app</span><span class="sxs-lookup"><span data-stu-id="1d15a-379">Test your logic app</span></span>

<span data-ttu-id="1d15a-380">To confirm whether the **Parse JSON** action creates the expected results, send yourself a notification that includes output from the **Parse JSON** action.</span><span class="sxs-lookup"><span data-stu-id="1d15a-380">To confirm whether the **Parse JSON** action creates the expected results, send yourself a notification that includes output from the **Parse JSON** action.</span></span>

1. <span data-ttu-id="1d15a-381">In your logic app, add an action that can send you the results from the **Parse JSON** action.</span><span class="sxs-lookup"><span data-stu-id="1d15a-381">In your logic app, add an action that can send you the results from the **Parse JSON** action.</span></span>

2. <span data-ttu-id="1d15a-382">In that action, click anywhere you want the results to appear.</span><span class="sxs-lookup"><span data-stu-id="1d15a-382">In that action, click anywhere you want the results to appear.</span></span> <span data-ttu-id="1d15a-383">When the dynamic content list opens, under the **Parse JSON** action, you can now select the properties from the parsed JSON content.</span><span class="sxs-lookup"><span data-stu-id="1d15a-383">When the dynamic content list opens, under the **Parse JSON** action, you can now select the properties from the parsed JSON content.</span></span>

   <span data-ttu-id="1d15a-384">This example uses the **Office 365 Outlook - Send an email** action and includes the **FirstName**, **LastName**, and **Email** fields in the email's body:</span><span class="sxs-lookup"><span data-stu-id="1d15a-384">This example uses the **Office 365 Outlook - Send an email** action and includes the **FirstName**, **LastName**, and **Email** fields in the email's body:</span></span>

   ![JSON properties in the "Send an email" action](./media/logic-apps-perform-data-operations/send-email-parse-json-action.png)

   <span data-ttu-id="1d15a-386">Here is the finished email action:</span><span class="sxs-lookup"><span data-stu-id="1d15a-386">Here is the finished email action:</span></span>

   ![Finished email action](./media/logic-apps-perform-data-operations/send-email-parse-json-action-2.png)

3. <span data-ttu-id="1d15a-388">Now, manually run your logic app.</span><span class="sxs-lookup"><span data-stu-id="1d15a-388">Now, manually run your logic app.</span></span> <span data-ttu-id="1d15a-389">On the designer toolbar, choose **Run**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-389">On the designer toolbar, choose **Run**.</span></span> 

   <span data-ttu-id="1d15a-390">Based on the email connector you used, here are the results you get:</span><span class="sxs-lookup"><span data-stu-id="1d15a-390">Based on the email connector you used, here are the results you get:</span></span>

   ![Email with "Join" action results](./media/logic-apps-perform-data-operations/parse-json-email-results.png)

<a name="select-action"></a>

## <a name="select-action"></a><span data-ttu-id="1d15a-392">Select action</span><span class="sxs-lookup"><span data-stu-id="1d15a-392">Select action</span></span>

<span data-ttu-id="1d15a-393">To create an array that has JSON objects built from values in an existing array, use the **Data operations - Select** action.</span><span class="sxs-lookup"><span data-stu-id="1d15a-393">To create an array that has JSON objects built from values in an existing array, use the **Data operations - Select** action.</span></span> <span data-ttu-id="1d15a-394">For example, you can create a JSON object for each value in an integer array by specifying the properties that each JSON object must have and how to map the values in the source array to those properties.</span><span class="sxs-lookup"><span data-stu-id="1d15a-394">For example, you can create a JSON object for each value in an integer array by specifying the properties that each JSON object must have and how to map the values in the source array to those properties.</span></span> <span data-ttu-id="1d15a-395">And although you can change the components in those JSON objects, the output array always has the same number of items as the source array.</span><span class="sxs-lookup"><span data-stu-id="1d15a-395">And although you can change the components in those JSON objects, the output array always has the same number of items as the source array.</span></span>

> [!NOTE]
> <span data-ttu-id="1d15a-396">For actions to use the array output from the **Select** action, either those actions must accept arrays as input, or you might have to transform the output array into another compatible format.</span><span class="sxs-lookup"><span data-stu-id="1d15a-396">For actions to use the array output from the **Select** action, either those actions must accept arrays as input, or you might have to transform the output array into another compatible format.</span></span> 

<span data-ttu-id="1d15a-397">If you prefer working in the code view editor, you can copy the example **Select** and **Initialize variable** action definitions from this article into your own logic app's underlying workflow definition: [Data operation code examples - Select](../logic-apps/logic-apps-data-operations-code-samples.md#select-action-example)</span><span class="sxs-lookup"><span data-stu-id="1d15a-397">If you prefer working in the code view editor, you can copy the example **Select** and **Initialize variable** action definitions from this article into your own logic app's underlying workflow definition: [Data operation code examples - Select](../logic-apps/logic-apps-data-operations-code-samples.md#select-action-example)</span></span> 

1. <span data-ttu-id="1d15a-398">In the <a href="https://portal.azure.com" target="_blank">Azure portal</a> or Visual Studio, open your logic app in Logic App Designer.</span><span class="sxs-lookup"><span data-stu-id="1d15a-398">In the <a href="https://portal.azure.com" target="_blank">Azure portal</a> or Visual Studio, open your logic app in Logic App Designer.</span></span> 

   <span data-ttu-id="1d15a-399">This example uses the Azure portal and a logic app with a **Recurrence** trigger and an **Initialize variable** action.</span><span class="sxs-lookup"><span data-stu-id="1d15a-399">This example uses the Azure portal and a logic app with a **Recurrence** trigger and an **Initialize variable** action.</span></span> 
   <span data-ttu-id="1d15a-400">The action is set up for creating a variable whose initial value is an array that has some sample integers.</span><span class="sxs-lookup"><span data-stu-id="1d15a-400">The action is set up for creating a variable whose initial value is an array that has some sample integers.</span></span> 
   <span data-ttu-id="1d15a-401">When you later test your logic app, you can manually run your app without waiting for the trigger to fire.</span><span class="sxs-lookup"><span data-stu-id="1d15a-401">When you later test your logic app, you can manually run your app without waiting for the trigger to fire.</span></span>

   ![Starting sample logic app](./media/logic-apps-perform-data-operations/sample-starting-logic-app-select-action.png)

2. <span data-ttu-id="1d15a-403">In your logic app where you want to create the array, follow one of these steps:</span><span class="sxs-lookup"><span data-stu-id="1d15a-403">In your logic app where you want to create the array, follow one of these steps:</span></span> 

   * <span data-ttu-id="1d15a-404">To add an action under the last step, choose **New step** > **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-404">To add an action under the last step, choose **New step** > **Add an action**.</span></span>

     ![Add action](./media/logic-apps-perform-data-operations/add-select-action.png)

   * <span data-ttu-id="1d15a-406">To add an action between steps, move your mouse over the connecting arrow so the plus sign (+) appears.</span><span class="sxs-lookup"><span data-stu-id="1d15a-406">To add an action between steps, move your mouse over the connecting arrow so the plus sign (+) appears.</span></span> 
   <span data-ttu-id="1d15a-407">Choose the plus sign, and then select **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-407">Choose the plus sign, and then select **Add an action**.</span></span>

3. <span data-ttu-id="1d15a-408">In the search box, enter "select" as your filter.</span><span class="sxs-lookup"><span data-stu-id="1d15a-408">In the search box, enter "select" as your filter.</span></span> <span data-ttu-id="1d15a-409">From the actions list, select this action: **Select**</span><span class="sxs-lookup"><span data-stu-id="1d15a-409">From the actions list, select this action: **Select**</span></span>

   ![Select the "Select" action](./media/logic-apps-perform-data-operations/select-select-action.png)

4. <span data-ttu-id="1d15a-411">In the **From** box, specify the source array you want.</span><span class="sxs-lookup"><span data-stu-id="1d15a-411">In the **From** box, specify the source array you want.</span></span>

   <span data-ttu-id="1d15a-412">For this example, when you click inside the **From** box, the dynamic content list appears so you can select the previously created variable:</span><span class="sxs-lookup"><span data-stu-id="1d15a-412">For this example, when you click inside the **From** box, the dynamic content list appears so you can select the previously created variable:</span></span>

   ![Select source array for Select action](./media/logic-apps-perform-data-operations/configure-select-action.png)

5. <span data-ttu-id="1d15a-414">In the **Map** box's left-hand column, provide the property name you want to assign each value in the source array.</span><span class="sxs-lookup"><span data-stu-id="1d15a-414">In the **Map** box's left-hand column, provide the property name you want to assign each value in the source array.</span></span> <span data-ttu-id="1d15a-415">In the right-hand column, specify an expression that represents the value you want to assign the property.</span><span class="sxs-lookup"><span data-stu-id="1d15a-415">In the right-hand column, specify an expression that represents the value you want to assign the property.</span></span>

   <span data-ttu-id="1d15a-416">This example specifies "Product_ID" as the property name to assign each value in the integer array by using the **item()** function in an expression that accesses each array item.</span><span class="sxs-lookup"><span data-stu-id="1d15a-416">This example specifies "Product_ID" as the property name to assign each value in the integer array by using the **item()** function in an expression that accesses each array item.</span></span> 

   ![Specify the JSON object property and values for the array you want to create](./media/logic-apps-perform-data-operations/configure-select-action-2.png)

   <span data-ttu-id="1d15a-418">Here is the finished action:</span><span class="sxs-lookup"><span data-stu-id="1d15a-418">Here is the finished action:</span></span>

   ![Finished Select action](./media/logic-apps-perform-data-operations/finished-select-action.png)

6. <span data-ttu-id="1d15a-420">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="1d15a-420">Save your logic app.</span></span> <span data-ttu-id="1d15a-421">On the designer toolbar, choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-421">On the designer toolbar, choose **Save**.</span></span>

<span data-ttu-id="1d15a-422">For more information about this action in your underlying workflow definition, see [Select action](../logic-apps/logic-apps-workflow-actions-triggers.md).</span><span class="sxs-lookup"><span data-stu-id="1d15a-422">For more information about this action in your underlying workflow definition, see [Select action](../logic-apps/logic-apps-workflow-actions-triggers.md).</span></span>

### <a name="test-your-logic-app"></a><span data-ttu-id="1d15a-423">Test your logic app</span><span class="sxs-lookup"><span data-stu-id="1d15a-423">Test your logic app</span></span>

<span data-ttu-id="1d15a-424">To confirm whether the **Select** action creates the expected results, send yourself a notification that includes output from the **Select** action.</span><span class="sxs-lookup"><span data-stu-id="1d15a-424">To confirm whether the **Select** action creates the expected results, send yourself a notification that includes output from the **Select** action.</span></span>

1. <span data-ttu-id="1d15a-425">In your logic app, add an action that can send you the results from the **Select** action.</span><span class="sxs-lookup"><span data-stu-id="1d15a-425">In your logic app, add an action that can send you the results from the **Select** action.</span></span>

2. <span data-ttu-id="1d15a-426">In that action, click anywhere you want the results to appear.</span><span class="sxs-lookup"><span data-stu-id="1d15a-426">In that action, click anywhere you want the results to appear.</span></span> <span data-ttu-id="1d15a-427">When the dynamic content list opens, choose **Expression**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-427">When the dynamic content list opens, choose **Expression**.</span></span> <span data-ttu-id="1d15a-428">To get the array output from the **Select** action, enter this expression that includes the **Select** action's name:</span><span class="sxs-lookup"><span data-stu-id="1d15a-428">To get the array output from the **Select** action, enter this expression that includes the **Select** action's name:</span></span>

   ```
   @actionBody('Select')
   ```

   <span data-ttu-id="1d15a-429">This example uses the **Office 365 Outlook - Send an email** action and includes the outputs from the **actionBody('Select')** expression in the email's body:</span><span class="sxs-lookup"><span data-stu-id="1d15a-429">This example uses the **Office 365 Outlook - Send an email** action and includes the outputs from the **actionBody('Select')** expression in the email's body:</span></span>

   ![Action outputs in the "Send an email" action](./media/logic-apps-perform-data-operations/send-email-select-action.png)

3. <span data-ttu-id="1d15a-431">Now, manually run your logic app.</span><span class="sxs-lookup"><span data-stu-id="1d15a-431">Now, manually run your logic app.</span></span> <span data-ttu-id="1d15a-432">On the designer toolbar, choose **Run**.</span><span class="sxs-lookup"><span data-stu-id="1d15a-432">On the designer toolbar, choose **Run**.</span></span> 

   <span data-ttu-id="1d15a-433">Based on the email connector you used, here are the results you get:</span><span class="sxs-lookup"><span data-stu-id="1d15a-433">Based on the email connector you used, here are the results you get:</span></span>

   ![Email with "Select" action results](./media/logic-apps-perform-data-operations/select-email-results.png)

## <a name="get-support"></a><span data-ttu-id="1d15a-435">Get support</span><span class="sxs-lookup"><span data-stu-id="1d15a-435">Get support</span></span>

* <span data-ttu-id="1d15a-436">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="1d15a-436">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>
* <span data-ttu-id="1d15a-437">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="1d15a-437">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d15a-438">Next steps</span><span class="sxs-lookup"><span data-stu-id="1d15a-438">Next steps</span></span>

* <span data-ttu-id="1d15a-439">Learn about [Logic Apps connectors](../connectors/apis-list.md)</span><span class="sxs-lookup"><span data-stu-id="1d15a-439">Learn about [Logic Apps connectors](../connectors/apis-list.md)</span></span>
