---
title: Create a function that connects to Azure services | Microsoft Docs
description: Use Azure Functions to create a serverless application that connects to other Azure services.
services: functions
documentationcenter: dev-center-name
author: yochay
manager: manager-alias
editor: ''
tags: ''
keywords: azure functions, functions, event processing, webhooks, dynamic compute, serverless architecture
ms.assetid: ab86065d-6050-46c9-a336-1bfc1fa4b5a1
ms.service: functions
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/01/2017
ms.author: rachelap; glenga
ms.openlocfilehash: 6c8fd9a60425bdf12be8bd8d13cb5c0dcd505186
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564646"
---
# <a name="use-azure-functions-to-create-a-function-that-connects-to-other-azure-services"></a><span data-ttu-id="4e182-104">Use Azure Functions to create a function that connects to other Azure services</span><span class="sxs-lookup"><span data-stu-id="4e182-104">Use Azure Functions to create a function that connects to other Azure services</span></span>

<span data-ttu-id="4e182-105">This topic shows you how to create a function in Azure Functions that listens to messages on an Azure Storage queue and copies the messages to rows in an Azure Storage table.</span><span class="sxs-lookup"><span data-stu-id="4e182-105">This topic shows you how to create a function in Azure Functions that listens to messages on an Azure Storage queue and copies the messages to rows in an Azure Storage table.</span></span> <span data-ttu-id="4e182-106">A timer triggered function is used to load messages into the queue.</span><span class="sxs-lookup"><span data-stu-id="4e182-106">A timer triggered function is used to load messages into the queue.</span></span> <span data-ttu-id="4e182-107">A second function reads from the queue and writes messages to the table.</span><span class="sxs-lookup"><span data-stu-id="4e182-107">A second function reads from the queue and writes messages to the table.</span></span> <span data-ttu-id="4e182-108">Both the queue and the table are created for you by Azure Functions based on the binding definitions.</span><span class="sxs-lookup"><span data-stu-id="4e182-108">Both the queue and the table are created for you by Azure Functions based on the binding definitions.</span></span> 

<span data-ttu-id="4e182-109">To make things more interesting, one function is written in JavaScript and the other is written in C# script.</span><span class="sxs-lookup"><span data-stu-id="4e182-109">To make things more interesting, one function is written in JavaScript and the other is written in C# script.</span></span> <span data-ttu-id="4e182-110">This demonstrates how a function app can have functions in various languages.</span><span class="sxs-lookup"><span data-stu-id="4e182-110">This demonstrates how a function app can have functions in various languages.</span></span> 

<span data-ttu-id="4e182-111">You can see this scenario demonstrated in a [video on Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).</span><span class="sxs-lookup"><span data-stu-id="4e182-111">You can see this scenario demonstrated in a [video on Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).</span></span>

## <a name="create-a-function-that-writes-to-the-queue"></a><span data-ttu-id="4e182-112">Create a function that writes to the queue</span><span class="sxs-lookup"><span data-stu-id="4e182-112">Create a function that writes to the queue</span></span>

<span data-ttu-id="4e182-113">Before you can connect to a storage queue, you need to create a function that loads the message queue.</span><span class="sxs-lookup"><span data-stu-id="4e182-113">Before you can connect to a storage queue, you need to create a function that loads the message queue.</span></span> <span data-ttu-id="4e182-114">This JavaScript function uses a timer trigger that writes a message to the queue every 10 seconds.</span><span class="sxs-lookup"><span data-stu-id="4e182-114">This JavaScript function uses a timer trigger that writes a message to the queue every 10 seconds.</span></span> <span data-ttu-id="4e182-115">If you don't already have an Azure account, check out the [Try Azure Functions](https://functions.azure.com/try) experience, or [create your free Azure account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="4e182-115">If you don't already have an Azure account, check out the [Try Azure Functions](https://functions.azure.com/try) experience, or [create your free Azure account](https://azure.microsoft.com/free/).</span></span>

1. <span data-ttu-id="4e182-116">Go to the Azure portal and locate your function app.</span><span class="sxs-lookup"><span data-stu-id="4e182-116">Go to the Azure portal and locate your function app.</span></span>

2. <span data-ttu-id="4e182-117">Click **New Function** > **TimerTrigger-JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="4e182-117">Click **New Function** > **TimerTrigger-JavaScript**.</span></span> 

3. <span data-ttu-id="4e182-118">Name the function **FunctionsBindingsDemo1**, enter a cron expression value of `0/10 * * * * *` for **Schedule**, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="4e182-118">Name the function **FunctionsBindingsDemo1**, enter a cron expression value of `0/10 * * * * *` for **Schedule**, and then click **Create**.</span></span>
   
    ![Add a timer triggered function](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-create-an-azure-connected-function/new-trigger-timer-function.png)

    <span data-ttu-id="4e182-120">You have now created a timer triggered function that runs every 10 seconds.</span><span class="sxs-lookup"><span data-stu-id="4e182-120">You have now created a timer triggered function that runs every 10 seconds.</span></span>

5. <span data-ttu-id="4e182-121">On the **Develop** tab, click **Logs** and view the activity in the log.</span><span class="sxs-lookup"><span data-stu-id="4e182-121">On the **Develop** tab, click **Logs** and view the activity in the log.</span></span> <span data-ttu-id="4e182-122">You see a log entry written every 10 seconds.</span><span class="sxs-lookup"><span data-stu-id="4e182-122">You see a log entry written every 10 seconds.</span></span>
   
    ![View the log to verify the function works](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-create-an-azure-connected-function/functionsbindingsdemo1-view-log.png)

## <a name="add-a-message-queue-output-binding"></a><span data-ttu-id="4e182-124">Add a message queue output binding</span><span class="sxs-lookup"><span data-stu-id="4e182-124">Add a message queue output binding</span></span>

1. <span data-ttu-id="4e182-125">On the **Integrate** tab, choose **New Output** > **Azure Queue Storage** > **Select**.</span><span class="sxs-lookup"><span data-stu-id="4e182-125">On the **Integrate** tab, choose **New Output** > **Azure Queue Storage** > **Select**.</span></span>

    ![Add a trigger timer function](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab.png)

2. <span data-ttu-id="4e182-127">Enter `myQueueItem` for **Message parameter name** and `functions-bindings` for **Queue name**, select an existing **Storage account connection** or click **new** to create a storage account connection, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="4e182-127">Enter `myQueueItem` for **Message parameter name** and `functions-bindings` for **Queue name**, select an existing **Storage account connection** or click **new** to create a storage account connection, and then click **Save**.</span></span>  

    ![Create the output binding to the storage queue](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab2.png)

1. <span data-ttu-id="4e182-129">Back in the **Develop** tab, append the following code to the function:</span><span class="sxs-lookup"><span data-stu-id="4e182-129">Back in the **Develop** tab, append the following code to the function:</span></span>
   
    ```javascript
   
    function myQueueItem() 
    {
        return {
            msg: "some message goes here",
            time: "time goes here"
        }
    }
   
    ```
2. <span data-ttu-id="4e182-130">Locate the *if* statement around line 9 of the function, and insert the following code after that statement.</span><span class="sxs-lookup"><span data-stu-id="4e182-130">Locate the *if* statement around line 9 of the function, and insert the following code after that statement.</span></span>
   
    ```javascript
   
    var toBeQed = myQueueItem();
    toBeQed.time = timeStamp;
    context.bindings.myQueueItem = toBeQed;
   
    ```  
   
    <span data-ttu-id="4e182-131">This code creates a **myQueueItem** and sets its **time** property to the current timeStamp.</span><span class="sxs-lookup"><span data-stu-id="4e182-131">This code creates a **myQueueItem** and sets its **time** property to the current timeStamp.</span></span> <span data-ttu-id="4e182-132">It then adds the new queue item to the context's **myQueueItem** binding.</span><span class="sxs-lookup"><span data-stu-id="4e182-132">It then adds the new queue item to the context's **myQueueItem** binding.</span></span>

3. <span data-ttu-id="4e182-133">Click **Save and Run**.</span><span class="sxs-lookup"><span data-stu-id="4e182-133">Click **Save and Run**.</span></span>

## <a name="view-storage-updates-by-using-storage-explorer"></a><span data-ttu-id="4e182-134">View storage updates by using Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="4e182-134">View storage updates by using Storage Explorer</span></span>
<span data-ttu-id="4e182-135">You can verify that your function is working by viewing messages in the queue you created.</span><span class="sxs-lookup"><span data-stu-id="4e182-135">You can verify that your function is working by viewing messages in the queue you created.</span></span>  <span data-ttu-id="4e182-136">You can connect to your storage queue by using Cloud Explorer in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4e182-136">You can connect to your storage queue by using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="4e182-137">However, the portal makes it easy to connect to your storage account by using Microsoft Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="4e182-137">However, the portal makes it easy to connect to your storage account by using Microsoft Azure Storage Explorer.</span></span>

1. <span data-ttu-id="4e182-138">In the **Integrate** tab, click your queue output binding > **Documentation**, then unhide the Connection String for your storage account and copy the value.</span><span class="sxs-lookup"><span data-stu-id="4e182-138">In the **Integrate** tab, click your queue output binding > **Documentation**, then unhide the Connection String for your storage account and copy the value.</span></span> <span data-ttu-id="4e182-139">You use this value to connect to your storage account.</span><span class="sxs-lookup"><span data-stu-id="4e182-139">You use this value to connect to your storage account.</span></span>

    ![Download Azure Storage Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab3.png)


2. <span data-ttu-id="4e182-141">If you haven't already done so, download and install [Microsoft Azure Storage Explorer](http://storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="4e182-141">If you haven't already done so, download and install [Microsoft Azure Storage Explorer](http://storageexplorer.com).</span></span> 
 
3. <span data-ttu-id="4e182-142">In Storage Explorer, click the connect to Azure Storage icon, paste the connection string in the field, and complete the wizard.</span><span class="sxs-lookup"><span data-stu-id="4e182-142">In Storage Explorer, click the connect to Azure Storage icon, paste the connection string in the field, and complete the wizard.</span></span>

    ![Storage Explorer add a connection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-create-an-azure-connected-function/functionsbindingsdemo1-storage-explorer.png)

4. <span data-ttu-id="4e182-144">Under **Local and attached**, expand **Storage Accounts** > your storage account > **Queues** > **functions-bindings** and verify that messages are written to the queue.</span><span class="sxs-lookup"><span data-stu-id="4e182-144">Under **Local and attached**, expand **Storage Accounts** > your storage account > **Queues** > **functions-bindings** and verify that messages are written to the queue.</span></span>

    ![View of messages in the queue](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer.png)

    <span data-ttu-id="4e182-146">If the queue does not exist or is empty, there is most likely a problem with your function binding or code.</span><span class="sxs-lookup"><span data-stu-id="4e182-146">If the queue does not exist or is empty, there is most likely a problem with your function binding or code.</span></span>

## <a name="create-a-function-that-reads-from-the-queue"></a><span data-ttu-id="4e182-147">Create a function that reads from the queue</span><span class="sxs-lookup"><span data-stu-id="4e182-147">Create a function that reads from the queue</span></span>

<span data-ttu-id="4e182-148">Now that you have messages being added to the queue, you can create another function that reads from the queue and writes the messages permanently to an Azure Storage table.</span><span class="sxs-lookup"><span data-stu-id="4e182-148">Now that you have messages being added to the queue, you can create another function that reads from the queue and writes the messages permanently to an Azure Storage table.</span></span>

1. <span data-ttu-id="4e182-149">Click **New Function** > **QueueTrigger-CSharp**.</span><span class="sxs-lookup"><span data-stu-id="4e182-149">Click **New Function** > **QueueTrigger-CSharp**.</span></span> 
 
2. <span data-ttu-id="4e182-150">Name the function `FunctionsBindingsDemo2`, enter **functions-bindings** in the **Queue name** field, select an existing storage account or create one, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="4e182-150">Name the function `FunctionsBindingsDemo2`, enter **functions-bindings** in the **Queue name** field, select an existing storage account or create one, and then click **Create**.</span></span>

    ![Add an output queue timer function](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-create-an-azure-connected-function/function-demo2-new-function.png) 

3. <span data-ttu-id="4e182-152">(Optional) You can verify that the new function works by viewing the new queue in Storage Explorer as before.</span><span class="sxs-lookup"><span data-stu-id="4e182-152">(Optional) You can verify that the new function works by viewing the new queue in Storage Explorer as before.</span></span> <span data-ttu-id="4e182-153">You can also use Cloud Explorer in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4e182-153">You can also use Cloud Explorer in Visual Studio.</span></span>  

4. <span data-ttu-id="4e182-154">(Optional) Refresh the **functions-bindings** queue and notice that items have been removed from the queue.</span><span class="sxs-lookup"><span data-stu-id="4e182-154">(Optional) Refresh the **functions-bindings** queue and notice that items have been removed from the queue.</span></span> <span data-ttu-id="4e182-155">The removal occurs because the function is bound to the **functions-bindings** queue as an input trigger and the function reads the queue.</span><span class="sxs-lookup"><span data-stu-id="4e182-155">The removal occurs because the function is bound to the **functions-bindings** queue as an input trigger and the function reads the queue.</span></span> 
 
## <a name="add-a-table-output-binding"></a><span data-ttu-id="4e182-156">Add a table output binding</span><span class="sxs-lookup"><span data-stu-id="4e182-156">Add a table output binding</span></span>

1. <span data-ttu-id="4e182-157">In FunctionsBindingsDemo2, click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span><span class="sxs-lookup"><span data-stu-id="4e182-157">In FunctionsBindingsDemo2, click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

    ![Add a binding to an Azure Storage table](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab.png) 

2. <span data-ttu-id="4e182-159">Enter `functionbindings` for **Table name** and `myTable` for **Table parameter name**, choose a **Storage account connection** or create a new one, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="4e182-159">Enter `functionbindings` for **Table name** and `myTable` for **Table parameter name**, choose a **Storage account connection** or create a new one, and then click **Save**.</span></span>

    ![Configure the Storage table binding](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab2.png)
   
3. <span data-ttu-id="4e182-161">In the **Develop** tab, replace the existing function code with the following:</span><span class="sxs-lookup"><span data-stu-id="4e182-161">In the **Develop** tab, replace the existing function code with the following:</span></span>
   
    ```cs
    
    using System;
    
    public static void Run(QItem myQueueItem, ICollector<TableItem> myTable, TraceWriter log)
    {    
        TableItem myItem = new TableItem
        {
            PartitionKey = "key",
            RowKey = Guid.NewGuid().ToString(),
            Time = DateTime.Now.ToString("hh.mm.ss.ffffff"),
            Msg = myQueueItem.Msg,
            OriginalTime = myQueueItem.Time    
        };
        
        // Add the item to the table binding collection.
        myTable.Add(myItem);
    
        log.Verbose($"C# Queue trigger function processed: {myItem.RowKey} | {myItem.Msg} | {myItem.Time}");
    }
    
    public class TableItem
    {
        public string PartitionKey {get; set;}
        public string RowKey {get; set;}
        public string Time {get; set;}
        public string Msg {get; set;}
        public string OriginalTime {get; set;}
    }
    
    public class QItem
    {
        public string Msg { get; set;}
        public string Time { get; set;}
    }
    ```
    <span data-ttu-id="4e182-162">The **TableItem** class represents a row in the storage table, and you add the item to the `myTable` collection of **TableItem** objects.</span><span class="sxs-lookup"><span data-stu-id="4e182-162">The **TableItem** class represents a row in the storage table, and you add the item to the `myTable` collection of **TableItem** objects.</span></span> <span data-ttu-id="4e182-163">You must set the **PartitionKey** and **RowKey** properties to be able to insert into the table.</span><span class="sxs-lookup"><span data-stu-id="4e182-163">You must set the **PartitionKey** and **RowKey** properties to be able to insert into the table.</span></span>

4. <span data-ttu-id="4e182-164">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="4e182-164">Click **Save**.</span></span>  <span data-ttu-id="4e182-165">Finally, you can verify the function works by viewing the table in Storage explorer or Visual Studio Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="4e182-165">Finally, you can verify the function works by viewing the table in Storage explorer or Visual Studio Cloud Explorer.</span></span>

5. <span data-ttu-id="4e182-166">(Optional) In your storage account in Storage Explorer, expand **Tables** > **functionsbindings** and verify that rows are added to the table.</span><span class="sxs-lookup"><span data-stu-id="4e182-166">(Optional) In your storage account in Storage Explorer, expand **Tables** > **functionsbindings** and verify that rows are added to the table.</span></span> <span data-ttu-id="4e182-167">You can do the same in Cloud Explorer in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4e182-167">You can do the same in Cloud Explorer in Visual Studio.</span></span>

    ![View of rows in the table](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer2.png)

    <span data-ttu-id="4e182-169">If the table does not exist or is empty, there is most likely a problem with your function binding or code.</span><span class="sxs-lookup"><span data-stu-id="4e182-169">If the table does not exist or is empty, there is most likely a problem with your function binding or code.</span></span> 
 
[!INCLUDE [More binding information](../../includes/functions-bindings-next-steps.md)]

## <a name="next-steps"></a><span data-ttu-id="4e182-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="4e182-170">Next steps</span></span>
<span data-ttu-id="4e182-171">For more information about Azure Functions, see the following topics:</span><span class="sxs-lookup"><span data-stu-id="4e182-171">For more information about Azure Functions, see the following topics:</span></span>

* [<span data-ttu-id="4e182-172">Azure Functions developer reference</span><span class="sxs-lookup"><span data-stu-id="4e182-172">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="4e182-173">Programmer reference for coding functions and defining triggers and bindings.</span><span class="sxs-lookup"><span data-stu-id="4e182-173">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="4e182-174">Testing Azure Functions</span><span class="sxs-lookup"><span data-stu-id="4e182-174">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="4e182-175">Describes various tools and techniques for testing your functions.</span><span class="sxs-lookup"><span data-stu-id="4e182-175">Describes various tools and techniques for testing your functions.</span></span>
* [<span data-ttu-id="4e182-176">How to scale Azure Functions</span><span class="sxs-lookup"><span data-stu-id="4e182-176">How to scale Azure Functions</span></span>](functions-scale.md)  
  <span data-ttu-id="4e182-177">Discusses service plans available with Azure Functions, including the Consumption hosting plan, and how to choose the right plan.</span><span class="sxs-lookup"><span data-stu-id="4e182-177">Discusses service plans available with Azure Functions, including the Consumption hosting plan, and how to choose the right plan.</span></span> 

[!INCLUDE [Getting help note](../../includes/functions-get-help.md)]












