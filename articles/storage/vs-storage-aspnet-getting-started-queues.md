---
title: Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET) | Microsoft Docs
description: How to get started using Azure queue storage in an ASP.NET project in Visual Studio after connecting to a storage account using Visual Studio Connected Services
services: storage
documentationcenter: ''
author: TomArcher
manager: douge
editor: ''
ms.assetid: 94ca3413-5497-433f-abbe-836f83a9de72
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/23/2016
ms.author: tarcher
ms.openlocfilehash: dd8bcd5a33db843375b4e277b43c7189e05190fc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556340"
---
# <a name="get-started-with-azure-queue-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="8aee6-103">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="8aee6-103">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="8aee6-104">Overview</span><span class="sxs-lookup"><span data-stu-id="8aee6-104">Overview</span></span>

<span data-ttu-id="8aee6-105">Azure queue storage provides cloud messaging between application components.</span><span class="sxs-lookup"><span data-stu-id="8aee6-105">Azure queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="8aee6-106">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span><span class="sxs-lookup"><span data-stu-id="8aee6-106">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="8aee6-107">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in the cloud, on the desktop, on an on-premises server, or on a mobile device.</span><span class="sxs-lookup"><span data-stu-id="8aee6-107">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in the cloud, on the desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="8aee6-108">Queue storage also supports managing asynchronous tasks and building process work flows.</span><span class="sxs-lookup"><span data-stu-id="8aee6-108">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

<span data-ttu-id="8aee6-109">This tutorial shows how to write ASP.NET code for some common scenarios using Azure queue storage entities.</span><span class="sxs-lookup"><span data-stu-id="8aee6-109">This tutorial shows how to write ASP.NET code for some common scenarios using Azure queue storage entities.</span></span> <span data-ttu-id="8aee6-110">These scenarios include common tasks such as creating an Azure queue, and adding, modifying, reading, and removing queue messages.</span><span class="sxs-lookup"><span data-stu-id="8aee6-110">These scenarios include common tasks such as creating an Azure queue, and adding, modifying, reading, and removing queue messages.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="8aee6-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8aee6-111">Prerequisites</span></span>

* [<span data-ttu-id="8aee6-112">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8aee6-112">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/visual-studio-homepage-vs.aspx)
* [<span data-ttu-id="8aee6-113">Azure storage account</span><span class="sxs-lookup"><span data-stu-id="8aee6-113">Azure storage account</span></span>](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="8aee6-114">Create an MVC controller</span><span class="sxs-lookup"><span data-stu-id="8aee6-114">Create an MVC controller</span></span> 

1. <span data-ttu-id="8aee6-115">In the **Solution Explorer**, right-click **Controllers**, and, from the context menu, select **Add->Controller**.</span><span class="sxs-lookup"><span data-stu-id="8aee6-115">In the **Solution Explorer**, right-click **Controllers**, and, from the context menu, select **Add->Controller**.</span></span>

    ![Add a controller to an ASP.NET MVC app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/vs-storage-aspnet-getting-started-queues/add-controller-menu.png)

1. <span data-ttu-id="8aee6-117">On the **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span><span class="sxs-lookup"><span data-stu-id="8aee6-117">On the **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Specify MVC controller type](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/vs-storage-aspnet-getting-started-queues/add-controller.png)

1. <span data-ttu-id="8aee6-119">On the **Add Controller** dialog, name the controller *QueuesController*, and select **Add**.</span><span class="sxs-lookup"><span data-stu-id="8aee6-119">On the **Add Controller** dialog, name the controller *QueuesController*, and select **Add**.</span></span>

    ![Name the MVC controller](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/vs-storage-aspnet-getting-started-queues/add-controller-name.png)

1. <span data-ttu-id="8aee6-121">Add the following *using* directives to the `QueuesController.cs` file:</span><span class="sxs-lookup"><span data-stu-id="8aee6-121">Add the following *using* directives to the `QueuesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Queue;
    ```
## <a name="create-a-queue"></a><span data-ttu-id="8aee6-122">Create a queue</span><span class="sxs-lookup"><span data-stu-id="8aee6-122">Create a queue</span></span>

<span data-ttu-id="8aee6-123">The following steps illustrate how to create a queue:</span><span class="sxs-lookup"><span data-stu-id="8aee6-123">The following steps illustrate how to create a queue:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="8aee6-124">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="8aee6-124">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="8aee6-125">Open the `QueuesController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="8aee6-125">Open the `QueuesController.cs` file.</span></span> 

1. <span data-ttu-id="8aee6-126">Add a method called **CreateQueue** that returns an **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="8aee6-126">Add a method called **CreateQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateQueue()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="8aee6-127">Within the **CreateQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span><span class="sxs-lookup"><span data-stu-id="8aee6-127">Within the **CreateQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="8aee6-128">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span><span class="sxs-lookup"><span data-stu-id="8aee6-128">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="8aee6-129">Get a **CloudQueueClient** object represents a queue service client.</span><span class="sxs-lookup"><span data-stu-id="8aee6-129">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```
1. <span data-ttu-id="8aee6-130">Get a **CloudQueue** object that represents a reference to the desired queue name.</span><span class="sxs-lookup"><span data-stu-id="8aee6-130">Get a **CloudQueue** object that represents a reference to the desired queue name.</span></span> <span data-ttu-id="8aee6-131">The **CloudQueueClient.GetQueueReference** method does not make a request against queue storage.</span><span class="sxs-lookup"><span data-stu-id="8aee6-131">The **CloudQueueClient.GetQueueReference** method does not make a request against queue storage.</span></span> <span data-ttu-id="8aee6-132">The reference is returned whether or not the queue exists.</span><span class="sxs-lookup"><span data-stu-id="8aee6-132">The reference is returned whether or not the queue exists.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="8aee6-133">Call the **CloudQueue.CreateIfNotExists** method to create the queue if it does not yet exist.</span><span class="sxs-lookup"><span data-stu-id="8aee6-133">Call the **CloudQueue.CreateIfNotExists** method to create the queue if it does not yet exist.</span></span> <span data-ttu-id="8aee6-134">The **CloudQueue.CreateIfNotExists** method returns **true** if the queue does not exist, and is successfully created.</span><span class="sxs-lookup"><span data-stu-id="8aee6-134">The **CloudQueue.CreateIfNotExists** method returns **true** if the queue does not exist, and is successfully created.</span></span> <span data-ttu-id="8aee6-135">Otherwise, **false** is returned.</span><span class="sxs-lookup"><span data-stu-id="8aee6-135">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = queue.CreateIfNotExists();
    ```

1. <span data-ttu-id="8aee6-136">Update the **ViewBag** with the name of the queue.</span><span class="sxs-lookup"><span data-stu-id="8aee6-136">Update the **ViewBag** with the name of the queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```

1. <span data-ttu-id="8aee6-137">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span><span class="sxs-lookup"><span data-stu-id="8aee6-137">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="8aee6-138">On the **Add View** dialog, enter **CreateQueue** for the view name, and select **Add**.</span><span class="sxs-lookup"><span data-stu-id="8aee6-138">On the **Add View** dialog, enter **CreateQueue** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="8aee6-139">Open `CreateQueue.cshtml`, and modify it so that it looks like the following code snippet:</span><span class="sxs-lookup"><span data-stu-id="8aee6-139">Open `CreateQueue.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Queue";
    }
    
    <h2>Create Queue results</h2>

    Creation of @ViewBag.QueueName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="8aee6-140">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="8aee6-140">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="8aee6-141">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="8aee6-141">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create queue", "CreateQueue", "Queues")</li>
    ```

1. <span data-ttu-id="8aee6-142">Run the application, and select **Create queue** to see results similar to the following screen shot:</span><span class="sxs-lookup"><span data-stu-id="8aee6-142">Run the application, and select **Create queue** to see results similar to the following screen shot:</span></span>
  
    ![Create queue](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/vs-storage-aspnet-getting-started-queues/create-queue-results.png)

    <span data-ttu-id="8aee6-144">As mentioned previously, the **CloudQueue.CreateIfNotExists** method returns **true** only when the queue doesn't exist and is created.</span><span class="sxs-lookup"><span data-stu-id="8aee6-144">As mentioned previously, the **CloudQueue.CreateIfNotExists** method returns **true** only when the queue doesn't exist and is created.</span></span> <span data-ttu-id="8aee6-145">Therefore, if you run the app when the queue exists, the method returns **false**.</span><span class="sxs-lookup"><span data-stu-id="8aee6-145">Therefore, if you run the app when the queue exists, the method returns **false**.</span></span> <span data-ttu-id="8aee6-146">To run the app multiple times, you must delete the queue before running the app again.</span><span class="sxs-lookup"><span data-stu-id="8aee6-146">To run the app multiple times, you must delete the queue before running the app again.</span></span> <span data-ttu-id="8aee6-147">Deleting the queue can be done via the **CloudQueue.Delete** method.</span><span class="sxs-lookup"><span data-stu-id="8aee6-147">Deleting the queue can be done via the **CloudQueue.Delete** method.</span></span> <span data-ttu-id="8aee6-148">You can also delete the queue using the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="8aee6-148">You can also delete the queue using the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="8aee6-149">Add a message to a queue</span><span class="sxs-lookup"><span data-stu-id="8aee6-149">Add a message to a queue</span></span>

<span data-ttu-id="8aee6-150">Once you've [created a queue](#create-a-queue), you can add messages to that queue.</span><span class="sxs-lookup"><span data-stu-id="8aee6-150">Once you've [created a queue](#create-a-queue), you can add messages to that queue.</span></span> <span data-ttu-id="8aee6-151">This section walks you through adding a message to a queue *test-queue*.</span><span class="sxs-lookup"><span data-stu-id="8aee6-151">This section walks you through adding a message to a queue *test-queue*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="8aee6-152">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="8aee6-152">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="8aee6-153">Open the `QueuesController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="8aee6-153">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="8aee6-154">Add a method called **AddMessage** that returns an **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="8aee6-154">Add a method called **AddMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddMessage()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="8aee6-155">Within the **AddMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span><span class="sxs-lookup"><span data-stu-id="8aee6-155">Within the **AddMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="8aee6-156">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span><span class="sxs-lookup"><span data-stu-id="8aee6-156">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="8aee6-157">Get a **CloudQueueClient** object represents a queue service client.</span><span class="sxs-lookup"><span data-stu-id="8aee6-157">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="8aee6-158">Get a **CloudQueueContainer** object that represents a reference to the queue.</span><span class="sxs-lookup"><span data-stu-id="8aee6-158">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="8aee6-159">Create the **CloudQueueMessage** object representing the message you want to add to the queue.</span><span class="sxs-lookup"><span data-stu-id="8aee6-159">Create the **CloudQueueMessage** object representing the message you want to add to the queue.</span></span> <span data-ttu-id="8aee6-160">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span><span class="sxs-lookup"><span data-stu-id="8aee6-160">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

    ```csharp
    CloudQueueMessage message = new CloudQueueMessage("Hello, Azure Queue Storage");
    ```

1. <span data-ttu-id="8aee6-161">Call the **CloudQueue.AddMessage** method to add the messaged to the queue.</span><span class="sxs-lookup"><span data-stu-id="8aee6-161">Call the **CloudQueue.AddMessage** method to add the messaged to the queue.</span></span>

    ```csharp
    queue.AddMessage(message);
    ```

1. <span data-ttu-id="8aee6-162">Create and set a couple of **ViewBag** properties for display in the view.</span><span class="sxs-lookup"><span data-stu-id="8aee6-162">Create and set a couple of **ViewBag** properties for display in the view.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```

1. <span data-ttu-id="8aee6-163">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span><span class="sxs-lookup"><span data-stu-id="8aee6-163">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="8aee6-164">On the **Add View** dialog, enter **AddMessage** for the view name, and select **Add**.</span><span class="sxs-lookup"><span data-stu-id="8aee6-164">On the **Add View** dialog, enter **AddMessage** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="8aee6-165">Open `AddMessage.cshtml`, and modify it so that it looks like the following code snippet:</span><span class="sxs-lookup"><span data-stu-id="8aee6-165">Open `AddMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add Message";
    }
    
    <h2>Add Message results</h2>
    
    The message '@ViewBag.Message' was added to the queue '@ViewBag.QueueName'.
    ```

1. <span data-ttu-id="8aee6-166">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="8aee6-166">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="8aee6-167">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="8aee6-167">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add message", "AddMessage", "Queues")</li>
    ```

1. <span data-ttu-id="8aee6-168">Run the application, and select **Add message** to see results similar to the following screen shot:</span><span class="sxs-lookup"><span data-stu-id="8aee6-168">Run the application, and select **Add message** to see results similar to the following screen shot:</span></span>
  
    ![Add  message](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/vs-storage-aspnet-getting-started-queues/add-message-results.png)

<span data-ttu-id="8aee6-170">The two sections - [Read a message from a queue without removing it](#read-a-message-from-a-queue-without-removing-it) and [Read and remove a message from a queue](#read-and-remove-a-message-from-a-queue) - illustrate how to read messages from a queue.</span><span class="sxs-lookup"><span data-stu-id="8aee6-170">The two sections - [Read a message from a queue without removing it](#read-a-message-from-a-queue-without-removing-it) and [Read and remove a message from a queue](#read-and-remove-a-message-from-a-queue) - illustrate how to read messages from a queue.</span></span>    

## <a name="read-a-message-from-a-queue-without-removing-it"></a><span data-ttu-id="8aee6-171">Read a message from a queue without removing it</span><span class="sxs-lookup"><span data-stu-id="8aee6-171">Read a message from a queue without removing it</span></span>

<span data-ttu-id="8aee6-172">This section illustrates how to peek at a queued message (read the first message without removing it).</span><span class="sxs-lookup"><span data-stu-id="8aee6-172">This section illustrates how to peek at a queued message (read the first message without removing it).</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="8aee6-173">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="8aee6-173">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="8aee6-174">Open the `QueuesController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="8aee6-174">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="8aee6-175">Add a method called **PeekMessage** that returns an **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="8aee6-175">Add a method called **PeekMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult PeekMessage()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="8aee6-176">Within the **PeekMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span><span class="sxs-lookup"><span data-stu-id="8aee6-176">Within the **PeekMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="8aee6-177">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span><span class="sxs-lookup"><span data-stu-id="8aee6-177">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="8aee6-178">Get a **CloudQueueClient** object represents a queue service client.</span><span class="sxs-lookup"><span data-stu-id="8aee6-178">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="8aee6-179">Get a **CloudQueueContainer** object that represents a reference to the queue.</span><span class="sxs-lookup"><span data-stu-id="8aee6-179">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="8aee6-180">Call the **CloudQueue.PeekMessage** method to read the first message in the queue without removing it from the queue.</span><span class="sxs-lookup"><span data-stu-id="8aee6-180">Call the **CloudQueue.PeekMessage** method to read the first message in the queue without removing it from the queue.</span></span> 

    ```csharp
    CloudQueueMessage message = queue.PeekMessage();
    ```

1. <span data-ttu-id="8aee6-181">Update the **ViewBag** with two values: the queue name and the message that was read.</span><span class="sxs-lookup"><span data-stu-id="8aee6-181">Update the **ViewBag** with two values: the queue name and the message that was read.</span></span> <span data-ttu-id="8aee6-182">The **CloudQueueMessage** object exposes two properties for getting the object's value: **CloudQueueMessage.AsBytes** and **CloudQueueMessage.AsString**.</span><span class="sxs-lookup"><span data-stu-id="8aee6-182">The **CloudQueueMessage** object exposes two properties for getting the object's value: **CloudQueueMessage.AsBytes** and **CloudQueueMessage.AsString**.</span></span> <span data-ttu-id="8aee6-183">**AsString** (used in this example) returns a string, while **AsBytes** returns a byte array.</span><span class="sxs-lookup"><span data-stu-id="8aee6-183">**AsString** (used in this example) returns a string, while **AsBytes** returns a byte array.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name; 
    ViewBag.Message = (message != null ? message.AsString : "");
    ```

1. <span data-ttu-id="8aee6-184">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span><span class="sxs-lookup"><span data-stu-id="8aee6-184">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="8aee6-185">On the **Add View** dialog, enter **PeekMessage** for the view name, and select **Add**.</span><span class="sxs-lookup"><span data-stu-id="8aee6-185">On the **Add View** dialog, enter **PeekMessage** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="8aee6-186">Open `PeekMessage.cshtml`, and modify it so that it looks like the following code snippet:</span><span class="sxs-lookup"><span data-stu-id="8aee6-186">Open `PeekMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "PeekMessage";
    }
    
    <h2>Peek Message results</h2>
    
    <table border="1">
        <tr><th>Queue</th><th>Peeked Message</th></tr>
        <tr><td>@ViewBag.QueueName</td><td>@ViewBag.Message</td></tr>
    </table>    
    ```

1. <span data-ttu-id="8aee6-187">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="8aee6-187">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="8aee6-188">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="8aee6-188">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Peek message", "PeekMessage", "Queues")</li>
    ```

1. <span data-ttu-id="8aee6-189">Run the application, and select **Peek message** to see results similar to the following screen shot:</span><span class="sxs-lookup"><span data-stu-id="8aee6-189">Run the application, and select **Peek message** to see results similar to the following screen shot:</span></span>
  
    ![Peek message](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/vs-storage-aspnet-getting-started-queues/peek-message-results.png)

## <a name="read-and-remove-a-message-from-a-queue"></a><span data-ttu-id="8aee6-191">Read and remove a message from a queue</span><span class="sxs-lookup"><span data-stu-id="8aee6-191">Read and remove a message from a queue</span></span>

<span data-ttu-id="8aee6-192">In this section, you learn how to read and remove a message from a queue.</span><span class="sxs-lookup"><span data-stu-id="8aee6-192">In this section, you learn how to read and remove a message from a queue.</span></span>   

> [!NOTE]
> 
> <span data-ttu-id="8aee6-193">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="8aee6-193">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="8aee6-194">Open the `QueuesController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="8aee6-194">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="8aee6-195">Add a method called **ReadMessage** that returns an **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="8aee6-195">Add a method called **ReadMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ReadMessage()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="8aee6-196">Within the **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span><span class="sxs-lookup"><span data-stu-id="8aee6-196">Within the **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="8aee6-197">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span><span class="sxs-lookup"><span data-stu-id="8aee6-197">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="8aee6-198">Get a **CloudQueueClient** object represents a queue service client.</span><span class="sxs-lookup"><span data-stu-id="8aee6-198">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="8aee6-199">Get a **CloudQueueContainer** object that represents a reference to the queue.</span><span class="sxs-lookup"><span data-stu-id="8aee6-199">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="8aee6-200">Call the **CloudQueue.GetMessage** method to read the first message in the queue.</span><span class="sxs-lookup"><span data-stu-id="8aee6-200">Call the **CloudQueue.GetMessage** method to read the first message in the queue.</span></span> <span data-ttu-id="8aee6-201">The **CloudQueue.GetMessage** method makes the message invisible for 30 seconds (by default) to any other code reading messages so that no other code can modify or delete the message while your processing it.</span><span class="sxs-lookup"><span data-stu-id="8aee6-201">The **CloudQueue.GetMessage** method makes the message invisible for 30 seconds (by default) to any other code reading messages so that no other code can modify or delete the message while your processing it.</span></span> <span data-ttu-id="8aee6-202">To change the amount of time the message is invisible, modify the **visibilityTimeout** parameter being passed to the **CloudQueue.GetMessage** method.</span><span class="sxs-lookup"><span data-stu-id="8aee6-202">To change the amount of time the message is invisible, modify the **visibilityTimeout** parameter being passed to the **CloudQueue.GetMessage** method.</span></span>

    ```csharp
    // This message will be invisible to other code for 30 seconds.
    CloudQueueMessage message = queue.GetMessage();     
    ```

1. <span data-ttu-id="8aee6-203">Call the **CloudQueueMessage.Delete** method to delete the message from the queue.</span><span class="sxs-lookup"><span data-stu-id="8aee6-203">Call the **CloudQueueMessage.Delete** method to delete the message from the queue.</span></span>

    ```csharp
    queue.DeleteMessage(message);
    ```

1. <span data-ttu-id="8aee6-204">Update the **ViewBag** with the message deleted, and the name of the queue.</span><span class="sxs-lookup"><span data-stu-id="8aee6-204">Update the **ViewBag** with the message deleted, and the name of the queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```
 
1. <span data-ttu-id="8aee6-205">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span><span class="sxs-lookup"><span data-stu-id="8aee6-205">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="8aee6-206">On the **Add View** dialog, enter **ReadMessage** for the view name, and select **Add**.</span><span class="sxs-lookup"><span data-stu-id="8aee6-206">On the **Add View** dialog, enter **ReadMessage** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="8aee6-207">Open `ReadMessage.cshtml`, and modify it so that it looks like the following code snippet:</span><span class="sxs-lookup"><span data-stu-id="8aee6-207">Open `ReadMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "ReadMessage";
    }
    
    <h2>Read Message results</h2>
    
    <table border="1">
        <tr><th>Queue</th><th>Read (and Deleted) Message</th></tr>
        <tr><td>@ViewBag.QueueName</td><td>@ViewBag.Message</td></tr>
    </table>
    ```

1. <span data-ttu-id="8aee6-208">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="8aee6-208">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="8aee6-209">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="8aee6-209">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Read/Delete message", "ReadMessage", "Queues")</li>
    ```

1. <span data-ttu-id="8aee6-210">Run the application, and select **Read/Delete message** to see results similar to the following screen shot:</span><span class="sxs-lookup"><span data-stu-id="8aee6-210">Run the application, and select **Read/Delete message** to see results similar to the following screen shot:</span></span>
  
    ![Read and delete message](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/vs-storage-aspnet-getting-started-queues/read-message-results.png)

## <a name="get-the-queue-length"></a><span data-ttu-id="8aee6-212">Get the queue length</span><span class="sxs-lookup"><span data-stu-id="8aee6-212">Get the queue length</span></span>

<span data-ttu-id="8aee6-213">This section illustrates how to get the queue length (number of messages).</span><span class="sxs-lookup"><span data-stu-id="8aee6-213">This section illustrates how to get the queue length (number of messages).</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="8aee6-214">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="8aee6-214">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="8aee6-215">Open the `QueuesController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="8aee6-215">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="8aee6-216">Add a method called **GetQueueLength** that returns an **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="8aee6-216">Add a method called **GetQueueLength** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetQueueLength()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="8aee6-217">Within the **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span><span class="sxs-lookup"><span data-stu-id="8aee6-217">Within the **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="8aee6-218">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span><span class="sxs-lookup"><span data-stu-id="8aee6-218">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="8aee6-219">Get a **CloudQueueClient** object represents a queue service client.</span><span class="sxs-lookup"><span data-stu-id="8aee6-219">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="8aee6-220">Get a **CloudQueueContainer** object that represents a reference to the queue.</span><span class="sxs-lookup"><span data-stu-id="8aee6-220">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="8aee6-221">Call the **CloudQueue.FetchAttributes** method to retrieve the queue's attributes (including its length).</span><span class="sxs-lookup"><span data-stu-id="8aee6-221">Call the **CloudQueue.FetchAttributes** method to retrieve the queue's attributes (including its length).</span></span> 

    ```csharp
    queue.FetchAttributes();
    ```

6. <span data-ttu-id="8aee6-222">Access the **CloudQueue.ApproximateMessageCount** property to get the queue's length.</span><span class="sxs-lookup"><span data-stu-id="8aee6-222">Access the **CloudQueue.ApproximateMessageCount** property to get the queue's length.</span></span>
 
    ```csharp
    int? nMessages = queue.ApproximateMessageCount;
    ```

1. <span data-ttu-id="8aee6-223">Update the **ViewBag** with the name of the queue, and its length.</span><span class="sxs-lookup"><span data-stu-id="8aee6-223">Update the **ViewBag** with the name of the queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Length = nMessages;
    ```
 
1. <span data-ttu-id="8aee6-224">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span><span class="sxs-lookup"><span data-stu-id="8aee6-224">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="8aee6-225">On the **Add View** dialog, enter **GetQueueLength** for the view name, and select **Add**.</span><span class="sxs-lookup"><span data-stu-id="8aee6-225">On the **Add View** dialog, enter **GetQueueLength** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="8aee6-226">Open `GetQueueLengthMessage.cshtml`, and modify it so that it looks like the following code snippet:</span><span class="sxs-lookup"><span data-stu-id="8aee6-226">Open `GetQueueLengthMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "GetQueueLength";
    }
    
    <h2>Get Queue Length results</h2>
    
    The queue '@ViewBag.QueueName' has a length of (number of messages): @ViewBag.Length
    ```

1. <span data-ttu-id="8aee6-227">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="8aee6-227">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="8aee6-228">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="8aee6-228">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get queue length", "GetQueueLength", "Queues")</li>
    ```

1. <span data-ttu-id="8aee6-229">Run the application, and select **Get queue length** to see results similar to the following screen shot:</span><span class="sxs-lookup"><span data-stu-id="8aee6-229">Run the application, and select **Get queue length** to see results similar to the following screen shot:</span></span>
  
    ![Get queue length](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/vs-storage-aspnet-getting-started-queues/get-queue-length-results.png)


## <a name="delete-a-queue"></a><span data-ttu-id="8aee6-231">Delete a queue</span><span class="sxs-lookup"><span data-stu-id="8aee6-231">Delete a queue</span></span>
<span data-ttu-id="8aee6-232">This section illustrates how to delete a queue.</span><span class="sxs-lookup"><span data-stu-id="8aee6-232">This section illustrates how to delete a queue.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="8aee6-233">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="8aee6-233">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="8aee6-234">Open the `QueuesController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="8aee6-234">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="8aee6-235">Add a method called **DeleteQueue** that returns an **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="8aee6-235">Add a method called **DeleteQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteQueue()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="8aee6-236">Within the **DeleteQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span><span class="sxs-lookup"><span data-stu-id="8aee6-236">Within the **DeleteQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="8aee6-237">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span><span class="sxs-lookup"><span data-stu-id="8aee6-237">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="8aee6-238">Get a **CloudQueueClient** object represents a queue service client.</span><span class="sxs-lookup"><span data-stu-id="8aee6-238">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="8aee6-239">Get a **CloudQueueContainer** object that represents a reference to the queue.</span><span class="sxs-lookup"><span data-stu-id="8aee6-239">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="8aee6-240">Call the **CloudQueue.Delete** method to delete the queue represented by the **CloudQueue** object.</span><span class="sxs-lookup"><span data-stu-id="8aee6-240">Call the **CloudQueue.Delete** method to delete the queue represented by the **CloudQueue** object.</span></span>

    ```csharp
    queue.Delete();
    ```

1. <span data-ttu-id="8aee6-241">Update the **ViewBag** with the name of the queue, and its length.</span><span class="sxs-lookup"><span data-stu-id="8aee6-241">Update the **ViewBag** with the name of the queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```
 
1. <span data-ttu-id="8aee6-242">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span><span class="sxs-lookup"><span data-stu-id="8aee6-242">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="8aee6-243">On the **Add View** dialog, enter **DeleteQueue** for the view name, and select **Add**.</span><span class="sxs-lookup"><span data-stu-id="8aee6-243">On the **Add View** dialog, enter **DeleteQueue** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="8aee6-244">Open `DeleteQueue.cshtml`, and modify it so that it looks like the following code snippet:</span><span class="sxs-lookup"><span data-stu-id="8aee6-244">Open `DeleteQueue.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "DeleteQueue";
    }
    
    <h2>Delete Queue results</h2>
    
    @ViewBag.QueueName deleted.
    ```

1. <span data-ttu-id="8aee6-245">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="8aee6-245">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="8aee6-246">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="8aee6-246">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete queue", "DeleteQueue", "Queues")</li>
    ```

1. <span data-ttu-id="8aee6-247">Run the application, and select **Get queue length** to see results similar to the following screen shot:</span><span class="sxs-lookup"><span data-stu-id="8aee6-247">Run the application, and select **Get queue length** to see results similar to the following screen shot:</span></span>
  
    ![Delete queue](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/vs-storage-aspnet-getting-started-queues/delete-queue-results.png)

## <a name="next-steps"></a><span data-ttu-id="8aee6-249">Next steps</span><span class="sxs-lookup"><span data-stu-id="8aee6-249">Next steps</span></span>
<span data-ttu-id="8aee6-250">View more feature guides to learn about additional options for storing data in Azure.</span><span class="sxs-lookup"><span data-stu-id="8aee6-250">View more feature guides to learn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="8aee6-251">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="8aee6-251">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="8aee6-252">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="8aee6-252">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-tables.md)








