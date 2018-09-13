---
title: Azure Quickstart - Create an event hub using the Azure portal | Microsoft Docs
description: In this quickstart, you learn how to create an Azure event hub using Azure portal and then send and receive events using .NET Standard SDK.
services: event-hubs
documentationcenter: ''
author: ShubhaVijayasarathy
manager: timlt
ms.service: event-hubs
ms.topic: quickstart
ms.custom: mvc
ms.date: 08/16/2018
ms.author: shvija
ms.openlocfilehash: 5c59d22c7b1e9e993d2686bfc4c2e389a17d9161
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857139"
---
# <a name="quickstart-create-an-event-hub-using-azure-portal"></a><span data-ttu-id="b9284-103">Quickstart: Create an event hub using Azure portal</span><span class="sxs-lookup"><span data-stu-id="b9284-103">Quickstart: Create an event hub using Azure portal</span></span>

<span data-ttu-id="b9284-104">Azure Event Hubs is a highly scalable data streaming platform and ingestion service capable of receiving and processing millions of events per second.</span><span class="sxs-lookup"><span data-stu-id="b9284-104">Azure Event Hubs is a highly scalable data streaming platform and ingestion service capable of receiving and processing millions of events per second.</span></span> <span data-ttu-id="b9284-105">This quickstart shows how to create an event hub using the [Azure portal](https://portal.azure.com), and then send to and receive from an event hub using the .NET Standard SDK.</span><span class="sxs-lookup"><span data-stu-id="b9284-105">This quickstart shows how to create an event hub using the [Azure portal](https://portal.azure.com), and then send to and receive from an event hub using the .NET Standard SDK.</span></span>

<span data-ttu-id="b9284-106">To complete this quickstart, you need an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="b9284-106">To complete this quickstart, you need an Azure subscription.</span></span> <span data-ttu-id="b9284-107">If you don't have one, [create a free account][] before you begin.</span><span class="sxs-lookup"><span data-stu-id="b9284-107">If you don't have one, [create a free account][] before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9284-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b9284-108">Prerequisites</span></span>

<span data-ttu-id="b9284-109">To complete this quickstart, make sure you have:</span><span class="sxs-lookup"><span data-stu-id="b9284-109">To complete this quickstart, make sure you have:</span></span>

- <span data-ttu-id="b9284-110">[Visual Studio 2017 Update 3 (version 15.3, 26730.01)](http://www.visualstudio.com/vs) or later.</span><span class="sxs-lookup"><span data-stu-id="b9284-110">[Visual Studio 2017 Update 3 (version 15.3, 26730.01)](http://www.visualstudio.com/vs) or later.</span></span>
- <span data-ttu-id="b9284-111">[.NET Standard SDK](https://www.microsoft.com/net/download/windows), version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="b9284-111">[.NET Standard SDK](https://www.microsoft.com/net/download/windows), version 2.0 or later.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="b9284-112">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="b9284-112">Create a resource group</span></span>

<span data-ttu-id="b9284-113">A resource group is a logical collection of Azure resources.</span><span class="sxs-lookup"><span data-stu-id="b9284-113">A resource group is a logical collection of Azure resources.</span></span> <span data-ttu-id="b9284-114">All resources are deployed and managed in a resource group.</span><span class="sxs-lookup"><span data-stu-id="b9284-114">All resources are deployed and managed in a resource group.</span></span> <span data-ttu-id="b9284-115">Do the following to create a resource group:</span><span class="sxs-lookup"><span data-stu-id="b9284-115">Do the following to create a resource group:</span></span>

1. <span data-ttu-id="b9284-116">In the left navigation, click **Resource groups**.</span><span class="sxs-lookup"><span data-stu-id="b9284-116">In the left navigation, click **Resource groups**.</span></span> <span data-ttu-id="b9284-117">Then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="b9284-117">Then click **Add**.</span></span>

   ![][1]

2. <span data-ttu-id="b9284-118">Type a unique name for the resource group.</span><span class="sxs-lookup"><span data-stu-id="b9284-118">Type a unique name for the resource group.</span></span> <span data-ttu-id="b9284-119">The system immediately checks to see if the name is available in the currently selected Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="b9284-119">The system immediately checks to see if the name is available in the currently selected Azure subscription.</span></span>

3. <span data-ttu-id="b9284-120">In **Subscription**, click the name of the Azure subscription in which you want to create the resource group.</span><span class="sxs-lookup"><span data-stu-id="b9284-120">In **Subscription**, click the name of the Azure subscription in which you want to create the resource group.</span></span>

4. <span data-ttu-id="b9284-121">Select a geographic location for the resource group.</span><span class="sxs-lookup"><span data-stu-id="b9284-121">Select a geographic location for the resource group.</span></span>

5. <span data-ttu-id="b9284-122">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b9284-122">Click **Create**.</span></span>

   ![][2]

## <a name="create-an-event-hubs-namespace"></a><span data-ttu-id="b9284-123">Create an Event Hubs namespace</span><span class="sxs-lookup"><span data-stu-id="b9284-123">Create an Event Hubs namespace</span></span>

<span data-ttu-id="b9284-124">An Event Hubs namespace provides a unique scoping container, referenced by its fully qualified domain name, in which you create one or more event hubs.</span><span class="sxs-lookup"><span data-stu-id="b9284-124">An Event Hubs namespace provides a unique scoping container, referenced by its fully qualified domain name, in which you create one or more event hubs.</span></span> <span data-ttu-id="b9284-125">To create a namespace in your resource group using the portal, do the following:</span><span class="sxs-lookup"><span data-stu-id="b9284-125">To create a namespace in your resource group using the portal, do the following:</span></span>

1. <span data-ttu-id="b9284-126">Log on to the [Azure portal][], and click **Create a resource** at the top left of the screen.</span><span class="sxs-lookup"><span data-stu-id="b9284-126">Log on to the [Azure portal][], and click **Create a resource** at the top left of the screen.</span></span>

2. <span data-ttu-id="b9284-127">Click **Internet of Things**, and then click **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="b9284-127">Click **Internet of Things**, and then click **Event Hubs**.</span></span>

3. <span data-ttu-id="b9284-128">In **Create namespace**, enter a namespace name.</span><span class="sxs-lookup"><span data-stu-id="b9284-128">In **Create namespace**, enter a namespace name.</span></span> <span data-ttu-id="b9284-129">The system immediately checks to see if the name is available.</span><span class="sxs-lookup"><span data-stu-id="b9284-129">The system immediately checks to see if the name is available.</span></span>

   ![](./media/event-hubs-create/create-event-hub1.png)

4. <span data-ttu-id="b9284-130">After making sure the namespace name is available, choose the pricing tier (Basic or Standard).</span><span class="sxs-lookup"><span data-stu-id="b9284-130">After making sure the namespace name is available, choose the pricing tier (Basic or Standard).</span></span> <span data-ttu-id="b9284-131">Also, choose an Azure subscription, resource group, and location in which to create the resource.</span><span class="sxs-lookup"><span data-stu-id="b9284-131">Also, choose an Azure subscription, resource group, and location in which to create the resource.</span></span>
 
5. <span data-ttu-id="b9284-132">Click **Create** to create the namespace.</span><span class="sxs-lookup"><span data-stu-id="b9284-132">Click **Create** to create the namespace.</span></span> <span data-ttu-id="b9284-133">You may have to wait a few minutes for the system to fully provision the resources.</span><span class="sxs-lookup"><span data-stu-id="b9284-133">You may have to wait a few minutes for the system to fully provision the resources.</span></span>

6. <span data-ttu-id="b9284-134">In the portal list of namespaces, click the newly created namespace.</span><span class="sxs-lookup"><span data-stu-id="b9284-134">In the portal list of namespaces, click the newly created namespace.</span></span>

7. <span data-ttu-id="b9284-135">Click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="b9284-135">Click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
8. <span data-ttu-id="b9284-136">Click the copy button to copy the **RootManageSharedAccessKey** connection string to the clipboard.</span><span class="sxs-lookup"><span data-stu-id="b9284-136">Click the copy button to copy the **RootManageSharedAccessKey** connection string to the clipboard.</span></span> <span data-ttu-id="b9284-137">Save this connection string in a temporary location, such as Notepad, to use later.</span><span class="sxs-lookup"><span data-stu-id="b9284-137">Save this connection string in a temporary location, such as Notepad, to use later.</span></span>
    
## <a name="create-an-event-hub"></a><span data-ttu-id="b9284-138">Create an event hub</span><span class="sxs-lookup"><span data-stu-id="b9284-138">Create an event hub</span></span>

<span data-ttu-id="b9284-139">To create an event hub within the namespace, do the following:</span><span class="sxs-lookup"><span data-stu-id="b9284-139">To create an event hub within the namespace, do the following:</span></span>

1. <span data-ttu-id="b9284-140">In the Event Hubs namespace list, click the newly created namespace.</span><span class="sxs-lookup"><span data-stu-id="b9284-140">In the Event Hubs namespace list, click the newly created namespace.</span></span>      
   
    ![](./media/event-hubs-quickstart-portal/create-event-hub2.png) 

2. <span data-ttu-id="b9284-141">In the namespace window, click **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="b9284-141">In the namespace window, click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-quickstart-portal/create-event-hub3.png)

1. <span data-ttu-id="b9284-142">At the top of the window, click **+ Add Event Hub**.</span><span class="sxs-lookup"><span data-stu-id="b9284-142">At the top of the window, click **+ Add Event Hub**.</span></span>
   
    ![](./media/event-hubs-quickstart-portal/create-event-hub4.png)
1. <span data-ttu-id="b9284-143">Type a name for your event hub, then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b9284-143">Type a name for your event hub, then click **Create**.</span></span>
   
    ![](./media/event-hubs-quickstart-portal/create-event-hub5.png)

<span data-ttu-id="b9284-144">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="b9284-144">Congratulations!</span></span> <span data-ttu-id="b9284-145">You have used the portal to create an Event Hubs namespace, and an event hub within that namespace.</span><span class="sxs-lookup"><span data-stu-id="b9284-145">You have used the portal to create an Event Hubs namespace, and an event hub within that namespace.</span></span>

## <a name="create-a-storage-account-for-event-processor-host"></a><span data-ttu-id="b9284-146">Create a storage account for Event Processor Host</span><span class="sxs-lookup"><span data-stu-id="b9284-146">Create a storage account for Event Processor Host</span></span>

<span data-ttu-id="b9284-147">The Event Processor Host is an intelligent agent that simplifies receiving events from Event Hubs by managing persistent checkpoints and parallel receives.</span><span class="sxs-lookup"><span data-stu-id="b9284-147">The Event Processor Host is an intelligent agent that simplifies receiving events from Event Hubs by managing persistent checkpoints and parallel receives.</span></span> <span data-ttu-id="b9284-148">For checkpointing, the Event Processor Host requires a storage account.</span><span class="sxs-lookup"><span data-stu-id="b9284-148">For checkpointing, the Event Processor Host requires a storage account.</span></span> <span data-ttu-id="b9284-149">The following example shows how to create a storage account and how to get its keys for access:</span><span class="sxs-lookup"><span data-stu-id="b9284-149">The following example shows how to create a storage account and how to get its keys for access:</span></span>

1. <span data-ttu-id="b9284-150">Log on to the [Azure portal][Azure portal], and click **New** at the top left of the screen.</span><span class="sxs-lookup"><span data-stu-id="b9284-150">Log on to the [Azure portal][Azure portal], and click **New** at the top left of the screen.</span></span>

2. <span data-ttu-id="b9284-151">Click **Storage**, then click **Storage account**.</span><span class="sxs-lookup"><span data-stu-id="b9284-151">Click **Storage**, then click **Storage account**.</span></span>
   
    ![](./media/event-hubs-quickstart-portal/create-storage1.png)

3. <span data-ttu-id="b9284-152">In **Create storage account**, type a name for the storage account.</span><span class="sxs-lookup"><span data-stu-id="b9284-152">In **Create storage account**, type a name for the storage account.</span></span> <span data-ttu-id="b9284-153">Choose an Azure subscription, resource group, and location in which to create the resource.</span><span class="sxs-lookup"><span data-stu-id="b9284-153">Choose an Azure subscription, resource group, and location in which to create the resource.</span></span> <span data-ttu-id="b9284-154">Then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b9284-154">Then click **Create**.</span></span>
   
    ![](./media/event-hubs-quickstart-portal/create-storage2.png)

4. <span data-ttu-id="b9284-155">In the list of storage accounts, click the newly created storage account.</span><span class="sxs-lookup"><span data-stu-id="b9284-155">In the list of storage accounts, click the newly created storage account.</span></span>

5. <span data-ttu-id="b9284-156">In the storage account window, click **Access keys**.</span><span class="sxs-lookup"><span data-stu-id="b9284-156">In the storage account window, click **Access keys**.</span></span> <span data-ttu-id="b9284-157">Copy the value of **key1** to use later.</span><span class="sxs-lookup"><span data-stu-id="b9284-157">Copy the value of **key1** to use later.</span></span>
   
    ![](./media/event-hubs-quickstart-portal/create-storage3.png)

## <a name="download-and-run-the-samples"></a><span data-ttu-id="b9284-158">Download and run the samples</span><span class="sxs-lookup"><span data-stu-id="b9284-158">Download and run the samples</span></span>

<span data-ttu-id="b9284-159">The next step is to run the sample code that sends events to an event hub, and receives those events using the Event Processor Host.</span><span class="sxs-lookup"><span data-stu-id="b9284-159">The next step is to run the sample code that sends events to an event hub, and receives those events using the Event Processor Host.</span></span> 

<span data-ttu-id="b9284-160">First, download the [SampleSender](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) and [SampleEphReceiver](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) samples from GitHub, or clone the [azure-event-hubs repo](https://github.com/Azure/azure-event-hubs).</span><span class="sxs-lookup"><span data-stu-id="b9284-160">First, download the [SampleSender](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) and [SampleEphReceiver](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) samples from GitHub, or clone the [azure-event-hubs repo](https://github.com/Azure/azure-event-hubs).</span></span>

### <a name="sender"></a><span data-ttu-id="b9284-161">Sender</span><span class="sxs-lookup"><span data-stu-id="b9284-161">Sender</span></span>

1. <span data-ttu-id="b9284-162">Open Visual Studio, then from the **File** menu, click **Open**, and then click **Project/Solution**.</span><span class="sxs-lookup"><span data-stu-id="b9284-162">Open Visual Studio, then from the **File** menu, click **Open**, and then click **Project/Solution**.</span></span>

2. <span data-ttu-id="b9284-163">Locate the **SampleSender** sample folder you downloaded previously, then double-click the SampleSender.sln file to load the project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b9284-163">Locate the **SampleSender** sample folder you downloaded previously, then double-click the SampleSender.sln file to load the project in Visual Studio.</span></span>

3. <span data-ttu-id="b9284-164">In Solution Explorer, double-click Program.cs to open the file in the Visual Studio editor.</span><span class="sxs-lookup"><span data-stu-id="b9284-164">In Solution Explorer, double-click Program.cs to open the file in the Visual Studio editor.</span></span>

4. <span data-ttu-id="b9284-165">Replace the `EventHubConnectionString` value with the connection string you obtained when you created the namespace.</span><span class="sxs-lookup"><span data-stu-id="b9284-165">Replace the `EventHubConnectionString` value with the connection string you obtained when you created the namespace.</span></span>

5. <span data-ttu-id="b9284-166">Replace `EventHubName` with the name of the event hub you created within that namespace.</span><span class="sxs-lookup"><span data-stu-id="b9284-166">Replace `EventHubName` with the name of the event hub you created within that namespace.</span></span>

6. <span data-ttu-id="b9284-167">From the **Build** menu, click **Build Solution** to ensure there are no errors.</span><span class="sxs-lookup"><span data-stu-id="b9284-167">From the **Build** menu, click **Build Solution** to ensure there are no errors.</span></span>

### <a name="receiver"></a><span data-ttu-id="b9284-168">Receiver</span><span class="sxs-lookup"><span data-stu-id="b9284-168">Receiver</span></span>

1. <span data-ttu-id="b9284-169">Open Visual Studio, then from the **File** menu, click **Open**, and then click **Project/Solution**.</span><span class="sxs-lookup"><span data-stu-id="b9284-169">Open Visual Studio, then from the **File** menu, click **Open**, and then click **Project/Solution**.</span></span>

2. <span data-ttu-id="b9284-170">Locate the **SampleEphReceiver** sample folder you downloaded in step 1, then double-click the SampleEphReceiver.sln file to load the project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b9284-170">Locate the **SampleEphReceiver** sample folder you downloaded in step 1, then double-click the SampleEphReceiver.sln file to load the project in Visual Studio.</span></span>

3. <span data-ttu-id="b9284-171">In Solution Explorer, double-click Program.cs to open the file in the Visual Studio editor.</span><span class="sxs-lookup"><span data-stu-id="b9284-171">In Solution Explorer, double-click Program.cs to open the file in the Visual Studio editor.</span></span>

4. <span data-ttu-id="b9284-172">Replace the following variable values:</span><span class="sxs-lookup"><span data-stu-id="b9284-172">Replace the following variable values:</span></span>
    1. <span data-ttu-id="b9284-173">`EventHubConnectionString`: Replace with the connection string you obtained when you created the namespace.</span><span class="sxs-lookup"><span data-stu-id="b9284-173">`EventHubConnectionString`: Replace with the connection string you obtained when you created the namespace.</span></span>
    2. <span data-ttu-id="b9284-174">`EventHubName`: The name of the event hub you created within that namespace.</span><span class="sxs-lookup"><span data-stu-id="b9284-174">`EventHubName`: The name of the event hub you created within that namespace.</span></span>
    3. <span data-ttu-id="b9284-175">`StorageContainerName`: The name of a storage container.</span><span class="sxs-lookup"><span data-stu-id="b9284-175">`StorageContainerName`: The name of a storage container.</span></span> <span data-ttu-id="b9284-176">Give it a unique name, and the container is created for you when you run the app.</span><span class="sxs-lookup"><span data-stu-id="b9284-176">Give it a unique name, and the container is created for you when you run the app.</span></span>
    4. <span data-ttu-id="b9284-177">`StorageAccountName`: The name of the storage account you created.</span><span class="sxs-lookup"><span data-stu-id="b9284-177">`StorageAccountName`: The name of the storage account you created.</span></span>
    5. <span data-ttu-id="b9284-178">`StorageAccountKey`: The storage account key you obtained from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b9284-178">`StorageAccountKey`: The storage account key you obtained from the Azure portal.</span></span>

5. <span data-ttu-id="b9284-179">From the **Build** menu, click **Build Solution** to ensure there are no errors.</span><span class="sxs-lookup"><span data-stu-id="b9284-179">From the **Build** menu, click **Build Solution** to ensure there are no errors.</span></span>

### <a name="run-the-apps"></a><span data-ttu-id="b9284-180">Run the apps</span><span class="sxs-lookup"><span data-stu-id="b9284-180">Run the apps</span></span>

<span data-ttu-id="b9284-181">First, run the **SampleSender** application and observe 100 messages being sent.</span><span class="sxs-lookup"><span data-stu-id="b9284-181">First, run the **SampleSender** application and observe 100 messages being sent.</span></span> <span data-ttu-id="b9284-182">Press **Enter** to end the program.</span><span class="sxs-lookup"><span data-stu-id="b9284-182">Press **Enter** to end the program.</span></span>

![][3]

<span data-ttu-id="b9284-183">Then, run the **SampleEphReceiver** app, and observe the messages being received into the Event Processor Host.</span><span class="sxs-lookup"><span data-stu-id="b9284-183">Then, run the **SampleEphReceiver** app, and observe the messages being received into the Event Processor Host.</span></span>

![][4]
 
## <a name="clean-up-resources"></a><span data-ttu-id="b9284-184">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="b9284-184">Clean up resources</span></span>

<span data-ttu-id="b9284-185">You can use the portal to remove the storage account, namespace, and event hub.</span><span class="sxs-lookup"><span data-stu-id="b9284-185">You can use the portal to remove the storage account, namespace, and event hub.</span></span> 

1. <span data-ttu-id="b9284-186">From the Azure portal, click **All resources** in the left-hand pane.</span><span class="sxs-lookup"><span data-stu-id="b9284-186">From the Azure portal, click **All resources** in the left-hand pane.</span></span> 
2. <span data-ttu-id="b9284-187">Click the storage account or namespace you want to delete.</span><span class="sxs-lookup"><span data-stu-id="b9284-187">Click the storage account or namespace you want to delete.</span></span> <span data-ttu-id="b9284-188">Deleting the namespace also removes any event hubs inside it.</span><span class="sxs-lookup"><span data-stu-id="b9284-188">Deleting the namespace also removes any event hubs inside it.</span></span>
3. <span data-ttu-id="b9284-189">On the menu bar at the top of the screen, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="b9284-189">On the menu bar at the top of the screen, click **Delete**.</span></span> <span data-ttu-id="b9284-190">Confirm the deletion.</span><span class="sxs-lookup"><span data-stu-id="b9284-190">Confirm the deletion.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b9284-191">Next steps</span><span class="sxs-lookup"><span data-stu-id="b9284-191">Next steps</span></span>

<span data-ttu-id="b9284-192">In this article, you created the Event Hubs namespace and other resources required to send and receive events from your event hub.</span><span class="sxs-lookup"><span data-stu-id="b9284-192">In this article, you created the Event Hubs namespace and other resources required to send and receive events from your event hub.</span></span> <span data-ttu-id="b9284-193">To learn more, continue with the following tutorial:</span><span class="sxs-lookup"><span data-stu-id="b9284-193">To learn more, continue with the following tutorial:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b9284-194">Visualize data anomalies on Event Hubs data streams</span><span class="sxs-lookup"><span data-stu-id="b9284-194">Visualize data anomalies on Event Hubs data streams</span></span>](event-hubs-tutorial-visualize-anomalies.md)

[create a free account]: https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio
[Azure portal]: https://portal.azure.com/
[1]: ./media/event-hubs-quickstart-portal/resource-groups1.png
[2]: ./media/event-hubs-quickstart-portal/resource-groups2.png
[3]: ./media/event-hubs-quickstart-portal/sender1.png
[4]: ./media/event-hubs-quickstart-portal/receiver1.png
