---
title: Create a function in Azure triggered by queue messages | Microsoft Docs
description: Use Azure Functions to create a serverless function that is invoked by a messages submitted to an Azure Storage queue.
services: azure-functions
documentationcenter: na
author: ggailey777
manager: jeconnoc
ms.assetid: 361da2a4-15d1-4903-bdc4-cc4b27fc3ff4
ms.service: azure-functions
ms.devlang: multiple
ms.topic: quickstart
ms.date: 03/28/2018
ms.author: glenga
ms.custom: mvc, cc996988-fb4f-47
ms.openlocfilehash: 0f4772406354a2168b3a2f52cbfa715c29b15d50
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866323"
---
# <a name="create-a-function-triggered-by-azure-queue-storage"></a><span data-ttu-id="a0b67-103">Create a function triggered by Azure Queue storage</span><span class="sxs-lookup"><span data-stu-id="a0b67-103">Create a function triggered by Azure Queue storage</span></span>

<span data-ttu-id="a0b67-104">Learn how to create a function that is triggered when messages are submitted to an Azure Storage queue.</span><span class="sxs-lookup"><span data-stu-id="a0b67-104">Learn how to create a function that is triggered when messages are submitted to an Azure Storage queue.</span></span>

![View message in the logs.](./media/functions-create-storage-queue-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="a0b67-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a0b67-106">Prerequisites</span></span>

- <span data-ttu-id="a0b67-107">Download and install the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="a0b67-107">Download and install the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

- <span data-ttu-id="a0b67-108">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="a0b67-108">An Azure subscription.</span></span> <span data-ttu-id="a0b67-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="a0b67-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="create-an-azure-function-app"></a><span data-ttu-id="a0b67-110">Create an Azure Function app</span><span class="sxs-lookup"><span data-stu-id="a0b67-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Function app successfully created.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="a0b67-112">Next, you create a function in the new function app.</span><span class="sxs-lookup"><span data-stu-id="a0b67-112">Next, you create a function in the new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-queue-triggered-function"></a><span data-ttu-id="a0b67-113">Create a Queue triggered function</span><span class="sxs-lookup"><span data-stu-id="a0b67-113">Create a Queue triggered function</span></span>

1. <span data-ttu-id="a0b67-114">Expand your function app and click the **+** button next to **Functions**.</span><span class="sxs-lookup"><span data-stu-id="a0b67-114">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="a0b67-115">If this is the first function in your function app, select **Custom function**.</span><span class="sxs-lookup"><span data-stu-id="a0b67-115">If this is the first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="a0b67-116">This displays the complete set of function templates.</span><span class="sxs-lookup"><span data-stu-id="a0b67-116">This displays the complete set of function templates.</span></span>

    ![Functions quickstart page in the Azure portal](./media/functions-create-storage-queue-triggered-function/add-first-function.png)

2. <span data-ttu-id="a0b67-118">In the search field, type `queue` and then choose your desired language for the Queue storage trigger template.</span><span class="sxs-lookup"><span data-stu-id="a0b67-118">In the search field, type `queue` and then choose your desired language for the Queue storage trigger template.</span></span>

    ![Choose the storage queue trigger template.](./media/functions-create-storage-queue-triggered-function/functions-create-queue-storage-trigger-portal.png)

3. <span data-ttu-id="a0b67-120">Use the settings as specified in the table below the image.</span><span class="sxs-lookup"><span data-stu-id="a0b67-120">Use the settings as specified in the table below the image.</span></span>
    <span data-ttu-id="a0b67-121">![Configure the storage queue triggered function.](./media/functions-create-storage-queue-triggered-function/functions-create-queue-storage-trigger-portal-2.png)</span><span class="sxs-lookup"><span data-stu-id="a0b67-121">![Configure the storage queue triggered function.](./media/functions-create-storage-queue-triggered-function/functions-create-queue-storage-trigger-portal-2.png)</span></span>
    
    | <span data-ttu-id="a0b67-122">Setting</span><span class="sxs-lookup"><span data-stu-id="a0b67-122">Setting</span></span> | <span data-ttu-id="a0b67-123">Suggested value</span><span class="sxs-lookup"><span data-stu-id="a0b67-123">Suggested value</span></span> | <span data-ttu-id="a0b67-124">Description</span><span class="sxs-lookup"><span data-stu-id="a0b67-124">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="a0b67-125">**Name**</span><span class="sxs-lookup"><span data-stu-id="a0b67-125">**Name**</span></span> | <span data-ttu-id="a0b67-126">Unique in your function app</span><span class="sxs-lookup"><span data-stu-id="a0b67-126">Unique in your function app</span></span> | <span data-ttu-id="a0b67-127">Name of this queue triggered function.</span><span class="sxs-lookup"><span data-stu-id="a0b67-127">Name of this queue triggered function.</span></span> |
    | <span data-ttu-id="a0b67-128">**Queue name**</span><span class="sxs-lookup"><span data-stu-id="a0b67-128">**Queue name**</span></span>   | <span data-ttu-id="a0b67-129">myqueue-items</span><span class="sxs-lookup"><span data-stu-id="a0b67-129">myqueue-items</span></span>    | <span data-ttu-id="a0b67-130">Name of the queue to connect to in your Storage account.</span><span class="sxs-lookup"><span data-stu-id="a0b67-130">Name of the queue to connect to in your Storage account.</span></span> |
    | <span data-ttu-id="a0b67-131">**Storage account connection**</span><span class="sxs-lookup"><span data-stu-id="a0b67-131">**Storage account connection**</span></span> | <span data-ttu-id="a0b67-132">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="a0b67-132">AzureWebJobStorage</span></span> | <span data-ttu-id="a0b67-133">You can use the storage account connection already being used by your function app, or create a new one.</span><span class="sxs-lookup"><span data-stu-id="a0b67-133">You can use the storage account connection already being used by your function app, or create a new one.</span></span>  |    

3. <span data-ttu-id="a0b67-134">Click **Create** to create your function.</span><span class="sxs-lookup"><span data-stu-id="a0b67-134">Click **Create** to create your function.</span></span>

<span data-ttu-id="a0b67-135">Next, you connect to your Azure Storage account and create the **myqueue-items** storage queue.</span><span class="sxs-lookup"><span data-stu-id="a0b67-135">Next, you connect to your Azure Storage account and create the **myqueue-items** storage queue.</span></span>

## <a name="create-the-queue"></a><span data-ttu-id="a0b67-136">Create the queue</span><span class="sxs-lookup"><span data-stu-id="a0b67-136">Create the queue</span></span>

1. <span data-ttu-id="a0b67-137">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span><span class="sxs-lookup"><span data-stu-id="a0b67-137">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="a0b67-138">You use these credentials to connect to the storage account in Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="a0b67-138">You use these credentials to connect to the storage account in Azure Storage Explorer.</span></span> <span data-ttu-id="a0b67-139">If you have already connected your storage account, skip to step 4.</span><span class="sxs-lookup"><span data-stu-id="a0b67-139">If you have already connected your storage account, skip to step 4.</span></span>

    ![Get the Storage account connection credentials.](./media/functions-create-storage-queue-triggered-function/functions-storage-account-connection.png)

1. <span data-ttu-id="a0b67-141">Run the [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click the connect icon on the left, choose **Use a storage account name and key**, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a0b67-141">Run the [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click the connect icon on the left, choose **Use a storage account name and key**, and click **Next**.</span></span>

    ![Run the Storage Account Explorer tool.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="a0b67-143">Enter the **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span><span class="sxs-lookup"><span data-stu-id="a0b67-143">Enter the **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span></span>

    ![Enter the storage credentials and connect.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-2.png)

1. <span data-ttu-id="a0b67-145">Expand the attached storage account, right-click **Queues**, click **Create Queue**, type `myqueue-items`, and then press enter.</span><span class="sxs-lookup"><span data-stu-id="a0b67-145">Expand the attached storage account, right-click **Queues**, click **Create Queue**, type `myqueue-items`, and then press enter.</span></span>

    ![Create a storage queue.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-create-queue.png)

<span data-ttu-id="a0b67-147">Now that you have a storage queue, you can test the function by adding a message to the queue.</span><span class="sxs-lookup"><span data-stu-id="a0b67-147">Now that you have a storage queue, you can test the function by adding a message to the queue.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="a0b67-148">Test the function</span><span class="sxs-lookup"><span data-stu-id="a0b67-148">Test the function</span></span>

1. <span data-ttu-id="a0b67-149">Back in the Azure portal, browse to your function, expand the **Logs** at the bottom of the page, and make sure that log streaming isn't paused.</span><span class="sxs-lookup"><span data-stu-id="a0b67-149">Back in the Azure portal, browse to your function, expand the **Logs** at the bottom of the page, and make sure that log streaming isn't paused.</span></span>

1. <span data-ttu-id="a0b67-150">In Storage Explorer, expand your storage account, **Queues**, and **myqueue-items**, then click **Add message**.</span><span class="sxs-lookup"><span data-stu-id="a0b67-150">In Storage Explorer, expand your storage account, **Queues**, and **myqueue-items**, then click **Add message**.</span></span>

    ![Add a message to the queue.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-add-message.png)

1. <span data-ttu-id="a0b67-152">Type your "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="a0b67-152">Type your "Hello World!"</span></span> <span data-ttu-id="a0b67-153">message in **Message text** and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="a0b67-153">message in **Message text** and click **OK**.</span></span>

1. <span data-ttu-id="a0b67-154">Wait for a few seconds, then go back to your function logs and verify that the new message has been read from the queue.</span><span class="sxs-lookup"><span data-stu-id="a0b67-154">Wait for a few seconds, then go back to your function logs and verify that the new message has been read from the queue.</span></span>

    ![View message in the logs.](./media/functions-create-storage-queue-triggered-function/functions-queue-storage-trigger-view-logs.png)

1. <span data-ttu-id="a0b67-156">Back in Storage Explorer, click **Refresh** and verify that the message has been processed and is no longer in the queue.</span><span class="sxs-lookup"><span data-stu-id="a0b67-156">Back in Storage Explorer, click **Refresh** and verify that the message has been processed and is no longer in the queue.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="a0b67-157">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="a0b67-157">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="a0b67-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="a0b67-158">Next steps</span></span>

<span data-ttu-id="a0b67-159">You have created a function that runs when a message is added to a storage queue.</span><span class="sxs-lookup"><span data-stu-id="a0b67-159">You have created a function that runs when a message is added to a storage queue.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="a0b67-160">For more information about Queue storage triggers, see [Azure Functions Storage queue bindings](functions-bindings-storage-queue.md).</span><span class="sxs-lookup"><span data-stu-id="a0b67-160">For more information about Queue storage triggers, see [Azure Functions Storage queue bindings](functions-bindings-storage-queue.md).</span></span>
