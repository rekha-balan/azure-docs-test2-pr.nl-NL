---
title: Add messages to an Azure Storage queue using Functions | Microsoft Docs
description: Use Azure Functions to create a serverless function that is invoked by an HTTP request and creates a message in an Azure Storage queue.
services: azure-functions
documentationcenter: na
author: ggailey777
manager: jeconnoc
ms.assetid: 0b609bc0-c264-4092-8e3e-0784dcc23b5d
ms.service: azure-functions
ms.devlang: multiple
ms.topic: quickstart
ms.date: 09/19/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 84783472adda9a4a74670f0579790aac69feb23d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870151"
---
# <a name="add-messages-to-an-azure-storage-queue-using-functions"></a><span data-ttu-id="f919b-103">Add messages to an Azure Storage queue using Functions</span><span class="sxs-lookup"><span data-stu-id="f919b-103">Add messages to an Azure Storage queue using Functions</span></span>

<span data-ttu-id="f919b-104">In Azure Functions, input and output bindings provide a declarative way to make data from external services available to your code.</span><span class="sxs-lookup"><span data-stu-id="f919b-104">In Azure Functions, input and output bindings provide a declarative way to make data from external services available to your code.</span></span> <span data-ttu-id="f919b-105">In this quickstart, you use an output binding to create a message in a queue when a function is triggered by an HTTP request.</span><span class="sxs-lookup"><span data-stu-id="f919b-105">In this quickstart, you use an output binding to create a message in a queue when a function is triggered by an HTTP request.</span></span> <span data-ttu-id="f919b-106">You use Azure Storage Explorer to view the queue messages that your function creates:</span><span class="sxs-lookup"><span data-stu-id="f919b-106">You use Azure Storage Explorer to view the queue messages that your function creates:</span></span>

![Queue message shown in Storage Explorer](./media/functions-integrate-storage-queue-output-binding/function-queue-storage-output-view-queue.png)

## <a name="prerequisites"></a><span data-ttu-id="f919b-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f919b-108">Prerequisites</span></span> 

<span data-ttu-id="f919b-109">To complete this quickstart:</span><span class="sxs-lookup"><span data-stu-id="f919b-109">To complete this quickstart:</span></span>

* <span data-ttu-id="f919b-110">Follow the directions in [Create your first function from the Azure portal](functions-create-first-azure-function.md) and don't do the **Clean up resources** step.</span><span class="sxs-lookup"><span data-stu-id="f919b-110">Follow the directions in [Create your first function from the Azure portal](functions-create-first-azure-function.md) and don't do the **Clean up resources** step.</span></span> <span data-ttu-id="f919b-111">That quickstart creates the function app and function that you use here.</span><span class="sxs-lookup"><span data-stu-id="f919b-111">That quickstart creates the function app and function that you use here.</span></span>

* <span data-ttu-id="f919b-112">Install [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="f919b-112">Install [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span> <span data-ttu-id="f919b-113">This is a tool you'll use to examine queue messages that your output binding creates.</span><span class="sxs-lookup"><span data-stu-id="f919b-113">This is a tool you'll use to examine queue messages that your output binding creates.</span></span>

## <a name="add-binding"></a><span data-ttu-id="f919b-114">Add an output binding</span><span class="sxs-lookup"><span data-stu-id="f919b-114">Add an output binding</span></span>

<span data-ttu-id="f919b-115">In this section, you use the portal UI to add a queue storage output binding to the function you created earlier.</span><span class="sxs-lookup"><span data-stu-id="f919b-115">In this section, you use the portal UI to add a queue storage output binding to the function you created earlier.</span></span> <span data-ttu-id="f919b-116">This binding will make it possible to write minimal code to create a message in a queue.</span><span class="sxs-lookup"><span data-stu-id="f919b-116">This binding will make it possible to write minimal code to create a message in a queue.</span></span> <span data-ttu-id="f919b-117">You don't have to write code for tasks such as opening a storage connection, creating a queue, or getting a reference to a queue.</span><span class="sxs-lookup"><span data-stu-id="f919b-117">You don't have to write code for tasks such as opening a storage connection, creating a queue, or getting a reference to a queue.</span></span> <span data-ttu-id="f919b-118">The Azure Functions runtime and queue output binding take care of those tasks for you.</span><span class="sxs-lookup"><span data-stu-id="f919b-118">The Azure Functions runtime and queue output binding take care of those tasks for you.</span></span>

1. <span data-ttu-id="f919b-119">In the Azure portal, open the function app page for the function app that you created in [Create your first function from the Azure portal](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="f919b-119">In the Azure portal, open the function app page for the function app that you created in [Create your first function from the Azure portal](functions-create-first-azure-function.md).</span></span> <span data-ttu-id="f919b-120">To do this, select **All services > Function Apps**, and then select your function app.</span><span class="sxs-lookup"><span data-stu-id="f919b-120">To do this, select **All services > Function Apps**, and then select your function app.</span></span>

2. <span data-ttu-id="f919b-121">Select the function that you created in that earlier quickstart.</span><span class="sxs-lookup"><span data-stu-id="f919b-121">Select the function that you created in that earlier quickstart.</span></span>

1. <span data-ttu-id="f919b-122">Select **Integrate > New output > Azure Queue storage**.</span><span class="sxs-lookup"><span data-stu-id="f919b-122">Select **Integrate > New output > Azure Queue storage**.</span></span>

1. <span data-ttu-id="f919b-123">Click **Select**.</span><span class="sxs-lookup"><span data-stu-id="f919b-123">Click **Select**.</span></span>
    
    ![Add a Queue storage output binding to a function in the Azure portal.](./media/functions-integrate-storage-queue-output-binding/function-add-queue-storage-output-binding.png)

3. <span data-ttu-id="f919b-125">Under **Azure Queue Storage output**, use the settings as specified in the table that follows this screenshot:</span><span class="sxs-lookup"><span data-stu-id="f919b-125">Under **Azure Queue Storage output**, use the settings as specified in the table that follows this screenshot:</span></span> 

    ![Add a Queue storage output binding to a function in the Azure portal.](./media/functions-integrate-storage-queue-output-binding/function-add-queue-storage-output-binding-2.png)

    | <span data-ttu-id="f919b-127">Setting</span><span class="sxs-lookup"><span data-stu-id="f919b-127">Setting</span></span>      |  <span data-ttu-id="f919b-128">Suggested value</span><span class="sxs-lookup"><span data-stu-id="f919b-128">Suggested value</span></span>   | <span data-ttu-id="f919b-129">Description</span><span class="sxs-lookup"><span data-stu-id="f919b-129">Description</span></span>                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | <span data-ttu-id="f919b-130">**Message parameter name**</span><span class="sxs-lookup"><span data-stu-id="f919b-130">**Message parameter name**</span></span> | <span data-ttu-id="f919b-131">outputQueueItem</span><span class="sxs-lookup"><span data-stu-id="f919b-131">outputQueueItem</span></span> | <span data-ttu-id="f919b-132">The name of the output binding parameter.</span><span class="sxs-lookup"><span data-stu-id="f919b-132">The name of the output binding parameter.</span></span> | 
    | <span data-ttu-id="f919b-133">**Storage account connection**</span><span class="sxs-lookup"><span data-stu-id="f919b-133">**Storage account connection**</span></span> | <span data-ttu-id="f919b-134">AzureWebJobsStorage</span><span class="sxs-lookup"><span data-stu-id="f919b-134">AzureWebJobsStorage</span></span> | <span data-ttu-id="f919b-135">You can use the storage account connection already being used by your function app, or create a new one.</span><span class="sxs-lookup"><span data-stu-id="f919b-135">You can use the storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="f919b-136">**Queue name**</span><span class="sxs-lookup"><span data-stu-id="f919b-136">**Queue name**</span></span>   | <span data-ttu-id="f919b-137">outqueue</span><span class="sxs-lookup"><span data-stu-id="f919b-137">outqueue</span></span>    | <span data-ttu-id="f919b-138">The name of the queue to connect to in your Storage account.</span><span class="sxs-lookup"><span data-stu-id="f919b-138">The name of the queue to connect to in your Storage account.</span></span> |

4. <span data-ttu-id="f919b-139">Click **Save** to add the binding.</span><span class="sxs-lookup"><span data-stu-id="f919b-139">Click **Save** to add the binding.</span></span>
 
<span data-ttu-id="f919b-140">Now that you have an output binding defined, you need to update the code to use the binding to add messages to a queue.</span><span class="sxs-lookup"><span data-stu-id="f919b-140">Now that you have an output binding defined, you need to update the code to use the binding to add messages to a queue.</span></span>  

## <a name="add-code-that-uses-the-output-binding"></a><span data-ttu-id="f919b-141">Add code that uses the output binding</span><span class="sxs-lookup"><span data-stu-id="f919b-141">Add code that uses the output binding</span></span>

<span data-ttu-id="f919b-142">In this section, you add code that writes a message to the output queue.</span><span class="sxs-lookup"><span data-stu-id="f919b-142">In this section, you add code that writes a message to the output queue.</span></span> <span data-ttu-id="f919b-143">The message includes the value that is passed to the HTTP trigger in the query string.</span><span class="sxs-lookup"><span data-stu-id="f919b-143">The message includes the value that is passed to the HTTP trigger in the query string.</span></span> <span data-ttu-id="f919b-144">For example, if the query string includes `name=Azure`, the queue message will be *Name passed to the function: Azure*.</span><span class="sxs-lookup"><span data-stu-id="f919b-144">For example, if the query string includes `name=Azure`, the queue message will be *Name passed to the function: Azure*.</span></span>

1. <span data-ttu-id="f919b-145">Select your function to display the function code in the editor.</span><span class="sxs-lookup"><span data-stu-id="f919b-145">Select your function to display the function code in the editor.</span></span> 

2. <span data-ttu-id="f919b-146">For a C# function, add a method parameter for the binding and write code to use it:</span><span class="sxs-lookup"><span data-stu-id="f919b-146">For a C# function, add a method parameter for the binding and write code to use it:</span></span>

   <span data-ttu-id="f919b-147">Add an **outputQueueItem** parameter to the method signature as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="f919b-147">Add an **outputQueueItem** parameter to the method signature as shown in the following example.</span></span> <span data-ttu-id="f919b-148">The parameter name is the same as what you entered for **Message parameter name** when you created the binding.</span><span class="sxs-lookup"><span data-stu-id="f919b-148">The parameter name is the same as what you entered for **Message parameter name** when you created the binding.</span></span>

   ```cs   
   public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, 
       ICollector<string> outputQueueItem, TraceWriter log)
   {
       ...
   }
   ```

   <span data-ttu-id="f919b-149">In the body of the C# function just before the `return` statement, add code that uses the parameter to create a queue message.</span><span class="sxs-lookup"><span data-stu-id="f919b-149">In the body of the C# function just before the `return` statement, add code that uses the parameter to create a queue message.</span></span>

   ```cs
   outputQueueItem.Add("Name passed to the function: " + name);     
   ```

3. <span data-ttu-id="f919b-150">For a JavaScript function, add code that uses the output binding on the `context.bindings` object to create a queue message.</span><span class="sxs-lookup"><span data-stu-id="f919b-150">For a JavaScript function, add code that uses the output binding on the `context.bindings` object to create a queue message.</span></span> <span data-ttu-id="f919b-151">Add this code before the`context.done` statement.</span><span class="sxs-lookup"><span data-stu-id="f919b-151">Add this code before the`context.done` statement.</span></span>

   ```javascript
   context.bindings.outputQueueItem = "Name passed to the function: " + 
               (req.query.name || req.body.name);
   ```

4. <span data-ttu-id="f919b-152">Select **Save** to save changes.</span><span class="sxs-lookup"><span data-stu-id="f919b-152">Select **Save** to save changes.</span></span>
 
## <a name="test-the-function"></a><span data-ttu-id="f919b-153">Test the function</span><span class="sxs-lookup"><span data-stu-id="f919b-153">Test the function</span></span> 

1. <span data-ttu-id="f919b-154">After the code changes are saved, select **Run**.</span><span class="sxs-lookup"><span data-stu-id="f919b-154">After the code changes are saved, select **Run**.</span></span> 

    ![Add a Queue storage output binding to a function in the Azure portal.](./media/functions-integrate-storage-queue-output-binding/functions-test-run-function.png)

   <span data-ttu-id="f919b-156">Notice that the **Request body** contains the `name` value *Azure*.</span><span class="sxs-lookup"><span data-stu-id="f919b-156">Notice that the **Request body** contains the `name` value *Azure*.</span></span> <span data-ttu-id="f919b-157">This value appears in the queue message that is created when the function is invoked.</span><span class="sxs-lookup"><span data-stu-id="f919b-157">This value appears in the queue message that is created when the function is invoked.</span></span>

   <span data-ttu-id="f919b-158">As an alternative to selecting **Run** here, you can call the function by entering a URL in a browser and specifying the `name` value in the query string.</span><span class="sxs-lookup"><span data-stu-id="f919b-158">As an alternative to selecting **Run** here, you can call the function by entering a URL in a browser and specifying the `name` value in the query string.</span></span> <span data-ttu-id="f919b-159">The browser method is shown in the [previous quickstart](functions-create-first-azure-function.md#test-the-function).</span><span class="sxs-lookup"><span data-stu-id="f919b-159">The browser method is shown in the [previous quickstart](functions-create-first-azure-function.md#test-the-function).</span></span>

2. <span data-ttu-id="f919b-160">Check the logs to make sure that the function succeeded.</span><span class="sxs-lookup"><span data-stu-id="f919b-160">Check the logs to make sure that the function succeeded.</span></span> 

<span data-ttu-id="f919b-161">A new queue named **outqueue** is created in your Storage account by the Functions runtime when the output binding is first used.</span><span class="sxs-lookup"><span data-stu-id="f919b-161">A new queue named **outqueue** is created in your Storage account by the Functions runtime when the output binding is first used.</span></span> <span data-ttu-id="f919b-162">You'll use Storage Explorer to verify that the queue and a message in it were created.</span><span class="sxs-lookup"><span data-stu-id="f919b-162">You'll use Storage Explorer to verify that the queue and a message in it were created.</span></span>

### <a name="connect-storage-explorer-to-your-account"></a><span data-ttu-id="f919b-163">Connect Storage Explorer to your account</span><span class="sxs-lookup"><span data-stu-id="f919b-163">Connect Storage Explorer to your account</span></span>

<span data-ttu-id="f919b-164">Skip this section if you have already installed Storage Explorer and connected it to the storage account that you're using with this quickstart.</span><span class="sxs-lookup"><span data-stu-id="f919b-164">Skip this section if you have already installed Storage Explorer and connected it to the storage account that you're using with this quickstart.</span></span>

2. <span data-ttu-id="f919b-165">Run the [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, select the connect icon on the left, choose **Use a storage account name and key**, and select **Next**.</span><span class="sxs-lookup"><span data-stu-id="f919b-165">Run the [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, select the connect icon on the left, choose **Use a storage account name and key**, and select **Next**.</span></span>

    ![Run the Storage Account Explorer tool.](./media/functions-integrate-storage-queue-output-binding/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="f919b-167">In the Azure portal, on the function app page, select your function and then select **Integrate**.</span><span class="sxs-lookup"><span data-stu-id="f919b-167">In the Azure portal, on the function app page, select your function and then select **Integrate**.</span></span>

1. <span data-ttu-id="f919b-168">Select the **Azure Queue storage** output binding that you added in an earlier step.</span><span class="sxs-lookup"><span data-stu-id="f919b-168">Select the **Azure Queue storage** output binding that you added in an earlier step.</span></span>

1. <span data-ttu-id="f919b-169">Expand the **Documentation** section at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="f919b-169">Expand the **Documentation** section at the bottom of the page.</span></span> 

   <span data-ttu-id="f919b-170">The portal shows credentials that you can use in Storage Explorer to connect to the storage account.</span><span class="sxs-lookup"><span data-stu-id="f919b-170">The portal shows credentials that you can use in Storage Explorer to connect to the storage account.</span></span>

   ![Get the Storage account connection credentials.](./media/functions-integrate-storage-queue-output-binding/function-get-storage-account-credentials.png)

1. <span data-ttu-id="f919b-172">Copy the **Account Name** value from the portal and paste it in the **Account name** box in Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="f919b-172">Copy the **Account Name** value from the portal and paste it in the **Account name** box in Storage Explorer.</span></span>
 
1. <span data-ttu-id="f919b-173">Click the show/hide icon next to **Account Key** to display the value, and then copy the **Account Key** value and paste it in the **Account key** box in Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="f919b-173">Click the show/hide icon next to **Account Key** to display the value, and then copy the **Account Key** value and paste it in the **Account key** box in Storage Explorer.</span></span>
  
3. <span data-ttu-id="f919b-174">Select **Next > Connect**.</span><span class="sxs-lookup"><span data-stu-id="f919b-174">Select **Next > Connect**.</span></span>

   ![Paste the storage credentials and connect.](./media/functions-integrate-storage-queue-output-binding/functions-storage-manager-connect-2.png)

### <a name="examine-the-output-queue"></a><span data-ttu-id="f919b-176">Examine the output queue</span><span class="sxs-lookup"><span data-stu-id="f919b-176">Examine the output queue</span></span>

4. <span data-ttu-id="f919b-177">In Storage Explorer, select the storage account that you're using for this quickstart.</span><span class="sxs-lookup"><span data-stu-id="f919b-177">In Storage Explorer, select the storage account that you're using for this quickstart.</span></span>

1. <span data-ttu-id="f919b-178">Expand the **Queues** node, and then select the queue named **outqueue**.</span><span class="sxs-lookup"><span data-stu-id="f919b-178">Expand the **Queues** node, and then select the queue named **outqueue**.</span></span> 

   <span data-ttu-id="f919b-179">The queue contains the message that the queue output binding created when you ran the HTTP-triggered function.</span><span class="sxs-lookup"><span data-stu-id="f919b-179">The queue contains the message that the queue output binding created when you ran the HTTP-triggered function.</span></span> <span data-ttu-id="f919b-180">If you invoked the function with the default `name` value of *Azure*, the queue message is *Name passed to the function: Azure*.</span><span class="sxs-lookup"><span data-stu-id="f919b-180">If you invoked the function with the default `name` value of *Azure*, the queue message is *Name passed to the function: Azure*.</span></span>

    ![Queue message shown in Storage Explorer](./media/functions-integrate-storage-queue-output-binding/function-queue-storage-output-view-queue.png)

2. <span data-ttu-id="f919b-182">Run the function again, and you'll see a new message appear in the queue.</span><span class="sxs-lookup"><span data-stu-id="f919b-182">Run the function again, and you'll see a new message appear in the queue.</span></span>  

## <a name="clean-up-resources"></a><span data-ttu-id="f919b-183">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="f919b-183">Clean up resources</span></span>

[!INCLUDE [Clean up resources](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="f919b-184">Next steps</span><span class="sxs-lookup"><span data-stu-id="f919b-184">Next steps</span></span>

<span data-ttu-id="f919b-185">In this quickstart, you added an output binding to an existing function.</span><span class="sxs-lookup"><span data-stu-id="f919b-185">In this quickstart, you added an output binding to an existing function.</span></span> <span data-ttu-id="f919b-186">For more information about binding to Queue storage, see [Azure Functions Storage queue bindings](functions-bindings-storage-queue.md).</span><span class="sxs-lookup"><span data-stu-id="f919b-186">For more information about binding to Queue storage, see [Azure Functions Storage queue bindings](functions-bindings-storage-queue.md).</span></span> 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]
