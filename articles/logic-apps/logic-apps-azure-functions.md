---
title: Add and run custom code in Azure Logic Apps with Azure Functions | Microsoft Docs
description: Learn how to add and run custom code snippets in Azure Logic Apps with Azure Functions
services: logic-apps
ms.service: logic-apps
author: ecfan
ms.author: estfan
manager: jeconnoc
ms.topic: article
ms.date: 08/20/2018
ms.reviewer: klam, LADocs
ms.suite: integration
ms.openlocfilehash: a63bd8e3b071ed996db8ad5aeaeb5e451b4d92e9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44798218"
---
# <a name="add-and-run-custom-code-snippets-in-azure-logic-apps-with-azure-functions"></a><span data-ttu-id="33432-103">Add and run custom code snippets in Azure Logic Apps with Azure Functions</span><span class="sxs-lookup"><span data-stu-id="33432-103">Add and run custom code snippets in Azure Logic Apps with Azure Functions</span></span>

<span data-ttu-id="33432-104">When you want to run only enough code that performs a specific job in your logic apps, you can create your own functions with [Azure Functions](../azure-functions/functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="33432-104">When you want to run only enough code that performs a specific job in your logic apps, you can create your own functions with [Azure Functions](../azure-functions/functions-overview.md).</span></span> <span data-ttu-id="33432-105">This service helps you create Node.js, C#, and F# code snippets so you don't have to build a complete app or the infrastructure for running your code.</span><span class="sxs-lookup"><span data-stu-id="33432-105">This service helps you create Node.js, C#, and F# code snippets so you don't have to build a complete app or the infrastructure for running your code.</span></span> <span data-ttu-id="33432-106">Azure Functions provides serverless computing in the cloud and is useful for performing tasks such as these examples:</span><span class="sxs-lookup"><span data-stu-id="33432-106">Azure Functions provides serverless computing in the cloud and is useful for performing tasks such as these examples:</span></span>

* <span data-ttu-id="33432-107">Extend your logic app's behavior with functions in Node.js or C#.</span><span class="sxs-lookup"><span data-stu-id="33432-107">Extend your logic app's behavior with functions in Node.js or C#.</span></span>
* <span data-ttu-id="33432-108">Perform calculations in your logic app workflow.</span><span class="sxs-lookup"><span data-stu-id="33432-108">Perform calculations in your logic app workflow.</span></span>
* <span data-ttu-id="33432-109">Apply advanced formatting or compute fields in your logic apps.</span><span class="sxs-lookup"><span data-stu-id="33432-109">Apply advanced formatting or compute fields in your logic apps.</span></span>

<span data-ttu-id="33432-110">You can also [call logic apps from inside Azure functions](#call-logic-app).</span><span class="sxs-lookup"><span data-stu-id="33432-110">You can also [call logic apps from inside Azure functions](#call-logic-app).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33432-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="33432-111">Prerequisites</span></span>

<span data-ttu-id="33432-112">To follow this article, you need these items:</span><span class="sxs-lookup"><span data-stu-id="33432-112">To follow this article, you need these items:</span></span>

* <span data-ttu-id="33432-113">If you don't have an Azure subscription yet, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span><span class="sxs-lookup"><span data-stu-id="33432-113">If you don't have an Azure subscription yet, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span></span> 

* <span data-ttu-id="33432-114">An Azure function app, which is a container for Azure functions, and your Azure function.</span><span class="sxs-lookup"><span data-stu-id="33432-114">An Azure function app, which is a container for Azure functions, and your Azure function.</span></span> <span data-ttu-id="33432-115">If you don't have a function app, [create your function app first](../azure-functions/functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="33432-115">If you don't have a function app, [create your function app first](../azure-functions/functions-create-first-azure-function.md).</span></span> <span data-ttu-id="33432-116">You can then create your function either [separately outside your logic app](#create-function-external), or [from inside your logic app](#create-function-designer) in the Logic App Designer.</span><span class="sxs-lookup"><span data-stu-id="33432-116">You can then create your function either [separately outside your logic app](#create-function-external), or [from inside your logic app](#create-function-designer) in the Logic App Designer.</span></span>

  <span data-ttu-id="33432-117">Both existing and new function apps and functions have the same requirements for working with logic apps:</span><span class="sxs-lookup"><span data-stu-id="33432-117">Both existing and new function apps and functions have the same requirements for working with logic apps:</span></span>

  * <span data-ttu-id="33432-118">Your function app must have the same Azure subscription as your logic app.</span><span class="sxs-lookup"><span data-stu-id="33432-118">Your function app must have the same Azure subscription as your logic app.</span></span>

  * <span data-ttu-id="33432-119">Your function uses an HTTP trigger, for example, the **HTTP trigger** function template for **JavaScript** or **C#**.</span><span class="sxs-lookup"><span data-stu-id="33432-119">Your function uses an HTTP trigger, for example, the **HTTP trigger** function template for **JavaScript** or **C#**.</span></span> 

    <span data-ttu-id="33432-120">The HTTP trigger template can accept content that has `application/json` type from your logic app.</span><span class="sxs-lookup"><span data-stu-id="33432-120">The HTTP trigger template can accept content that has `application/json` type from your logic app.</span></span> 
    <span data-ttu-id="33432-121">When you add an Azure function to your logic app, the Logic App Designer shows custom functions created from this template within your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="33432-121">When you add an Azure function to your logic app, the Logic App Designer shows custom functions created from this template within your Azure subscription.</span></span> 

  * <span data-ttu-id="33432-122">Your function doesn't use custom routes unless you've defined an [OpenAPI definition](../azure-functions/functions-openapi-definition.md), formerly known as a [Swagger file](http://swagger.io/).</span><span class="sxs-lookup"><span data-stu-id="33432-122">Your function doesn't use custom routes unless you've defined an [OpenAPI definition](../azure-functions/functions-openapi-definition.md), formerly known as a [Swagger file](http://swagger.io/).</span></span> 
  
  * <span data-ttu-id="33432-123">If you've defined an OpenAPI definition for your function, the Logic Apps Designer gives you a richer experience for working with function parameters.</span><span class="sxs-lookup"><span data-stu-id="33432-123">If you've defined an OpenAPI definition for your function, the Logic Apps Designer gives you a richer experience for working with function parameters.</span></span> <span data-ttu-id="33432-124">Before your logic app can find and access functions that have OpenAPI definitions, [set up your function app by following these steps](#function-swagger).</span><span class="sxs-lookup"><span data-stu-id="33432-124">Before your logic app can find and access functions that have OpenAPI definitions, [set up your function app by following these steps](#function-swagger).</span></span>

* <span data-ttu-id="33432-125">The logic app where you want to add the function, including a [trigger](../logic-apps/logic-apps-overview.md#logic-app-concepts) as the first step in your logic app</span><span class="sxs-lookup"><span data-stu-id="33432-125">The logic app where you want to add the function, including a [trigger](../logic-apps/logic-apps-overview.md#logic-app-concepts) as the first step in your logic app</span></span> 

  <span data-ttu-id="33432-126">Before you can add actions that can run functions, your logic app must start with a trigger.</span><span class="sxs-lookup"><span data-stu-id="33432-126">Before you can add actions that can run functions, your logic app must start with a trigger.</span></span>

  <span data-ttu-id="33432-127">If you're new to logic apps, review [What is Azure Logic Apps](../logic-apps/logic-apps-overview.md) and [Quickstart: Create your first logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="33432-127">If you're new to logic apps, review [What is Azure Logic Apps](../logic-apps/logic-apps-overview.md) and [Quickstart: Create your first logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span></span>

<a name="create-function-external"></a>

## <a name="create-functions-outside-logic-apps"></a><span data-ttu-id="33432-128">Create functions outside logic apps</span><span class="sxs-lookup"><span data-stu-id="33432-128">Create functions outside logic apps</span></span>

<span data-ttu-id="33432-129">In the <a href="https://portal.azure.com" target="_blank">Azure portal</a>, create your Azure function app, which must have the same Azure subscription as your logic app, and then create your Azure function.</span><span class="sxs-lookup"><span data-stu-id="33432-129">In the <a href="https://portal.azure.com" target="_blank">Azure portal</a>, create your Azure function app, which must have the same Azure subscription as your logic app, and then create your Azure function.</span></span>
<span data-ttu-id="33432-130">If you're new to creating Azure functions, learn how to [create your first function in the Azure portal](../azure-functions/functions-create-first-azure-function.md), but note these requirements for creating functions that you can call from logic apps:</span><span class="sxs-lookup"><span data-stu-id="33432-130">If you're new to creating Azure functions, learn how to [create your first function in the Azure portal](../azure-functions/functions-create-first-azure-function.md), but note these requirements for creating functions that you can call from logic apps:</span></span>

* <span data-ttu-id="33432-131">Make sure you select the **HTTP trigger** function template for either **JavaScript** or **C#**.</span><span class="sxs-lookup"><span data-stu-id="33432-131">Make sure you select the **HTTP trigger** function template for either **JavaScript** or **C#**.</span></span>

  ![HTTP trigger - JavaScript or C#](./media/logic-apps-azure-functions/http-trigger-function.png)

<a name="function-swagger"></a>

* <span data-ttu-id="33432-133">Optionally, if you [generate an API definition](../azure-functions/functions-openapi-definition.md), formerly known as a [Swagger file](http://swagger.io/), for your function, you can get a richer experience when you work with function parameters in the Logic Apps Designer.</span><span class="sxs-lookup"><span data-stu-id="33432-133">Optionally, if you [generate an API definition](../azure-functions/functions-openapi-definition.md), formerly known as a [Swagger file](http://swagger.io/), for your function, you can get a richer experience when you work with function parameters in the Logic Apps Designer.</span></span> <span data-ttu-id="33432-134">To set up your function app so your logic app can find and use functions that have Swagger descriptions, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="33432-134">To set up your function app so your logic app can find and use functions that have Swagger descriptions, follow these steps:</span></span>

  1. <span data-ttu-id="33432-135">Make sure your function app is actively running.</span><span class="sxs-lookup"><span data-stu-id="33432-135">Make sure your function app is actively running.</span></span>

  2. <span data-ttu-id="33432-136">In your function app, set up [Cross-Origin Resource Sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing) so all origins are permitted by following these steps:</span><span class="sxs-lookup"><span data-stu-id="33432-136">In your function app, set up [Cross-Origin Resource Sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing) so all origins are permitted by following these steps:</span></span>

     1. <span data-ttu-id="33432-137">From the **Function Apps** list, select your function app > **Platform features** > **CORS**.</span><span class="sxs-lookup"><span data-stu-id="33432-137">From the **Function Apps** list, select your function app > **Platform features** > **CORS**.</span></span>

        ![Select your function app > "Platform features" > "CORS"](./media/logic-apps-azure-functions/function-platform-features-cors.png)

     2. <span data-ttu-id="33432-139">Under **CORS**, add the `*` wildcard character, but remove all the other origins in the list, and choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="33432-139">Under **CORS**, add the `*` wildcard character, but remove all the other origins in the list, and choose **Save**.</span></span>

        ![Set "CORS\* to the wildcard character "\*"](./media/logic-apps-azure-functions/function-platform-features-cors-origins.png)

### <a name="access-property-values-inside-http-requests"></a><span data-ttu-id="33432-141">Access property values inside HTTP requests</span><span class="sxs-lookup"><span data-stu-id="33432-141">Access property values inside HTTP requests</span></span>

<span data-ttu-id="33432-142">Webhook functions can accept HTTP requests as inputs and pass those requests to other functions.</span><span class="sxs-lookup"><span data-stu-id="33432-142">Webhook functions can accept HTTP requests as inputs and pass those requests to other functions.</span></span> <span data-ttu-id="33432-143">For example, although Logic Apps has [functions that convert DateTime values](../logic-apps/workflow-definition-language-functions-reference.md), this basic sample JavaScript function shows how you can access a property inside a request object that's passed to the function and perform operations on that property value.</span><span class="sxs-lookup"><span data-stu-id="33432-143">For example, although Logic Apps has [functions that convert DateTime values](../logic-apps/workflow-definition-language-functions-reference.md), this basic sample JavaScript function shows how you can access a property inside a request object that's passed to the function and perform operations on that property value.</span></span> <span data-ttu-id="33432-144">To access properties inside objects, this example uses the [dot (.) operator](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Operators/Property_accessors):</span><span class="sxs-lookup"><span data-stu-id="33432-144">To access properties inside objects, this example uses the [dot (.) operator](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Operators/Property_accessors):</span></span> 

```javascript
function convertToDateString(request, response){
   var data = request.body;
   response = {
      body: data.date.ToDateString();
   }
}
```

<span data-ttu-id="33432-145">Here's what happens inside this function:</span><span class="sxs-lookup"><span data-stu-id="33432-145">Here's what happens inside this function:</span></span>

1. <span data-ttu-id="33432-146">The function creates a `data` variable and assigns the `body` object inside the `request` object to that variable.</span><span class="sxs-lookup"><span data-stu-id="33432-146">The function creates a `data` variable and assigns the `body` object inside the `request` object to that variable.</span></span> <span data-ttu-id="33432-147">The function uses the dot (.) operator to reference the `body` object inside the `request` object:</span><span class="sxs-lookup"><span data-stu-id="33432-147">The function uses the dot (.) operator to reference the `body` object inside the `request` object:</span></span> 

   ```javascript
   var data = request.body;
   ```

2. <span data-ttu-id="33432-148">The function can now access the `date` property through the `data` variable, and convert that property value from DateTime type to DateString type by calling the `ToDateString()` function.</span><span class="sxs-lookup"><span data-stu-id="33432-148">The function can now access the `date` property through the `data` variable, and convert that property value from DateTime type to DateString type by calling the `ToDateString()` function.</span></span> <span data-ttu-id="33432-149">The function also returns the result through the `body` property in the function's response:</span><span class="sxs-lookup"><span data-stu-id="33432-149">The function also returns the result through the `body` property in the function's response:</span></span> 

   ```javascript
   body: data.date.ToDateString();
   ```

<span data-ttu-id="33432-150">Now that you've created your Azure function, follow the steps for how to [add functions to logic apps](#add-function-logic-app).</span><span class="sxs-lookup"><span data-stu-id="33432-150">Now that you've created your Azure function, follow the steps for how to [add functions to logic apps](#add-function-logic-app).</span></span>

<a name="create-function-designer"></a>

## <a name="create-functions-inside-logic-apps"></a><span data-ttu-id="33432-151">Create functions inside logic apps</span><span class="sxs-lookup"><span data-stu-id="33432-151">Create functions inside logic apps</span></span>

<span data-ttu-id="33432-152">Before you can create an Azure function starting from inside your logic app in the Logic App Designer, you must first have an Azure function app, which is a container for your functions.</span><span class="sxs-lookup"><span data-stu-id="33432-152">Before you can create an Azure function starting from inside your logic app in the Logic App Designer, you must first have an Azure function app, which is a container for your functions.</span></span> <span data-ttu-id="33432-153">If you don't have a function app, create that function app first.</span><span class="sxs-lookup"><span data-stu-id="33432-153">If you don't have a function app, create that function app first.</span></span> <span data-ttu-id="33432-154">See [Create your first function in the Azure portal](../azure-functions/functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="33432-154">See [Create your first function in the Azure portal](../azure-functions/functions-create-first-azure-function.md).</span></span> 

1. <span data-ttu-id="33432-155">In the <a href="https://portal.azure.com" target="_blank">Azure portal</a>, open your logic app in the Logic App Designer.</span><span class="sxs-lookup"><span data-stu-id="33432-155">In the <a href="https://portal.azure.com" target="_blank">Azure portal</a>, open your logic app in the Logic App Designer.</span></span> 

2. <span data-ttu-id="33432-156">To create and add your function, follow the step that applies to your scenario:</span><span class="sxs-lookup"><span data-stu-id="33432-156">To create and add your function, follow the step that applies to your scenario:</span></span>

   * <span data-ttu-id="33432-157">Under the last step in your logic app's workflow, choose **New step**.</span><span class="sxs-lookup"><span data-stu-id="33432-157">Under the last step in your logic app's workflow, choose **New step**.</span></span>

   * <span data-ttu-id="33432-158">Between existing steps in your logic app's workflow, move your mouse over the arrow, choose the plus (+) sign, and then select **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="33432-158">Between existing steps in your logic app's workflow, move your mouse over the arrow, choose the plus (+) sign, and then select **Add an action**.</span></span>

3. <span data-ttu-id="33432-159">In the search box, enter "azure functions" as your filter.</span><span class="sxs-lookup"><span data-stu-id="33432-159">In the search box, enter "azure functions" as your filter.</span></span>
<span data-ttu-id="33432-160">From the actions list, select this action: **Choose an Azure function - Azure Functions**</span><span class="sxs-lookup"><span data-stu-id="33432-160">From the actions list, select this action: **Choose an Azure function - Azure Functions**</span></span> 

   ![Find "Azure functions"](./media/logic-apps-azure-functions/find-azure-functions-action.png)

4. <span data-ttu-id="33432-162">From the function apps list, select your function app.</span><span class="sxs-lookup"><span data-stu-id="33432-162">From the function apps list, select your function app.</span></span> <span data-ttu-id="33432-163">After the actions list opens, select this action: **Azure Functions - Create New Function**</span><span class="sxs-lookup"><span data-stu-id="33432-163">After the actions list opens, select this action: **Azure Functions - Create New Function**</span></span>

   ![Select your function app](./media/logic-apps-azure-functions/select-function-app-create-function.png)

5. <span data-ttu-id="33432-165">In the function definition editor, define your function:</span><span class="sxs-lookup"><span data-stu-id="33432-165">In the function definition editor, define your function:</span></span>

   1. <span data-ttu-id="33432-166">In the **Function name** box, provide a name for your function.</span><span class="sxs-lookup"><span data-stu-id="33432-166">In the **Function name** box, provide a name for your function.</span></span> 

   2. <span data-ttu-id="33432-167">In the **Code** box, add your code to the function template, including the response and payload you want returned to your logic app after your function finishes running.</span><span class="sxs-lookup"><span data-stu-id="33432-167">In the **Code** box, add your code to the function template, including the response and payload you want returned to your logic app after your function finishes running.</span></span> 

      ![Define your function](./media/logic-apps-azure-functions/function-definition.png)

      <span data-ttu-id="33432-169">In the template's code, the *`context` object* refers to the message that your logic app sends through the **Request Body** field in a later step.</span><span class="sxs-lookup"><span data-stu-id="33432-169">In the template's code, the *`context` object* refers to the message that your logic app sends through the **Request Body** field in a later step.</span></span> 
      <span data-ttu-id="33432-170">To access the `context` object's properties from inside your function, use this syntax:</span><span class="sxs-lookup"><span data-stu-id="33432-170">To access the `context` object's properties from inside your function, use this syntax:</span></span> 

      `context.body.<property-name>`

      <span data-ttu-id="33432-171">For example, to reference the `content` property inside the `context` object, use this syntax:</span><span class="sxs-lookup"><span data-stu-id="33432-171">For example, to reference the `content` property inside the `context` object, use this syntax:</span></span> 

      `context.body.content`

      <span data-ttu-id="33432-172">The template code also includes an `input` variable, which stores the value from the `data` parameter so your function can perform operations on that value.</span><span class="sxs-lookup"><span data-stu-id="33432-172">The template code also includes an `input` variable, which stores the value from the `data` parameter so your function can perform operations on that value.</span></span> 
      <span data-ttu-id="33432-173">Inside JavaScript functions, the `data` variable is also a shortcut for `context.body`.</span><span class="sxs-lookup"><span data-stu-id="33432-173">Inside JavaScript functions, the `data` variable is also a shortcut for `context.body`.</span></span>

      > [!NOTE]
      > <span data-ttu-id="33432-174">The `body` property here applies to the `context` object and isn't the same as the **Body** token from an action's output, which you might also pass to your function.</span><span class="sxs-lookup"><span data-stu-id="33432-174">The `body` property here applies to the `context` object and isn't the same as the **Body** token from an action's output, which you might also pass to your function.</span></span> 
 
   3. <span data-ttu-id="33432-175">When you're done, choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="33432-175">When you're done, choose **Create**.</span></span>

6. <span data-ttu-id="33432-176">In the **Request Body** box, provide your function's input, which must be formatted as a JavaScript Object Notation (JSON) object.</span><span class="sxs-lookup"><span data-stu-id="33432-176">In the **Request Body** box, provide your function's input, which must be formatted as a JavaScript Object Notation (JSON) object.</span></span> 

   <span data-ttu-id="33432-177">This input is the *context object* or message that your logic app sends to your function.</span><span class="sxs-lookup"><span data-stu-id="33432-177">This input is the *context object* or message that your logic app sends to your function.</span></span> <span data-ttu-id="33432-178">When you click in the **Request Body** field, the dynamic content list appears so you can select tokens for outputs from previous steps.</span><span class="sxs-lookup"><span data-stu-id="33432-178">When you click in the **Request Body** field, the dynamic content list appears so you can select tokens for outputs from previous steps.</span></span> <span data-ttu-id="33432-179">This example specifies that the context payload contains a property named `content` that has the **From** token's value from the email trigger:</span><span class="sxs-lookup"><span data-stu-id="33432-179">This example specifies that the context payload contains a property named `content` that has the **From** token's value from the email trigger:</span></span>

   !["Request Body" example - context object payload](./media/logic-apps-azure-functions/function-request-body-example.png)

   <span data-ttu-id="33432-181">Here, the context object isn't cast as a string, so the object's content gets added directly to the JSON payload.</span><span class="sxs-lookup"><span data-stu-id="33432-181">Here, the context object isn't cast as a string, so the object's content gets added directly to the JSON payload.</span></span> <span data-ttu-id="33432-182">However, when the context object isn't a JSON token that passes a string, a JSON object, or a JSON array, you get an error.</span><span class="sxs-lookup"><span data-stu-id="33432-182">However, when the context object isn't a JSON token that passes a string, a JSON object, or a JSON array, you get an error.</span></span> <span data-ttu-id="33432-183">So, if this example used the **Received Time** token instead, you can cast the context object as a string by adding double-quotation marks:</span><span class="sxs-lookup"><span data-stu-id="33432-183">So, if this example used the **Received Time** token instead, you can cast the context object as a string by adding double-quotation marks:</span></span>  

   ![Cast object as string](./media/logic-apps-azure-functions/function-request-body-string-cast-example.png)

7. <span data-ttu-id="33432-185">To specify other details such as the method to use, request headers, or query parameters, choose **Show advanced options**.</span><span class="sxs-lookup"><span data-stu-id="33432-185">To specify other details such as the method to use, request headers, or query parameters, choose **Show advanced options**.</span></span>

<a name="add-function-logic-app"></a>

## <a name="add-existing-functions-to-logic-apps"></a><span data-ttu-id="33432-186">Add existing functions to logic apps</span><span class="sxs-lookup"><span data-stu-id="33432-186">Add existing functions to logic apps</span></span>

<span data-ttu-id="33432-187">To call existing Azure functions from your logic apps, you can add Azure functions like any other action in the Logic App Designer.</span><span class="sxs-lookup"><span data-stu-id="33432-187">To call existing Azure functions from your logic apps, you can add Azure functions like any other action in the Logic App Designer.</span></span> 

1. <span data-ttu-id="33432-188">In the <a href="https://portal.azure.com" target="_blank">Azure portal</a>, open your logic app in the Logic App Designer.</span><span class="sxs-lookup"><span data-stu-id="33432-188">In the <a href="https://portal.azure.com" target="_blank">Azure portal</a>, open your logic app in the Logic App Designer.</span></span> 

2. <span data-ttu-id="33432-189">Under the step where you want to add the function, choose **New step** > **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="33432-189">Under the step where you want to add the function, choose **New step** > **Add an action**.</span></span> 

3. <span data-ttu-id="33432-190">In the search box, enter "azure functions" as your filter.</span><span class="sxs-lookup"><span data-stu-id="33432-190">In the search box, enter "azure functions" as your filter.</span></span>
<span data-ttu-id="33432-191">From the actions list, select this action: **Choose an Azure function - Azure Functions**</span><span class="sxs-lookup"><span data-stu-id="33432-191">From the actions list, select this action: **Choose an Azure function - Azure Functions**</span></span> 

   ![Find "Azure functions"](./media/logic-apps-azure-functions/find-azure-functions-action.png)

4. <span data-ttu-id="33432-193">From the function apps list, select your function app.</span><span class="sxs-lookup"><span data-stu-id="33432-193">From the function apps list, select your function app.</span></span> <span data-ttu-id="33432-194">After the functions list appears, select your function.</span><span class="sxs-lookup"><span data-stu-id="33432-194">After the functions list appears, select your function.</span></span> 

   ![Select your function app and Azure function](./media/logic-apps-azure-functions/select-function-app-existing-function.png)

   <span data-ttu-id="33432-196">For functions that have API definitions (Swagger descriptions) and are [set up so your logic app can find and access those functions](#function-swagger), you can select **Swagger actions**:</span><span class="sxs-lookup"><span data-stu-id="33432-196">For functions that have API definitions (Swagger descriptions) and are [set up so your logic app can find and access those functions](#function-swagger), you can select **Swagger actions**:</span></span>

   ![Select your function app, "Swagger actions"", and your Azure function](./media/logic-apps-azure-functions/select-function-app-existing-function-swagger.png)

5. <span data-ttu-id="33432-198">In the **Request Body** box, provide your function's input, which must be formatted as a JavaScript Object Notation (JSON) object.</span><span class="sxs-lookup"><span data-stu-id="33432-198">In the **Request Body** box, provide your function's input, which must be formatted as a JavaScript Object Notation (JSON) object.</span></span> 

   <span data-ttu-id="33432-199">This input is the *context object* or message that your logic app sends to your function.</span><span class="sxs-lookup"><span data-stu-id="33432-199">This input is the *context object* or message that your logic app sends to your function.</span></span> <span data-ttu-id="33432-200">When you click in the **Request Body** field, the dynamic content list appears so you can select tokens for outputs from previous steps.</span><span class="sxs-lookup"><span data-stu-id="33432-200">When you click in the **Request Body** field, the dynamic content list appears so you can select tokens for outputs from previous steps.</span></span> <span data-ttu-id="33432-201">This example specifies that the context payload contains a property named `content` that has the **From** token's value from the email trigger:</span><span class="sxs-lookup"><span data-stu-id="33432-201">This example specifies that the context payload contains a property named `content` that has the **From** token's value from the email trigger:</span></span>

   !["Request Body" example - context object payload](./media/logic-apps-azure-functions/function-request-body-example.png)

   <span data-ttu-id="33432-203">Here, the context object isn't cast as a string, so the object's content gets added directly to the JSON payload.</span><span class="sxs-lookup"><span data-stu-id="33432-203">Here, the context object isn't cast as a string, so the object's content gets added directly to the JSON payload.</span></span> <span data-ttu-id="33432-204">However, when the context object isn't a JSON token that passes a string, a JSON object, or a JSON array, you get an error.</span><span class="sxs-lookup"><span data-stu-id="33432-204">However, when the context object isn't a JSON token that passes a string, a JSON object, or a JSON array, you get an error.</span></span> <span data-ttu-id="33432-205">So, if this example used the **Received Time** token instead, you can cast the context object as a string by adding double-quotation marks:</span><span class="sxs-lookup"><span data-stu-id="33432-205">So, if this example used the **Received Time** token instead, you can cast the context object as a string by adding double-quotation marks:</span></span> 

   ![Cast object as string](./media/logic-apps-azure-functions/function-request-body-string-cast-example.png)

6. <span data-ttu-id="33432-207">To specify other details such as the method to use, request headers, or query parameters, choose **Show advanced options**.</span><span class="sxs-lookup"><span data-stu-id="33432-207">To specify other details such as the method to use, request headers, or query parameters, choose **Show advanced options**.</span></span>

<a name="call-logic-app"></a>

## <a name="call-logic-apps-from-functions"></a><span data-ttu-id="33432-208">Call logic apps from functions</span><span class="sxs-lookup"><span data-stu-id="33432-208">Call logic apps from functions</span></span>

<span data-ttu-id="33432-209">When you want to trigger a logic app from inside an Azure function, the logic app must start with a trigger that provides a callable endpoint.</span><span class="sxs-lookup"><span data-stu-id="33432-209">When you want to trigger a logic app from inside an Azure function, the logic app must start with a trigger that provides a callable endpoint.</span></span> <span data-ttu-id="33432-210">For example, you can start the logic app with the **HTTP**, **Request**, **Azure Queues**, or **Event Grid** trigger.</span><span class="sxs-lookup"><span data-stu-id="33432-210">For example, you can start the logic app with the **HTTP**, **Request**, **Azure Queues**, or **Event Grid** trigger.</span></span> <span data-ttu-id="33432-211">Inside your function, send an HTTP POST request to the trigger's URL, and include the payload you want that logic app to process.</span><span class="sxs-lookup"><span data-stu-id="33432-211">Inside your function, send an HTTP POST request to the trigger's URL, and include the payload you want that logic app to process.</span></span> <span data-ttu-id="33432-212">For more information, see [Call, trigger, or nest logic apps](../logic-apps/logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="33432-212">For more information, see [Call, trigger, or nest logic apps](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

## <a name="get-support"></a><span data-ttu-id="33432-213">Get support</span><span class="sxs-lookup"><span data-stu-id="33432-213">Get support</span></span>

* <span data-ttu-id="33432-214">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="33432-214">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>
* <span data-ttu-id="33432-215">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="33432-215">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="33432-216">Next steps</span><span class="sxs-lookup"><span data-stu-id="33432-216">Next steps</span></span>

* <span data-ttu-id="33432-217">Learn about [Logic Apps connectors](../connectors/apis-list.md)</span><span class="sxs-lookup"><span data-stu-id="33432-217">Learn about [Logic Apps connectors](../connectors/apis-list.md)</span></span>
